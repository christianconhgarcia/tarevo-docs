# Codex Prompt — Sprint 0 Technical Foundation

Usa este prompt en Codex cuando el repositorio `tarevo-platform` este creado.

## Prompt

Actua como arquitecto senior full-stack. Implementa Sprint 0 de Tarevo siguiendo estrictamente la documentacion del repositorio `tarevo-docs`.

Documentos obligatorios a leer antes de escribir codigo:

1. `00-Constitution/Atlas-Constitution.md` o su version actual equivalente de Tarevo.
2. `04-Infrastructure/INF-001-Produccion.md`.
3. `06-Security/SEC-001-Security-Architecture.md`.
4. `03-Blueprint/Permission-Matrix.md`.
5. `03-Blueprint/Business-Rules-Registry.md`.
6. `03-Blueprint/Event-Registry.md`.
7. `03-Blueprint/API-Registry.md`.
8. `05-Development/SPRINT-0-TECHNICAL-FOUNDATION.md`.
9. `05-Development/DEVELOPER-PLAYBOOK.md`.
10. `05-Development/CODING-STANDARDS.md`.

## Objetivo Sprint 0

Crear la base tecnica de Tarevo, no funcionalidades completas de negocio.

Debe quedar listo:

- Laravel backend.
- React + TypeScript + Vite frontend.
- Docker local.
- PostgreSQL.
- Redis preparado.
- Autenticacion base.
- Multi-tenant base.
- Middleware tenant resolver.
- Roles y permisos base.
- Entitlements base.
- Auditoria base.
- Eventos internos base.
- Health checks.
- Tests minimos.

## Stack obligatorio

- Backend: Laravel.
- Frontend: React + TypeScript + Vite.
- DB: PostgreSQL.
- Cache/colas: Redis preparado.
- Infra: Docker Compose local.
- Arquitectura: monolito modular.

## Restricciones

No implementar:

- DTE.
- Certificado SII.
- WooCommerce.
- Mercado Libre.
- IA.
- Microservicios.
- Kubernetes.
- WebSockets.
- POS fisico.
- Funcionalidades V2.

## Criterios de aceptacion

- El proyecto corre localmente con Docker.
- Backend responde `/health`.
- Frontend carga pantalla de login.
- Login base funciona.
- Tenant isolation tiene test.
- Permisos base tienen test.
- PostgreSQL funciona.
- Redis preparado.
- README tecnico explica como levantar el proyecto.
- No hay secretos hardcodeados.

## Regla

Si falta informacion, no inventes reglas de negocio. Crea una seccion `OPEN_QUESTIONS.md` con preguntas concretas y continua solo con lo que este definido.
