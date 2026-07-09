# Slice 01 — Customer Activation

Estado: Aprobado para especificacion V1
Prioridad: Critica
Mundo: Public Website + Tenant ERP + SuperAdmin

## Objetivo
Permitir que un visitante pase de conocer Tarevo a realizar su primera venta sin ayuda del soporte.

Meta de activacion: registro -> primera venta en menos de 15 minutos.

## Alcance V1

Incluye:

- Landing publica.
- Registro.
- Login.
- Recuperacion de contrasena.
- Verificacion de correo.
- Crear empresa.
- Crear sucursal.
- Crear bodega.
- Crear caja.
- Crear primer producto.
- Abrir caja.
- Primera venta.
- Dashboard inicial.
- Checklist inteligente de onboarding.
- Eventos de Customer Success.

No incluye:

- Configuracion tributaria SII.
- Certificado digital.
- DTE.
- WooCommerce.
- Mercado Libre.
- IA Menora.
- App movil.

## Principio clave
La configuracion tributaria no bloquea la primera venta. El cliente puede descubrir valor antes de subir certificado digital o configurar DTE.

## Flujo principal

```text
Landing
  -> Planes
  -> Registro
  -> Verificar correo
  -> Crear empresa
  -> Dashboard inicial
  -> Checklist onboarding
  -> Crear sucursal
  -> Crear bodega
  -> Crear caja
  -> Crear producto
  -> Abrir caja
  -> POS
  -> Primera venta
  -> Dashboard operativo
```

## Pantallas

- SCR-PW-001 Landing.
- SCR-PW-002 Planes.
- SCR-PW-004 Registro.
- SCR-PW-005 Login.
- SCR-PW-006 Recuperar contrasena.
- SCR-PW-007 Verificar correo.
- SCR-TE-001 Dashboard inicial.
- SCR-TE-002 Checklist onboarding.
- SCR-TE-003 Crear empresa.
- SCR-TE-004 Crear sucursal.
- SCR-TE-005 Crear bodega.
- SCR-TE-006 Crear caja.
- SCR-TE-008 Crear producto.
- SCR-TE-019 POS.
- SCR-TE-020 Apertura de caja.

## Reglas de negocio aplicables

- BR-1001 Empresa pertenece a tenant.
- BR-1003 Empresa debe tener al menos una sucursal.
- BR-2002 Codigo de producto unico por empresa.
- BR-5001 No puede venderse con caja cerrada.
- BR-6001 Solo una apertura activa por caja.
- BR-7001 Venta asociada a ticket.
- BR-7002 Venta pagada requiere metodo de pago.
- BR-10001 Toda accion requiere autenticacion.
- BR-10002 Toda accion requiere autorizacion.

## Eventos

- UserRegistered.
- EmailVerified.
- TenantCreated.
- BranchCreated.
- WarehouseCreated.
- CashRegisterCreated.
- ProductCreated.
- CashOpened.
- TicketCreated.
- PaymentRecorded.
- SaleCompleted.
- FirstSaleCompleted.

## APIs principales

- API-001 Registrar usuario.
- API-002 Verificar correo.
- API-003 Login.
- API-004 Crear tenant.
- API-005 Crear sucursal.
- API-006 Crear bodega.
- API-007 Crear caja.
- API-008 Crear producto.
- API-011 Abrir caja.
- API-013 Crear ticket.
- API-014 Registrar pago.
- API-015 Completar venta.

## Entidades principales

- User.
- Tenant.
- Company.
- Branch.
- Warehouse.
- CashRegister.
- CashSession.
- Product.
- InventoryItem.
- Ticket.
- Sale.
- Payment.
- AuditLog.
- OnboardingProgress.

## UX

Dashboard inicial no debe estar vacio. Debe mostrar checklist:

- Crear empresa.
- Crear sucursal.
- Crear bodega.
- Crear caja.
- Crear producto.
- Abrir caja.
- Primera venta.

Al completar la primera venta se muestra mensaje de celebracion.

## SuperAdmin / Customer Success

SuperAdmin debe ver clientes en estados:

- Registrado sin empresa.
- Empresa creada sin primera venta.
- Onboarding incompleto.
- Primera venta completada.

## Casos limite

- Email ya registrado.
- Subdominio ocupado.
- Usuario abandona onboarding.
- Caja ya abierta.
- Producto sin stock.
- Pago incompleto.
- Venta fallida por permisos.

## Definition of Done

- Registro, login y recuperacion funcionando.
- Verificacion por correo funcionando.
- Tenant creado con aislamiento.
- Checklist persistente.
- Primera venta completa.
- Eventos y auditoria activos.
- Permisos validados en backend.
- Responsive desktop/tablet/mobile.
- Tests de flujo principal.

## Prompt base para Codex
Implementa Slice 01 siguiendo Constitution, Security, Infrastructure, Database Model, Permission Matrix, Event Registry, API Registry y Business Rules Registry. No implementar DTE ni certificado SII en este slice. Priorizar flujo registro -> primera venta.
