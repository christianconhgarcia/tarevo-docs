# User Flow Master

Version: 0.2
Estado: Aprobado

## Objetivo
Definir los recorridos principales de Tarevo desde la perspectiva del usuario y del negocio.

## Regla transversal de acceso

Tarevo no debe decidir la experiencia por el nombre del rol. Después del login:

```text
Login
  -> Obtener permisos efectivos
  -> Aplicar empresa, sucursal, bodega y caja asignadas
  -> Resolver pantalla inicial
  -> Construir menú y dashboard según permisos
```

Roles protegidos del sistema:

- Propietario.
- Administrador.

Todos los demás roles son personalizados por empresa. Sus nombres son libres y su comportamiento depende de permisos, asignaciones y pantalla inicial.

## Flow 01 — Del visitante a la primera venta

```text
Landing
  -> Planes
  -> Registro
  -> Verificar correo
  -> Crear empresa
  -> Crear sucursal
  -> Crear bodega
  -> Crear caja
  -> Crear producto
  -> Abrir caja
  -> Primera venta
```

Evento final esperado: FirstSaleCompleted.

## Flow 02 — Usuario existente entra al sistema

```text
Login
  -> Resolver tenant activo
  -> Cargar permisos efectivos
  -> Cargar asignaciones operativas
  -> Si tiene una sola area operativa: abrir esa area
  -> Si tiene varias areas: abrir dashboard personalizado
  -> Si no tiene permisos: mostrar Sin acceso asignado
```

Ejemplos:

- Solo POS: abrir POS.
- POS + caja: abrir POS y permitir operacion de caja.
- Inventario + ubicaciones: abrir Inventario.
- Picking + packing: abrir Picking y packing.
- Varias areas: abrir Dashboard personalizado.

## Flow 03 — Administrador gestiona productos

```text
Login
  -> Productos
  -> Crear o editar producto
  -> Actualizar precio / datos / foto
  -> Guardar
  -> Auditoria
```

## Flow 04 — Rol personalizado de bodega prepara picking

```text
Login
  -> Resolver permisos de warehouse
  -> Picking y packing
  -> Ver lista
  -> Confirmar ubicacion
  -> Preparar productos
  -> Marcar listo
```

El rol puede tener cualquier nombre. El acceso depende de permisos de warehouse y picking.

## Flow 05 — Rol personalizado opera caja

```text
Login
  -> Resolver permisos POS y caja
  -> Abrir POS como pantalla inicial
  -> Abrir caja si corresponde
  -> Cobrar ventas
  -> Cerrar caja
  -> Arqueo
```

El rol puede llamarse Cajero, Operador POS, Vendedor de caja u otro nombre.

## Flow 06 — Rol personalizado revisa reportes

```text
Login
  -> Resolver permiso de reportes
  -> Reportes
  -> Seleccionar reporte
  -> Filtrar fecha / sucursal / caja
  -> Exportar si tiene permiso
```

## Flow 07 — Administrador crea un rol personalizado

```text
Administracion
  -> Usuarios y roles
  -> Crear rol personalizado
  -> Elegir plantilla o comenzar vacio
  -> Asignar permisos por modulo
  -> Definir pantalla inicial: automatica o manual
  -> Guardar
  -> Asignar rol a usuario
```

Plantillas sugeridas:

- Cajero.
- Vendedor.
- Bodega.
- Supervisor.
- Compras.
- Contabilidad.

Las plantillas no son roles obligatorios: solo preseleccionan permisos editables.

## Flow 08 — SuperAdmin revisa una empresa

```text
SuperAdmin Login
  -> Dashboard
  -> Empresas
  -> Detalle empresa
  -> Plan / pagos / almacenamiento / DTE / soporte
```

## Flow 09 — Soporte resuelve ticket

```text
SuperAdmin
  -> Tickets
  -> Abrir ticket
  -> Revisar empresa
  -> Revisar logs
  -> Responder
  -> Cerrar ticket
```

## Customer Journey

### Primer dia
- Registro.
- Empresa creada.
- Primera sucursal.
- Primera caja.
- Primer producto.
- Primera venta.

### Primera semana
- Importa productos.
- Invita usuarios.
- Crea roles personalizados.
- Configura bodegas.
- Revisa primeros reportes.

### Primer mes
- Ajusta permisos y pantallas iniciales.
- Usa reportes.
- Evalua Warehouse.
- Configura dominio propio si su plan lo permite.
- Evalua DTE.

### Seis meses
- Agrega sucursales.
- Agrega cajas.
- Compra mas almacenamiento.
- Activa Apps adicionales.

## Success Path

```text
Registro
  -> Empresa creada
  -> Sucursal creada
  -> Caja creada
  -> Producto creado
  -> Primera venta
  -> 10 ventas
  -> 100 ventas
  -> Primer reporte consultado
  -> Cliente activado
```

## Uso para Customer Success

El SuperAdmin debe poder detectar:

- clientes que no terminaron onboarding;
- clientes que no hicieron primera venta;
- clientes inactivos;
- clientes cerca de limites;
- clientes con riesgo de cancelacion.
