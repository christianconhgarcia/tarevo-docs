# Atlas Decision Log (ADL)

Este documento registra decisiones aprobadas durante Sprint 0 y decisiones posteriores que afectan la arquitectura oficial de Tarevo.

## ADL-000 - Nombre comercial

Nombre comercial aprobado: Atlas.  
Nombre tecnico: Atlas Platform.

## ADL-001 - Mercado inicial

Atlas iniciara en Chile.

## ADL-002 - Atlas no es solo facturacion

Atlas sera una plataforma de gestion comercial. La facturacion electronica sera una capacidad, no la identidad del producto.

## ADL-003 - Nucleo independiente del pais

El nucleo del ERP sera independiente de reglas tributarias. Chile/SII sera un modulo.

## ADL-004 - ERP como sistema maestro

Atlas sera el sistema maestro de productos, stock, ventas y clientes. Canales externos no modifican stock directamente.

## ADL-005 - Apps como modelo modular

Atlas se organizara como Apps activables por plan.

## ADL-006 - Self-Service SaaS

El cliente debe poder registrarse, pagar, crear empresa, escoger subdominio y activar su cuenta sin intervencion manual.

## ADL-007 - PostgreSQL

PostgreSQL sera la base de datos principal de Atlas.

## ADL-008 - Infraestructura inicial

Infraestructura inicial: Hetzner Cloud + Coolify self-hosted + Docker + PostgreSQL + Redis + Cloudflare + R2 + Resend.

## ADL-009 - No Hostinger/cPanel

Atlas no se desarrollara para hosting compartido, FTP, cPanel o almacenamiento persistente local.

## ADL-010 - R2 para archivos

Fotos, logos, PDFs, XML y archivos de clientes se guardaran en Cloudflare R2 o servicio compatible S3.

## ADL-011 - Almacenamiento por plan

Atlas podra vender almacenamiento incluido y adicional por empresa.

## ADL-012 - Secretos fuera del codigo

Ninguna clave o certificado privado se guarda en codigo, frontend, GitHub o chat.

## ADL-013 - Seguridad por diseno

Atlas se disenara bajo Secure by Design.

## ADL-014 - Separacion ticket, pago y DTE

Ticket, pago y DTE son entidades distintas.

## ADL-015 - Estaciones de venta configurables

Cada estacion puede tener capacidades diferentes: crear tickets, cobrar, emitir DTE, cerrar caja, anular, etc.

## ADL-016 - Ciclo de vida del ticket

Los tickets pueden estar creados, pendientes, pagados, anulados, expirados, con boleta, con factura o finalizados. No se eliminan sin trazabilidad.

## ADL-017 - Caja central

Atlas soportara flujos donde una estacion crea tickets y otra cobra/emite documento.

## ADL-018 - Prevencion de doble documentacion tributaria

Atlas debe prevenir emitir boleta y factura por la misma venta sin flujo correcto.

## ADL-019 - Terminales POS fisicos no entran en V1

La integracion con Getnet, Transbank, Redelcom, SumUp u otros se deja disenada mediante Payment Terminal Adapter, pero no conectada en V1.

## ADL-020 - Atlas Warehouse

Bodega sera una App premium: Atlas Warehouse.

## ADL-021 - Separacion Inventory/Warehouse

Inventory controla cantidades, costos y kardex. Warehouse controla bodegas, ubicaciones, traspasos, picking, packing y recepcion.

## ADL-022 - Multi-bodega nativo

Una empresa puede tener multiples bodegas, sucursales y centros de distribucion.

## ADL-023 - Producto unico por empresa

El producto se registra una vez. El stock se distribuye por bodega, sucursal, ubicacion y canal.

## ADL-024 - Arquitectura basada en eventos

Las Apps no se llaman directamente. Publican y escuchan eventos.

## ADL-025 - Escalabilidad diferida

La arquitectura se prepara para crecer, pero no se incorporan servicios pagos ni complejidad antes de necesitarlo.

## ADL-026 - V1 disciplinada

La V1 incluira Core, POS, Inventory, Warehouse inicial, DTE Chile, CRM basico, reportes, landing, billing y SuperAdmin. Integraciones avanzadas quedan para roadmap.

## ADL-027 - Primero arquitectura, despues programacion

No se desarrolla una funcionalidad sin documento o decision relacionada.

## ADL-028 - Impresion POS multiplataforma por adaptadores

Tarevo POS tendra una abstraccion comun de impresion y adaptadores por plataforma. Windows y macOS usaran QZ Tray mediante Tarevo Print Connector. Android usara una app Tarevo POS con bridge nativo y SDK/servicio de impresora del fabricante cuando corresponda.

La logica de venta no debe acoplarse a QZ, Sunmi, iMin, PAX ni otra marca especifica.

## ADL-029 - QZ con firma backend

Las solicitudes QZ se firman en backend con SHA512. El frontend recibe el certificado publico y la firma necesaria, pero nunca la clave privada.

La clave privada permanece fuera del codigo y se configura en runtime mediante `QZ_PRIVATE_KEY_B64`.

## ADL-030 - Preferencias de impresion son locales por computador

La impresora de tickets, etiquetas, A4, papel y ajustes de impresion se guardan por computador/navegador y tenant. No son configuracion global de la empresa porque cada estacion puede tener hardware diferente.

## ADL-031 - Fallo de impresion no invalida venta

La impresion es un efecto posterior a una venta confirmada. Si QZ, la impresora, el bridge Android o cualquier capa local falla, la venta confirmada permanece exitosa.

Regla permanente:

```text
fallo de impresion != fallo de venta
```

## ADL-032 - Tarevo Print Connector autoservicio

Tarevo ofrecera un instalador autoservicio desde `Configuracion > Impresion` para preparar equipos Windows y macOS sin intervencion obligatoria de soporte.

Windows tendra instalador `.exe` y macOS `.pkg`. Los instaladores pueden incluir QZ Tray, certificado publico Tarevo, inicio automatico y verificacion, pero nunca secretos de backend.

## ADL-033 - Android conserva el POS web como fuente de verdad

La app Android de Tarevo cargara `pos.gettarevo.com` mediante WebView seguro y usara un bridge nativo solo para capacidades de hardware.

Los cambios normales del POS web no requieren publicar una nueva APK. Solo los cambios de la capa nativa, SDK, bridge o hardware requieren una nueva version Android.

## ADL-034 - Un solo renderer de ticket

Vista previa, impresion Windows/macOS y adaptadores Android deben compartir la misma fuente canonica de contenido del ticket. No se mantendran plantillas divergentes para preview e impresion.

La arquitectura completa esta documentada en:

```text
03-Architecture/POS-Printing-Architecture.md
```
