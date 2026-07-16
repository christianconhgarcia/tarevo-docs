# Screen Registry

Version: 0.6
Estado: Aprobado y actualizado con la implementación V1

## Objetivo

Inventariar las pantallas oficiales de Tarevo. Ninguna pantalla nueva puede desarrollarse sin declarar su mundo, módulo, ruta y alcance de acceso.

## Convención

- SCR: Screen
- PW: Public Website
- TE: Tenant ERP
- SA: SuperAdmin Console

## Public Website

| ID | Mundo | Módulo | Pantalla | Ruta / ubicación | Prioridad | V1 | Estado |
|---|---|---|---|---|---|---|---|
| SCR-PW-001 | Public Website | Marketing | Landing | `/` | Alta | Sí | Implementada |
| SCR-PW-002 | Public Website | Marketing | Planes | Sección `#precios` del landing | Alta | Sí | Consolidada |
| SCR-PW-003 | Public Website | Marketing | Comparativa | `/compare` | Media | Sí | Implementada en Fase 6 |
| SCR-PW-004 | Public Website | Auth | Registro | `/register` | Alta | Sí | Implementada |
| SCR-PW-005 | Public Website | Auth | Login | `/login` | Alta | Sí | Implementada |
| SCR-PW-006 | Public Website | Auth | Recuperar contraseña | `/forgot-password` y `/reset-password` | Alta | Sí | Implementada |
| SCR-PW-007 | Public Website | Auth | Verificar correo | `/verify-email` | Alta | Sí | Implementada |
| SCR-PW-008 | Public Website | Customer Portal | Portal del cliente | Sin ruta | Baja | No beta inicial | Postergada |
| SCR-PW-009 | Public Website | Customer Portal | Gestión de suscripción | `/app/admin/billing` autenticado | Alta | Sí | Consolidada en Tenant ERP |
| SCR-PW-010 | Public Website | CMS | FAQ pública | Sección `#preguntas` del landing | Media | Sí | Consolidada |

## Tenant ERP

| ID | Mundo | Módulo | Pantalla | Ruta / ubicación | Prioridad | V1 | Estado |
|---|---|---|---|---|---|---|---|
| SCR-TE-001 | Tenant ERP | Dashboard | Inicio | `/app` | Alta | Sí | Implementada |
| SCR-TE-002 | Tenant ERP | Onboarding | Checklist inicial | `/onboarding` | Alta | Sí | Implementada |
| SCR-TE-003 | Tenant ERP | Empresa | Crear empresa | Onboarding / Administración | Alta | Sí | Implementada |
| SCR-TE-004 | Tenant ERP | Sucursales | Crear sucursal | Onboarding / Administración | Alta | Sí | Implementada |
| SCR-TE-005 | Tenant ERP | Bodegas | Crear bodega | Onboarding / Inventario | Alta | Sí | Implementada |
| SCR-TE-006 | Tenant ERP | Caja | Crear caja | Onboarding / Caja | Alta | Sí | Implementada |
| SCR-TE-007 | Tenant ERP | Productos | Listado | `/app/catalog` | Alta | Sí | Implementada |
| SCR-TE-008 | Tenant ERP | Productos | Crear producto | Acción dentro de `/app/catalog` | Alta | Sí | Implementada |
| SCR-TE-009 | Tenant ERP | Productos | Editar producto | Acción dentro de `/app/catalog` | Alta | Sí | Implementada |
| SCR-TE-010 | Tenant ERP | Productos | Categorías | Sección dentro de `/app/catalog` | Media | Sí | Consolidada |
| SCR-TE-011 | Tenant ERP | Productos | Marcas | Sección dentro de `/app/catalog` | Media | Sí | Consolidada |
| SCR-TE-012 | Tenant ERP | Inventario | Stock | `/app/inventory` | Alta | Sí | Implementada |
| SCR-TE-013 | Tenant ERP | Inventario | Kardex | `/app/inventory/kardex` | Alta | Sí | Implementada |
| SCR-TE-014 | Tenant ERP | Inventario | Ajustes | Flujo dentro de Inventario/Kardex | Alta | Sí | Consolidada |
| SCR-TE-015 | Tenant ERP | Warehouse | Bodegas | Inventario / Administración | Alta | Sí | Implementada |
| SCR-TE-016 | Tenant ERP | Warehouse | Ubicaciones | `/app/inventory/locations` | Alta | Sí | Implementada |
| SCR-TE-017 | Tenant ERP | Warehouse | Transferencias | `/app/inventory/transfers` | Alta | Sí | Implementada |
| SCR-TE-018 | Tenant ERP | Warehouse | Picking y packing | `/app/picking-packing` | Media | Sí | Implementada |
| SCR-TE-019 | Tenant ERP | POS | Venta rápida | `/pos` y `/app/pos` | Alta | Sí | Implementada |
| SCR-TE-020 | Tenant ERP | Caja | Apertura | `/app/cash` | Alta | Sí | Implementada |
| SCR-TE-021 | Tenant ERP | Caja | Cierre | `/app/cash` | Alta | Sí | Implementada |
| SCR-TE-022 | Tenant ERP | Caja | Arqueo | `/app/cash` | Alta | Sí | Implementada con arqueo ciego |
| SCR-TE-023 | Tenant ERP | Ventas | Historial | `/app/sales` | Alta | Sí | Implementada |
| SCR-TE-024 | Tenant ERP | Ventas | Detalle venta | Flujo dentro de `/app/sales` | Alta | Sí | Implementada |
| SCR-TE-025 | Tenant ERP | Clientes | Listado | `/app/customers` | Alta | Sí | Implementada |
| SCR-TE-026 | Tenant ERP | Clientes | Ficha cliente | Flujo dentro de `/app/customers` | Media | Sí | Implementada |
| SCR-TE-027 | Tenant ERP | Compras | Órdenes y proveedores | `/app/purchases` | Media | Sí | Implementada |
| SCR-TE-028 | Tenant ERP | Compras | Recepción | Flujo dentro de `/app/purchases` | Media | Sí | Implementada |
| SCR-TE-029 | Tenant ERP | Reportes | Ventas | `/app/reports` | Alta | Sí | Implementada |
| SCR-TE-030 | Tenant ERP | Reportes | Inventario | `/app/reports` | Alta | Sí | Implementada |
| SCR-TE-031 | Tenant ERP | Reportes | Caja | `/app/reports` | Alta | Sí | Implementada |
| SCR-TE-032 | Tenant ERP | Configuración | Empresa | `/app/admin` | Alta | Sí | Implementada |
| SCR-TE-033 | Tenant ERP | Configuración | Usuarios | `/app/admin` | Alta | Sí | Implementada |
| SCR-TE-034 | Tenant ERP | Configuración | Roles y permisos | `/app/admin` | Alta | Sí | Implementada |
| SCR-TE-035 | Tenant ERP | Configuración | DTE | `/app/dte` | Alta | Sí | Interfaz implementada; proveedor externo pendiente |
| SCR-TE-036 | Tenant ERP | Ventas | Historial de devoluciones | `/app/sales/refunds` | Alta | Sí | Implementada |
| SCR-TE-037 | Tenant ERP | Catálogo | Variantes y lotes | `/app/catalog/variants` | Media | Sí | Implementada |
| SCR-TE-038 | Tenant ERP | Catálogo | Importación | Acción dentro de `/app/catalog` | Alta | Sí | Implementada |
| SCR-TE-039 | Tenant ERP | Catálogo | Integraciones | `/app/catalog/integrations` | Media | Sí | Implementada |
| SCR-TE-040 | Tenant ERP | Inventario | Conteos físicos | `/app/inventory/counts` | Alta | Sí | Implementada |
| SCR-TE-041 | Tenant ERP | Reportes | Preparación operativa | `/app/reports/operations` | Media | Sí | Implementada |
| SCR-TE-042 | Tenant ERP | Administración | Plan, facturación y soporte | `/app/admin/billing` | Alta | Sí | Implementada; Flow externo pendiente |

## Consolidación de rutas

Las rutas legacy se mantienen como redirects cuando corresponde:

- `/app/commerce` → `/app/catalog/integrations`
- `/app/refunds` → `/app/sales/refunds`
- `/app/inventory-control` → `/app/inventory/kardex`
- `/app/management` → `/app/reports`
- `/app/operations` → `/app/reports/operations`
- `/app/billing` → `/app/admin/billing`
- `/app/catalog/products` → `/app/catalog`
- `/app/catalog/categories` → `/app/catalog`
- `/app/catalog/brands` → `/app/catalog`
- `/app/catalog/pricing` → `/app/catalog`
- `/app/catalog/import` → `/app/catalog`

## SuperAdmin Console

| ID | Mundo | Módulo | Pantalla | Ruta / ubicación | Prioridad | V1 | Estado |
|---|---|---|---|---|---|---|---|
| SCR-SA-001 | SuperAdmin | Dashboard | Inicio global | `/superadmin` > Dashboard global | Alta | Sí | Implementada |
| SCR-SA-002 | SuperAdmin | Empresas | Listado | `/superadmin` > Empresas | Alta | Sí | Implementada |
| SCR-SA-003 | SuperAdmin | Empresas | Detalle empresa | `/superadmin` > Empresas > Ver detalle | Alta | Sí | Implementada en Fase 6 |
| SCR-SA-004 | SuperAdmin | Planes | Listado planes | Suscripciones / Configuración global | Alta | Sí | Consolidada |
| SCR-SA-005 | SuperAdmin | Planes | Entitlements | Suscripciones y límites efectivos | Alta | Sí | Implementada en backend; resumen consolidado |
| SCR-SA-006 | SuperAdmin | Billing | Suscripciones | `/superadmin` > Suscripciones | Alta | Sí | Implementada |
| SCR-SA-007 | SuperAdmin | Billing | Pagos | Suscripciones / proveedor externo | Alta | Sí | Parcial; Flow pendiente |
| SCR-SA-008 | SuperAdmin | Customer Success | Onboarding clientes | `/superadmin` > Customer Success | Alta | Sí | Implementada |
| SCR-SA-009 | SuperAdmin | Soporte | Tickets | `/superadmin` > Tickets de soporte | Alta | Sí | Implementada |
| SCR-SA-010 | SuperAdmin | CMS | Landing CMS | `/superadmin` > Landing CMS | Media | Sí | Implementada |
| SCR-SA-011 | SuperAdmin | Infraestructura | Health checks | `/superadmin` > Infraestructura y `/superadmin/operations` | Alta | Sí | Implementada |
| SCR-SA-012 | SuperAdmin | Feature Flags | Funciones | `/superadmin` > Feature Flags | Media | Sí | Implementada |
| SCR-SA-013 | SuperAdmin | Configuración | Global | `/superadmin` > Configuración global | Alta | Sí | Implementada en Fase 6 |

## Regla

El Screen Registry se amplía por Epic o fase. El ID de una pantalla nunca debe cambiar aunque cambie su nombre visible, ubicación o nivel de consolidación.
