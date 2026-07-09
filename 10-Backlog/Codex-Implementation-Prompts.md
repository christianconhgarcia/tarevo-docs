# Codex Implementation Prompts - Tarevo

Documento: CODEX-001  
Version: 1.0  
Estado: Draft operativo  
Fecha: 2026-07-09

## 1. Regla general

Codex no debe recibir instrucciones amplias como "crea Tarevo".

Cada tarea debe indicar:

- Documentos que debe leer.
- Modulo exacto.
- Alcance permitido.
- Restricciones.
- Criterios de aceptacion.
- Archivos que debe modificar.
- Archivos que no debe tocar si aplica.

## 2. Prompt base obligatorio

```text
Antes de escribir codigo, lee estos documentos del repositorio tarevo-docs:

- 00-Constitution/Tarevo-Constitution.md
- 01-Product/Product-Vision.md
- 01-Product/Module-Scope-V1.md
- 02-Business/PRD-General-Chile.md
- 03-Architecture/Architecture-Principles.md
- 04-Infrastructure/INF-001-Produccion.md
- 05-Database/Conceptual-Data-Model.md
- 06-Security/SEC-001-Security-Architecture.md
- 08-ADL/ADL.md

No implementes nada fuera de esos documentos.
No hardcodees secretos.
No hagas una version demo.
No mezcles datos entre empresas.
No agregues servicios pagos sin decision documentada.
Si necesitas tomar una decision tecnica nueva, proponla primero como entrada ADL.
```

## 3. Prompt 001 - Bootstrap del proyecto

```text
Crea el bootstrap inicial de Tarevo Platform.

Objetivo:
Preparar la base tecnica del producto sin implementar modulos de negocio todavia.

Debe incluir:
- Estructura de proyecto clara.
- Configuracion de entorno.
- Variables de entorno de ejemplo sin secretos reales.
- Linter/formato si corresponde.
- Docker o preparacion Docker si aplica al stack aprobado.
- README tecnico inicial.

No debe incluir:
- POS.
- Inventario.
- DTE.
- Billing real.
- Datos mock como si fueran produccion.

Criterio de aceptacion:
El proyecto debe poder instalarse, ejecutarse localmente y dejar claro donde se agregaran Core, POS, Inventory, Warehouse y DTE.
```

## 4. Prompt 002 - Autenticacion segura

```text
Implementa solamente autenticacion segura para Tarevo.

Lee primero:
- Tarevo Constitution
- SEC-001 Security Architecture
- Conceptual Data Model
- Module Scope V1

Debe incluir:
- Registro de usuario owner inicial.
- Login.
- Logout.
- Hash seguro de password.
- Sesiones o tokens seguros segun arquitectura aprobada.
- Rate limiting.
- Recuperacion de contrasena preparada para correo transaccional.
- Auditoria de login exitoso y fallido.

No debe incluir:
- POS.
- Inventario.
- DTE.
- Pagos.
- Integraciones externas reales si no estan configuradas.

Criterio de aceptacion:
Un usuario puede registrarse, iniciar sesion y cerrar sesion sin exponer secretos ni permitir fuerza bruta basica.
```

## 5. Prompt 003 - Multiempresa y roles

```text
Implementa el nucleo multiempresa y roles/permisos.

Debe incluir:
- Company.
- CompanyUser.
- Role.
- Permission.
- RolePermission.
- Middleware o guard para aislar datos por empresa.
- Permisos iniciales para Owner, Admin, Vendedor, Cajero, Bodeguero y Supervisor.

Regla critica:
Ninguna consulta operativa puede devolver datos de otra empresa.

Criterio de aceptacion:
Dos empresas distintas pueden existir en la misma plataforma sin ver datos entre ellas.
```

## 6. Prompt 004 - Productos e inventario base

```text
Implementa solamente productos, categorias y stock base.

Debe incluir:
- CRUD de productos.
- Categorias.
- SKU/codigo de barras.
- Precio y costo.
- Imagen preparada para storage externo.
- StockBalance.
- StockMovement.
- Ajuste manual con motivo.

No debe incluir:
- POS completo.
- DTE.
- Marketplace.

Criterio de aceptacion:
Un admin puede crear productos y ajustar stock dejando kardex auditable.
```

## 7. Prompt 005 - POS y tickets internos

```text
Implementa POS y tickets internos sin DTE real.

Debe incluir:
- Pantalla POS.
- Busqueda de productos.
- Crear ticket.
- Agregar/quitar items segun permisos.
- Ticket pendiente.
- Ticket pagado.
- Ticket anulado con motivo.
- Descuento de stock al confirmar venta pagada segun regla aprobada.

Regla critica:
Ticket no es boleta ni factura.

Criterio de aceptacion:
Una venta puede registrarse como ticket pagado y descontar stock con auditoria.
```

## 8. Prompt 006 - Caja y pagos mixtos

```text
Implementa caja central y pagos mixtos.

Debe incluir:
- Medios de pago configurables.
- Multiples pagos por ticket.
- Validacion de total pagado.
- Reporte de pagos por fecha, usuario y metodo.
- Caja puede cobrar ticket creado por otro vendedor.

No debe incluir:
- Integracion con Transbank u otro terminal fisico.

Criterio de aceptacion:
Un ticket puede pagarse con dos o mas medios y quedar cuadrado contra el total.
```

## 9. Prompt 007 - Warehouse basico

```text
Implementa Warehouse basico.

Debe incluir:
- Bodegas.
- Ubicaciones.
- Stock por bodega.
- Traspasos.
- Stock en transito.
- Recepcion de traspaso.
- Picking basico.

Criterio de aceptacion:
Un producto puede moverse de una bodega a otra sin duplicar stock disponible.
```

## 10. Prompt 008 - DTE Chile via proveedor externo

```text
Implementa la capa inicial DTE Chile como adaptador a proveedor externo.

Debe incluir:
- TaxProfile.
- TaxDocument.
- Boleta.
- Factura.
- Nota de credito.
- Nota de debito.
- Estados de emision.
- Manejo de errores y reintentos.

No debe incluir:
- Motor DTE propio directo al SII.
- Certificacion tributaria propia.

Criterio de aceptacion:
Desde un ticket pagado se puede crear una solicitud de DTE y guardar su estado, sin acoplar el POS al proveedor especifico.
```

## 11. Prompt 009 - SuperAdmin

```text
Implementa panel SuperAdmin inicial.

Debe incluir:
- Listado de empresas.
- Ver estado de empresa.
- Cambiar plan.
- Suspender/reactivar empresa.
- Ver consumo basico.
- Ver errores criticos.
- Auditoria de acciones SuperAdmin.

Regla critica:
SuperAdmin no debe editar ventas, pagos, stock o DTE sin una accion auditada y justificada.
```

## 12. Prompt 010 - Reportes V1

```text
Implementa reportes V1.

Debe incluir:
- Ventas por rango de fecha.
- Pagos por metodo.
- Tickets anulados.
- Stock bajo.
- Movimientos de inventario.
- DTE emitidos/fallidos.

No debe incluir:
- BI avanzado.
- Graficos complejos innecesarios.

Criterio de aceptacion:
Admin puede entender ventas, caja e inventario sin exportar a Excel.
```
