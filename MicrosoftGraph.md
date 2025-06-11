# 🚀 Ejemplo de uso de Microsoft Graph

| Paso | Comando | Descripción |
|------|---------|-------------|
| 1️⃣ | `Install-Package Microsoft.graph` | Instalar los paquetes necesarios para usar Microsoft Graph |
| 2️⃣ | `Connect-MgGraph -Scopes "User.Read", "Group.ReadWrite.All"` | Conectarse a Microsoft Graph |
| 3️⃣ | `Remove-MgUserPhoto -UserId "user@domain"` | Borrar la foto de un usuario en concreto |
| 4️⃣ | `Get-MgUserPhoto -UserId "user@domain"` | Verificar si el usuario tiene foto en su perfil de O365 |
| 5️⃣ | `Set-OwaMailboxPolicy -Identity "OwaMailboxPolicy-Default" -SetPhotoEnabled $false` | Anula la posibilidad de que el usuario pueda poner una foto de perfil en su usuario de O365 |

<details>
<summary>🔐 <b>Conectarse con permisos adecuados y eliminar fotos de todos los usuarios habilitados</b></summary>

```powershell
Connect-MgGraph -Scopes "User.ReadWrite.All"
# Obtener todos los usuarios habilitados
$usuarios = Get-MgUser -All -Filter "accountEnabled eq true" # obtener todas las cuentas activas

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
```
</details>

---

## 👤 Gestión de usuarios

- **Obtener todos los usuarios**
  ```powershell
  Get-MgUser
  ```

- **Obtener un usuario específico**
  ```powershell
  Get-MgUser -UserId user@dominio.com
  ```

- **Crear un nuevo usuario**
  ```powershell
  New-MgUser -DisplayName "Nuevo Usuario" -UserPrincipalName "nuevo@dominio.com" -MailNickname "nuevo" -AccountEnabled $true -PasswordProfile @{ ForceChangePasswordNextSignIn = $true; Password = "Password123!" }
  ```

- **Actualizar un usuario**
  ```powershell
  Update-MgUser -UserId user@dominio.com -JobTitle "Nuevo Cargo"
  ```

- **Eliminar un usuario**
  ```powershell
  Remove-MgUser -UserId user@dominio.com
  ```

---

## 👥 Gestión de Grupos

- **Obtener todos los grupos**
  ```powershell
  Get-MgGroup
  ```

- **Obtener miembros de un grupo**
  ```powershell
  Get-MgGroupMember -GroupId <GroupId>
  ```

- **Crear un nuevo grupo**
  ```powershell
  New-MgGroup -DisplayName "Equipo de Ventas" -MailEnabled $true -MailNickname "ventas" -SecurityEnabled $false -GroupTypes "Unified"
  ```

- **Añadir un miembro al grupo**
  ```powershell
  Add-MgGroupMember -GroupId <GroupId> -DirectoryObjectId <UserId>
  ```

---

## 📧 Correo y 📅 Calendario

- **Obtener mensajes de un usuario**
  ```powershell
  Get-MgUserMessage -UserId user@dominio.com
  ```

- **Obtener eventos del calendario de un usuario**
  ```powershell
  Get-MgUserCalendarEvent -UserId user@dominio.com
  ```

---

## 🛠️ Aplicaciones

- **Obtener todas las aplicaciones registradas**
  ```powershell
  Get-MgApplication
  ```

- **Obtener detalles de una app**
  ```powershell
  Get-MgApplication -ApplicationId <AppId>
  ```

---

## 🔌 Desconectar sesión de Graph

```powershell
Disconnect-MgGraph
```

---

## 🆘 Adicionales

- **Buscar comandos relacionados:**
  ```powershell
  Find-MgGraphCommand -Command Get-MgUser
  ```

