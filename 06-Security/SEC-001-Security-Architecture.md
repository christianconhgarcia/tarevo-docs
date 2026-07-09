# SEC-001 - Security Architecture

Documento: SEC-001  
Version: 1.0  
Estado: Draft aprobado para Sprint 0

## 1. Principio

Atlas se disenara bajo el principio Secure by Design.

La seguridad no se agregara despues. Debe existir desde el inicio en autenticacion, base de datos, infraestructura, archivos, pagos, DTE, APIs y auditoria.

## 2. Amenaza asumida

Atlas debe asumir que sera atacado.

Amenazas esperadas:

- Fuerza bruta en login.
- Robo de sesiones.
- Acceso cruzado entre empresas.
- Exposicion de claves.
- Subida de archivos maliciosos.
- Ataques a APIs.
- Abuso de formularios publicos.
- Intentos de modificar precios, pagos o DTE.

## 3. Autenticacion

Requisitos:

- Passwords con Argon2 o bcrypt.
- Nunca guardar contrasenas en texto plano.
- Recuperacion de contrasena con token seguro de un solo uso.
- Expiracion de tokens.
- Rate limiting en login.
- Bloqueo temporal por intentos fallidos.
- Verificacion de email.
- 2FA preparado para futuro.

## 4. Sesiones

- Usar access token de corta duracion.
- Refresh token seguro.
- Rotacion de refresh tokens.
- Cierre de sesion por dispositivo.
- Revocacion de sesiones desde el panel.

## 5. Permisos

- Validacion de permisos en backend, no solo frontend.
- Roles por empresa.
- Permisos por App.
- Entitlements por plan.
- Ninguna ruta critica puede depender solo de la UI.

## 6. Multiempresa

Regla absoluta:

Un usuario de una empresa nunca puede ver, consultar, modificar o inferir datos de otra empresa.

Toda consulta debe filtrar por `company_id` o mecanismo equivalente.

## 7. Secretos

Prohibido:

- Claves en codigo.
- Claves en GitHub.
- Claves en frontend.
- Claves en chat.
- Certificados sin cifrar.

Permitido:

- Variables de entorno.
- Coolify Secrets.
- GitHub Secrets.
- Cifrado en base de datos con clave maestra fuera de la DB.

## 8. Certificados y DTE

Los certificados digitales de clientes deben:

- Subirse mediante canal seguro.
- Guardarse cifrados.
- Usarse solo en procesos autorizados.
- Auditar cada uso.
- Alertar vencimiento.

## 9. Archivos

Archivos en R2:

- Validar tipo.
- Validar tamano.
- Renombrar archivos.
- No confiar en extension.
- Asociar siempre a empresa.
- URLs firmadas si aplica.

## 10. Auditoria

Registrar:

- Login.
- Logout.
- Fallos de login.
- Cambios de precio.
- Cambios de stock.
- Cambios de plan.
- Cambios de permisos.
- Emision DTE.
- Anulacion de tickets.
- Notas de credito.
- Cierre de caja.
- Subida/eliminacion de archivos.

## 11. Infraestructura

- HTTPS obligatorio.
- Firewall.
- Cloudflare.
- Backups automaticos.
- Logs de errores.
- Health checks.
- Monitoreo de servicios.

## 12. Regla para Codex

Codex no debe implementar endpoints sin autenticacion, no debe crear datos globales sin aislamiento multiempresa y no debe omitir validaciones en backend.
