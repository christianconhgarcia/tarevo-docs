# Tarevo Project Status

Version: 0.6
Estado: Desarrollo activo / V1 funcional cerrada

## Producto

- Marca: Tarevo
- Dominio: gettarevo.com
- Mercado inicial: Chile
- Modelo: SaaS ERP para PYMEs
- Estado actual: V1 funcional implementada, consolidación de plataforma y preparación de integraciones externas

## Hitos

| Hito | Nombre | Estado |
|---|---|---|
| HITO-01 | Empresa | Completado |
| HITO-02 | Arquitectura | Completado |
| HITO-03 | Blueprint | Cerrado conceptualmente; actualización continua |
| HITO-04 | PRD / Product Specification | Implementado para V1; continúa por incrementos |
| HITO-05 | Desarrollo | V1 funcional completada; mejoras continuas |
| HITO-06 | QA | En progreso |
| HITO-07 | Beta | Pendiente de piloto controlado |
| HITO-08 | Producción | Infraestructura desplegada; activaciones externas y validación final pendientes |

## Decisiones principales

- Marca: Tarevo.
- Dominio: gettarevo.com.
- Backend: Laravel.
- Frontend: React + TypeScript + Vite.
- Base de datos: PostgreSQL.
- Arquitectura: monolito modular.
- Infraestructura objetivo: Cloudflare + Hetzner + Coolify + Docker.
- Storage inicial: local con abstracción hacia Cloudflare R2.
- Redis: activo para colas, caché y coordinación cuando aporta valor.
- WebSockets: no V1.
- SuperAdmin separado de Tenant ERP.
- Public Website administrable por bloques desde SuperAdmin.
- La autorización efectiva se resuelve en backend por tenant; el frontend solo adapta navegación y experiencia.
- POS funciona como superficie standalone y también conserva acceso protegido desde el shell.
- Productos, categorías, marcas, precios e importación se consolidan en una sola experiencia de Catálogo.

## Estado funcional V1

Implementado en la rama productiva:

- Landing, registro, verificación de correo, login y recuperación de contraseña.
- Onboarding y aprovisionamiento automático de empresa, sucursal, bodega y caja.
- Dashboard financiero y dashboard operativo adaptado a permisos.
- Productos, categorías, marcas, variantes, precios e importación CSV.
- Proveedores, órdenes de compra y recepciones.
- Inventario, Kardex, ubicaciones, ajustes, transferencias, conteos, lotes, picking y packing.
- POS, tickets pendientes, caja principal, pagos simples y mixtos.
- Apertura, movimientos, cierre y arqueo ciego de caja.
- Ventas, clientes, anulaciones y devoluciones parciales.
- Reportes, exportaciones, auditoría tenant y diagnóstico operativo.
- Administración de empresa, usuarios, roles, permisos, invitaciones y asignaciones usuario-sucursal-caja.
- Planes, suscripción, límites, soporte y portal de facturación tenant.
- SuperAdmin con dashboard, empresas, suscripciones, Customer Success, soporte, CMS, feature flags e infraestructura.
- Catálogo público e integración WooCommerce.
- Navegación unificada, responsive y filtrada por permisos.

## Desarrollo por fases

- Sprint 0: base técnica, Docker, CI, multi-tenant, autenticación, permisos, auditoría y eventos internos.
- Slice 01: activación del cliente y primera venta.
- Slice 02: catálogo, compras, inventario y warehouse.
- Slice 03: POS, caja, ventas y clientes.
- Slice 04: administración, reportes y SuperAdmin.
- Fase 1: navegación unificada.
- Fase 2: agrupación funcional.
- Fase 3: asignaciones usuario-sucursal-caja.
- Fase 4: permisos efectivos, multi-rol, navegación dinámica y protección de acciones.
- Fase 5: preparación operativa, arqueo ciego y cierre funcional V1.
- Waves A-D: cierre de estructura, reportes, conectores, devoluciones, lotes y operación interna.
- V2.1: catálogo público, WooCommerce y centro de integraciones.
- Mejoras posteriores: dashboard por permisos, privacidad visual, catálogo unificado, plantilla CSV y rediseño final del POS.
- Fase 6: consolidación documental y cierre de pantallas de plataforma.

## Dependencias externas pendientes

### Flow

El código de solicitudes de cambio de plan, checkout, confirmación, webhook, idempotencia y activación de entitlements está preparado. Sigue pendiente:

- cuenta comercial habilitada;
- credenciales sandbox y producción;
- configuración de URLs productivas;
- prueba real de checkout, retorno y webhook;
- validación de pagos fallidos, renovaciones, cancelación y periodo de gracia.

### DTE Chile

La cuenta DTE, configuración cifrada, adaptadores, estados, emisión, consulta, reintentos, anulaciones y notas están preparados. Sigue pendiente:

- selección final de proveedor;
- credenciales y certificado;
- prueba de conexión;
- validación sandbox;
- piloto de boleta, factura, nota de crédito y nota de débito;
- validación de PDF/XML y estados reales.

## Riesgos pendientes

- Registrar marca Tarevo en INAPI.
- Seleccionar y contratar proveedor DTE.
- Activar y validar Flow.
- Confirmar costos reales y capacidad de infraestructura para beta.
- Definir política final de soporte y SLA.
- Completar prueba de backup y restauración.
- Ejecutar QA productivo por perfiles y multiempresa.

## Próximo trabajo

Fase 6 — Consolidación documental y pantallas de plataforma:

1. Actualizar Screen Registry, navegación y estado del proyecto.
2. Incorporar comparativa pública de planes.
3. Incorporar ficha integral de empresa en SuperAdmin.
4. Incorporar Configuración global en SuperAdmin.
5. Registrar decisiones sobre pantallas consolidadas.
6. Preparar el checklist de activación de Flow/DTE, QA y piloto.

## Regla operativa

Si una decisión no está documentada y aprobada, no se implementa. Toda pantalla debe declarar mundo, módulo, ruta y permisos o alcance de plataforma antes de incorporarse.
