# 📄 Obtener un CSV con los usuarios que tienen asignado un tipo de licencia en concreto

## 📝 Script PowerShell para obtener usuarios con licencias específicas

```powershell
# Conectar a Microsoft Graph con los permisos necesarios
Connect-MgGraph -Scopes "User.Read.All", "Organization.Read.All"

# Definir las licencias válidas para clasificación de documentos
$licenciasValidas = @(
    "ENTERPRISEPREMIUM",    # Microsoft 365 E5
    "ENTERPRISEPACK",       # Microsoft 365 E3
    "BUSINESS_PREMIUM",     # Business Premium
    "EMS",                  # EMS E5
    "E5_COMPLIANCE"         # Microsoft 365 E5 Compliance
)

# Obtener los SKUs disponibles en el tenant
$skus = Get-MgSubscribedSku

# Obtener todos los usuarios con sus licencias asignadas
$usuarios = Get-MgUser -All -Property "DisplayName,UserPrincipalName,AssignedLicenses"

# Filtrar usuarios con licencias válidas
$usuariosConClasificacion = @()

foreach ($usuario in $usuarios) {
    foreach ($lic in $usuario.AssignedLicenses) {
        $sku = $skus | Where-Object { $_.SkuId -eq $lic.SkuId }
        if ($sku -and ($licenciasValidas -contains $sku.SkuPartNumber)) {
            $usuariosConClasificacion += [PSCustomObject]@{
                Nombre   = $usuario.DisplayName
                Usuario  = $usuario.UserPrincipalName
                Licencia = $sku.SkuPartNumber
            }
            break
        }
    }
}

# Exportar resultados a CSV
$usuariosConClasificacion | Export-Csv "usuarios_con_clasificacion_documentos.csv" -NoTypeInformation -Encoding UTF8
```
