# User Flow Master

Version: 0.1
Estado: Aprobado

## Objetivo
Definir los recorridos principales de Tarevo desde la perspectiva del usuario y del negocio.

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

## Flow 02 — Cliente existente hace una venta

```text
Login
  -> Dashboard
  -> Abrir caja si esta cerrada
  -> POS
  -> Agregar producto
  -> Cobrar
  -> Generar ticket/venta
  -> Cerrar flujo
```

## Flow 03 — Administrador gestiona productos

```text
Login
  -> Productos
  -> Crear o editar producto
  -> Actualizar precio / datos / foto
  -> Guardar
  -> Auditoria
```

## Flow 04 — Bodeguero prepara picking

```text
Login
  -> Warehouse
  -> Picking
  -> Ver lista
  -> Confirmar ubicacion
  -> Preparar productos
  -> Marcar listo
```

## Flow 05 — Cajero opera caja

```text
Login
  -> Caja
  -> Abrir caja
  -> POS
  -> Cobrar ventas
  -> Cerrar caja
  -> Arqueo
```

## Flow 06 — Supervisor revisa reportes

```text
Login
  -> Reportes
  -> Seleccionar reporte
  -> Filtrar fecha / sucursal / caja
  -> Exportar si tiene permiso
```

## Flow 07 — SuperAdmin revisa una empresa

```text
SuperAdmin Login
  -> Dashboard
  -> Empresas
  -> Detalle empresa
  -> Plan / pagos / almacenamiento / DTE / soporte
```

## Flow 08 — Soporte resuelve ticket

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
- Configura bodegas.
- Revisa primeros reportes.

### Primer mes
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
