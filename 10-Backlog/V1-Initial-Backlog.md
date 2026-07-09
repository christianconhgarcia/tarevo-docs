# Atlas V1 - Initial Backlog

Documento: BACKLOG-001  
Version: 1.0  
Estado: Draft

## Epic 1 - Atlas Core

### CORE-001 - Multiempresa

Como plataforma, necesito aislar completamente los datos por empresa para operar como SaaS.

Criterios:

- Crear empresa.
- Slug unico.
- Subdominio asociado.
- Estado de empresa.
- Plan asociado.

### CORE-002 - Usuarios y roles

Como administrador de empresa, quiero crear usuarios y asignar permisos.

### CORE-003 - Entitlements

Como plataforma, quiero activar o bloquear funciones segun plan.

## Epic 2 - Auth y seguridad

### AUTH-001 - Registro

Cliente se registra desde landing y crea cuenta inicial.

### AUTH-002 - Login seguro

Login con rate limiting, sesiones seguras y auditoria.

### AUTH-003 - Recuperacion de contrasena

Token de un solo uso enviado por Resend.

## Epic 3 - Billing y planes

### BILL-001 - Planes

Crear planes Starter, Pro, Business/Enterprise.

### BILL-002 - Recursos incluidos

Controlar usuarios, DTE, almacenamiento, sucursales, bodegas, cajas y Apps.

### BILL-003 - Suspension progresiva

Avisos, periodo de gracia, modo restringido y suspension.

## Epic 4 - POS y tickets

### POS-001 - Crear ticket

Vendedor crea ticket interno no tributario.

### POS-002 - Ciclo de vida del ticket

Estados: creado, pendiente, pagado, anulado, expirado, con boleta, con factura, finalizado.

### POS-003 - Caja central

Una estacion puede cobrar tickets generados por otra.

### POS-004 - Pago mixto

Registrar multiples medios de pago por ticket.

### POS-005 - Anular ticket

Anular con motivo y auditoria.

## Epic 5 - Inventory

### INV-001 - Productos

Crear productos con SKU, codigo de barras, nombre, categoria, costo, precio, imagen.

### INV-002 - Kardex

Registrar movimientos de stock.

### INV-003 - Compras y recepcion

Registrar compra y aumentar stock.

## Epic 6 - Warehouse

### WH-001 - Multiples bodegas

Crear bodegas por empresa.

### WH-002 - Ubicaciones

Crear estructura de ubicaciones: pasillo, rack, nivel, posicion.

### WH-003 - Traspasos

Mover stock entre bodegas con estados y stock en transito.

### WH-004 - Picking basico

Generar lista de picking por ticket/pedido.

## Epic 7 - DTE Chile

### DTE-001 - Configuracion tributaria

Configurar certificado, CAF y proveedor DTE.

### DTE-002 - Boleta

Emitir boleta desde ticket pagado.

### DTE-003 - Factura

Emitir factura desde ticket pagado con cliente/receptor.

### DTE-004 - Nota de credito

Crear nota de credito vinculada a documento original.

## Epic 8 - SuperAdmin

### SA-001 - Dashboard plataforma

Ver empresas, pagos, DTE, almacenamiento, errores y estado general.

### SA-002 - Gestion de empresas

Suspender, reactivar, cambiar plan, extender gracia, agregar recursos.

## Epic 9 - Infraestructura

### INF-001 - Docker

Proyecto preparado para Docker y Coolify.

### INF-002 - R2 Storage

Subida de archivos a R2 y calculo de uso por empresa.

### INF-003 - Resend

Correos transaccionales.
