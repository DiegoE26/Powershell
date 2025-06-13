# 🚀 Exportar Usuarios con Licencias y Cargo Específico a CSV

Este procedimiento te permite obtener un archivo CSV con los usuarios que tienen ciertas licencias y un cargo específico en Microsoft 365.

---

## Script PowerShell Completo

Guarda el siguiente script como `Exportar-Usuarios-Responsables.ps1` y ejecútalo en PowerShell con permisos adecuados. Este script conecta a Microsoft Graph, filtra usuarios por cargo y licencias, y exporta los resultados a un archivo CSV.

```powershell
# 1. Conexión a Microsoft Graph
Connect-MgGraph -Scopes "User.Read.All"

# 2. Licencias válidas
$licenciasValidas = @(
    "ENTERPRISEPREMIUM",         # Microsoft 365 E5
    "ENTERPRISEPACK",            # Microsoft 365 E3
    "BUSINESS_PREMIUM",          # Business Premium
    "EMS",                       # EMS E5
    "E5_COMPLIANCE"              # Microsoft 365 E5 Compliance
)

# 3. Obtener SKUs disponibles
$skus = Get-MgSubscribedSku | Select-Object SkuId, @{Name="SkuPartNumber"; Expression = { $_.SkuPartNumber.ToUpper() } }

# 4. Definir cargos de responsabilidad
$regexResponsables = "(?i)(RESPONSABLE|DIRECTOR|SUBDIRECTOR)"

# 5. Obtener usuarios
$usuarios = Get-MgUser -All -Property "DisplayName,UserPrincipalName,JobTitle,AssignedLicenses"

# 6. Procesar y exportar resultados
$resultado = @()

foreach ($usuario in $usuarios) {
    if ($usuario.JobTitle -and ($usuario.JobTitle -match $regexResponsables)) {

        # Verificar licencias asignadas
        $licenciasAsignadas = @()
        foreach ($lic in $usuario.AssignedLicenses) {
            $sku = $skus | Where-Object { $_.SkuId -eq $lic.SkuId }
            if ($sku) {
                $licenciasAsignadas += $sku.SkuPartNumber
            }
        }

        # Verificar si tiene al menos una licencia válida
        $tieneLicencia = $false

        if ($licenciasAsignadas | Where-Object { $licenciasValidas -contains $_ }) {
            $tieneLicencia = $true
        }

        # Caso especial: ENTERPRISEPACK + una complementaria válida
        if ($licenciasAsignadas -contains "ENTERPRISEPACK" -and (
            $licenciasAsignadas -contains "EMS_E5" -or
            $licenciasAsignadas -contains "M365_E5_COMPLIANCE" -or
            $licenciasAsignadas -contains "AIP_PREMIUMP2")) {
            $tieneLicencia = $true
        }

        # Añadir solo si cumple las condiciones
        if ($tieneLicencia) {
            $resultado += [PSCustomObject]@{
                Nombre    = $usuario.DisplayName
                Usuario   = $usuario.UserPrincipalName
                Cargo     = $usuario.JobTitle
                Licencias = ($licenciasAsignadas -join ", ")
            }
        }
    }
}

# Exportar a CSV
$resultado | Export-Csv "responsables_con_clasificacion.csv" -NoTypeInformation -Encoding UTF8

Write-Host "Exportación completada: responsables_con_clasificacion.csv" -ForegroundColor Green
```

## 7. Resultado

Al finalizar, tendrás un archivo llamado **responsables_con_clasificacion.csv** con los usuarios que cumplen los criterios de cargo y licencias.

