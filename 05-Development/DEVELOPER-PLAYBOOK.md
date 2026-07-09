# Tarevo Developer Playbook

Estado: Aprobado
Version: 0.1

## Objetivo
Dar a Codex y a cualquier desarrollador humano una guia unica para construir Tarevo sin improvisar arquitectura, patrones ni reglas.

## Lectura obligatoria antes de programar

1. Constitution.
2. Product Vision.
3. Architecture.
4. Infrastructure.
5. Security.
6. Database Model.
7. Permission Matrix.
8. Business Rules Registry.
9. Event Registry.
10. API Registry.
11. Slice correspondiente.

## Principios obligatorios

- No hardcodear secretos.
- No saltarse tenant_id.
- No confiar en frontend.
- No modificar stock directamente.
- No crear endpoints sin permisos.
- No crear pantallas no registradas.
- No agregar servicios pagos sin aprobacion.
- No implementar V2 dentro de V1.

## Flujo de desarrollo

```text
Leer Slice
  -> Identificar pantallas
  -> Identificar APIs
  -> Identificar reglas
  -> Crear migraciones
  -> Crear backend
  -> Crear frontend
  -> Agregar eventos
  -> Agregar auditoria
  -> Agregar tests
  -> Validar Definition of Done
```

## Como crear un modulo

Cada modulo debe incluir:

- Dominio.
- Modelos.
- Migraciones.
- Servicios.
- Policies.
- Requests/validaciones.
- Controllers/API.
- Eventos.
- Tests.
- UI.

## Como crear una pantalla

Cada pantalla debe declarar:

- Screen ID.
- Mundo.
- Modulo.
- Ruta.
- Roles/permisos.
- Estados UI.
- APIs.
- Eventos.
- Business Rules.

## Como crear una API

Cada API debe:

- Validar autenticacion.
- Validar tenant.
- Validar permisos.
- Validar entitlements si aplica.
- Validar datos.
- Ejecutar logica en servicio.
- Registrar auditoria si aplica.
- Emitir eventos si aplica.
- Responder errores consistentes.

## Como crear migraciones

Reglas:

- Usar UUID publico cuando corresponda.
- Usar tenant_id en tablas de negocio.
- Usar timestamps.
- Usar soft deletes para entidades criticas.
- Crear indices por tenant, estado, fecha, codigo y busquedas frecuentes.
- No eliminar columnas criticas sin ADR.

## Testing minimo

Cada modulo debe tener:

- Tests de permisos.
- Tests de tenant isolation.
- Tests de reglas de negocio.
- Tests de flujo feliz.
- Tests de errores importantes.

## Commits

Usar conventional commits:

- feat:
- fix:
- docs:
- refactor:
- test:
- chore:

## Regla final
Si Codex no esta seguro, debe detenerse y dejar pregunta/TODO documentado. No debe inventar reglas de negocio.
