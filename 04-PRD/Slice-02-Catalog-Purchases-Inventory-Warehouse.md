# Slice 02 — Catalog, Purchases, Inventory & Warehouse

Estado: Aprobado para especificacion V1
Prioridad: Critica
Mundo: Tenant ERP

## Objetivo
Permitir que una empresa administre catalogo, proveedores, compras, recepcion de mercaderia, stock, Kardex, ubicaciones y movimientos logisticos basicos.

## Alcance V1

Incluye:

- Productos.
- Categorias.
- Marcas.
- Variantes.
- Unidades.
- Proveedores basicos.
- Importacion Excel/CSV con vista previa.
- Fotos de productos.
- Ordenes de compra.
- Recepcion parcial y total.
- Stock por bodega/ubicacion.
- Kardex.
- Ajustes con motivo.
- Conteos fisicos.
- Bodegas.
- Ubicaciones jerarquicas.
- Transferencias.
- Picking basico.
- Packing basico.
- Lotes basicos.

No incluye V1:

- PEPS/FIFO.
- UEPS/LIFO.
- Optimizacion avanzada de rutas.
- Forecast de compras.
- Integraciones WooCommerce/Shopify/ML.

## Decisiones principales

- Productos pertenecen al tenant, no a la sucursal.
- Stock pertenece a sucursal/bodega/ubicacion.
- El stock nunca se modifica directamente; siempre mediante movimientos.
- Metodo de costo V1: promedio ponderado.
- Producto, Variante y StockItem son conceptos separados.

## Flujo operativo

```text
Crear producto
  -> Crear proveedor
  -> Crear orden de compra
  -> Recibir mercaderia
  -> Generar movimiento de inventario
  -> Actualizar stock
  -> Ubicar producto
  -> Consultar Kardex
  -> Transferir si aplica
  -> Preparar picking
```

## Pantallas

Productos:

- SCR-TE-007 Listado productos.
- SCR-TE-008 Crear producto.
- SCR-TE-009 Editar producto.
- SCR-TE-010 Categorias.
- SCR-TE-011 Marcas.

Inventario:

- SCR-TE-012 Stock.
- SCR-TE-013 Kardex.
- SCR-TE-014 Ajustes.

Warehouse:

- SCR-TE-015 Bodegas.
- SCR-TE-016 Ubicaciones.
- SCR-TE-017 Transferencias.
- SCR-TE-018 Picking.

Compras:

- SCR-TE-027 Ordenes de compra.
- SCR-TE-028 Recepcion.

## Modelo de producto

Producto:

- SKU interno.
- Codigo de barras.
- Nombre.
- Nombre corto.
- Descripcion.
- Estado.
- Categoria.
- Marca.
- Etiquetas.
- Precio compra.
- Precio venta.
- IVA.
- Unidad.
- Maneja stock.
- Stock minimo.
- Peso/dimensiones.
- Imagen principal.
- Galeria.

Variante:

- Producto padre.
- Atributos.
- SKU variante.
- Codigo de barras variante.
- Precio opcional.
- Estado.

StockItem:

- Variante/producto.
- Bodega.
- Ubicacion.
- Cantidad.
- Cantidad reservada.
- Costo promedio.

## Compras

Estados de orden de compra:

- Borrador.
- Enviada.
- Parcialmente recibida.
- Recibida.
- Cancelada.

Recepcion:

- Puede ser parcial.
- Genera InventoryMovement.
- Actualiza costo promedio.
- Requiere usuario, fecha y referencia.

## Inventario

Movimiento de inventario debe tener:

- Tipo.
- Origen.
- Producto/variante.
- Cantidad.
- Bodega.
- Ubicacion.
- Usuario.
- Fecha.
- Motivo.
- Referencia.

Tipos de movimiento:

- Compra.
- Venta.
- Ajuste.
- Transferencia salida.
- Transferencia entrada.
- Conteo.
- Devolucion.

## Warehouse

Ubicacion jerarquica:

```text
Bodega -> Pasillo -> Rack -> Nivel -> Posicion
```

Codigo visible ejemplo:

```text
A-02-B-04-08
```

Transferencia estados:

- Creada.
- En preparacion.
- En transito.
- Recibida.
- Finalizada.
- Cancelada.

## Reglas de negocio aplicables

- BR-2001 a BR-2006.
- BR-3001 a BR-3005.
- BR-4001 a BR-4005.
- BR-8001 a BR-8002.

## Eventos

- ProductCreated.
- ProductUpdated.
- StockAdjusted.
- WarehouseCreated.
- TransferRequested.
- TransferReceived.
- PurchaseOrderCreated.
- PurchaseReceived.
- InventoryCountCompleted.

## APIs principales

- Crear/editar/listar productos.
- Importar productos.
- Crear categoria.
- Crear marca.
- Crear proveedor.
- Crear orden de compra.
- Recibir orden.
- Listar stock.
- Consultar Kardex.
- Ajustar stock.
- Crear bodega.
- Crear ubicacion.
- Crear transferencia.
- Recibir transferencia.

## Permisos

- products.view/create/update/delete/import/export.
- inventory.view/adjust/count/view_kardex.
- warehouse.view/create/update/transfer/pick/pack/receive/manage_locations.
- purchases.view/create/receive/cancel.

## Casos limite

- Codigo duplicado.
- Producto con movimientos no puede eliminarse.
- Recepcion mayor a compra sin permiso.
- Transferencia mayor al stock disponible.
- Ubicacion inexistente.
- Archivo Excel con errores.
- Imagen demasiado pesada.
- Producto inactivo.

## Definition of Done

- Catalogo completo operativo.
- Importador con vista previa y errores.
- Compras y recepcion generan stock.
- Kardex inmutable.
- Ajustes requieren motivo.
- Warehouse con ubicaciones.
- Transferencias auditadas.
- Tests de inventario y costos.

## Prompt base para Codex
Implementa Slice 02 como modulo de Catalogo, Compras, Inventario y Warehouse. No modificar stock directamente. Todo cambio de stock debe pasar por InventoryMovement. Usar promedio ponderado en V1. No implementar integraciones ecommerce en este slice.
