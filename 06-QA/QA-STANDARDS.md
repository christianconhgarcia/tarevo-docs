# QA Standards

Estado: Aprobado
Version: 0.1

## Objetivo
Definir el estandar minimo de calidad antes de considerar terminado un slice, pantalla, API o release.

## Tipos de prueba

### Backend

- Unit tests.
- Feature tests.
- Permission tests.
- Tenant isolation tests.
- Business rule tests.

### Frontend

- Render basico.
- Estados loading/empty/error/success.
- Validaciones.
- Responsive.
- Accesibilidad basica.

### Integracion

- Flujos completos por slice.
- Registro -> primera venta.
- Compra -> recepcion -> stock.
- POS -> pago -> venta.

## Checklist por slice

- Todas las APIs protegidas.
- Todas las reglas aplicables implementadas.
- Eventos emitidos.
- Auditoria registrada.
- Permisos backend validados.
- Entitlements validados.
- UI no muestra funciones no disponibles.
- Errores claros.
- Tests principales pasan.

## Bugs

Se clasifican:

- Critico: bloquea operacion o compromete datos/seguridad.
- Alto: rompe flujo importante.
- Medio: afecta uso pero tiene alternativa.
- Bajo: visual o menor.

## No se puede lanzar si

- Hay bugs criticos.
- Hay fuga de tenant.
- Hay endpoints sin permisos.
- Hay secretos expuestos.
- Hay migraciones destructivas sin respaldo.

## Regla para Codex
Codex debe crear o actualizar tests junto con la funcionalidad. No se acepta feature critica sin tests minimos.
