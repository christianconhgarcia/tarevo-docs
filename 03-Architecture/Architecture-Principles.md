# Architecture Principles - Tarevo

Documento: ARCH-001  
Version: 1.1  
Estado: Aprobado para Tarevo V1  
Fecha de alineacion: 2026-07-12

## 1. Principio central

Tarevo sera una plataforma SaaS modular, multiempresa, cloud-first y preparada para produccion desde el primer dia.

No se desarrollara pensando en Hostinger, cPanel o hosting compartido.

## 2. Arquitectura conceptual

```text
Landing / Registro / Portal Cliente
        |
Tarevo Core SaaS
        |
Auth - Billing - Plans - Entitlements - Companies - Users
        |
Apps internas
        |
POS - Inventory - Warehouse - DTE - CRM - Reports - Catalog
        |
Event Bus / Workers / Audit Logs
```

## 3. Apps, no modulos rigidos

Tarevo se organizara como Apps activables por plan.

Apps V1:

- Tarevo Core.
- Tarevo POS.
- Tarevo Inventory.
- Tarevo Warehouse.
- Tarevo DTE.
- Tarevo CRM basico.
- Tarevo Reports.
- Tarevo Catalog preparado.

## 4. Arquitectura basada en eventos

Los modulos no deben depender directamente entre si.

Ejemplo:

```text
POS publica evento: sale.paid
Inventory escucha y descuenta stock
Warehouse escucha y registra movimiento
DTE escucha y emite documento si corresponde
Reports escucha y actualiza metricas
CRM escucha y actualiza historial del cliente
```

## 5. Separacion ticket, pago y DTE

Tarevo separa tres entidades:

- Ticket: intencion comercial interna.
- Pago: transaccion financiera.
- DTE: documento tributario.

Esto permite flujos con caja central, tickets pendientes, pagos mixtos y distintas configuraciones tributarias por caja.

## 6. Estaciones de venta

No todas las cajas son iguales. Tarevo tendra estaciones configurables.

Capacidades por estacion:

- Crear tickets.
- Cobrar.
- Emitir boleta.
- Emitir factura.
- Emitir nota de credito.
- Anular ticket.
- Abrir/cerrar caja.
- Ver tickets pendientes.

## 7. Multiempresa y subdominios

Cada empresa tendra un slug unico.

Ejemplo:

```text
ferreteriagomez.app.gettarevo.com
supercool.app.gettarevo.com
```

La aplicacion debe resolver la empresa desde el subdominio y aislar datos estrictamente.

## 8. Inventario y bodega

Producto se registra una sola vez por empresa.

El stock se distribuye por bodega, sucursal, ubicacion y canal.

Inventario controla cantidades y costos. Warehouse controla ubicaciones fisicas, picking, recepcion y traspasos.

## 9. Integraciones futuras

Las integraciones con Shopify, Mercado Libre, WhatsApp, terminales POS fisicos y app movil quedaran preparadas mediante adaptadores, eventos e interfaces, pero no se implementaran en V1.

## 10. Regla para Codex

Codex debe implementar siempre contra interfaces y contratos documentados. No debe acoplar directamente Apps entre si ni usar datos falsos como solucion final.
