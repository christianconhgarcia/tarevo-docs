# Screen Registry

Version: 0.1
Estado: Aprobado como estructura inicial

## Objetivo
Inventariar las pantallas oficiales de Tarevo. Ninguna pantalla puede desarrollarse si no existe en este registro.

## Convencion

- SCR: Screen
- PW: Public Website
- TE: Tenant ERP
- SA: SuperAdmin Console

## Public Website

| ID | Mundo | Modulo | Pantalla | Prioridad | V1 |
|---|---|---|---|---|---|
| SCR-PW-001 | Public Website | Marketing | Landing | Alta | Si |
| SCR-PW-002 | Public Website | Marketing | Planes | Alta | Si |
| SCR-PW-003 | Public Website | Marketing | Comparativa | Media | Si |
| SCR-PW-004 | Public Website | Auth | Registro | Alta | Si |
| SCR-PW-005 | Public Website | Auth | Login | Alta | Si |
| SCR-PW-006 | Public Website | Auth | Recuperar contrasena | Alta | Si |
| SCR-PW-007 | Public Website | Auth | Verificar correo | Alta | Si |
| SCR-PW-008 | Public Website | Customer Portal | Portal del cliente | Alta | Si |
| SCR-PW-009 | Public Website | Customer Portal | Gestion de suscripcion | Alta | Si |
| SCR-PW-010 | Public Website | CMS | FAQ publica | Media | Si |

## Tenant ERP

| ID | Mundo | Modulo | Pantalla | Prioridad | V1 |
|---|---|---|---|---|---|
| SCR-TE-001 | Tenant ERP | Dashboard | Inicio | Alta | Si |
| SCR-TE-002 | Tenant ERP | Onboarding | Checklist inicial | Alta | Si |
| SCR-TE-003 | Tenant ERP | Empresa | Crear empresa | Alta | Si |
| SCR-TE-004 | Tenant ERP | Sucursales | Crear sucursal | Alta | Si |
| SCR-TE-005 | Tenant ERP | Bodegas | Crear bodega | Alta | Si |
| SCR-TE-006 | Tenant ERP | Caja | Crear caja | Alta | Si |
| SCR-TE-007 | Tenant ERP | Productos | Listado | Alta | Si |
| SCR-TE-008 | Tenant ERP | Productos | Crear producto | Alta | Si |
| SCR-TE-009 | Tenant ERP | Productos | Editar producto | Alta | Si |
| SCR-TE-010 | Tenant ERP | Productos | Categorias | Media | Si |
| SCR-TE-011 | Tenant ERP | Productos | Marcas | Media | Si |
| SCR-TE-012 | Tenant ERP | Inventario | Stock | Alta | Si |
| SCR-TE-013 | Tenant ERP | Inventario | Kardex | Alta | Si |
| SCR-TE-014 | Tenant ERP | Inventario | Ajustes | Alta | Si |
| SCR-TE-015 | Tenant ERP | Warehouse | Bodegas | Alta | Si |
| SCR-TE-016 | Tenant ERP | Warehouse | Ubicaciones | Alta | Si |
| SCR-TE-017 | Tenant ERP | Warehouse | Transferencias | Alta | Si |
| SCR-TE-018 | Tenant ERP | Warehouse | Picking | Media | Si |
| SCR-TE-019 | Tenant ERP | POS | Venta rapida | Alta | Si |
| SCR-TE-020 | Tenant ERP | Caja | Apertura | Alta | Si |
| SCR-TE-021 | Tenant ERP | Caja | Cierre | Alta | Si |
| SCR-TE-022 | Tenant ERP | Caja | Arqueo | Alta | Si |
| SCR-TE-023 | Tenant ERP | Ventas | Historial | Alta | Si |
| SCR-TE-024 | Tenant ERP | Ventas | Detalle venta | Alta | Si |
| SCR-TE-025 | Tenant ERP | Clientes | Listado | Alta | Si |
| SCR-TE-026 | Tenant ERP | Clientes | Ficha cliente | Media | Si |
| SCR-TE-027 | Tenant ERP | Compras | Ordenes | Media | Si |
| SCR-TE-028 | Tenant ERP | Compras | Recepcion | Media | Si |
| SCR-TE-029 | Tenant ERP | Reportes | Ventas | Alta | Si |
| SCR-TE-030 | Tenant ERP | Reportes | Inventario | Alta | Si |
| SCR-TE-031 | Tenant ERP | Reportes | Caja | Alta | Si |
| SCR-TE-032 | Tenant ERP | Configuracion | Empresa | Alta | Si |
| SCR-TE-033 | Tenant ERP | Configuracion | Usuarios | Alta | Si |
| SCR-TE-034 | Tenant ERP | Configuracion | Roles y permisos | Alta | Si |
| SCR-TE-035 | Tenant ERP | Configuracion | DTE | Alta | Si |

### Pantallas incorporadas al shell persistente en Fase 1

Estas pantallas ya existian en producto y quedaron accesibles desde la navegacion unificada:

| Ruta | Mundo | Modulo | Pantalla |
|---|---|---|---|
| `/app/commerce` | Tenant ERP | Catalogo | Catalogo web e integraciones |
| `/app/refunds` | Tenant ERP | Ventas | Historial de devoluciones |
| `/app/inventory-control` | Tenant ERP | Inventario | Inventario avanzado |
| `/app/billing` | Tenant ERP | Administracion | Plan y facturacion |
| `/app/management` | Tenant ERP | Reportes | Control y reportes |
| `/app/operations` | Tenant ERP | Operaciones | Diagnostico operativo |

## SuperAdmin Console

| ID | Mundo | Modulo | Pantalla | Prioridad | V1 |
|---|---|---|---|---|---|
| SCR-SA-001 | SuperAdmin | Dashboard | Inicio global | Alta | Si |
| SCR-SA-002 | SuperAdmin | Empresas | Listado | Alta | Si |
| SCR-SA-003 | SuperAdmin | Empresas | Detalle empresa | Alta | Si |
| SCR-SA-004 | SuperAdmin | Planes | Listado planes | Alta | Si |
| SCR-SA-005 | SuperAdmin | Planes | Entitlements | Alta | Si |
| SCR-SA-006 | SuperAdmin | Billing | Suscripciones | Alta | Si |
| SCR-SA-007 | SuperAdmin | Billing | Pagos | Alta | Si |
| SCR-SA-008 | SuperAdmin | Customer Success | Onboarding clientes | Alta | Si |
| SCR-SA-009 | SuperAdmin | Soporte | Tickets | Alta | Si |
| SCR-SA-010 | SuperAdmin | CMS | Landing CMS | Media | Si |
| SCR-SA-011 | SuperAdmin | Infraestructura | Health checks | Alta | Si |
| SCR-SA-012 | SuperAdmin | Feature Flags | Funciones | Media | Si |
| SCR-SA-013 | SuperAdmin | Configuracion | Global | Alta | Si |

## Regla
El Screen Registry se ampliara por Epic. El ID de una pantalla nunca debe cambiar aunque cambie su nombre visible.
