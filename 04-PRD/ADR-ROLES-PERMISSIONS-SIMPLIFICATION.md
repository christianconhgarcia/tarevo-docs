# ADR — Simplificación de roles, permisos y experiencia inicial

Estado: Aprobado para implementación futura
Fecha: 2026-07-16

## Contexto

Tarevo dispone de permisos granulares y puede asociar usuarios con roles, sucursales, bodegas y cajas. La experiencia actual presenta demasiados roles predefinidos, lo que dificulta la configuración y obliga a las empresas a adaptarse a nombres que no siempre representan su operación.

La decisión es simplificar la interfaz sin debilitar la seguridad ni convertir el nombre del rol en una regla de negocio.

## Decisión

Tarevo mantendrá únicamente dos roles protegidos del sistema:

1. **Propietario**
   - Máxima autoridad dentro del tenant.
   - Administra propiedad, facturación sensible, seguridad y continuidad administrativa.
   - No puede eliminarse el último propietario activo.

2. **Administrador**
   - Acceso operativo y administrativo amplio.
   - Puede gestionar configuración, usuarios y operación según los permisos definidos para esta función.
   - No reemplaza al propietario para acciones exclusivas de propiedad o facturación sensible.

Todos los demás roles serán personalizados por cada empresa.

## Roles personalizados

Cada tenant podrá crear roles con:

- nombre libre;
- descripción opcional;
- permisos agrupados por módulo;
- pantalla inicial;
- asignaciones de sucursal, bodega y caja por usuario;
- estado activo o inactivo.

Ejemplos de nombres posibles, sin carácter obligatorio:

- Cajero;
- Operador POS;
- Encargado de tienda;
- Bodega;
- Preparación de pedidos;
- Compras;
- Contabilidad.

El nombre del rol nunca determinará el acceso. La autorización dependerá exclusivamente de los permisos efectivos y del contexto operativo asignado.

## Plantillas de inicio

Al crear un rol personalizado, la interfaz podrá ofrecer plantillas opcionales:

- Vacío;
- Cajero;
- Vendedor;
- Bodega;
- Supervisor;
- Compras;
- Contabilidad.

Las plantillas solo preseleccionan permisos. El usuario administrador puede cambiar el nombre y modificar cualquier permiso permitido.

## Pantalla inicial

Cada rol personalizado tendrá una preferencia de pantalla inicial:

- Automática;
- Dashboard;
- Punto de venta;
- Productos;
- Inventario;
- Ubicaciones;
- Picking y packing;
- Compras;
- Ventas;
- Reportes;
- Administración.

### Resolución automática

Cuando la pantalla inicial sea Automática, Tarevo resolverá el destino según los permisos efectivos:

- solo POS o POS + caja: abrir POS;
- inventario y ubicaciones: abrir Inventario;
- picking y packing: abrir Picking y packing;
- compras y recepciones: abrir Compras;
- reportes: abrir Reportes;
- varias áreas funcionales: abrir Dashboard adaptado;
- ningún permiso operativo: mostrar Sin acceso asignado.

La pantalla inicial elegida no concede permisos. Si el usuario no tiene acceso a esa ruta, Tarevo debe usar la primera ruta válida según sus permisos.

## Dashboard adaptado

La ruta `/app` será única, pero su contenido cambiará según los permisos efectivos.

Ejemplos:

- usuario POS/caja: apertura de caja, sesión activa, ventas del turno y acceso directo al POS;
- usuario de inventario: bajo stock, transferencias, conteos y ubicaciones;
- usuario de picking: pendientes, asignados, en preparación y listos;
- administrador: KPIs generales, alertas, ventas, inventario y accesos administrativos.

No se crearán dashboards separados por nombre de rol.

## Navegación

El menú se construirá únicamente con permisos efectivos:

- sin permiso de lectura: el módulo no aparece;
- con lectura: aparece en modo consulta;
- crear, editar, eliminar, aprobar o exportar se controlan con permisos independientes cuando corresponda.

Ocultar una opción no reemplaza la autorización. El backend seguirá siendo la fuente de verdad y deberá rechazar rutas y acciones no autorizadas.

## Permisos agrupados

La interfaz no mostrará una lista técnica plana. Los permisos se organizarán por módulos:

- Punto de venta;
- Caja;
- Productos;
- Inventario;
- Warehouse y ubicaciones;
- Compras;
- Ventas y devoluciones;
- Clientes;
- Reportes;
- Empresa y configuración;
- Usuarios y roles;
- Facturación y plan;
- Integraciones.

Dentro de cada módulo se distinguirán acciones como ver, crear, editar, eliminar, aprobar, exportar o administrar.

## Regla de asignación de roles

En la experiencia inicial, cada usuario tendrá un rol principal visible.

La arquitectura podrá conservar soporte interno para varios roles, pero la interfaz estándar no promoverá combinaciones múltiples. Cuando una persona necesite permisos de varias áreas, se recomienda crear un rol personalizado que represente su responsabilidad real.

## Migración conceptual

Los roles operativos predefinidos actuales no se usarán como reglas permanentes. Durante la implementación deberán convertirse en roles personalizados equivalentes o en plantillas de creación.

La migración debe preservar:

- permisos efectivos;
- usuarios asociados;
- asignaciones de sucursal;
- asignaciones de bodega;
- asignaciones de caja;
- protección del propietario;
- historial de auditoría.

## Criterios de aceptación futuros

- Solo Propietario y Administrador se presentan como roles protegidos del sistema.
- El tenant puede crear, editar, duplicar, desactivar y eliminar roles personalizados no asignados.
- El nombre del rol no se usa para autorizar ni redirigir.
- El menú, dashboard y destino inicial dependen de permisos efectivos.
- Las rutas profundas siguen protegidas por backend.
- El último propietario no puede eliminarse ni perder su rol.
- Un rol con acceso exclusivo a POS abre directamente el POS al iniciar sesión.
- Un rol con varias áreas abre un dashboard adaptado.
- Un usuario sin permisos recibe una pantalla clara de acceso pendiente.

## Fuera de alcance de esta decisión

Este documento no implementa cambios de código. La ejecución se realizará después de completar el diseño de permisos por módulo, migración, pruebas y aprobación explícita.
