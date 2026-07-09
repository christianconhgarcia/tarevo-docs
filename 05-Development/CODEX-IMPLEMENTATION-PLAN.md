# Codex Implementation Plan

Estado: Aprobado
Version: 0.1

## Objetivo
Definir el orden en que Codex debe implementar Tarevo V1.

## Regla principal
Codex no debe implementar el proyecto completo de una sola vez. Debe implementar por slices, respetando documentacion, arquitectura, seguridad y reglas de negocio.

## Orden de implementacion

### Sprint 0 — Base tecnica

- Crear Laravel backend.
- Crear React + TypeScript + Vite frontend.
- Dockerizar proyecto.
- Configurar PostgreSQL.
- Configurar Redis preparado.
- Configurar autenticacion base.
- Configurar multi-tenant base.
- Configurar permisos base.
- Configurar auditoria base.

### Sprint 1 — Slice 01 Customer Activation

- Public Website minimo.
- Registro.
- Login.
- Verificacion correo.
- Crear tenant.
- Crear sucursal.
- Crear bodega.
- Crear caja.
- Crear producto.
- Abrir caja.
- Primera venta.
- Dashboard inicial.

### Sprint 2 — Slice 02 Catalog, Purchases, Inventory & Warehouse

- Catalogo.
- Importador.
- Proveedores.
- Compras.
- Recepcion.
- Inventario.
- Kardex.
- Bodegas.
- Ubicaciones.
- Transferencias.
- Picking basico.

### Sprint 3 — Slice 03 POS, Cash, Sales & Customers

- POS completo V1.
- Caja completa V1.
- Ventas.
- Clientes.
- Devoluciones basicas.
- Reimpresion.

### Sprint 4 — Slice 04 Admin, Reports, Billing & SuperAdmin

- Configuracion.
- Usuarios.
- Roles.
- Reportes.
- Billing.
- SuperAdmin.
- Customer Success.
- Tickets soporte.
- CMS landing.

## Prohibido en V1

- Microservicios.
- Kubernetes.
- WebSockets complejos.
- IA Menora.
- App movil.
- Integraciones ecommerce.
- POS fisicos.
- Motor avanzado de reglas.

## Definition of Done global

Cada slice debe incluir:

- Backend.
- Frontend.
- Migraciones.
- APIs.
- Permisos.
- Eventos.
- Auditoria.
- Validaciones.
- Tests.
- Responsive.
- Documentacion actualizada.

## Regla de calidad
Si Codex detecta ambiguedad, no debe inventar. Debe proponer una pregunta o abrir un TODO documentado.
