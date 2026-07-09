# Domain Dictionary

Version: 0.1
Estado: Aprobado

## Objetivo
Definir el vocabulario oficial de Tarevo para que negocio, documentacion, codigo y UI usen los mismos conceptos.

## Regla general

La interfaz inicial sera en espanol. El codigo usara ingles.

| Espanol UI | Codigo | Definicion |
|---|---|---|
| Empresa | Tenant / Company | Organizacion cliente que usa Tarevo. |
| Tenant | Tenant | Unidad de aislamiento multiempresa. |
| Sucursal | Branch | Ubicacion comercial de una empresa. |
| Bodega | Warehouse | Lugar fisico donde se almacena inventario. |
| Ubicacion | Location | Posicion especifica dentro de una bodega. |
| Producto | Product | Articulo vendible o inventariable. |
| Variante | Product Variant | Version de un producto, por ejemplo talla o color. |
| Stock | Stock | Cantidad disponible o registrada. |
| Movimiento | Inventory Movement | Registro que modifica o explica el stock. |
| Kardex | Stock Ledger | Historial cronologico de movimientos de inventario. |
| Ticket | Ticket | Documento operativo del POS, puede existir sin pago. |
| Venta | Sale | Operacion comercial confirmada. |
| Pago | Payment | Registro financiero asociado a venta o ticket. |
| Caja | Cash Session | Sesion financiera donde se registran cobros. |
| POS | POS | Interfaz para realizar ventas. |
| DTE | DTE | Documento Tributario Electronico. |
| Permiso | Permission | Capacidad asignada a rol o usuario. |
| Rol | Role | Conjunto de permisos. |
| Entitlement | Entitlement | Derecho comercial habilitado por plan. |
| SuperAdmin | Platform Admin | Usuario interno de Tarevo. |
| Customer Success | Customer Success | Area que impulsa adopcion y reduce churn. |
| Feature Flag | Feature Flag | Interruptor para habilitar funciones sin desplegar codigo. |
| Epic | Epic | Unidad funcional grande del producto. |
| Screen | Screen | Pantalla individual del sistema. |
| Event | Event | Hecho importante ocurrido en el sistema. |
| Business Rule | Business Rule | Regla oficial de negocio. |
| Blueprint | Blueprint | Conjunto de especificaciones funcionales del producto. |

## Terminos prohibidos o desaconsejados

- No usar "almacen" en UI; usar "bodega".
- No usar "orden" para ventas; usar ticket o venta segun corresponda.
- No usar "admin del sistema" para usuarios internos; usar SuperAdmin.
- No confundir caja con POS.
- No confundir permiso con entitlement.

## Diferencias clave

### Ticket vs Venta

Ticket: intencion operativa o documento temporal. Puede estar pendiente o sin pago.

Venta: operacion comercial confirmada.

### Caja vs POS

Caja: sesion financiera.

POS: interfaz donde se registra la operacion.

### Permiso vs Entitlement

Permiso: lo que un usuario puede hacer.

Entitlement: lo que el plan contratado permite usar.

## Regla para Codex
Si aparece un concepto nuevo en codigo o documentacion, primero debe agregarse aqui o justificarse su uso.
