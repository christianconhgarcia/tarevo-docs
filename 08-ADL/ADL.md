# Tarevo Decision Log (ADL)

Este documento registra decisiones aprobadas durante Sprint 0 y su alineacion posterior con la marca final Tarevo.

## ADL-000 - Nombre comercial

Nombre comercial aprobado: Tarevo.  
Nombre tecnico: Tarevo Platform.  
Esta decision reemplaza el nombre de trabajo anterior Atlas.

## ADL-001 - Mercado inicial

Tarevo iniciara en Chile.

## ADL-002 - Tarevo no es solo facturacion

Tarevo sera una plataforma de gestion comercial. La facturacion electronica sera una capacidad, no la identidad del producto.

## ADL-003 - Nucleo independiente del pais

El nucleo del ERP sera independiente de reglas tributarias. Chile/SII sera un modulo.

## ADL-004 - ERP como sistema maestro

Tarevo sera el sistema maestro de productos, stock, ventas y clientes. Canales externos no modifican stock directamente.

## ADL-005 - Apps como modelo modular

Tarevo se organizara como Apps activables por plan.

## ADL-006 - Self-Service SaaS

El cliente debe poder registrarse, pagar, crear empresa, escoger subdominio y activar su cuenta sin intervencion manual.

## ADL-007 - PostgreSQL

PostgreSQL sera la base de datos principal de Tarevo.

## ADL-008 - Infraestructura inicial

Infraestructura inicial: Hetzner Cloud + Coolify self-hosted + Docker + PostgreSQL + Redis + Cloudflare + R2 + Resend.

## ADL-009 - No Hostinger/cPanel

Tarevo no se desarrollara para hosting compartido, FTP, cPanel o almacenamiento persistente local como arquitectura final.

## ADL-010 - R2 para archivos

Fotos, logos, PDFs, XML y archivos de clientes se guardaran en Cloudflare R2 o servicio compatible S3.

## ADL-011 - Almacenamiento por plan

Tarevo podra vender almacenamiento incluido y adicional por empresa.

## ADL-012 - Secretos fuera del codigo

Ninguna clave o certificado se guarda en codigo, frontend, GitHub o chat.

## ADL-013 - Seguridad por diseno

Tarevo se disenara bajo Secure by Design.

## ADL-014 - Separacion ticket, pago y DTE

Ticket, pago y DTE son entidades distintas.

## ADL-015 - Estaciones de venta configurables

Cada estacion puede tener capacidades diferentes: crear tickets, cobrar, emitir DTE, cerrar caja, anular, etc.

## ADL-016 - Ciclo de vida del ticket

Los tickets pueden estar creados, pendientes, pagados, anulados, expirados, con boleta, con factura o finalizados. No se eliminan sin trazabilidad.

## ADL-017 - Caja central

Tarevo soportara flujos donde una estacion crea tickets y otra cobra/emite documento.

## ADL-018 - Prevencion de doble documentacion tributaria

Tarevo debe prevenir emitir boleta y factura por la misma venta sin flujo correcto.

## ADL-019 - Terminales POS fisicos no entran en V1

La integracion con Getnet, Transbank, Redelcom, SumUp u otros se deja disenada mediante Payment Terminal Adapter, pero no conectada en V1.

## ADL-020 - Tarevo Warehouse

Bodega sera una App premium: Tarevo Warehouse.

## ADL-021 - Separacion Inventory/Warehouse

Inventory controla cantidades, costos y kardex. Warehouse controla bodegas, ubicaciones, traspasos, picking, packing y recepcion.

## ADL-022 - Multi-bodega nativo

Una empresa puede tener multiples bodegas, sucursales y centros de distribucion.

## ADL-023 - Producto unico por empresa

El producto se registra una vez. El stock se distribuye por bodega, sucursal, ubicacion y canal.

## ADL-024 - Arquitectura basada en eventos

Las Apps no se llaman directamente. Publican y escuchan eventos.

## ADL-025 - Escalabilidad diferida

La arquitectura se prepara para crecer, pero no se incorporan servicios pagos ni complejidad antes de necesitarlos.

## ADL-026 - V1 disciplinada

La V1 incluira Core, POS, Inventory, Warehouse inicial, DTE Chile, CRM basico, reportes, landing, billing y SuperAdmin. Integraciones avanzadas quedan para roadmap.

## ADL-027 - Primero arquitectura, despues programacion

No se desarrolla una funcionalidad sin documento o decision relacionada.

## ADL-028 - Fuente oficial de verdad

La documentacion vigente en `tarevo-docs` es la fuente oficial para producto, arquitectura y alcance. Cuando exista contradiccion, se aplica este orden:

1. Constitucion.
2. ADL aprobado mas reciente.
3. Blueprints y registros maestros.
4. PRD de slice aprobado.
5. Backlog y documentos operativos.
6. Codigo existente, que debe corregirse si contradice una decision superior.

## ADL-029 - Estrategia de ramas

- `main`: codigo integrado y aprobado.
- `production`: version desplegada o lista para desplegar.
- ramas de trabajo: cambios aislados y revisables.

Los cambios de documentacion de Fase 0 se preparan en una rama y se integran tras revision.
