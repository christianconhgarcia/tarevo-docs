# Navigation Master

Version: 0.1
Estado: Aprobado

## Objetivo
Definir la navegacion principal de Tarevo antes de disenar pantallas individuales.

## Mundos de Tarevo

Tarevo se divide en tres mundos:

1. Public Website
2. Tenant ERP
3. SuperAdmin Console

Ninguna funcionalidad debe mezclarse entre mundos sin una justificacion explicita.

## Public Website

Navegacion publica:

- Inicio
- Caracteristicas
- Apps
- Planes
- Comparativa
- FAQ
- Contacto
- Login
- Registro

Flujo principal:

```text
Landing
  -> Planes
  -> Registro
  -> Verificar correo
  -> Crear empresa
  -> Onboarding
  -> Primera venta
```

## Tenant ERP

Navegacion principal:

- Dashboard
- Ventas
  - POS
  - Tickets
  - Pagos
  - Devoluciones
- Productos
  - Listado
  - Crear producto
  - Categorias
  - Marcas
  - Variantes
  - Importar
  - Exportar
- Inventario
  - Stock
  - Kardex
  - Ajustes
  - Conteos
  - Alertas
- Warehouse
  - Bodegas
  - Ubicaciones
  - Transferencias
  - Picking
  - Packing
  - Recepcion
  - Lotes
- Compras
  - Ordenes
  - Recepcion
  - Proveedores
- Clientes
- Reportes
- Configuracion
  - Empresa
  - Sucursales
  - Bodegas
  - Cajas
  - Usuarios
  - Roles
  - Permisos
  - DTE
  - Integraciones

### Fase 1 - Navegacion unificada implementada

La Fase 1 reorganiza los modulos existentes en una barra lateral persistente bajo `/app/*` sin cambiar reglas de negocio ni contratos de API.

Mapa implementado:

- Inicio: Dashboard.
- Ventas y caja: Punto de venta, Cajas y sesiones, Historial de ventas, Historial de devoluciones, DTE Chile, Clientes.
- Catalogo: Productos, Catalogo web e integraciones.
- Inventario y logistica: Existencias y bodegas, Inventario avanzado, Picking y packing.
- Compras: Ordenes y proveedores.
- Reportes y control: Control y reportes, Diagnostico operativo.
- Administracion: Administracion, Plan y facturacion.

Detalle tecnico y criterios: `05-Development/PHASE-1-UNIFIED-NAVIGATION.md`.

### Fase 2 - Agrupacion funcional implementada

La Fase 2 mantiene la navegacion unificada de Fase 1 y reordena las rutas visibles por funcion real del negocio, sin nuevos endpoints ni cambios de reglas.

Mapa implementado:

- Inicio: Dashboard.
- Ventas y caja: Punto de venta, Cajas y sesiones, Historial de ventas, Devoluciones, DTE Chile, Clientes.
- Catalogo: Productos, Categorias, Marcas, Variantes, Precios y margenes, Importar, Catalogo web e integraciones.
- Inventario y logistica: Existencias, Kardex y trazabilidad, Ubicaciones, Transferencias, Conteos, Picking y packing.
- Compras: Ordenes y proveedores.
- Reportes: Reportes, Preparacion de la empresa.
- Administracion: Empresa y usuarios, Plan, facturacion y soporte.

Redirects legacy obligatorios:

- `/app/commerce` -> `/app/catalog/integrations`
- `/app/refunds` -> `/app/sales/refunds`
- `/app/inventory-control` -> `/app/inventory/kardex`
- `/app/management` -> `/app/reports`
- `/app/operations` -> `/app/reports/operations`
- `/app/billing` -> `/app/admin/billing`

Detalle tecnico y criterios: `05-Development/PHASE-2-FUNCTIONAL-GROUPING.md`.

## SuperAdmin Console

Navegacion principal:

- Dashboard
- Empresas
- Planes
- Billing
- Customer Success
- Tickets de soporte
- Landing CMS
- Infraestructura
- Integraciones
- Feature Flags
- Analytics
- Configuracion Global

## Regla para Codex

Toda pantalla nueva debe declarar su mundo, modulo, ruta y permisos antes de implementarse.
