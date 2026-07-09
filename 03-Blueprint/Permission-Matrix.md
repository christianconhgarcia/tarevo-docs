# Permission Matrix

Version: 0.1
Estado: Aprobado

## Objetivo
Definir el modelo oficial de permisos de Tarevo.

## Principio
Tarevo no se basa solo en roles. Se basa en capacidades.

Un rol es un conjunto de permisos. Un entitlement es un derecho comercial asociado al plan.

## Capas

1. Usuario autenticado.
2. Tenant correcto.
3. Rol.
4. Permisos.
5. Entitlements del plan.
6. Estado de la suscripcion.

## Roles iniciales Tenant ERP

- Propietario
- Administrador
- Supervisor
- Cajero
- Vendedor
- Bodeguero
- Compras
- Contador
- Solo lectura

## Roles SuperAdmin

- CEO
- Operaciones
- Customer Success
- Soporte
- Facturacion
- Desarrollo
- Solo lectura

## Permisos base

### Productos

```text
products.view
products.create
products.update
products.delete
products.import
products.export
products.manage_categories
products.manage_brands
```

### Inventario

```text
inventory.view
inventory.adjust
inventory.count
inventory.view_kardex
inventory.manage_min_stock
```

### Warehouse

```text
warehouse.view
warehouse.create
warehouse.update
warehouse.transfer
warehouse.pick
warehouse.pack
warehouse.receive
warehouse.manage_locations
```

### POS y Ventas

```text
sales.pos_access
sales.create
sales.cancel
sales.refund
sales.discount
sales.change_price
sales.view_history
sales.reprint
```

### Caja

```text
cash.open
cash.close
cash.view
cash.adjust
cash.view_differences
cash.export
```

### Clientes

```text
customers.view
customers.create
customers.update
customers.delete
customers.export
```

### Reportes

```text
reports.view
reports.export
reports.view_profit
reports.view_cash
reports.view_inventory
```

### Configuracion

```text
settings.company.update
settings.branches.manage
settings.warehouses.manage
settings.cash_registers.manage
settings.dte.manage
settings.integrations.manage
```

### Usuarios

```text
users.view
users.invite
users.update
users.disable
roles.manage
permissions.manage
```

## Entitlements iniciales

```text
plan.users.limit
plan.cash_registers.limit
plan.branches.limit
plan.warehouses.limit
plan.storage.limit_gb
plan.custom_domain.enabled
plan.warehouse.enabled
plan.catalog.enabled
plan.crm.enabled
plan.dte.enabled
```

## Reglas

- Un usuario puede tener permiso, pero si el plan no tiene entitlement, la funcion queda bloqueada.
- La UI debe ocultar o bloquear funciones no permitidas.
- El backend siempre valida permisos y entitlements.
- Nunca confiar solo en el frontend.

## Matriz resumida Tenant

| Accion | Cajero | Supervisor | Admin | Propietario |
|---|---|---|---|---|
| Crear venta | Si | Si | Si | Si |
| Anular venta | No | Si | Si | Si |
| Cambiar precio | No | No | Si | Si |
| Abrir caja | Si | Si | Si | Si |
| Cerrar caja | Si | Si | Si | Si |
| Ver utilidad | No | Si | Si | Si |
| Crear producto | No | No | Si | Si |
| Ajustar inventario | No | Si | Si | Si |
| Gestionar usuarios | No | No | Si | Si |

## Regla para Codex
Toda ruta, pantalla y accion debe declarar permisos requeridos. No se aceptan endpoints criticos sin autorizacion.
