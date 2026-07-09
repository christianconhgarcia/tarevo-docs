# Business Rules Registry

Version: 0.1
Estado: Aprobado

## Objetivo
Centralizar las reglas de negocio oficiales de Tarevo.

Ningun modulo debe implementar reglas de negocio que contradigan este documento.

## Convencion

- BR: Business Rule
- Las reglas no cambian de ID aunque cambie su redaccion.

## Empresa

| ID | Regla | V1 |
|---|---|---|
| BR-1001 | Toda empresa pertenece a un unico tenant. | Si |
| BR-1002 | Un usuario puede pertenecer a varias empresas solo si fue invitado. | Si |
| BR-1003 | Una empresa debe tener al menos una sucursal. | Si |
| BR-1004 | No puede eliminarse la ultima sucursal; solo desactivarse. | Si |

## Productos

| ID | Regla | V1 |
|---|---|---|
| BR-2001 | Todo producto pertenece a una empresa. | Si |
| BR-2002 | Todo producto debe tener codigo unico dentro de la empresa. | Si |
| BR-2003 | El nombre puede repetirse, el codigo no. | Si |
| BR-2004 | No puede eliminarse un producto con movimientos; solo desactivarse. | Si |
| BR-2005 | Toda modificacion importante del producto genera auditoria. | Si |
| BR-2006 | Las fotos no eliminan el producto; solo cambian referencias. | Si |

## Inventario

| ID | Regla | V1 |
|---|---|---|
| BR-3001 | No se permite stock negativo salvo politica explicita por empresa. | Si |
| BR-3002 | Todo movimiento de inventario debe quedar registrado. | Si |
| BR-3003 | Todo ajuste requiere motivo. | Si |
| BR-3004 | El Kardex nunca puede editarse. | Si |
| BR-3005 | Los conteos fisicos generan diferencias; no modifican historial. | Si |

## Warehouse

| ID | Regla | V1 |
|---|---|---|
| BR-4001 | Una ubicacion pertenece a una sola bodega. | Si |
| BR-4002 | Un producto puede existir en varias ubicaciones. | Si |
| BR-4003 | No puede transferirse mas stock del disponible. | Si |
| BR-4004 | Toda transferencia tiene estados: pendiente, en transito, recibida, cancelada. | Si |
| BR-4005 | El picking solo puede marcarse completo una vez. | Si |

## POS

| ID | Regla | V1 |
|---|---|---|
| BR-5001 | No puede venderse con caja cerrada. | Si |
| BR-5002 | No puede venderse un producto inactivo. | Si |
| BR-5003 | Descuentos superiores al limite requieren autorizacion. | Si |
| BR-5004 | El precio puede modificarse solo segun permisos. | Si |
| BR-5005 | Todo ticket genera auditoria. | Si |
| BR-5006 | Un ticket puede existir sin pago. | Si |
| BR-5007 | Un ticket puede estar pendiente, pagado, anulado o expirado. | Si |

## Caja

| ID | Regla | V1 |
|---|---|---|
| BR-6001 | Solo puede existir una apertura activa por caja. | Si |
| BR-6002 | Toda apertura requiere monto inicial. | Si |
| BR-6003 | Todo cierre calcula diferencias. | Si |
| BR-6004 | Toda diferencia requiere motivo. | Si |
| BR-6005 | No puede cerrarse dos veces la misma caja. | Si |

## Ventas

| ID | Regla | V1 |
|---|---|---|
| BR-7001 | Toda venta debe estar asociada a un ticket. | Si |
| BR-7002 | Toda venta pagada debe tener al menos un metodo de pago. | Si |
| BR-7003 | Se permiten pagos mixtos. | Si |
| BR-7004 | Una venta anulada nunca desaparece. | Si |
| BR-7005 | Toda devolucion genera movimiento inverso. | Si |

## Compras

| ID | Regla | V1 |
|---|---|---|
| BR-8001 | No puede recibirse mas cantidad que la orden de compra salvo autorizacion. | Si |
| BR-8002 | Toda recepcion aumenta inventario mediante movimientos. | Si |

## Clientes

| ID | Regla | V1 |
|---|---|---|
| BR-9001 | El cliente puede ser opcional para boleta simple. | Si |
| BR-9002 | La factura requiere datos exigidos por normativa aplicable. | Si |

## Usuarios y seguridad

| ID | Regla | V1 |
|---|---|---|
| BR-10001 | Toda accion requiere autenticacion. | Si |
| BR-10002 | Toda accion requiere autorizacion. | Si |
| BR-10003 | Los permisos siempre se validan en backend. | Si |

## Billing

| ID | Regla | V1 |
|---|---|---|
| BR-12001 | Al vencer la suscripcion comienza periodo de gracia. | Si |
| BR-12002 | Al terminar el periodo de gracia la empresa pasa a modo suspendido. | Si |
| BR-12003 | Nunca se eliminan datos por falta de pago. | Si |

## SuperAdmin

| ID | Regla | V1 |
|---|---|---|
| BR-13001 | Ningun operador puede eliminar empresas fisicamente. | Si |
| BR-13002 | Todo cambio de plan queda auditado. | Si |
| BR-13003 | Toda modificacion de precios queda auditada. | Si |
| BR-13004 | Los Feature Flags afectan solo a empresas autorizadas. | Si |

## Reglas configurables por empresa

Tarevo debe permitir politicas de negocio configurables por empresa, por ejemplo:

- Permitir stock negativo.
- Requerir cliente en todas las ventas.
- Permitir modificar precios en POS.
- Permitir descuentos hasta cierto porcentaje.
- Requerir arqueo obligatorio.

## V2

Motor de reglas avanzado tipo Rule Engine.

## Regla para Codex
Antes de implementar una funcionalidad, Codex debe identificar las Business Rules aplicables. Si falta una regla, debe actualizarse este registro antes de implementar.
