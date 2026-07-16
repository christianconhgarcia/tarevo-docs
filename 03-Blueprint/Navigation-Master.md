# Navigation Master

Version: 0.6
Estado: Aprobado y alineado con production

## Objetivo

Definir la navegación principal vigente de Tarevo y registrar las consolidaciones realizadas durante el desarrollo.

## Mundos de Tarevo

Tarevo se divide en tres mundos:

1. Public Website.
2. Tenant ERP.
3. SuperAdmin Console.

Ninguna funcionalidad debe mezclarse entre mundos sin una justificación explícita.

## Public Website

Navegación y superficies públicas vigentes:

- Inicio: `/`.
- Producto y módulos: secciones del landing.
- DTE Chile: sección del landing.
- Planes: sección `#precios` del landing.
- Comparativa: `/compare`.
- FAQ: sección `#preguntas` del landing.
- Login: `/login`.
- Registro: `/register`.
- Verificación: `/verify-email`.
- Recuperación: `/forgot-password` y `/reset-password`.
- Invitaciones: `/accept-invitation`.

Flujo principal:

```text
Landing
  -> Planes o Comparativa
  -> Registro
  -> Verificar correo
  -> Onboarding
  -> Empresa / sucursal / bodega / caja
  -> Primer producto
  -> Apertura de caja
  -> Primera venta
```

Decisiones de consolidación:

- Planes permanece dentro del landing.
- FAQ permanece dentro del landing.
- La comparativa sí tiene ruta independiente.
- La gestión de suscripción permanece dentro del Tenant ERP autenticado.
- El portal público del cliente se posterga hasta validar su necesidad durante beta.

## Tenant ERP

Navegación principal vigente:

### Dashboard

- Dashboard financiero para usuarios con `reports.view`.
- Dashboard operativo para usuarios sin acceso a información financiera global.

### Ventas y caja

- Punto de venta.
- Cajas y sesiones.
- Historial de ventas.
- Devoluciones.
- DTE Chile.
- Clientes.

### Catálogo

- Productos.
- Categorías, marcas, precios e importación consolidados dentro de Productos.
- Variantes y lotes.
- Catálogo web e integraciones.

### Inventario y logística

- Existencias.
- Kardex y trazabilidad.
- Ubicaciones.
- Transferencias.
- Conteos físicos.
- Picking y packing.

### Compras

- Órdenes, proveedores y recepciones.

### Reportes

- Reportes.
- Preparación de la empresa / diagnóstico operativo.

### Administración

- Empresa y usuarios.
- Roles y permisos.
- Invitaciones.
- Asignaciones usuario-sucursal-caja.
- Plan, facturación y soporte.

## Rutas vigentes del Tenant ERP

- `/app` — Dashboard.
- `/app/catalog` — Productos y gestión consolidada de catálogo.
- `/app/catalog/variants` — Variantes y lotes.
- `/app/catalog/integrations` — Catálogo web e integraciones.
- `/app/purchases` — Compras y proveedores.
- `/app/inventory` — Existencias.
- `/app/inventory/kardex` — Kardex y trazabilidad.
- `/app/inventory/locations` — Ubicaciones.
- `/app/inventory/transfers` — Transferencias.
- `/app/inventory/counts` — Conteos físicos.
- `/app/picking-packing` — Picking y packing.
- `/app/pos` — Acceso POS dentro del shell.
- `/pos` — POS standalone.
- `/app/cash` — Cajas y sesiones.
- `/app/sales` — Historial de ventas.
- `/app/sales/refunds` — Devoluciones.
- `/app/dte` — DTE Chile.
- `/app/customers` — Clientes.
- `/app/reports` — Reportes.
- `/app/reports/operations` — Preparación operativa.
- `/app/admin` — Empresa, usuarios, roles y permisos.
- `/app/admin/billing` — Plan, facturación y soporte.

## Redirects legacy obligatorios

- `/app/commerce` → `/app/catalog/integrations`.
- `/app/refunds` → `/app/sales/refunds`.
- `/app/inventory-control` → `/app/inventory/kardex`.
- `/app/management` → `/app/reports`.
- `/app/operations` → `/app/reports/operations`.
- `/app/billing` → `/app/admin/billing`.
- `/app/catalog/products` → `/app/catalog`.
- `/app/catalog/categories` → `/app/catalog`.
- `/app/catalog/brands` → `/app/catalog`.
- `/app/catalog/pricing` → `/app/catalog`.
- `/app/catalog/import` → `/app/catalog`.

## Evolución implementada

### Fase 1 — Navegación unificada

- Shell persistente bajo `/app/*`.
- Sidebar de escritorio.
- Drawer móvil.
- Selector de empresa.
- POS independiente.

### Fase 2 — Agrupación funcional

- Reorganización por función del negocio.
- Consolidación de rutas.
- Redirects legacy.

### Fase 3 — Asignaciones operativas

- Asignación de usuario a sucursal y caja dentro de Administración.
- No se crea una ruta principal duplicada.

### Fase 4 — Permisos y navegación dinámica

- Navegación filtrada por permisos efectivos.
- Protección de rutas profundas y acciones.
- Grupos vacíos ocultos.
- Soporte multi-rol.

### Fase 5 — Cierre operativo

- Dashboard adaptado por permisos.
- Diagnóstico operativo.
- Arqueo ciego.
- Cierre funcional V1.

### Fase 6 — Consolidación de plataforma

- Comparativa pública en `/compare`.
- Ficha integral desde `SuperAdmin > Empresas > Ver detalle`.
- Configuración global dentro de SuperAdmin.
- Actualización documental del estado real del producto.

Detalle: `05-Development/PHASE-6-PLATFORM-CONSOLIDATION.md`.

## SuperAdmin Console

Navegación principal vigente:

- Dashboard global.
- Empresas.
  - Listado.
  - Detalle de empresa.
- Suscripciones.
- Customer Success.
- Tickets de soporte.
- Landing CMS.
- Feature Flags.
- Infraestructura.
- Configuración global.

Ruta adicional:

- `/superadmin/operations` — operación interna, almacenamiento, actividad y errores críticos.

## Regla de implementación

Toda pantalla nueva debe declarar:

- mundo;
- módulo;
- ruta o ubicación;
- permisos o alcance de plataforma;
- relación con pantallas consolidadas;
- dependencia externa, cuando exista.
