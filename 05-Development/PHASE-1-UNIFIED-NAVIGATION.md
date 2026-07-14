# Phase 1 - Unified Navigation

Estado: Implementado en rama `phase-1-unified-navigation` de `tarevo-platform`.

## Objetivo

Unificar el acceso a los modulos existentes de Tenant ERP en una barra lateral persistente, eliminando accesos flotantes y evitando que el selector de empresa obstruya el contenido.

## Alcance

- Navegacion lateral persistente para pantallas bajo `/app`.
- Registro tipado de grupos, submodulos, rutas, iconos, permisos opcionales y modo de apertura.
- Rutas profundas basadas en React Router.
- Paginas standalone existentes renderizables en modo embedded dentro del shell.
- POS abierto mediante accion explicita del item de navegacion con fallback a `/pos`.
- Sidebar colapsable en escritorio con estado persistido en localStorage.
- Drawer movil con cierre por Escape y backdrop.
- Selector de empresa integrado en la barra lateral.

## Fuera de Alcance

- Asignacion de usuarios a cajas.
- Fusion de modulos duplicados.
- Cambios de reglas de POS, caja, ventas, inventario, billing o DTE.
- Cambios de permisos backend, roles, entitlements o contratos de API.
- Migraciones o cambios de modelo de datos.
- Nuevos endpoints.

## Mapa del Menu

- Inicio
  - Dashboard: `/app`
- Ventas y caja
  - Punto de venta: `/pos` con `openMode: popup`
  - Cajas y sesiones: `/app/cash`
  - Historial de ventas: `/app/sales`
  - Historial de devoluciones: `/app/refunds`
  - DTE Chile: `/app/dte`
  - Clientes: `/app/customers`
- Catalogo
  - Productos: `/app/catalog`
  - Catalogo web e integraciones: `/app/commerce`
- Inventario y logistica
  - Existencias y bodegas: `/app/inventory`
  - Inventario avanzado: `/app/inventory-control`
  - Picking y packing: `/app/picking-packing`
- Compras
  - Ordenes y proveedores: `/app/purchases`
- Reportes y control
  - Control y reportes: `/app/management`
  - Diagnostico operativo: `/app/operations`
- Administracion
  - Administracion: `/app/admin`
  - Plan y facturacion: `/app/billing`

## Rutas

`/app/*` entra siempre por `TenantShell`.

Las rutas internas se resuelven con React Router y no dependen de estado local de tab. Recargar una ruta como `/app/sales`, `/app/billing` o `/app/inventory-control` debe volver a la misma pantalla dentro del shell.

`/pos` se mantiene como ventana independiente para el flujo POS.

## Comportamiento Desktop, Tablet y Movil

Desktop:

- Sidebar persistente.
- Grupos desplegables.
- Estado activo por ruta.
- Colapsado recordado en `tarevo_tenant_sidebar_collapsed`.

Tablet:

- El contenido se reajusta sin superposicion de quick links.
- El shell mantiene el ancho del contenido con `minmax(0, 1fr)`.

Movil:

- La navegacion se abre como drawer desde el encabezado.
- Se cierra al seleccionar una opcion, con Escape o tocando el backdrop.
- El fondo queda bloqueado mientras el drawer esta abierto.

## Modulos Migrados Desde Botones Flotantes

- Catalogo e integraciones -> `/app/commerce`
- Devoluciones -> `/app/refunds`
- Inventario avanzado -> `/app/inventory-control`
- Facturacion y planes -> `/app/billing`
- Control y reportes -> `/app/management`
- Cierre operativo -> `/app/operations`

## Decisiones de Arquitectura

- `tenantNavigation.ts` es la fuente de verdad del menu.
- `tenantNavigationUtils.ts` resuelve item activo, titulo y grupo expandido desde la URL.
- `TenantShell` contiene el layout persistente y rutas internas.
- `TenantSidebar`, `SidebarGroup`, `SidebarItem` y `MobileNavigationDrawer` separan responsabilidades visuales.
- Las paginas que antes eran independientes aceptan `embedded` para ocultar encabezados globales y enlaces de retorno cuando se renderizan dentro del shell.
- `permissionKeys` queda preparado para Fase 4. En esta fase no se inventa filtrado de permisos si la sesion no trae capacidades tenant suficientes.

## Archivos Principales

- `apps/web/src/navigation/tenantNavigation.ts`
- `apps/web/src/navigation/tenantNavigationUtils.ts`
- `apps/web/src/shells/TenantShell.tsx`
- `apps/web/src/shells/navigation/TenantSidebar.tsx`
- `apps/web/src/shells/navigation/MobileNavigationDrawer.tsx`
- `apps/web/src/shells/TenantShell.css`
- `apps/web/src/TenantSwitcher.css`
- `apps/web/src/App.tsx`

## Criterios de Aceptacion

- No quedan quick links flotantes sobre `/app`.
- Todos los modulos existentes son accesibles desde la barra lateral.
- La ruta activa queda resaltada.
- Las categorias son desplegables.
- Las URLs profundas bajo `/app` funcionan.
- El selector de empresa no queda en posicion flotante sobre el contenido.
- El POS conserva apertura independiente.
- Login, logout y ProtectedRoute se mantienen.
- No hay cambios de backend ni reglas de negocio.
- Build y tests frontend pasan.

## Limitaciones Pendientes

Fase 2:

- Revisar consolidacion visual fina por modulo si se decide redisenar pantallas internas.

Fase 3:

- Agregar asignacion de usuarios a cajas cuando exista definicion funcional y backend correspondiente.

Fase 4:

- Conectar `permissionKeys` del menu a capacidades tenant completas cuando la sesion o un endpoint provea permisos suficientes.
- Definir comportamiento oficial para ocultar, deshabilitar o explicar cada modulo sin permiso o sin entitlement.
