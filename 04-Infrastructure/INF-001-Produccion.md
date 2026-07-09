# INF-001 - Infraestructura de Produccion

Documento: INF-001  
Version: 1.0  
Estado: Draft aprobado para Sprint 0

## 1. Objetivo

Definir la infraestructura inicial de Atlas para evitar que el proyecto sea desarrollado como una web de hosting compartido.

Atlas debe nacer como plataforma cloud portable, desplegable con Docker y preparada para escalar.

## 2. Decision principal

Infraestructura inicial recomendada:

```text
Dominio .com
Cloudflare DNS
Hetzner Cloud VPS
Coolify self-hosted
Docker
PostgreSQL
Redis
Cloudflare R2
Resend
GitHub
```

## 3. Dominio

Se recomienda usar dominio `.com` para no limitar la marca a Chile.

Ejemplos a evaluar:

- atlas.com si estuviera disponible.
- atlaspos.com.
- atlascommerce.com.
- getatlas.com.

## 4. DNS y Cloudflare

Cloudflare se usara para:

- DNS.
- Wildcard subdomains.
- Proteccion basica.
- Cache de assets.
- Reduccion de carga sobre el servidor.

Registro requerido:

```text
*.atlas.com -> servidor principal
atlas.com -> landing
www.atlas.com -> landing
```

## 5. Servidor

Proveedor inicial recomendado: Hetzner Cloud.

Configuracion inicial sugerida:

- 8 vCPU.
- 16 GB RAM.
- NVMe.
- Ubuntu.
- Docker.
- Coolify self-hosted.

La app principal, API, PostgreSQL, Redis y workers pueden vivir inicialmente en un solo servidor, separados logicamente por contenedores.

## 6. Coolify

Coolify se usara como panel de despliegue self-hosted.

Ventajas:

- Deploy desde GitHub.
- Manejo de servicios Docker.
- Variables de entorno.
- Bases de datos.
- SSL.
- Logs.
- Sin dependencia inicial de Vercel/Railway/Render.

## 7. Almacenamiento de archivos

No se guardaran archivos subidos por clientes en el disco local del VPS.

Cloudflare R2 sera el almacenamiento inicial para:

- Fotos de productos.
- Logos.
- Imagenes de catalogo.
- PDFs.
- XML.
- Adjuntos.

## 8. Almacenamiento por plan

Atlas podra vender almacenamiento incluido y adicional.

Ejemplo inicial:

```text
Starter: 2 GB
Pro: 20 GB
Business: 100 GB
Extras: +10 GB / +50 GB / +100 GB
```

Reglas:

- 80%: aviso.
- 90%: aviso fuerte y correo.
- 100%: bloquear nuevas subidas, sin bloquear ventas.
- Nunca impedir ventas por falta de espacio.

## 9. Correos transaccionales

Proveedor inicial: Resend.

Usos:

- Bienvenida.
- Verificacion de email.
- Recuperacion de contrasena.
- Pago fallido.
- Cuenta suspendida.
- Certificado por vencer.
- Limite DTE cercano.

## 10. Secretos

Ninguna clave se entrega por chat ni se sube al repositorio.

Variables esperadas:

```text
DATABASE_URL
REDIS_URL
RESEND_API_KEY
JWT_SECRET
REFRESH_TOKEN_SECRET
ENCRYPTION_KEY
CLOUDFLARE_R2_ACCESS_KEY_ID
CLOUDFLARE_R2_SECRET_ACCESS_KEY
R2_BUCKET_NAME
APP_URL
API_URL
```

## 11. Escalado futuro

Cuando Atlas crezca:

```text
Servidor 1: App/API
Servidor 2: PostgreSQL
Servidor 3: Workers/colas
R2: archivos
Cloudflare: DNS/cache/proteccion
```

## 12. Regla para Codex

Codex debe desarrollar Atlas usando Docker, variables de entorno y servicios desacoplados. No debe crear codigo pensado para cPanel, FTP, Hostinger o archivos persistentes locales.
