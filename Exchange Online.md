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

## 👥 Consultar miembros de una lista de distribución dinámica

```powershell
Get-Recipient -RecipientPreviewFilter (Get-DynamicDistributionGroup "CTAG-Responsables departamento").RecipientFilter
```

_Muestra los miembros reales de una lista de distribución dinámica._

---

## 🔍 Filtrar usuarios por atributos personalizados

```powershell
Get-Mailbox -Filter {CustomAttribute5 -like "DTSD"}
```

_Obtiene los usuarios cuyo valor del atributo 5 sea `DTSD`._

```powershell
(Get-Mailbox -Filter {(CustomAttribute5 -like "DTC") -or (CustomAttribute5 -like "SORD")}).COUNT
```

_Muestra el número de usuarios que cumplen con `DTC` o `SORD` en el atributo 5._

---

## 🛠️ Modificar reglas de distribución dinámica

```powershell
Set-DynamicDistributionGroup -Identity "CTAG-Responsables Departamento" -RecipientFilter '((CustomAttribute5 -eq "DTC") -or (CustomAttribute5 -eq "SORD")) -and (-not(Name -like "SystemMailbox{{*")) -and (-not(Name -like "CAS_{{*")) -and (-not(RecipientTypeDetailsValue -eq "MailboxPlan")) -and (-not(RecipientTypeDetailsValue -eq "DiscoveryMailbox")) -and (-not(RecipientTypeDetailsValue -eq "PublicFolderMailbox")) -and (-not(RecipientTypeDetailsValue -eq "ArbitrationMailbox")) -and (-not(RecipientTypeDetailsValue -eq "AuditLogMailbox")) -and (-not(RecipientTypeDetailsValue -eq "AuxAuditLogMailbox")) -and (-not(RecipientTypeDetailsValue -eq "SupervisoryReviewPolicyMailbox"))'
```

_Modifica la regla de filtrado de la lista de distribución dinámica `CTAG-Responsables Departamento`._

---

## 📧 Reglas de transporte de correo

```powershell
New-TransportRule -Name "Reenvio Ped" -RecipientAddressContainsWords "pedidos@domain" -BlindCopyTo "ventas@domain"
```

_Crea una nueva regla de correo que reenvía mensajes enviados a `pedidos@domain` con copia oculta a `ventas@domain`._

```powershell
Set-TransportRule "Reenvio Ped" -SentTo "pedidos@domain"
```

_Modifica las condiciones de envío de la regla de transporte "Reenvio Ped"._

---

## 📅 Eliminar eventos del calendario

```powershell
Remove-CalendarEvents -Identity "usuario@domain" -CancelOrganizedMeetings -QueryStartDate "2023-01-01"
```

_Elimina todas las reuniones organizadas por el usuario desde la fecha indicada. **El usuario debe seguir existiendo en Exchange.**_

---
