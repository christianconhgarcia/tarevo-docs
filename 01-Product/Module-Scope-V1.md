# Module Scope V1 - Tarevo

Documento: MODULE-SCOPE-001  
Version: 1.0  
Estado: Draft aprobado para Sprint 0  
Fecha: 2026-07-09

## 1. Proposito

Definir que incluye y que no incluye cada modulo de Tarevo V1 para evitar que Codex implemente funcionalidades fuera de alcance.

## 2. Tarevo Core

### Incluye

- Multiempresa.
- Creacion de empresa.
- Slug y subdominio.
- Usuarios.
- Roles.
- Permisos.
- Planes y entitlements.
- Auditoria base.
- Configuracion general de empresa.

### No incluye

- Contabilidad completa.
- RRHH.
- Firma electronica avanzada.
- Multi-pais completo en V1.

## 3. Tarevo POS

### Incluye

- Pantalla POS rapida.
- Busqueda de productos.
- Carrito/ticket.
- Tickets pendientes.
- Tickets pagados.
- Tickets anulados.
- Caja central.
- Medios de pago.
- Pago mixto.
- Reporte de pagos.

### No incluye

- Integracion con terminal de pago fisico.
- Venta offline.
- App nativa iOS/Android.

## 4. Tarevo Inventory

### Incluye

- Productos.
- Categorias.
- SKU/codigo.
- Imagen de producto.
- Precio y costo.
- Stock disponible.
- Kardex.
- Ajustes con motivo.
- Compras/recepcion basica.

### No incluye

- Prediccion avanzada de demanda.
- Reposicion automatica con IA.
- Integracion con proveedores externos.

## 5. Tarevo Warehouse

### Incluye

- Multiples bodegas.
- Ubicaciones internas.
- Stock por bodega.
- Traspasos.
- Stock en transito.
- Picking basico.
- Recepcion de traspasos.

### No incluye

- RFID.
- Rutas de despacho.
- Gestion avanzada de transporte.

## 6. Tarevo DTE Chile

### Incluye

- Configuracion tributaria de empresa.
- Datos de receptor.
- Boleta.
- Factura.
- Nota de credito.
- Nota de debito.
- Estados de DTE.
- Adaptador a proveedor externo.

### No incluye

- Motor DTE propio directo al SII.
- Certificacion tributaria propia en V1.
- Contabilidad completa.

## 7. Tarevo Reports

### Incluye

- Ventas por fecha.
- Ventas por usuario.
- Pagos por medio.
- Caja.
- Stock bajo.
- Movimientos de inventario.
- Tickets anulados.
- DTE emitidos y fallidos.

### No incluye

- BI avanzado.
- Cubos analiticos.
- Dashboards personalizados por cliente.

## 8. Tarevo SuperAdmin

### Incluye

- Ver empresas.
- Ver planes.
- Cambiar plan.
- Suspender/reactivar empresa.
- Ver consumo de almacenamiento.
- Ver errores criticos.
- Ver actividad reciente.

### No incluye

- Acceso libre a datos sensibles del cliente sin trazabilidad.
- Edicion directa de ventas o stock sin auditoria.

## 9. Regla de alcance

Si una funcionalidad no aparece en este documento o en el PRD General Chile, debe pasar primero por una decision en ADL antes de ser implementada.
