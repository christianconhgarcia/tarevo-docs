# PRD General Chile - Tarevo

Documento: PRD-CHILE-001  
Version: 1.0  
Estado: Draft aprobado para Sprint 0  
Fecha: 2026-07-09  
Owner: Chris

## 1. Objetivo

Definir el alcance funcional inicial de Tarevo para operar en Chile como plataforma SaaS de gestion comercial para PYMEs.

Este PRD no describe codigo. Describe el producto que Codex debera implementar por etapas respetando Constitucion, arquitectura, seguridad y decisiones aprobadas.

## 2. Hipotesis principal

Las PYMEs chilenas necesitan una plataforma simple para vender, controlar inventario, ordenar bodega, registrar pagos y emitir documentos tributarios sin depender de multiples sistemas separados.

Tarevo debe empezar por resolver bien la operacion diaria antes de agregar integraciones avanzadas.

## 3. Usuario objetivo

### 3.1 Cliente comprador

Dueno, administrador o encargado de una PYME que necesita controlar ventas, stock, caja y documentacion tributaria.

### 3.2 Usuarios operativos

- Vendedor.
- Cajero.
- Bodeguero.
- Administrador de tienda.
- Supervisor.
- Contador externo o usuario de consulta.

### 3.3 Usuario plataforma

Equipo interno de Tarevo con rol SuperAdmin para administrar empresas, planes, suspensiones, limites, errores y configuraciones globales.

## 4. Alcance geografico V1

Chile.

Implicaciones:

- Moneda principal: CLP.
- Impuestos y DTE preparados para Chile.
- RUT empresa y RUT receptor.
- Boleta, factura, nota de credito y nota de debito como documentos objetivo.
- Adaptador inicial hacia proveedor DTE externo, no motor tributario propio contra SII.

## 5. Principios de producto

- El POS debe ser rapido y usable en tienda real.
- El inventario debe ser confiable, auditable y trazable.
- El ticket interno no es lo mismo que el documento tributario.
- La caja debe poder cobrar tickets generados por diferentes vendedores o estaciones.
- Los permisos deben impedir errores operativos y abuso.
- La plataforma debe poder suspender una empresa sin borrar sus datos.
- Todo cambio critico debe ser auditable.

## 6. Flujo principal de cliente

1. Cliente entra a landing.
2. Escoge plan.
3. Crea cuenta.
4. Registra datos de empresa.
5. Escoge subdominio.
6. Activa prueba o paga plan.
7. Configura sucursal, bodega, caja y usuarios.
8. Carga productos.
9. Empieza a vender.
10. Revisa reportes y stock.

## 7. Flujo POS V1

1. Vendedor inicia sesion.
2. Abre pantalla POS.
3. Busca producto por nombre, SKU o codigo de barras.
4. Agrega productos al ticket.
5. Ajusta cantidad si tiene permiso.
6. Deja ticket pendiente o envia a caja.
7. Cajero cobra con uno o varios medios de pago.
8. Ticket pasa a pagado.
9. Sistema permite emitir boleta o factura segun corresponda.
10. Se registra movimiento de stock y auditoria.

## 8. Flujo inventario V1

1. Admin crea producto.
2. Admin o bodeguero registra recepcion o compra.
3. Stock aumenta en bodega/sucursal correspondiente.
4. Ventas descuentan stock.
5. Ajustes requieren motivo.
6. Kardex registra entrada, salida, ajuste, traspaso o anulacion.

## 9. Flujo bodega V1

1. Empresa crea una o mas bodegas.
2. Define ubicaciones internas.
3. Asocia stock a bodega y ubicacion.
4. Genera traspasos entre bodegas/sucursales.
5. El stock en traspaso no debe contarse como disponible para venta.
6. Al recibir traspaso, stock queda disponible en destino.

## 10. Flujo DTE Chile V1

1. Ticket queda pagado.
2. Usuario decide emitir boleta o factura.
3. Para factura, receptor debe tener datos tributarios minimos.
4. Tarevo genera solicitud al proveedor DTE externo.
5. Se guarda estado del documento.
6. Si falla, se registra error y se permite reintentar segun reglas.

## 11. Planes iniciales sugeridos

### Starter

- 1 empresa.
- 1 sucursal.
- Usuarios limitados.
- POS basico.
- Inventario basico.
- Reportes basicos.

### Pro

- Mas usuarios.
- Mas bodegas.
- Caja central.
- Reportes ampliados.
- DTE segun limite.

### Business

- Multiples sucursales.
- Warehouse completo.
- Mas almacenamiento.
- Soporte prioritario.
- Configuraciones avanzadas.

## 12. Fuera de alcance V1

- Integracion directa con Mercado Libre.
- Integracion directa con WooCommerce.
- Integracion directa con Shopify.
- WhatsApp automatizado.
- App movil nativa.
- IA operativa.
- BI avanzado.
- Motor DTE propio directo contra SII.
- Integracion con terminales de pago fisicos.

## 13. Riesgos

- Querer construir demasiados modulos antes de validar clientes reales.
- Subestimar DTE y normativa chilena.
- Mezclar ticket, pago y documento tributario.
- No separar tenant/empresa desde el inicio.
- No definir permisos antes de construir pantallas.
- Depender de servicios pagos antes de vender.

## 14. Criterio de exito V1

Tarevo V1 sera exitosa si permite que una PYME chilena pueda:

- Crear su empresa.
- Configurar usuarios.
- Cargar productos.
- Vender en POS.
- Registrar pagos.
- Controlar stock.
- Revisar reportes basicos.
- Emitir DTE mediante proveedor externo.
- Operar sin intervencion manual del equipo Tarevo.
