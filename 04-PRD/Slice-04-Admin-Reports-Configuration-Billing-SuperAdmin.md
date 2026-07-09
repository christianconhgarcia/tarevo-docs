# Slice 04 — Reports, Configuration, Billing & SuperAdmin

Estado: Aprobado para especificacion V1
Prioridad: Alta
Mundo: Tenant ERP + Public Website + SuperAdmin

## Objetivo
Cerrar la V1 operativa de Tarevo incorporando reportes, configuracion, usuarios, billing, suscripciones, SuperAdmin, soporte y CMS de landing.

## Alcance V1

Incluye:

- Usuarios.
- Roles.
- Permisos.
- Configuracion empresa.
- Sucursales.
- Bodegas.
- Cajas.
- Politicas de negocio.
- Reportes basicos.
- Billing.
- Planes.
- Suscripciones.
- Periodo de gracia.
- Suspension.
- SuperAdmin.
- Customer Success.
- Tickets soporte.
- Landing CMS por bloques.
- Health checks basicos.
- Feature Flags.

No incluye V1:

- Motor avanzado de reglas.
- A/B testing real.
- IA Menora.
- SLA enterprise avanzado.
- Multi pais.

## Tenant ERP — Configuracion

Pantallas:

- Empresa.
- Sucursales.
- Bodegas.
- Cajas.
- Usuarios.
- Roles y permisos.
- Politicas de negocio.
- DTE placeholder.
- Integraciones placeholder.

Politicas configurables V1:

- Permitir stock negativo.
- Requerir cliente en ventas.
- Permitir modificar precios en POS.
- Descuento maximo sin autorizacion.
- Requerir arqueo obligatorio.

## Tenant ERP — Reportes

Reportes V1:

- Ventas por fecha.
- Ventas por caja.
- Ventas por vendedor.
- Productos mas vendidos.
- Stock actual.
- Stock bajo.
- Kardex.
- Movimientos de caja.
- Compras por proveedor.

Cada reporte debe soportar:

- Filtros por fecha.
- Filtros por sucursal si aplica.
- Exportacion si el usuario tiene permiso.
- Paginacion.

## Billing

Planes V1:

- Starter CLP 19.990.
- Pro CLP 34.990.
- Business CLP 59.990.
- Enterprise cotizacion.

Reglas:

- 7 dias de gracia.
- Suspender nuevas ventas tras gracia.
- No eliminar datos por falta de pago.
- Reactivacion automatica al pagar.
- Downgrade inactiva recursos excedentes, no los elimina.

## SuperAdmin Console

Modulos:

- Dashboard global.
- Empresas.
- Planes.
- Entitlements.
- Suscripciones.
- Pagos.
- Customer Success.
- Tickets.
- Landing CMS.
- Infraestructura.
- Feature Flags.
- Configuracion global.

Dashboard global debe mostrar:

- MRR.
- ARR.
- Clientes activos.
- Clientes suspendidos.
- Clientes en onboarding.
- Primera venta completada.
- Tickets abiertos.
- Pagos vencidos.
- Uso almacenamiento.
- Health checks.

## Customer Success

Estados de cliente:

- Registrado.
- Empresa creada.
- Onboarding incompleto.
- Primera venta completada.
- Activo.
- En riesgo.
- Suspendido.

Indicadores:

- Ultimo login.
- Ventas ultimos 7 dias.
- Onboarding %.
- Tickets abiertos.
- Pago vencido.

## Landing CMS

V1 sera CMS por bloques, no constructor visual.

Bloques editables:

- Hero.
- Beneficios.
- Apps.
- Planes.
- Comparativa.
- FAQ.
- Testimonios.
- SEO basico.

Tarevo controla el diseño; SuperAdmin controla el contenido.

## Reglas de negocio aplicables

- BR-10001 a BR-10003.
- BR-12001 a BR-12003.
- BR-13001 a BR-13004.
- Politicas configurables de negocio.

## Eventos

- UserInvited.
- RoleUpdated.
- PermissionUpdated.
- BusinessPolicyUpdated.
- ReportExported.
- SubscriptionActivated.
- SubscriptionPastDue.
- SubscriptionSuspended.
- SupportTicketCreated.
- FeatureFlagUpdated.
- LandingBlockUpdated.
- HealthCheckFailed.

## APIs principales

- Gestion de usuarios.
- Gestion de roles.
- Gestion de permisos.
- Actualizar configuracion empresa.
- Actualizar politicas de negocio.
- Consultar reportes.
- Exportar reportes.
- Listar planes.
- Gestionar suscripcion.
- SuperAdmin listar empresas.
- SuperAdmin cambiar plan.
- SuperAdmin suspender empresa.
- Crear/gestionar tickets.
- Editar bloques landing.
- Health checks.

## Permisos

Tenant:

- users.view/invite/update/disable.
- roles.manage.
- permissions.manage.
- reports.view/export/view_profit/view_cash/view_inventory.
- settings.company.update.
- settings.branches.manage.
- settings.warehouses.manage.
- settings.cash_registers.manage.

SuperAdmin:

- platform.tenants.view.
- platform.tenants.update.
- platform.tenants.suspend.
- platform.billing.manage.
- platform.support.manage.
- platform.cms.manage.
- platform.infrastructure.view.
- platform.feature_flags.manage.

## Casos limite

- Usuario intenta superar limite del plan.
- Cliente baja de plan con recursos excedentes.
- Suscripcion vencida.
- Empresa suspendida intentando vender.
- Reporte muy grande.
- Usuario sin permiso intenta exportar.
- CMS con contenido incompleto.
- Feature flag mal configurado.

## Definition of Done

- Configuracion completa para operar tenant.
- Reportes basicos funcionales.
- Billing con gracia y suspension.
- SuperAdmin operativo.
- Customer Success visible.
- Tickets soporte funcionales.
- CMS landing editable por bloques.
- Auditoria y permisos activos.

## Prompt base para Codex
Implementa Slice 04 como capa administrativa y comercial de Tarevo. Separar claramente Tenant ERP de SuperAdmin. No mezclar permisos de cliente con permisos internos de plataforma. No implementar CMS libre tipo WordPress; usar bloques estructurados.
