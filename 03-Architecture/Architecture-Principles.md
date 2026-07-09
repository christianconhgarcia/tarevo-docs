# Architecture Principles - Atlas

Documento: ARCH-001  
Version: 1.0  
Estado: Draft aprobado para Sprint 0

## 1. Principio central

Atlas sera una plataforma SaaS modular, multiempresa, cloud-first y preparada para produccion desde el primer dia.

No se desarrollara pensando en Hostinger, cPanel o hosting compartido.

## 2. Arquitectura conceptual

```text
Landing / Registro / Portal Cliente
        |
Atlas Core SaaS
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

Atlas se organizara como Apps activables por plan.

Apps V1:

- Atlas Core.
- Atlas POS.
- Atlas Inventory.
- Atlas Warehouse.
- Atlas DTE.
- Atlas CRM basico.
- Atlas Reports.
- Atlas Catalog preparado.

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

Atlas separa tres entidades:

- Ticket: intencion comercial interna.
- Pago: transaccion financiera.
- DTE: documento tributario.

Esto permite flujos con caja central, tickets pendientes, pagos mixtos y distintas configuraciones tributarias por caja.

## 6. Estaciones de venta

No todas las cajas son iguales. Atlas tendra estaciones configurables.

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
ferreteriagomez.atlas.com
supercool.atlas.com
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
