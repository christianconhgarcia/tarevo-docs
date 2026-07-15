# Phase 4: Permissions, Roles, and Dynamic Navigation

## Objective

Phase 4 centralizes tenant permission resolution and uses the resulting context consistently across API authorization, role administration, invitations, user assignment, and frontend navigation.

The application must not rely on role names in the frontend for access decisions. UI visibility is a convenience layer only; backend permissions remain the enforcement layer.

## Effective Permission Model

Effective tenant permissions are resolved from:

- Active global or tenant-specific roles assigned to the user for the current tenant.
- Tenant role permission overrides when a role has tenant-specific permissions.
- Canonical role permissions when a role has no tenant-specific override.
- Active user account status.
- Active tenant status.
- Active tenant membership.

Tenant overrides are evaluated per role. An override on one assigned role does not remove baseline permissions from another assigned role.

Platform permissions are excluded from tenant permission resolution and remain separate platform-console permissions.

## `/api/me` Tenant Context

Authenticated tenant requests return:

- `user`
- `tenant`
- `membership.status`
- `roles`
- `permissions`
- `capabilities`
- `operational_context.cash`

The frontend uses this context to persist the active session, filter navigation, guard routes, and show permitted actions.

## Roles

Tenant role management supports:

- Viewing canonical and tenant-specific roles.
- Editing tenant-visible role name and description.
- Editing tenant role permissions with dependency validation.
- Creating tenant-specific custom roles.
- Cloning an existing role into a tenant-specific role.
- Activating and deactivating roles.

Protected roles:

- `owner` stays active.
- `owner` keeps all tenant permissions.
- The last active owner cannot be disabled or demoted.

Role assignment supports multiple roles per user. A user can only assign roles whose permissions they are allowed to grant, unless they hold `permissions.manage`.

## Invitations

Invitations support multiple tenant roles through `role_ids` while remaining backward compatible with `role_id`.

Invitation validation ensures:

- Roles belong to the tenant or are canonical tenant roles.
- Platform roles cannot be assigned through tenant invitations.
- Inactive roles cannot be assigned.
- The inviter cannot grant permissions outside their effective permission set unless they hold `permissions.manage`.

## Navigation And Route Guards

Tenant navigation declares permission keys for each module. The shell filters navigation groups using the effective permissions from `/api/me`.

Routes are guarded separately so direct URLs do not bypass hidden navigation.

Examples:

- `/app/cash` requires `cash.view`.
- `/app/catalog/pricing` requires `products.update`.
- `/app/admin` accepts administrative permissions such as `settings.company.update`, `users.view`, or `roles.manage`, then loads only allowed sections.
- `/pos` requires `sales.pos_access`.

## Operational Restrictions

Phase 3 user-branch-cash assignment remains enforced:

- Users without active cash assignment remain blocked unless they have the intended global cash access permissions.
- Unauthorized cash registers are rejected.
- Cross-tenant resources are blocked by tenant scoping.
- A user can keep only one open cash session.

## Manual QA Checklist

1. Log in as owner.
2. Open Administracion > Empresa and create/edit a branch.
3. Open Ventas y caja > Cajas y sesiones and create/edit/activate/deactivate a cash register.
4. Open Administracion > Usuarios and confirm the created cash register appears in user cash assignment.
5. Assign a user to an active branch and active cash register.
6. Log in as that user and confirm `/api/me` includes only their effective roles, permissions, capabilities, and cash context.
7. Confirm the user can open only the assigned cash register.
8. Confirm a user without assignment still receives the cash assignment rejection.
9. Confirm a cross-tenant cash register is rejected.
10. Confirm a second open session for the same user is rejected.
11. Create a custom role and assign only view permissions.
12. Confirm navigation hides modules outside that role.
13. Try direct URLs for hidden modules and confirm the route guard shows no access.
14. Try to disable or demote the last owner and confirm the API rejects it.
15. Clone a role, deactivate the clone, and confirm it is not assignable.
16. Confirm POS opens in the popup and does not show configuration actions without the required permission.
17. Navigate between modules and confirm the global “Validando sesion...” screen does not reappear during internal tenant navigation.

## Validation Commands

```bash
cd apps/api
php artisan test
composer audit

cd ../..
npm run test --prefix apps/web
npm run build --prefix apps/web
npm audit --prefix apps/web
git diff --check
docker compose config
```
