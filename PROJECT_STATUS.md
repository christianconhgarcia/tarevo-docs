# Tarevo Project Status

Version: 0.2
Estado: Vivo

## Producto

- Marca: Tarevo
- Dominio: gettarevo.com
- Mercado inicial: Chile
- Modelo: SaaS ERP para PYMEs
- Estado: V1 funcional cerrada; QA y piloto en progreso

## Hitos

| Hito | Nombre | Estado |
|---|---|---|
| HITO-01 | Empresa | Completado |
| HITO-02 | Arquitectura | Completado |
| HITO-03 | Blueprint | Cerrado conceptualmente |
| HITO-04 | PRD / Product Specification | Actualizado |
| HITO-05 | Desarrollo V1 | Completado |
| HITO-06 | Consolidacion de pantallas y documentos | Completado |
| HITO-07 | Activacion externa Flow / DTE | Postergado para el final |
| HITO-08 | QA integral y piloto | En progreso |
| HITO-09 | Beta controlada | Pendiente |

## Decisiones principales

- Marca: Tarevo.
- Dominio: gettarevo.com.
- Backend: Laravel.
- Frontend: React + TypeScript + Vite.
- Base de datos: PostgreSQL.
- Arquitectura: monolito modular.
- Infraestructura objetivo: Cloudflare + Hetzner + Coolify + Docker.
- Storage inicial: local con abstraccion hacia Cloudflare R2.
- Redis: preparado, usar cuando aporte valor.
- WebSockets: no V1.
- SuperAdmin separado de Tenant ERP.
- Public Website administrable por bloques desde SuperAdmin.

## Decision aprobada — simplificacion de roles y permisos

La experiencia del Tenant ERP se simplificara con este modelo:

### Roles protegidos del sistema

- Propietario.
- Administrador.

El Propietario conserva las funciones sensibles de propiedad, seguridad, facturacion y continuidad de la cuenta. El Administrador dispone de administracion operativa amplia, pero no sustituye al Propietario para acciones criticas.

### Roles personalizados

Todos los demas roles seran creados por cada empresa con:

- nombre libre;
- permisos configurables por modulo y accion;
- una pantalla inicial seleccionable o automatica;
- asignaciones de sucursal, bodega y caja;
- plantillas opcionales que solo marcan permisos recomendados.

Los nombres Cajero, Vendedor, Bodega, Supervisor, Compras y Contabilidad se consideran plantillas o ejemplos, no roles obligatorios del sistema.

### Reglas de experiencia y seguridad

- La navegacion, el dashboard y la pantalla inicial dependen de permisos efectivos, no del nombre del rol.
- Un usuario con acceso exclusivo a POS puede entrar directamente al POS.
- Un usuario con permisos de inventario y ubicaciones recibe una experiencia operativa centrada en esos modulos.
- Cuando existen varias areas disponibles, `/app` muestra un dashboard reducido segun permisos.
- Sin permisos efectivos se muestra una pantalla de acceso no configurado.
- El frontend oculta opciones no autorizadas, pero el backend sigue siendo la fuente de verdad.
- En la primera version de esta simplificacion, la interfaz asignara un rol principal por usuario. El soporte interno para multiples roles puede mantenerse para compatibilidad y evolucion futura.
- Nunca se puede dejar un tenant sin Propietario.

Documento rector: `04-Product-Specification/ROLE-PERMISSION-MODEL.md`.

## Riesgos pendientes

- Registrar marca Tarevo en INAPI.
- Activar y validar proveedor DTE.
- Activar y validar proveedor de pagos.
- Confirmar costos reales de servidor.
- Definir politica final de soporte y SLA.
- Definir migracion de usuarios que actualmente usan roles operativos predefinidos.

## Proximo trabajo

1. Traducir el modelo aprobado de roles y permisos a un plan tecnico de migracion.
2. Ejecutar QA y piloto de los flujos actuales.
3. Implementar la simplificacion de roles solo despues de aprobar migracion, compatibilidad y criterios de aceptacion.
4. Mantener Flow y DTE como fase final.

## Regla operativa

Si una decision no esta documentada y aprobada, no se implementa.
