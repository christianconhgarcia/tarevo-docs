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
