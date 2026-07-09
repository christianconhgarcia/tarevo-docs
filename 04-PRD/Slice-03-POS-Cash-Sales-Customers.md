# Slice 03 — POS, Cash, Sales & Customers

Estado: Aprobado para especificacion V1
Prioridad: Critica
Mundo: Tenant ERP

## Objetivo
Permitir que una empresa venda, cobre, gestione caja, registre clientes, consulte ventas y procese anulaciones/devoluciones basicas.

## Alcance V1

Incluye:

- POS rapido.
- Busqueda por codigo, nombre y codigo de barras.
- Ticket pendiente.
- Ticket pagado.
- Ticket anulado.
- Pago efectivo.
- Pago tarjeta.
- Pago transferencia.
- Pago mixto.
- Apertura de caja.
- Cierre de caja.
- Arqueo.
- Historial de ventas.
- Detalle de venta.
- Reimpresion.
- Clientes basicos.
- Devolucion basica.

No incluye V1:

- Integracion POS fisico.
- Gift Cards.
- Fidelizacion.
- Cupones avanzados.
- Facturacion electronica automatica.

## Flujo principal POS

```text
Login cajero
  -> Verificar caja abierta
  -> Buscar producto
  -> Agregar al ticket
  -> Aplicar descuento si tiene permiso
  -> Seleccionar cliente opcional
  -> Cobrar
  -> Registrar pago
  -> Completar venta
  -> Descontar stock
  -> Emitir ticket interno
```

## Flujo ticket pendiente

```text
POS
  -> Crear ticket
  -> Cliente va a caja principal
  -> Cajero principal cobra
  -> Ticket pasa a pagado
  -> Venta completada
```

## Pantallas

- SCR-TE-019 POS venta rapida.
- SCR-TE-020 Apertura de caja.
- SCR-TE-021 Cierre de caja.
- SCR-TE-022 Arqueo.
- SCR-TE-023 Historial de ventas.
- SCR-TE-024 Detalle venta.
- SCR-TE-025 Listado clientes.
- SCR-TE-026 Ficha cliente.

## Estados POS

- Caja cerrada.
- Caja abierta sin ticket.
- Ticket en edicion.
- Pago pendiente.
- Pago parcial.
- Pago completado.
- Venta completada.
- Error.

## Reglas de negocio aplicables

- BR-5001 No vender con caja cerrada.
- BR-5002 No vender producto inactivo.
- BR-5003 Descuentos superiores al limite requieren autorizacion.
- BR-5004 Precio modificable solo con permiso.
- BR-5006 Ticket puede existir sin pago.
- BR-5007 Estados de ticket.
- BR-6001 Una apertura activa por caja.
- BR-6004 Diferencia requiere motivo.
- BR-7001 Venta asociada a ticket.
- BR-7002 Venta pagada requiere metodo de pago.
- BR-7003 Pagos mixtos permitidos.
- BR-7004 Venta anulada nunca desaparece.
- BR-7005 Devolucion genera movimiento inverso.
- BR-9001 Cliente opcional.

## Eventos

- CashOpened.
- CashClosed.
- TicketCreated.
- TicketCancelled.
- PaymentRecorded.
- SaleCompleted.
- SaleCancelled.
- RefundCreated.
- CustomerCreated.
- CustomerUpdated.

## APIs principales

- Abrir caja.
- Cerrar caja.
- Crear ticket.
- Agregar item a ticket.
- Quitar item.
- Aplicar descuento.
- Registrar pago.
- Completar venta.
- Anular ticket.
- Listar ventas.
- Ver detalle venta.
- Reimprimir ticket.
- Crear cliente.
- Actualizar cliente.
- Procesar devolucion.

## Entidades

- CashRegister.
- CashSession.
- CashMovement.
- Ticket.
- TicketItem.
- Sale.
- SaleItem.
- Payment.
- Customer.
- InventoryMovement.
- AuditLog.

## Permisos

- sales.pos_access.
- sales.create.
- sales.cancel.
- sales.refund.
- sales.discount.
- sales.change_price.
- sales.view_history.
- sales.reprint.
- cash.open.
- cash.close.
- cash.view.
- cash.adjust.
- customers.view/create/update.

## UX

POS debe ser rapido, apto para teclado y lector de codigo de barras.

Prioridades UX:

- Busqueda instantanea.
- Total visible siempre.
- Boton cobrar destacado.
- Estado de caja visible.
- Alertas claras cuando no haya stock.
- No bloquear con modales innecesarios.

## Casos limite

- Caja cerrada.
- Caja ya abierta por otro usuario.
- Producto sin stock.
- Producto inactivo.
- Permiso insuficiente para descuento.
- Pago mixto incompleto.
- Venta anulada.
- Devolucion parcial.
- Diferencia de caja.

## Definition of Done

- POS permite venta completa.
- Caja abre/cierra con arqueo.
- Pagos mixtos funcionan.
- Venta descuenta stock mediante InventoryMovement.
- Historial y detalle disponibles.
- Reimpresion disponible.
- Auditoria completa.
- Tests de flujo venta y caja.

## Prompt base para Codex
Implementa Slice 03 centrado en POS, caja, ventas y clientes. No implementar DTE ni integraciones de POS fisico. La venta debe descontar inventario mediante eventos/movimientos y nunca modificar stock directamente.
