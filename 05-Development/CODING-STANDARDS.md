# Coding Standards

Estado: Aprobado
Version: 0.1

## Objetivo
Definir estandares de codigo para mantener Tarevo legible, seguro y mantenible.

## Backend

- Seguir convenciones de Laravel.
- Usar servicios para logica de negocio.
- Usar Form Requests para validacion.
- Usar Policies/Gates para autorizacion.
- Usar eventos para acciones relevantes.
- Evitar controladores con logica extensa.
- Evitar archivos gigantes.

## Frontend

- React + TypeScript.
- Componentes pequenos.
- Props tipadas.
- Estados explicitos.
- No duplicar componentes.
- No mezclar logica de negocio con UI compleja.
- Manejo consistente de loading, empty, error y success.

## Naming

- Codigo en ingles.
- UI en espanol.
- Entidades segun Domain Dictionary.
- No usar terminos prohibidos.

## Seguridad

- No secretos en codigo.
- No logs de tokens/passwords.
- No endpoints sin auth salvo publicos.
- No queries sin tenant cuando aplique.

## Performance

- Paginacion obligatoria en listados grandes.
- Evitar N+1.
- Indices para filtros frecuentes.
- No cargar todo si no es necesario.

## Calidad

- ESLint/Prettier o equivalentes.
- Tests obligatorios en logica critica.
- Conventional commits.
- Documentar decisiones raras con ADR.

## Regla para Codex
Codex debe priorizar claridad y mantenibilidad sobre soluciones rapidas o magicas.
