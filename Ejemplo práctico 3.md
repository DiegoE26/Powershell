# 🧾 Script PowerShell para eliminar fotos de usuarios en Microsoft Graph

Este script se conecta a Microsoft Graph con permisos adecuados y elimina la foto de perfil de todos los usuarios habilitados. Si un usuario no tiene foto, se notifica; si ocurre otro error, se muestra una advertencia.

## 💻 Script

```
# Conectarse con permisos adecuados
Connect-MgGraph -Scopes "User.ReadWrite.All"

# Obtener todos los usuarios habilitados
$usuarios = Get-MgUser -All -Filter "accountEnabled eq true"

foreach ($usuario in $usuarios) {
    try {
        Write-Host "Eliminando foto para $($usuario.UserPrincipalName)..."
        Remove-MgUserPhoto -UserId $usuario.Id -ErrorAction Stop
        Write-Host "✅ Foto eliminada para $($usuario.UserPrincipalName)"
    }
    catch {
        if ($_.Exception.Message -like "*ImageNotFound*") {
            Write-Host "ℹ️ No había foto para $($usuario.UserPrincipalName)"
        } else {
            Write-Warning "⚠️ Error con $($usuario.UserPrincipalName): $_"
        }
    }
}
