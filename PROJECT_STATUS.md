# Tarevo Project Status

Version: 0.1
Estado: Vivo

## Producto

- Marca: Tarevo
- Dominio: gettarevo.com
- Mercado inicial: Chile
- Modelo: SaaS ERP para PYMEs
- Estado: Product Specification / PRD inicial

## Hitos

| Hito | Nombre | Estado |
|---|---|---|
| HITO-01 | Empresa | Completado |
| HITO-02 | Arquitectura | Completado |
| HITO-03 | Blueprint | Cerrado conceptualmente |
| HITO-04 | PRD / Product Specification | En progreso |
| HITO-05 | Desarrollo | No iniciado |
| HITO-06 | QA | No iniciado |
| HITO-07 | Beta | No iniciado |
| HITO-08 | Produccion | No iniciado |

## Decisiones principales

- Marca: Tarevo.
- Dominio: gettarevo.com.
- Backend: Laravel.
- Frontend: React + TypeScript + Vite.
- Base de datos: PostgreSQL.
- Arquitectura: monolito modular.
- Infraestructura objetivo: Cloudflare + Hetzner + Coolify + Docker.
- Storage inicial: local con abstraccion hacia Cloudflare R2.
- Redis: preparado, usar cuando aporte valor.
- WebSockets: no V1.
- SuperAdmin separado de Tenant ERP.
- Public Website administrable por bloques desde SuperAdmin.

## Riesgos pendientes

- Registrar marca Tarevo en INAPI.
- Definir proveedor DTE.
- Definir proveedor de pagos.
- Confirmar costos reales de servidor.
- Definir politica final de soporte y SLA.

## Proximo trabajo

PRD EPIC-01: Del visitante a la primera venta.

## Regla operativa

Si una decision no esta documentada y aprobada, no se implementa.
