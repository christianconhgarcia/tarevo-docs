# Event Registry

Version: 0.1
Estado: Aprobado como estructura inicial

## Objetivo
Definir los eventos de negocio y plataforma que permitiran desacoplar modulos en Tarevo.

## Principio
Toda accion relevante genera un evento. Los modulos escuchan eventos sin acoplarse directamente entre si.

## Convencion

- EVT: Event
- Nombre en PascalCase
- Versionar eventos si cambian de contrato

## Eventos iniciales

| ID | Evento | Productor | Consumidores iniciales | V1 |
|---|---|---|---|---|
| EVT-001 | UserRegistered | Auth | Audit, Analytics, Customer Success | Si |
| EVT-002 | EmailVerified | Auth | Customer Success | Si |
| EVT-003 | TenantCreated | Core | Billing, Audit, Analytics | Si |
| EVT-004 | BranchCreated | Core | Audit, Onboarding | Si |
| EVT-005 | WarehouseCreated | Warehouse | Audit, Onboarding | Si |
| EVT-006 | CashRegisterCreated | Cash | Audit, Onboarding | Si |
| EVT-007 | ProductCreated | Products | Inventory, Audit, Search | Si |
| EVT-008 | ProductUpdated | Products | Audit, Search | Si |
| EVT-009 | StockAdjusted | Inventory | Audit, Reports | Si |
| EVT-010 | CashOpened | Cash | Audit, Reports | Si |
| EVT-011 | CashClosed | Cash | Audit, Reports | Si |
| EVT-012 | TicketCreated | POS | Audit, Reports | Si |
| EVT-013 | TicketCancelled | POS | Audit, Reports | Si |
| EVT-014 | PaymentRecorded | POS/Cash | Cash, Reports, Audit | Si |
| EVT-015 | SaleCompleted | POS | Inventory, Cash, Reports, Audit, Customer Success | Si |
| EVT-016 | FirstSaleCompleted | POS | Onboarding, Customer Success, Analytics | Si |
| EVT-017 | TransferRequested | Warehouse | Inventory, Audit | Si |
| EVT-018 | TransferReceived | Warehouse | Inventory, Reports, Audit | Si |
| EVT-019 | SubscriptionActivated | Billing | Entitlements, Audit | Si |
| EVT-020 | SubscriptionPastDue | Billing | SuperAdmin, Notifications | Si |
| EVT-021 | SubscriptionSuspended | Billing | Entitlements, Notifications | Si |
| EVT-022 | StorageLimitWarning | Platform | Notifications, SuperAdmin | Si |
| EVT-023 | SupportTicketCreated | Support | SuperAdmin, Customer Success | Si |
| EVT-024 | DteIssued | DTE | Reports, Audit | Si |
| EVT-025 | BackupCompleted | Infrastructure | SuperAdmin, Audit | Si |
| EVT-026 | BackupFailed | Infrastructure | SuperAdmin, Alerts | Si |
| EVT-027 | UserCashAssignmentsUpdated | Admin | Audit, Reports, Customer Success | Si |

## Estructura minima de evento

```json
{
  "event_id": "uuid",
  "event_name": "SaleCompleted",
  "event_version": "1.0",
  "tenant_id": "uuid|null",
  "actor_id": "uuid|null",
  "occurred_at": "datetime",
  "payload": {}
}
```

## Reglas

- Los eventos no reemplazan la base de datos transaccional.
- Los eventos deben ser idempotentes cuando sea posible.
- Los consumidores no deben romper la operacion principal si fallan procesos secundarios.
- Los eventos criticos deben quedar auditados.

## Regla para Codex
Cada nuevo evento debe agregarse a este registro antes de implementarse.
