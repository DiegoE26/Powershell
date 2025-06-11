# Gestión de Active Directory con PowerShell

La gestión de **Active Directory (AD)** mediante **PowerShell** es una práctica esencial para los administradores de sistemas modernos. PowerShell proporciona una interfaz de línea de comandos poderosa y flexible que permite automatizar tareas administrativas, mejorar la eficiencia y reducir errores humanos. Gracias a sus cmdlets específicos para AD, es posible administrar usuarios, grupos, equipos y políticas de manera rápida y centralizada, incluso en entornos grandes y complejos.

---

## Beneficios principales

- ⚡ **Automatización**: Ejecuta tareas repetitivas en segundos mediante scripts.
- 👥 **Gestión masiva**: Administra múltiples objetos simultáneamente con un solo comando.
- 🔒 **Seguridad**: Aplica cambios de forma controlada y auditable, minimizando riesgos.
- 📈 **Eficiencia**: Ahorra tiempo y recursos en la administración diaria.

---

## Ejemplos prácticos

- **Crear un nuevo usuario:**
    ```powershell
    New-ADUser -Name "Juan Pérez" -SamAccountName jperez -AccountPassword (Read-Host -AsSecureString "Contraseña") -Enabled $true
    ```

- **Agregar un usuario a un grupo:**
    ```powershell
    Add-ADGroupMember -Identity "TI" -Members jperez
    ```

- **Listar todos los usuarios activos:**
    ```powershell
    Get-ADUser -Filter {Enabled -eq $true}
    ```

- **Restablecer la contraseña de un usuario:**
    ```powershell
    Set-ADAccountPassword -Identity jperez -Reset -NewPassword (Read-Host -AsSecureString "Nueva contraseña")
    ```

> ¡PowerShell es la herramienta clave para una administración moderna, eficiente y segura de Active Directory!

