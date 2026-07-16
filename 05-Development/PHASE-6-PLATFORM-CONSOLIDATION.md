# Fase 6 — Consolidación documental y cierre de pantallas de plataforma

Version: 1.0
Estado: Implementada en rama de trabajo

## Objetivo

Cerrar la brecha entre la documentación histórica de Tarevo y el estado real de la rama `production`, sin ampliar innecesariamente el núcleo ERP V1.

La fase consolida tres pantallas que sí aportan valor antes del piloto:

1. Comparativa pública de planes.
2. Ficha integral de empresa en SuperAdmin.
3. Configuración global de SuperAdmin.

También actualiza el estado oficial del proyecto y deja explícitas las dependencias externas de Flow y DTE.

## Fuera de alcance

- Conectar credenciales reales de Flow.
- Contratar o activar proveedor DTE.
- Crear un portal público del cliente.
- Separar Planes y FAQ en páginas independientes adicionales.
- Cambiar reglas de negocio del Tenant ERP.
- Cambiar permisos, migraciones o contratos existentes.
- Reemplazar la experiencia consolidada de Catálogo.
- Modificar el POS aprobado.

## Decisiones

### Planes y FAQ

Se mantienen dentro del landing principal para evitar duplicación de contenido. La nueva comparativa pública complementa esas secciones con una tabla detallada.

### Gestión de suscripción

Se mantiene autenticada dentro de `Administración > Plan, facturación y soporte`. No se crea portal público separado en esta fase.

### Portal del cliente

Se posterga hasta validar necesidad comercial durante beta.

### Ajustes de inventario

La funcionalidad permanece dentro de Inventario/Kardex. No se crea una ruta principal adicional en esta fase.

## Pantalla 1 — Comparativa pública de planes

### Mundo

Public Website

### Ruta

`/compare`

### Acceso

Público.

### Contenido

- Starter.
- Pro.
- Business.
- Enterprise.
- Precio comercial aprobado.
- Descripción de cada plan.
- Tabla comparativa.
- Empresas, sucursales y usuarios.
- POS y caja.
- Caja principal y pagos mixtos.
- Inventario y Kardex.
- Warehouse, picking y packing.
- Reportes.
- DTE Chile.
- WooCommerce.
- Soporte.
- Límites y entitlements.
- CTA de registro o cotización.

### Reglas

- La tabla comercial es orientativa.
- Los límites efectivos provienen de la suscripción y entitlements del backend.
- Los cambios de plan no se activan sin confirmación del proveedor de pagos.
- Enterprise continúa como cotización.
- No se simulan cobros.

## Pantalla 2 — Ficha integral de empresa

### Mundo

SuperAdmin Console

### Ubicación

`SuperAdmin > Empresas > Ver detalle`

### Acceso

Sesión con rol de plataforma y permisos existentes de gestión/lectura de empresas.

### Contenido

- Nombre comercial.
- Slug interno.
- Estado de empresa.
- Usuarios registrados.
- Plan.
- Estado de suscripción.
- MRR de la suscripción.
- Ciclo de cobro.
- Renovación.
- Periodo de gracia.
- Progreso de onboarding.
- Última actividad.
- Señales de riesgo.
- Soporte relacionado cuando el contrato actual permite asociarlo.
- Acción de suspender o reactivar.

### Reglas

- No se cambia el plan directamente desde la ficha.
- Suspensión y reactivación reutilizan el endpoint existente.
- No se exponen secretos.
- No se mezclan permisos tenant con permisos de plataforma.

## Pantalla 3 — Configuración global

### Mundo

SuperAdmin Console

### Ubicación

`SuperAdmin > Configuración global`

### Acceso

Sesión de plataforma.

### Contenido inicial

- Mercado inicial.
- Moneda y contexto tributario.
- Duración canónica del trial.
- Periodo de gracia.
- Resumen de bloques CMS publicados.
- Resumen de feature flags habilitados.
- Empresas activas.
- Estado de proveedores externos.
- Reglas globales de seguridad.

### Alcance de escritura

La primera versión es una vista consolidada y segura. No permite editar secretos, URLs críticas ni políticas globales no modeladas en backend.

Los cambios ya soportados continúan en:

- Landing CMS.
- Feature Flags.
- Empresas.
- Suscripciones.
- Soporte.

## Documentación actualizada

- `PROJECT_STATUS.md`.
- Este documento de Fase 6.
- El Screen Registry y Navigation Master deben referenciar esta fase al fusionarse.

## Archivos principales de implementación

- `apps/web/src/pages/ComparePlansPage.tsx`
- `apps/web/src/pages/ComparePlansPage.css`
- `apps/web/src/pages/ComparePlansPage.test.tsx`
- `apps/web/src/App.tsx`
- `apps/web/src/shells/SuperAdminShell.tsx`
- `apps/web/src/shells/SuperAdminPhase6.css`

## Criterios de aceptación

- `/compare` es accesible sin sesión.
- La comparativa presenta los cuatro planes.
- Enterprise conserva flujo de cotización.
- La tabla no promete límites que sustituyan entitlements.
- SuperAdmin incorpora `Configuración global`.
- Desde Empresas se puede abrir una ficha integral.
- La ficha reutiliza datos reales de `PlatformOverview`.
- Suspender/reactivar sigue usando el endpoint existente.
- No se agregan secretos ni credenciales.
- No se alteran reglas del Tenant ERP.
- Frontend build aprobado.
- Tests frontend aprobados.
- Diseño responsive revisado.

## Pendientes posteriores

### Fase 7 — Activación Flow y DTE

- Credenciales sandbox.
- URLs productivas.
- Checkout y webhook Flow.
- Proveedor DTE.
- Certificado.
- Emisión sandbox.
- PDF/XML.
- Piloto controlado.

### Fase 8 — QA integral y piloto

- Perfiles owner, administrador, supervisor, cajero, vendedor y bodeguero.
- Multiempresa.
- Responsive.
- Backups y restauración.
- Workers y scheduler.
- Prueba de operación completa.

### Fase 9 — Beta controlada

- Tenant piloto.
- Criterios GO/NO-GO.
- Soporte.
- Registro de incidencias.
- Release candidate.
