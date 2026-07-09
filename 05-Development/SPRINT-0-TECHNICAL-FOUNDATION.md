# Sprint 0 — Technical Foundation

Estado: Aprobado para inicio de desarrollo
Prioridad: Critica

## Objetivo
Crear la base tecnica minima y correcta para que todos los slices de Tarevo puedan desarrollarse sobre una arquitectura estable, segura y portable.

## Stack aprobado

- Backend: Laravel.
- Frontend: React + TypeScript + Vite.
- Base de datos: PostgreSQL.
- Cache/colas: Redis preparado.
- Infraestructura local: Docker Compose.
- Infraestructura produccion: Hetzner + Coolify + Docker + Cloudflare.
- Arquitectura: monolito modular.

## Entregables Sprint 0

### 1. Repositorio base

Crear estructura de proyecto preparada para monolito modular.

Carpetas sugeridas:

```text
/apps
  /api
  /web
/packages
  /shared
  /ui
  /config
/infra
/docs
```

Si se decide monorepo Laravel + React en una sola raiz, debe mantenerse separacion clara entre backend, frontend e infraestructura.

### 2. Docker local

Servicios minimos:

- app/api.
- web.
- postgres.
- redis.
- queue worker.
- scheduler.

### 3. Backend base

Debe incluir:

- Laravel instalado.
- Configuracion env.
- PostgreSQL.
- Migraciones base.
- Auth base.
- Multi-tenant base.
- Middleware tenant resolver.
- Auditoria base.
- Permisos base.
- Eventos base.
- Health check.

### 4. Frontend base

Debe incluir:

- React + TypeScript + Vite.
- Router.
- Layout base.
- Auth pages.
- Tenant shell.
- SuperAdmin shell preparado.
- UI base.
- Cliente API.
- Manejo de errores.
- Loading states.

### 5. Seguridad base

- Cookies HttpOnly o mecanismo aprobado seguro.
- CSRF si aplica.
- Rate limiting.
- Validacion de tenant en backend.
- Password hashing seguro.
- Recuperacion de contrasena preparada.

### 6. Multi-tenant base

Toda entidad de negocio debe usar tenant_id.

Regla: ninguna query de negocio puede ejecutarse sin contexto tenant salvo SuperAdmin con permiso explicito.

### 7. Roles y permisos base

Implementar:

- roles.
- permissions.
- role_permissions.
- user_tenant_roles.
- entitlements por plan.

### 8. Auditoria base

Toda accion critica debe generar audit log con:

- tenant_id.
- actor_id.
- action.
- entity_type.
- entity_id.
- previous_data si aplica.
- new_data si aplica.
- ip/user agent si aplica.
- timestamp.

### 9. Eventos base

Crear infraestructura para publicar eventos internos aunque inicialmente se procesen dentro del mismo monolito.

### 10. Testing base

- Tests backend.
- Tests frontend basicos.
- Test de tenant isolation.
- Test de permisos.
- Test de login.

## Prohibido en Sprint 0

- Implementar modulos funcionales grandes.
- DTE.
- WebSockets.
- Microservicios.
- Kubernetes.
- Integraciones externas pagas.
- Guardar secretos en codigo.

## Definition of Done

Sprint 0 termina cuando:

- El proyecto corre localmente con Docker.
- Backend responde health check.
- Frontend carga login.
- Usuario puede autenticarse.
- Tenant resolver funciona.
- Permisos base funcionan.
- PostgreSQL funciona.
- Redis preparado.
- Tests base pasan.
- README tecnico permite levantar el proyecto sin preguntar.

## Prompt para Codex
Construye Sprint 0 de Tarevo siguiendo la documentacion en tarevo-docs. No implementar funcionalidades de negocio fuera de la base tecnica. Priorizar arquitectura limpia, Docker, multi-tenant, auth, permisos, auditoria, eventos y tests base.
