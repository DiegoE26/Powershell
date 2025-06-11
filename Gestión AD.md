# Comandos Útiles de PowerShell para Gestión de AD, Microsoft Graph y Exchange Online

---

## 1. Active Directory (AD)

### Importar módulo AD
```powershell
Import-Module ActiveDirectory
```

### Usuarios

- Obtener todos los usuarios
```powershell
Get-ADUser -Filter *
```

- Obtener un usuario específico
```powershell
Get-ADUser -Identity usuario
```

- Crear un nuevo usuario
```powershell
New-ADUser -Name "Juan Perez" -GivenName Juan -Surname Perez -SamAccountName jperez -UserPrincipalName jperez@dominio.com -AccountPassword (ConvertTo-SecureString "Contraseña123" -AsPlainText -Force) -Enabled $true
```

- Modificar usuario
```powershell
Set-ADUser -Identity jperez -Title "Administrador de Sistemas"
```

- Deshabilitar usuario
```powershell
Disable-ADAccount -Identity jperez
```

- Eliminar usuario
```powershell
Remove-ADUser -Identity jperez
```

### Grupos

- Obtener todos los grupos
```powershell
Get-ADGroup -Filter *
```

- Crear grupo
```powershell
New-ADGroup -Name "Equipo-IT" -GroupScope Global -GroupCategory Security
```

- Añadir usuario a grupo
```powershell
Add-ADGroupMember -Identity "Equipo-IT" -Members jperez
```

- Eliminar usuario de grupo
```powershell
Remove-ADGroupMember -Identity "Equipo-IT" -Members jperez -Confirm:$false
```

### OU (Unidades Organizativas)

- Obtener OUs
```powershell
Get-ADOrganizationalUnit -Filter *
```

- Crear OU
```powershell
New-ADOrganizationalUnit -Name "DepartamentoVentas" -Path "DC=dominio,DC=com"
```

---

## 2. Microsoft Graph PowerShell

### Conectar con Microsoft Graph
```powershell
Connect-MgGraph -Scopes "User.Read.All", "Group.ReadWrite.All"
```

### Obtener usuarios
```powershell
Get-MgUser
```

### Crear usuario (ejemplo básico)
```powershell
New-MgUser -AccountEnabled $true -DisplayName "Juan Perez" -MailNickname "jperez" -UserPrincipalName "jperez@dominio.com" -PasswordProfile @{ ForceChangePasswordNextSignIn = $true; Password = "Contraseña123" }
```

### Obtener grupos
```powershell
Get-MgGroup
```

### Añadir miembro a grupo
```powershell
Add-MgGroupMember -GroupId <GroupId> -DirectoryObjectId <UserId>
```

---

## 3. Exchange Online PowerShell

### Conectar a Exchange Online
```powershell
Connect-ExchangeOnline -UserPrincipalName usuario@dominio.com
```

### Obtener buzones
```powershell
Get-Mailbox
```

### Ver detalles de un buzón
```powershell
Get-Mailbox -Identity usuario@dominio.com | Format-List
```

### Establecer reenvío
```powershell
Set-Mailbox -Identity usuario@dominio.com -ForwardingSmtpAddress usuario_destino@dominio.com
```

### Asignar permisos de buzón
```powershell
Add-MailboxPermission -Identity usuario@dominio.com -User otro_usuario@dominio.com -AccessRights FullAccess -InheritanceType All
```

### Ver reglas de bandeja de entrada
```powershell
Get-InboxRule -Mailbox usuario@dominio.com
```

### Quitar una regla
```powershell
Remove-InboxRule -Identity "Nombre de la regla" -Mailbox usuario@dominio.com
```

### Otorgar permiso de "Enviar como"
```powershell
Add-RecipientPermission -Identity usuario@dominio.com -Trustee otro_usuario@dominio.com -AccessRights SendAs
```

### Ver direcciones proxy (alias)
```powershell
Get-Mailbox usuario@dominio.com | Select-Object -ExpandProperty EmailAddresses
```

### Agregar un alias
```powershell
Set-Mailbox -Identity usuario@dominio.com -EmailAddresses @{add="alias@dominio.com"}
```

---
