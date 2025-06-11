# Gestión de Exchange Online con PowerShell
¡Lleva la administración de Exchange Online al siguiente nivel usando PowerShell!

---

## Ventajas de gestionar Exchange Online con PowerShell

- **Automatización avanzada**: Ejecuta tareas rutinarias y complejas de forma automática, ahorrando tiempo y esfuerzo.
- **Gestión masiva**: Modifica, crea o elimina múltiples usuarios y buzones simultáneamente con comandos sencillos.
- **Personalización total**: Adapta scripts a las necesidades específicas de tu organización para una administración a medida.
- **Acceso a funciones avanzadas**: Configura opciones y parámetros que no están disponibles en la interfaz gráfica.
- **Mayor control y precisión**: Minimiza errores humanos y garantiza una gestión consistente y eficiente.
- **Compatibilidad con MFA**: PowerShell para Exchange Online es totalmente compatible con la autenticación multifactor (MFA), garantizando seguridad y cumplimiento en el acceso.

> **Gestiona Exchange Online de manera profesional, optimizando procesos y mejorando la productividad.**

---

### Ejemplos de uso

```powershell
# Obtener todos los buzones activos
Get-Mailbox -ResultSize Unlimited

# Restablecer la contraseña de un usuario
Set-Mailbox -Identity usuario@dominio.com -Password (ConvertTo-SecureString -String "NuevaContraseña123" -AsPlainText -Force)

# Habilitar el reenvío de correo para un usuario
Set-Mailbox -Identity usuario@dominio.com -ForwardingSMTPAddress "otro@dominio.com"
```
