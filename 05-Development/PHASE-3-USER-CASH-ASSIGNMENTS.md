# Phase 3 - User Cash Assignments

Version: 0.1
Estado: Implementado localmente
Fecha: 2026-07-14

## Objetivo

Cerrar la brecha entre permisos generales de caja y autorizacion operativa real por usuario, sucursal y caja.

## Alcance implementado

- Asignacion de usuarios a sucursales autorizadas.
- Asignacion de usuarios a cajas autorizadas.
- Sucursal principal y caja predeterminada por usuario.
- Indicador `can_switch_cash_register` para permitir o bloquear cambio de caja entre cajas autorizadas.
- Restriccion backend para abrir caja solo si el usuario tiene asignacion activa o acceso global administrativo.
- Restriccion backend para impedir mas de una sesion de caja abierta por usuario.
- Restriccion backend para impedir administrar sesiones de caja abiertas por otro usuario, salvo acceso global administrativo.
- Contexto POS/caja con sucursal, caja, usuario y sesion activa.
- Administracion de asignaciones desde `Administracion > Usuarios`.

## Acceso global administrativo

Un usuario se considera operador global de caja solo si tiene todos estos permisos:

```text
settings.cash_registers.manage
cash.open
cash.view
```

Los usuarios sin ese acceso global deben tener asignaciones explicitas para operar caja.

## Nuevas entidades

### user_branch_assignments

Relaciona un usuario con una sucursal autorizada dentro del tenant.

Campos principales:

- tenant_id
- user_id
- branch_id
- is_primary
- is_active
- assigned_by
- updated_by
- deactivated_by
- assigned_at
- deactivated_at

### user_cash_register_assignments

Relaciona un usuario con una caja autorizada dentro del tenant.

Campos principales:

- tenant_id
- user_id
- branch_id
- cash_register_id
- is_default
- can_switch_cash_register
- is_active
- assigned_by
- updated_by
- deactivated_by
- assigned_at
- deactivated_at

## APIs implementadas

| Metodo | Ruta | Permiso | Uso |
|---|---|---|---|
| GET | `/api/v1/admin/users/{id}/cash-assignments` | `users.view` | Obtener asignacion operativa de un usuario |
| PUT | `/api/v1/admin/users/{id}/cash-assignments` | `users.update` | Guardar sucursales, cajas, principal, predeterminada y cambio de caja |
| GET | `/api/v1/pos/context` | `sales.pos_access` | Devuelve contexto POS con asignaciones autorizadas |
| GET | `/api/v1/cash-registers` | `cash.view` | Devuelve solo cajas autorizadas para el usuario, salvo acceso global |
| POST | `/api/v1/cash-sessions/open-session` | `cash.open` | Valida asignacion antes de abrir caja |

## Auditoria y eventos

Acciones auditadas:

- `user_branch_assignment.created`
- `user_branch_assignment.updated`
- `user_branch_assignment.deactivated`
- `user_cash_register_assignment.created`
- `user_cash_register_assignment.updated`
- `user_cash_register_assignment.deactivated`
- `cash_assignment.rejected`

Evento interno:

- `UserCashAssignmentsUpdated`

## Compatibilidad preservada

- Owner/Admin mantienen operacion global por permisos existentes.
- Los modos POS `direct`, `central` e `hybrid` no cambian.
- Las reglas de inventario, billing, planes y DTE no cambian.
- Los endpoints de caja existentes conservan sus rutas y payloads principales.

## Verificacion local

- `npm run build --prefix apps/web`
- `npm run test --prefix apps/web -- CashTab CashClosureHistory`
- `npm run test --prefix apps/web`

Backend pendiente de ejecucion local por entorno: no hay `php`/`composer` en PATH y Docker Desktop no estaba activo al verificar.
