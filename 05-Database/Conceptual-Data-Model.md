# Conceptual Data Model - Tarevo

Documento: DB-001  
Version: 1.0  
Estado: Draft  
Fecha: 2026-07-09

## 1. Proposito

Definir las entidades principales de Tarevo antes de crear modelos, migraciones o tablas.

Este documento no reemplaza el diseno fisico de base de datos. Sirve como mapa conceptual para que Codex no improvise relaciones.

## 2. Principio multiempresa

Toda entidad operativa debe pertenecer a una empresa mediante `company_id` o equivalente.

Regla: ningun usuario operativo puede leer, modificar o borrar datos de otra empresa.

## 3. Entidades Core

### PlatformUser

Usuario autenticado en la plataforma.

Campos conceptuales:

- id
- name
- email
- password_hash
- status
- created_at
- updated_at

### Company

Empresa cliente que usa Tarevo.

Campos conceptuales:

- id
- legal_name
- trade_name
- tax_id
- country
- currency
- status
- plan_id
- created_at
- updated_at

### CompanyUser

Relacion entre usuario y empresa.

Campos conceptuales:

- id
- company_id
- user_id
- role_id
- status
- invited_at
- accepted_at

### Role

Rol visible para el cliente.

Campos conceptuales:

- id
- company_id nullable para roles globales
- name
- description

### Permission

Permiso atomico reutilizable.

Campos conceptuales:

- id
- key
- description

### RolePermission

Relacion entre rol y permiso.

## 4. Entidades comerciales

### Branch

Sucursal o punto de operacion.

Campos conceptuales:

- id
- company_id
- name
- address
- status

### Warehouse

Bodega fisica o logica.

Campos conceptuales:

- id
- company_id
- branch_id nullable
- name
- status

### WarehouseLocation

Ubicacion interna dentro de una bodega.

Campos conceptuales:

- id
- company_id
- warehouse_id
- aisle
- rack
- level
- position
- label

### Product

Producto vendible o inventariable.

Campos conceptuales:

- id
- company_id
- sku
- barcode
- name
- description
- category_id
- cost_price
- sale_price
- tax_category
- image_url
- status

### Category

Categoria de producto.

Campos conceptuales:

- id
- company_id
- parent_id nullable
- name
- slug

## 5. Entidades de inventario

### StockBalance

Saldo actual por producto, bodega y ubicacion.

Campos conceptuales:

- id
- company_id
- product_id
- warehouse_id
- location_id nullable
- quantity_available
- quantity_reserved
- quantity_in_transit

### StockMovement

Kardex o movimiento historico.

Campos conceptuales:

- id
- company_id
- product_id
- warehouse_id
- location_id nullable
- type
- quantity
- reference_type
- reference_id
- reason
- created_by
- created_at

Tipos iniciales:

- purchase_receipt
- sale
- adjustment
- transfer_out
- transfer_in
- cancellation

### StockTransfer

Traspaso entre bodegas.

Campos conceptuales:

- id
- company_id
- source_warehouse_id
- destination_warehouse_id
- status
- created_by
- received_by
- created_at
- received_at

### StockTransferItem

Item dentro de un traspaso.

Campos conceptuales:

- id
- transfer_id
- product_id
- quantity

## 6. Entidades POS

### SalesStation

Estacion de venta o caja configurada.

Campos conceptuales:

- id
- company_id
- branch_id
- name
- type
- status

### Ticket

Documento interno de venta. No es DTE.

Campos conceptuales:

- id
- company_id
- branch_id
- station_id
- seller_user_id
- cashier_user_id nullable
- customer_id nullable
- status
- subtotal
- tax_total
- discount_total
- total
- created_at
- paid_at
- cancelled_at

Estados iniciales:

- created
- pending
- paid
- cancelled
- expired
- with_receipt
- with_invoice
- finalized

### TicketItem

Producto dentro del ticket.

Campos conceptuales:

- id
- ticket_id
- product_id
- quantity
- unit_price
- discount
- total

### Payment

Pago asociado a un ticket.

Campos conceptuales:

- id
- company_id
- ticket_id
- method
- amount
- currency
- exchange_rate nullable
- reference
- received_by
- created_at

## 7. Entidades DTE Chile

### TaxProfile

Configuracion tributaria de la empresa.

Campos conceptuales:

- id
- company_id
- rut
- razon_social
- giro
- address
- comuna
- city
- dte_provider
- status

### TaxDocument

Documento tributario emitido o solicitado.

Campos conceptuales:

- id
- company_id
- ticket_id
- type
- folio
- status
- provider_id
- xml_url
- pdf_url
- error_message
- issued_at

Tipos iniciales:

- boleta
- factura
- nota_credito
- nota_debito

## 8. Entidades SaaS/Billing

### Plan

Plan comercial.

Campos conceptuales:

- id
- name
- price
- currency
- billing_period
- status

### PlanEntitlement

Limites y funcionalidades por plan.

Campos conceptuales:

- id
- plan_id
- key
- value

### Subscription

Suscripcion de una empresa.

Campos conceptuales:

- id
- company_id
- plan_id
- status
- current_period_start
- current_period_end
- trial_ends_at

## 9. Auditoria

### AuditLog

Registro de acciones criticas.

Campos conceptuales:

- id
- company_id nullable
- user_id nullable
- action
- entity_type
- entity_id
- old_values
- new_values
- ip_address
- user_agent
- created_at

## 10. Reglas criticas

- Nunca borrar fisicamente ventas, pagos, movimientos de stock o DTE sin una politica explicita.
- Preferir estados sobre eliminacion dura en entidades operativas.
- Todo ajuste manual de stock requiere motivo.
- Todo cambio de plan o suspension requiere auditoria.
- El ticket, el pago y el DTE son entidades separadas.
