# 06 — Infrastructure

Documento: INF-001  
Version: 1.1  
Estado: Aprobado para Tarevo V1  
Fecha: 2026-07-09

## 1. Objetivo

Definir la infraestructura inicial de Tarevo para que el proyecto nazca como una plataforma cloud seria, portable, segura y escalable, sin caer en complejidad innecesaria ni gastos prematuros.

Tarevo no debe desarrollarse como una web para hosting compartido, cPanel, FTP o Hostinger. Debe desarrollarse como una aplicacion Dockerizada, portable y preparada para operar en produccion.

## 2. Principio rector

Simple primero. Escalable despues.

La infraestructura debe permitir crecer, pero no se contrataran servicios, servidores ni herramientas pagas antes de que exista una necesidad real.

Regla financiera:

Si un servicio no ayuda a vender, operar mejor, reducir riesgo real o atender clientes actuales, no entra en la V1.

## 3. Arquitectura inicial aprobada

```text
Usuario / Cliente
        |
Cloudflare DNS / Proxy / Cache
        |
Hetzner Cloud VPS
        |
Coolify self-hosted
        |
Docker
        |
Laravel API + React Frontend
        |
PostgreSQL
Redis
Workers / Queues
Scheduler
Storage local inicial
        |
Cloudflare R2 cuando se justifique
Resend cuando se implemente correo transaccional
```

## 4. Dominio

Dominio comprado:

- Dominio: gettarevo.com
- Costo: USD 10.46
- Vigencia: 1 ano
- Uso: dominio comercial inicial de Tarevo

Estructura objetivo:

```text
gettarevo.com              Landing publica
www.gettarevo.com          Landing publica
app.gettarevo.com          Aplicacion principal
api.gettarevo.com          API
status.gettarevo.com       Estado del sistema
 docs.gettarevo.com         Documentacion publica futura
```

Nota: la marca sera Tarevo. El prefijo `get` solo forma parte del dominio inicial.

## 5. Subdominios de clientes

Tarevo debe soportar subdominios por empresa.

Ejemplo:

```text
ferreteriagomez.app.gettarevo.com
supercool.app.gettarevo.com
```

Cada subdominio debe resolver el tenant correspondiente.

## 6. Dominios personalizados

Tarevo debe permitir que un cliente conecte un dominio o subdominio propio.

Ejemplos:

```text
erp.ferreteriagomez.cl
ventas.empresa.cl
tienda.empresa.cl
```

Reglas comerciales iniciales:

- Starter: solo subdominio de Tarevo.
- Pro: dominio propio incluido.
- Business: dominio propio incluido.
- Enterprise: multiples dominios segun contrato.

## 7. Cloudflare

Cloudflare se usara para:

- DNS.
- Wildcard subdomains.
- SSL.
- Proxy.
- Proteccion basica.
- Cache de assets publicos.
- Reduccion de carga sobre el VPS.

Registros objetivo:

```text
gettarevo.com                 -> landing
www.gettarevo.com             -> landing
app.gettarevo.com             -> app
*.app.gettarevo.com           -> tenants
api.gettarevo.com             -> API
status.gettarevo.com          -> status futuro
```

Plan inicial: gratuito.

No contratar Cloudflare Pro/Business hasta que exista una necesidad real de seguridad, reglas avanzadas o rendimiento.

## 8. Servidor

Proveedor inicial aprobado: Hetzner Cloud.

Configuracion inicial sugerida para produccion temprana:

- 8 vCPU.
- 16 GB RAM.
- NVMe.
- Ubuntu LTS.
- Docker.
- Coolify self-hosted.

La aplicacion principal, API, PostgreSQL, Redis, workers y scheduler pueden vivir inicialmente en un solo VPS, separados logicamente por contenedores.

No comprar servidor antes de que exista un MVP listo para desplegar.

## 9. Coolify

Coolify sera el panel self-hosted de despliegue.

Funciones:

- Deploy desde GitHub.
- Manejo de Docker.
- Variables de entorno.
- Servicios internos.
- Logs.
- SSL.
- Rollbacks simples.

Decision:

Usar Coolify self-hosted gratuito al inicio. No pagar Coolify Cloud hasta que administrar varios servidores lo justifique.

## 10. Docker

Toda la plataforma debe ejecutarse mediante Docker.

Servicios esperados:

```text
app                 Laravel + React build servido segun arquitectura final
postgres            PostgreSQL
redis               Redis
worker              Laravel queue worker
scheduler           Laravel scheduler
nginx/caddy         Reverse proxy si aplica
```

Codex debe desarrollar pensando en contenedores, no en FTP ni rutas locales de hosting compartido.

## 11. Base de datos

Base de datos aprobada: PostgreSQL.

Inicio:

- PostgreSQL dentro del VPS.
- Backups automatizados.
- Acceso restringido.
- Sin exposicion publica directa.

Escalado futuro:

- Separar PostgreSQL a servidor dedicado cuando el uso lo justifique.
- Evaluar managed database solo cuando el costo se compense con estabilidad y menor carga operativa.

## 12. Redis

Redis se deja preparado para:

- Cache.
- Queues.
- Rate limiting.
- Sesiones si se decide usarlo.

No debe usarse innecesariamente en la primera etapa si la app no lo requiere.

## 13. Workers y queues

Tarevo debe usar colas para tareas pesadas.

Ejemplos:

- Enviar correos.
- Importar Excel/CSV.
- Generar PDFs.
- Generar reportes pesados.
- Procesar DTE.
- Sincronizaciones futuras.
- Calculo de metricas.

El usuario no debe esperar procesos largos en pantalla.

## 14. Scheduler

Usar Laravel Scheduler para tareas programadas.

Usos:

- Recordatorios de pago.
- Suspension progresiva.
- Limpieza de archivos temporales.
- Backups.
- Alertas de certificados.
- Alertas de almacenamiento.
- Alertas de limites de DTE.

## 15. WebSockets

No implementar WebSockets en V1.

Motivo:

- Aumentan complejidad operativa.
- No son indispensables para validar el producto.
- Pueden agregarse luego si se necesita tiempo real real.

Alternativa V1:

- Polling moderado.
- Refetch controlado.
- Notificaciones normales.

## 16. Storage

Decision de costos:

- Inicio: almacenamiento local controlado para desarrollo y primeras pruebas.
- Produccion con clientes: preparar abstraccion para migrar a Cloudflare R2 sin reescribir modulos.
- No guardar archivos de clientes de forma permanente sin una estrategia clara de backups.

Cloudflare R2 se usara para:

- Fotos de productos.
- Logos.
- Imagenes de catalogo.
- PDFs.
- XML.
- Adjuntos.

## 17. Almacenamiento por plan

Recursos aprobados:

```text
Starter: 5 GB
Pro: 25 GB
Business: 100 GB
Enterprise: personalizado
```

Reglas:

- 80%: aviso visual.
- 90%: aviso visual + correo.
- 100%: bloquear nuevas subidas.
- Nunca bloquear ventas por falta de almacenamiento.

## 18. Correos transaccionales

Proveedor inicial: Resend.

No crear cuenta ni configurar Resend hasta que se implemente:

- Verificacion de email.
- Recuperacion de contrasena.
- Invitaciones.
- Alertas de pago.

Usos futuros:

- Bienvenida.
- Verificacion.
- Recuperacion de contrasena.
- Pago fallido.
- Cuenta suspendida.
- Certificado por vencer.
- Limite DTE cercano.

## 19. Backups

Backups obligatorios desde la primera version con datos reales.

Reglas:

- Backups diarios de PostgreSQL.
- Retencion minima inicial: 7 dias.
- Backups fuera del servidor principal cuando haya clientes reales.
- Prueba periodica de restauracion.

No basta con generar backups. Debe probarse que se pueden restaurar.

## 20. Monitoreo y salud del sistema

Tarevo debe tener un panel interno de salud.

Servicios a monitorear:

- App.
- API.
- PostgreSQL.
- Redis.
- Workers.
- Scheduler.
- Storage.
- Correos.
- Backups.

V1 puede iniciar con health checks simples y logs centralizados basicos.

## 21. Variables de entorno

Variables esperadas:

```text
APP_NAME=Tarevo
APP_ENV
APP_URL
API_URL
DATABASE_URL
REDIS_URL
RESEND_API_KEY
JWT_SECRET
REFRESH_TOKEN_SECRET
ENCRYPTION_KEY
CLOUDFLARE_R2_ACCESS_KEY_ID
CLOUDFLARE_R2_SECRET_ACCESS_KEY
R2_BUCKET_NAME
DTE_PROVIDER_API_KEY
PAYMENT_PROVIDER_API_KEY
```

Regla absoluta:

Ningun secreto se guarda en GitHub, frontend, chat, documentacion publica o codigo fuente.

## 22. Servicios que NO entran en V1

Prohibidos salvo decision aprobada:

- Kubernetes.
- Microservicios.
- Kafka.
- RabbitMQ.
- Elasticsearch.
- Redis Cloud.
- Managed PostgreSQL pago.
- Vercel.
- Railway.
- Render.
- Multiples VPS sin necesidad.
- Servicios de IA pagos.
- WebSockets complejos.

## 23. Escalado futuro

Fase 1:

```text
1 VPS: App + API + PostgreSQL + Redis + Workers
```

Fase 2:

```text
Servidor 1: App/API
Servidor 2: PostgreSQL
R2: archivos
```

Fase 3:

```text
Servidor 1: App/API
Servidor 2: PostgreSQL
Servidor 3: Workers
Balanceador
R2
Monitoreo dedicado
```

Fase 4:

Evaluar servicios gestionados solo si reducen riesgo y el MRR lo justifica.

## 24. Regla para Codex

Codex debe desarrollar Tarevo usando Docker, variables de entorno, servicios desacoplados y arquitectura portable.

Codex no debe:

- Crear una version demo no productiva.
- Hardcodear secretos.
- Guardar archivos permanentes sin abstraccion de storage.
- Asumir Hostinger, cPanel, FTP o hosting compartido.
- Implementar microservicios en V1.
- Instalar servicios pagos sin aprobacion.

## 25. Estado del documento

Este documento queda aprobado como guia de infraestructura para Tarevo V1.

Cambios futuros requieren actualizacion del ADL.
