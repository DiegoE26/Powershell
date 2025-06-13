# Comprobación y aviso de expiración de contraseñas en Active Directory

Este documento describe un script de PowerShell que permite:

- Obtener información de una lista de usuarios ficticios en Active Directory.
- Comprobar el estado de la contraseña de cada usuario.
- Enviar un aviso por correo electrónico si la contraseña está próxima a expirar.

A continuación se muestra el script:

```powershell
# Lista genérica de usuarios (nombres ficticios)
$usuarios = @("usuario01", "usuario02", "usuario03", "usuario04", "usuario05")

# Primera parte: obtener información de usuarios habilitados
foreach ($usuario in $usuarios) {
    $user = Get-ADUser -Identity $usuario -Properties mail, Enabled
    if ($user.Enabled) {
        $user | Select Name, SamAccountName, Mail
    }
}

# Segunda parte: comprobar estado de la contraseña y enviar aviso si va a caducar
foreach ($usuario in $usuarios) {
    $user = Get-ADUser -Identity $usuario -Properties PasswordLastSet, Mail, Enabled
    if (-not $user.Enabled) {
        continue
    }

    $fechaUltimaContraseña = $user.PasswordLastSet
    $mail = $user.Mail

    Write-Host "----------------------------- $usuario $fechaUltimaContraseña -----------------------------" -ForegroundColor Green

    $fechaActual = Get-Date
    $diferencia = New-TimeSpan -Start $fechaUltimaContraseña -End $fechaActual

    Write-Host $fechaActual -ForegroundColor Cyan
    Write-Host $diferencia.Days -ForegroundColor Red

    $diasRestantes = 42 - $diferencia.Days

    $expiracion = Get-ADUser -Identity $usuario -Properties msDS-UserPasswordExpiryTimeComputed | 
        Select-Object @{Name="ExpirationDate"; Expression={[datetime]::FromFileTime($_."msDS-UserPasswordExpiryTimeComputed")}} |
        ForEach-Object { $_.ExpirationDate }

    if ($diferencia.Days -ge 35) {
        $EmailFrom = "noreply@empresa.com"
        $EmailTo = $mail
        $Subject = "⚠️ Tu contraseña expirará en $diasRestantes días"
        $Body = @"
Hola,

La contraseña de tu cuenta **$usuario** expirará en **$diasRestantes días**, el **$expiracion**.

Tienes estas opciones para cambiarla:

1. Iniciar sesión en un equipo físico o por RDP y cambiarla manualmente.
2. Contactar con el departamento de sistemas para un reinicio forzado.
3. Esperar a que expire y cambiarla desde: https://portal.seguro.empresa.com (recomendado).

Un saludo.
"@

        $SMTPServer = "smtp.empresa.com"
        $puerto = 25
        $usarSSL = $true

        Send-MailMessage -From $EmailFrom -To $EmailTo -Subject $Subject -Body $Body -SmtpServer $SMTPServer -Encoding utf8
    }
}
```
