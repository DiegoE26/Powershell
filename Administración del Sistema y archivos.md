## Comandos de PowerShell para Administración del Sistema

A continuación se presentan comandos comunes para la administración del sistema en PowerShell, junto con una breve explicación de cada uno:

| Comando                  | Descripción                                                                                  |
|--------------------------|----------------------------------------------------------------------------------------------|
| `Get-Process`            | Obtiene una lista de los procesos en ejecución en el sistema.                                |
| `Stop-Process`           | Detiene uno o más procesos en ejecución.                                                     |
| `Start-Process`          | Inicia un nuevo proceso.                                                                    |
| `Get-Service`            | Muestra información sobre los servicios instalados.                                          |
| `Start-Service`          | Inicia un servicio detenido.                                                                |
| `Stop-Service`           | Detiene un servicio en ejecución.                                                           |
| `Restart-Service`        | Reinicia un servicio.                                                                       |
| `Set-Service`            | Cambia la configuración de un servicio.                                                     |
| `Get-EventLog`           | Obtiene eventos de los registros de eventos clásicos de Windows.                            |
| `Clear-EventLog`         | Borra todos los eventos de un registro de eventos.                                          |
| `Get-WinEvent`           | Recupera eventos de los registros de eventos y proveedores de eventos.                      |
| `Get-ComputerInfo`       | Muestra información detallada del sistema.                                                  |
| `Restart-Computer`       | Reinicia el equipo local o remoto.                                                          |
| `Stop-Computer`          | Apaga el equipo local o remoto.                                                             |
| `Get-LocalUser`          | Obtiene usuarios locales del sistema.                                                       |
| `New-LocalUser`          | Crea un nuevo usuario local.                                                                |
| `Remove-LocalUser`       | Elimina un usuario local.                                                                   |
| `Set-LocalUser`          | Modifica las propiedades de un usuario local.                                               |
| `Get-LocalGroup`         | Muestra los grupos locales del sistema.                                                     |
| `Add-LocalGroupMember`   | Agrega un usuario o grupo a un grupo local.                                                 |
| `Remove-LocalGroupMember`| Elimina un usuario o grupo de un grupo local.                                               |
| `Get-HotFix`             | Muestra las actualizaciones instaladas en el sistema.                                       |
| `Get-Command`            | Lista todos los comandos disponibles en PowerShell.                                         |
| `Get-Help`               | Muestra ayuda sobre comandos de PowerShell.                                                 |
| `Set-ExecutionPolicy`    | Cambia la política de ejecución de scripts de PowerShell.                                   |
| `Get-ExecutionPolicy`    | Muestra la política de ejecución actual.                                                    |
| `Get-InstalledModule`    | Lista los módulos instalados.                                                               |
| `Install-Module`         | Instala un módulo desde un repositorio.                                                     |
| `Update-Module`          | Actualiza un módulo instalado.                                                              |
| `Get-ScheduledTask`      | Muestra las tareas programadas en el sistema.                                               |
| `Register-ScheduledTask` | Crea una nueva tarea programada.                                                            |
| `Unregister-ScheduledTask`| Elimina una tarea programada.                                                              |
| `Get-EventSubscriber`    | Muestra los suscriptores de eventos registrados.                                            |
| `Register-ObjectEvent`   | Registra un evento para un objeto.                                                          |
| `Unregister-Event`       | Elimina la suscripción a un evento.                                                         |
| `Get-Job`                | Muestra los trabajos en segundo plano.                                                      |
| `Start-Job`              | Inicia un nuevo trabajo en segundo plano.                                                   |
| `Stop-Job`               | Detiene un trabajo en segundo plano.                                                        |
| `Receive-Job`            | Recupera los resultados de un trabajo en segundo plano.                                     |
| `Remove-Job`             | Elimina un trabajo en segundo plano.                                                        |
| `Get-PSDrive`            | Muestra las unidades de PowerShell disponibles.                                             |
| `New-PSDrive`            | Crea una nueva unidad de PowerShell.                                                        |
| `Remove-PSDrive`         | Elimina una unidad de PowerShell.                                                           |
| `Get-PSSession`          | Muestra las sesiones remotas activas.                                                       |
| `New-PSSession`          | Crea una nueva sesión remota.                                                               |
| `Remove-PSSession`       | Elimina una sesión remota.                                                                  |
| `Enter-PSSession`        | Inicia una sesión interactiva remota.                                                       |
| `Exit-PSSession`         | Finaliza una sesión interactiva remota.                                                     |
| `Invoke-Command`         | Ejecuta comandos en equipos locales o remotos.                                              |
| `Get-Variable`           | Muestra las variables de PowerShell.                                                        |
| `Set-Variable`           | Crea o modifica una variable.                                                               |
| `Remove-Variable`        | Elimina una variable.                                                                       |
| `Get-Module`             | Muestra los módulos cargados o disponibles.                                                 |
| `Import-Module`          | Importa un módulo a la sesión actual.                                                       |
| `Remove-Module`          | Elimina un módulo de la sesión actual.                                                      |
| `Get-WmiObject`          | Obtiene información de administración de Windows (WMI).                                     |
| `Set-WmiInstance`        | Modifica instancias de WMI.                                                                 |
| `Remove-WmiObject`       | Elimina instancias de WMI.                                                                  |
| `Get-CimInstance`        | Obtiene información de administración de Windows (CIM).                                     |
| `Set-CimInstance`        | Modifica instancias de CIM.                                                                 |
| `Remove-CimInstance`     | Elimina instancias de CIM.                                                                  |

---

## Comandos de PowerShell para Administración de Archivos

A continuación se muestran comandos esenciales para la administración de archivos en PowerShell, junto con una breve descripción de su función:

| Comando             | Descripción                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| `Get-ChildItem`     | Lista archivos y carpetas en un directorio.                                 |
| `Get-Item`          | Obtiene información sobre un archivo o carpeta específico.                  |
| `Set-Item`          | Cambia el valor de un archivo o carpeta.                                    |
| `Remove-Item`       | Elimina archivos o carpetas.                                                |
| `Copy-Item`         | Copia archivos o carpetas a otra ubicación.                                 |
| `Move-Item`         | Mueve archivos o carpetas a otra ubicación.                                 |
| `Rename-Item`       | Cambia el nombre de un archivo o carpeta.                                   |
| `New-Item`          | Crea un nuevo archivo o carpeta.                                            |
| `Clear-Item`        | Borra el contenido de un archivo o carpeta.                                 |
| `Get-Content`       | Muestra el contenido de un archivo.                                         |
| `Set-Content`       | Reemplaza el contenido de un archivo.                                       |
| `Add-Content`       | Agrega contenido a un archivo existente.                                    |
| `Clear-Content`     | Elimina todo el contenido de un archivo.                                    |
| `Out-File`          | Envía la salida de un comando a un archivo.                                 |
| `Out-String`        | Convierte la salida en una cadena de texto.                                 |
| `Test-Path`         | Verifica si una ruta existe.                                                |
| `Split-Path`        | Divide una ruta en sus componentes.                                         |
| `Join-Path`         | Combina partes de una ruta en una sola.                                     |
| `Resolve-Path`      | Muestra la ruta completa de un archivo o carpeta.                           |
| `Convert-Path`      | Convierte una ruta relativa en absoluta.                                    |
| `Get-Location`      | Muestra el directorio actual.                                               |
| `Set-Location`      | Cambia el directorio actual.                                                |
| `Push-Location`     | Guarda la ubicación actual y cambia a otra.                                 |
| `Pop-Location`      | Vuelve a la ubicación guardada previamente.                                 |
| `New-PSDrive`       | Crea una nueva unidad de PowerShell.                                        |
| `Remove-PSDrive`    | Elimina una unidad de PowerShell.                                           |
| `Get-Acl`           | Obtiene los permisos de archivos o carpetas.                                |
| `Set-Acl`           | Cambia los permisos de archivos o carpetas.                                 |
| `Get-FileHash`      | Calcula el hash de un archivo.                                              |
| `Compress-Archive`  | Comprime archivos o carpetas en un archivo ZIP.                             |
| `Expand-Archive`    | Extrae archivos de un archivo ZIP.                                          |
| `Get-Unique`        | Filtra elementos duplicados de una lista.                                   |
| `Measure-Object`    | Realiza cálculos (conteo, suma, promedio) sobre objetos.                    |
| `Select-String`     | Busca texto dentro de archivos.                                             |
| `Export-Csv`        | Exporta datos a un archivo CSV.                                             |
| `Import-Csv`        | Importa datos desde un archivo CSV.                                         |
| `Export-Clixml`     | Exporta objetos a un archivo XML.                                           |
| `Import-Clixml`     | Importa objetos desde un archivo XML.                                       |
| `Format-Table`      | Da formato tabular a la salida.                                             |
| `Format-List`       | Da formato de lista a la salida.                                            |
| `Format-Wide`       | Muestra la salida en columnas anchas.                                       |

---

### Ejemplo visual de uso

```powershell
# Listar archivos en el directorio actual
Get-ChildItem

# Copiar un archivo
Copy-Item -Path archivo.txt -Destination C:\Backup\archivo.txt

# Buscar una palabra en archivos de texto
Select-String -Path *.txt -Pattern "PowerShell"
```
