# Fase 8 — QA integral y piloto controlado

Estado: En ejecución

## Decisión de secuencia

La Fase 7, correspondiente a la activación real de Flow y DTE, se pospone para el cierre final. La Fase 8 se ejecuta antes para validar el núcleo interno de Tarevo sin depender de proveedores externos.

## Objetivo

Comprobar que Tarevo puede operar de forma segura, consistente y usable con un tenant piloto antes de abrir una beta controlada.

## Alcance

- Suite CI completa.
- QA funcional por módulo.
- QA por perfiles y permisos.
- Aislamiento multi-tenant.
- Cambio seguro de empresa activa.
- Responsive y accesibilidad.
- Smoke test de producción.
- Backup y restauración.
- Health checks, worker y scheduler.
- Registro y priorización de incidencias.
- Decisión GO/NO-GO.

## Perfiles mínimos

- Propietario.
- Administrador.
- Supervisor.
- Cajero.
- Vendedor.
- Bodeguero.
- Usuario multiempresa.
- SuperAdmin.

Los escenarios se validan por permisos efectivos; los nombres de rol se usan únicamente para organizar la matriz de QA.

## Flujos críticos

1. Registro, verificación, login y onboarding.
2. Creación o importación de productos.
3. Apertura de caja y primera venta.
4. Venta inmediata y ticket enviado a caja principal.
5. Pago simple y mixto.
6. Arqueo ciego y cierre.
7. Devolución parcial y comprobante.
8. Compra y recepción parcial/total.
9. Transferencia con recepción y diferencias.
10. Conteo físico y ajuste.
11. Picking y packing.
12. Gestión de usuarios, roles e invitaciones.
13. Cambio multiempresa.
14. Reportes y exportaciones.
15. SuperAdmin: empresa, soporte, CMS, flags e infraestructura.

## Evidencia

Cada prueba debe registrar:

- fecha;
- ambiente y versión;
- perfil;
- tenant, sucursal y caja;
- ruta;
- pasos;
- resultado esperado;
- resultado obtenido;
- evidencia;
- severidad;
- responsable y estado.

## Severidades

- P0: pérdida de datos, fuga cross-tenant, cobro incorrecto o sistema inutilizable.
- P1: flujo crítico bloqueado sin alternativa.
- P2: función degradada con alternativa.
- P3: incidencia visual, texto o mejora.

## Definition of Done

- CI completa en verde.
- Cero P0 abiertas.
- Cero P1 abiertas.
- Aislamiento tenant validado.
- Flujos críticos completados.
- Responsive validado en 1440×900, 1024×768 y 390×844.
- Backup y restauración comprobados.
- Health checks operativos.
- Tenant piloto aislado.
- Soporte y rollback definidos.
- Decisión GO/NO-GO documentada.

## Siguiente fase

Después de Fase 8 corresponde la beta controlada. La activación externa de Flow y DTE se realizará al final, cuando el núcleo interno y el piloto estén aprobados.
