# API Registry

Version: 0.1
Estado: Aprobado como estructura inicial

## Objetivo
Definir contratos de negocio para APIs de Tarevo. Este documento no es solo una lista de endpoints; define actores, permisos, reglas, eventos, entidades y errores.

## Convencion

- API: contrato de API
- Los endpoints finales pueden ajustarse, pero el contrato de negocio debe respetarse.

## Contratos iniciales

| ID | Contrato | Mundo | Permiso | Eventos |
|---|---|---|---|---|
| API-001 | Registrar usuario | Public Website | publico | UserRegistered |
| API-002 | Verificar correo | Public Website | publico | EmailVerified |
| API-003 | Login | Public Website | publico | LoginSucceeded/LoginFailed |
| API-004 | Crear tenant/empresa | Tenant ERP | authenticated | TenantCreated |
| API-005 | Crear sucursal | Tenant ERP | settings.branches.manage | BranchCreated |
| API-006 | Crear bodega | Tenant ERP | settings.warehouses.manage | WarehouseCreated |
| API-007 | Crear caja | Tenant ERP | settings.cash_registers.manage | CashRegisterCreated |
| API-008 | Crear producto | Tenant ERP | products.create | ProductCreated |
| API-009 | Actualizar producto | Tenant ERP | products.update | ProductUpdated |
| API-010 | Ajustar stock | Tenant ERP | inventory.adjust | StockAdjusted |
| API-011 | Abrir caja | Tenant ERP | cash.open | CashOpened |
| API-012 | Cerrar caja | Tenant ERP | cash.close | CashClosed |
| API-013 | Crear ticket | Tenant ERP | sales.create | TicketCreated |
| API-014 | Registrar pago | Tenant ERP | sales.create | PaymentRecorded |
| API-015 | Completar venta | Tenant ERP | sales.create | SaleCompleted |
| API-016 | Anular ticket | Tenant ERP | sales.cancel | TicketCancelled |
| API-017 | Crear transferencia | Tenant ERP | warehouse.transfer | TransferRequested |
| API-018 | Recibir transferencia | Tenant ERP | warehouse.receive | TransferReceived |
| API-019 | Listar empresas | SuperAdmin | platform.tenants.view | none |
| API-020 | Cambiar plan | SuperAdmin | platform.billing.manage | SubscriptionChanged |
| API-021 | Suspender empresa | SuperAdmin | platform.tenants.suspend | SubscriptionSuspended |
| API-022 | Crear ticket soporte | Public/Tenant | support.create | SupportTicketCreated |
| API-023 | Consultar asignacion operativa de usuario | Tenant ERP | users.view | none |
| API-024 | Actualizar asignacion operativa de usuario | Tenant ERP | users.update | UserCashAssignmentsUpdated |

## Formato de contrato

Cada API debe documentarse asi:

```text
API-XXX
Nombre:
Actor:
Mundo:
Permisos:
Entitlements:
Business Rules:
Eventos:
Entidades:
Errores posibles:
Auditoria:
```

## Reglas globales

- Toda API de negocio valida tenant.
- Toda API privada valida autenticacion.
- Toda API critica valida permisos.
- Toda API dependiente de plan valida entitlements.
- Ninguna API confia en datos enviados por frontend.
- Las respuestas de error deben ser consistentes.
- Toda API paginada debe soportar filtros y ordenamiento cuando aplique.
- Las APIs de caja deben validar permiso y asignacion operativa de usuario cuando el usuario no tenga acceso global administrativo.

## Regla para Codex
Codex no debe crear endpoints nuevos sin registrarlos aqui o vincularlos a un contrato existente.
