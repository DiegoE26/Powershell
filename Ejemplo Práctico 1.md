# Automatización de Salas en Exchange Online

Este documento describe cómo automatizar la creación de salas y su agrupación en una Room List en Exchange Online usando PowerShell.

## Pasos

1. **Conectar a Exchange Online**
2. **Leer el archivo CSV con las salas**
3. **Crear cada sala si no existe**
4. **Crear una Room List (grupo de salas)**
5. **Agregar todas las salas al Room List**

---

```powershell
# Paso 1: Conectar a Exchange Online
Write-Host "Conectando a Exchange Online..." -ForegroundColor Cyan
Connect-ExchangeOnline -UserPrincipalName admin@tudominio.com

# Paso 2: Leer el archivo CSV
$salas = Import-Csv -Path "./salas.csv"

# Paso 3: Crear cada sala
foreach ($sala in $salas) {
    Write-Host "Creando sala: $($sala.Name) con alias $($sala.Alias)" -ForegroundColor Green
    
    # Verifica si ya existe
    $existe = Get-Mailbox -Identity $sala.Alias -ErrorAction SilentlyContinue
    if ($existe) {
        Write-Host "  ➤ Ya existe, omitiendo..." -ForegroundColor Yellow
        continue
    }

    # Crear la sala
    New-Mailbox -Name $sala.Name -Alias $sala.Alias -Room
}

# Paso 4: Crear Room List (grupo de salas)
$roomListName = "Todas las Salas"
$roomListAlias = "todaslasalas"

# Verificar si ya existe
$roomList = Get-DistributionGroup -Identity $roomListAlias -ErrorAction SilentlyContinue
if (!$roomList) {
    Write-Host "Creando Room List '$roomListName'..." -ForegroundColor Cyan
    New-DistributionGroup -Name $roomListName -Alias $roomListAlias -RoomList
} else {
    Write-Host "Room List '$roomListName' ya existe." -ForegroundColor Yellow
}

# Paso 5: Agregar todas las salas al Room List
foreach ($sala in $salas) {
    try {
        Add-DistributionGroupMember -Identity $roomListAlias -Member $sala.Alias -ErrorAction Stop
        Write-Host "  ➤ Agregada $($sala.Alias) al grupo '$roomListAlias'" -ForegroundColor Green
    } catch {
        Write-Host "  ⚠️ Ya estaba en el grupo o falló: $($sala.Alias)" -ForegroundColor Yellow
    }
}

Write-Host "✅ Proceso completo." -ForegroundColor Cyan
```
