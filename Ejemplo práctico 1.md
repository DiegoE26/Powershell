# 📸 Copia Automática de Carpetas de Fotos al NAS

¡Automatiza la copia de tus carpetas de fotos desde la tarjeta SD al NAS con este sencillo script en PowerShell!

---

## ⚙️ Configuración y Uso

```powershell
$sdFolderPath = "D:\DCIM"  # Ruta específica de la tarjeta SD donde están las carpetas
$nasPath = "\\Servidor\Ruta\FOTOS"  # Ruta de destino en el NAS

# Función para copiar carpetas cuyo nombre termina en MSDCF desde D:\DCIM al NAS
function Copy-FoldersToNAS {
    if (Test-Path $sdFolderPath) {
        # Obtener la fecha actual en formato YYYY-MM-DD
        $dateString = Get-Date -Format "yyyyMMdd_"

        # Obtener todas las carpetas dentro de D:\DCIM que terminan en MSDCF
        $folders = Get-ChildItem -Path $sdFolderPath -Directory | Where-Object { $_.Name -match "MSDCF$" }

        foreach ($folder in $folders) {
            # Generar el nuevo nombre de la carpeta con la fecha
            $newFolderName = "{0}{1}" -f $dateString, $folder.Name
            $destinationPath = Join-Path -Path $nasPath -ChildPath $newFolderName

            # Si la carpeta ya existe, solo copiar archivos nuevos sin sobrescribir
            if (Test-Path $destinationPath) {
                Write-Host "La carpeta '$newFolderName' ya existe. Añadiendo solo archivos nuevos..."
                Get-ChildItem -Path $folder.FullName -Recurse | ForEach-Object {
                    $targetFile = Join-Path -Path $destinationPath -ChildPath $_.FullName.Substring($folder.FullName.Length + 1)
                    if (!(Test-Path $targetFile)) {
                        Copy-Item -Path $_.FullName -Destination $targetFile -Force
                        Write-Host "Archivo '$_' añadido a '$destinationPath'"
                    }
                }
            } else {
                # Copiar la carpeta completa al NAS si no existe
                Copy-Item -Path $folder.FullName -Destination $destinationPath -Recurse -Force
                Write-Host "Carpeta '$($folder.Name)' copiada como '$newFolderName'"
            }
        }

        Write-Host "Proceso de copia completado."
    } else {
        Write-Host "La carpeta D:\DCIM no existe o la tarjeta SD no está conectada."
    }
}

Copy-FoldersToNAS
```

---

> 💡 **Consejo:**  
> Inserta tu tarjeta SD y ejecuta este script para respaldar tus fotos de forma rápida y organizada.

