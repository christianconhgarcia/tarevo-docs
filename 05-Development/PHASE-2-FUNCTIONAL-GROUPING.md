# Phase 2 - Functional Grouping

Version: 0.1
Estado: Implementado localmente

## Objetivo

Agrupar la navegacion del Tenant ERP por funcion real de negocio, conservando la navegacion unificada de Fase 1 y sin modificar backend, APIs, migraciones ni reglas de negocio.

## Alcance

- Corregir el colapso real de categorias del sidebar.
- Reubicar rutas visibles bajo grupos funcionales.
- Mantener redirects desde rutas legacy de Fase 1.
- Reutilizar pantallas y componentes existentes.
- Mantener el drawer movil equivalente al sidebar desktop.
- Mantener intacto el popup POS.

Fuera de alcance:

- Asignacion usuario-caja.
- Menu dinamico por permisos.
- Nuevos endpoints.
- Cambios en modelos, migraciones o reglas de negocio.

## Causa raiz del sidebar

Las categorias se renderizaban con `hidden`, pero la regla CSS de la lista interna definia `display: grid` y anulaba el comportamiento nativo de `[hidden]`. Ademas, el grupo activo se reinyectaba en el set expandido durante cada render, lo que impedia cerrar manualmente la categoria activa.

Fix aplicado:

- Regla explicita `.tenant-nav-group__items[hidden] { display: none; }`.
- Persistencia de grupos abiertos en `localStorage`.
- Apertura automatica solo cuando cambia el grupo activo de ruta.
- Cierre manual permitido incluso en la categoria activa.
- Drawer movil usa la misma fuente de navegacion.

## Mapa funcional

| Grupo | Rutas principales |
|---|---|
| Inicio | `/app` |
| Ventas y caja | `/app/pos`, `/app/cash-register`, `/app/sales`, `/app/sales/refunds`, `/app/dte`, `/app/customers` |
| Catalogo | `/app/catalog`, `/app/catalog/categories`, `/app/catalog/brands`, `/app/catalog/variants`, `/app/catalog/pricing`, `/app/catalog/import`, `/app/catalog/integrations` |
| Inventario y logistica | `/app/inventory`, `/app/inventory/kardex`, `/app/inventory/locations`, `/app/inventory/transfers`, `/app/inventory/counts`, `/app/picking` |
| Compras | `/app/purchases` |
| Reportes | `/app/reports`, `/app/reports/operations` |
| Administracion | `/app/admin`, `/app/admin/billing` |

## Redirects legacy

| Legacy | Nuevo destino |
|---|---|
| `/app/commerce` | `/app/catalog/integrations` |
| `/app/refunds` | `/app/sales/refunds` |
| `/app/inventory-control` | `/app/inventory/kardex` |
| `/app/management` | `/app/reports` |
| `/app/operations` | `/app/reports/operations` |
| `/app/billing` | `/app/admin/billing` |

Los redirects preservan `search` y `hash`.

## Duplicados y consolidacion

- Productos, categorias, marcas, variantes, precios e importacion viven bajo Catalogo.
- Existencias, kardex, ubicaciones, transferencias y conteos viven bajo Inventario y logistica.
- Devoluciones queda bajo Ventas y caja.
- Billing queda bajo Administracion.
- Reportes y diagnostico operativo quedan bajo Reportes.
- La vista legacy de estructura operativa no queda expuesta como tab principal de Inventario.

## Validacion esperada

- `npm ci`
- `npm test`
- `npm run build`
- `npm audit`
- Tests backend si existen y el entorno local los permite.
- `docker compose -f docker-compose.yml config`
- `docker compose -f docker-compose.production.yml config` cuando exista la configuracion de entorno requerida.
- QA visual desktop/tablet/mobile.
