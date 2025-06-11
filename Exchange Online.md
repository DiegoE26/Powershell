# 📦 Gestión de Exchange Online con PowerShell

## 📥 Instalar Módulo

```powershell
Install-Module -Name ExchangeOnlineManagement
```

_Instala el módulo de PowerShell necesario para conectarse a Exchange Online._

---

## 🔌 Conectar con Exchange

```powershell
Connect-ExchangeOnline -UserPrincipalName usuario@domain
```

_Abre la conexión con Exchange usando tu UPN._

---


### 👥 Gestión de Buzones de Correo

#### Obtener todos los buzones
```powershell
Get-Mailbox
```

#### Obtener buzones con licencia
```powershell
Get-Mailbox -RecipientTypeDetails UserMailbox
```

#### Ver detalles de un buzón
```powershell
Get-Mailbox -Identity usuario@dominio.com | Format-List
```
#### Establecer reenvío de correo
```powershell
Set-Mailbox -Identity usuario@dominio.com -ForwardingSmtpAddress usuario_destino@dominio.com
```

#### Asignar permisos de buzón a otro usuario
```powershell
Add-MailboxPermission -Identity usuario@dominio.com -User otro_usuario@dominio.com -AccessRights FullAccess -InheritanceType All
```

---

## 👥 Consultar miembros de una lista de distribución dinámica

```powershell
Get-Recipient -RecipientPreviewFilter (Get-DynamicDistributionGroup DistributionList").RecipientFilter
```

_Muestra los miembros reales de una lista de distribución dinámica._

---

## 🔍 Filtrar usuarios por atributos personalizados

```powershell
Get-Mailbox -Filter {CustomAttribute5 -like "Atributte"}
```

_Obtiene los usuarios cuyo valor del atributo 5 sea `Atributte`._

```powershell
(Get-Mailbox -Filter {(CustomAttribute5 -like "Atributte") -or (CustomAttribute5 -like "Atributte2")}).COUNT
```

_Muestra el número de usuarios que cumplen con `Atributte` o `Atributte2` en el atributo 5._

---

## 🛠️ Modificar reglas de distribución dinámica

```powershell
Set-DynamicDistributionGroup -Identity "DistributionList" -RecipientFilter '((CustomAttribute5 -eq "DTC") -or (CustomAttribute5 -eq "SORD")) -and (-not(Name -like "SystemMailbox{{*")) -and (-not(Name -like "CAS_{{*")) -and (-not(RecipientTypeDetailsValue -eq "MailboxPlan")) -and (-not(RecipientTypeDetailsValue -eq "DiscoveryMailbox")) -and (-not(RecipientTypeDetailsValue -eq "PublicFolderMailbox")) -and (-not(RecipientTypeDetailsValue -eq "ArbitrationMailbox")) -and (-not(RecipientTypeDetailsValue -eq "AuditLogMailbox")) -and (-not(RecipientTypeDetailsValue -eq "AuxAuditLogMailbox")) -and (-not(RecipientTypeDetailsValue -eq "SupervisoryReviewPolicyMailbox"))'
```

_Modifica la regla de filtrado de la lista de distribución dinámica `DistributionList`._

---

## 📧 Reglas de transporte de correo

```powershell
New-TransportRule -Name "Reenvio Ped" -RecipientAddressContainsWords "mail1" -BlindCopyTo "mail2"
```

_Crea una nueva regla de correo que reenvía mensajes enviados a `mail1` con copia oculta a `mail2`._

```powershell
Set-TransportRule "Reenvio Ped" -SentTo "mail"
```

_Modifica las condiciones de envío de la regla de transporte "Reenvio Ped"._

#### Ver reglas de bandeja de entrada
```powershell
Get-InboxRule -Mailbox usuario@dominio.com
```

#### Quitar una regla
```powershell
Remove-InboxRule -Identity "Nombre de la regla" -Mailbox usuario@dominio.com
```


---

## 📅 Eliminar eventos del calendario

```powershell
Remove-CalendarEvents -Identity "usuario@domain" -CancelOrganizedMeetings -QueryStartDate "2023-01-01"
```

_Elimina todas las reuniones organizadas por el usuario desde la fecha indicada. **El usuario debe seguir existiendo en Exchange.**_

---

### 🔐 Permisos y Delegaciones

#### Otorgar permiso de "Enviar como"
```powershell
Add-RecipientPermission -Identity usuario@dominio.com -Trustee otro_usuario@dominio.com -AccessRights SendAs
```

#### Otorgar permiso de "Enviar en nombre de"
```powershell
Set-Mailbox -Identity usuario@dominio.com -GrantSendOnBehalfTo otro_usuario@dominio.com
```

---

### 📬 Alias y Direcciones de Correo

#### Ver direcciones de correo (proxy addresses)
```powershell
Get-Mailbox usuario@dominio.com | Select-Object -ExpandProperty EmailAddresses
```

#### Agregar un alias
```powershell
Set-Mailbox -Identity usuario@dominio.com -EmailAddresses @{add="alias@dominio.com"}
```

---

### 📊 Cuotas y Tamaños de Buzón

#### Ver uso del buzón
```powershell
Get-MailboxStatistics -Identity usuario@dominio.com
```

#### Establecer límites de buzón
```powershell
Set-Mailbox -Identity usuario@dominio.com -IssueWarningQuota 1.9GB -ProhibitSendQuota 2GB -ProhibitSendReceiveQuota 2.3GB
```

---

### 🚫 Litigio y Retención

#### Activar retención por litigio (Litigation Hold)
```powershell
Set-Mailbox -Identity usuario@dominio.com -LitigationHoldEnabled $true
```

---

### 🪩 Eliminación de Buzones y Usuarios

#### Deshabilitar un buzón (no borra usuario)
```powershell
Disable-Mailbox -Identity usuario@dominio.com
```

#### Eliminar permanentemente un buzón (deshabilitado previamente)
```powershell
Remove-Mailbox -Identity usuario@dominio.com
```

---
