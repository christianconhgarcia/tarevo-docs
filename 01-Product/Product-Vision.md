# Product Vision - Tarevo

Documento: PRD-001  
Version: 1.1  
Estado: Draft aprobado para Sprint 0  
Fecha: 2026-07-09

## 1. Que es Tarevo

Tarevo es una plataforma SaaS para administrar negocios. Combina POS, inventario, bodega, caja, clientes, proveedores, reportes, suscripciones, catalogo web y facturacion electronica para PYMEs.

Tarevo nace enfocado en Chile, pero su nucleo no sera chileno. El nucleo sera internacional y el modulo tributario inicial sera Chile/SII.

## 2. Que NO es Tarevo

Tarevo no es:

- Solo un sistema de facturacion.
- Solo un POS.
- Un software contable completo.
- Un sistema instalado por cliente.
- Una coleccion de modulos desconectados.
- Una app improvisada para hosting compartido.
- Una version demo sin seguridad real.

## 3. Problema que resuelve

Muchas PYMEs trabajan con Excel, POS antiguos, sistemas separados, inventarios duplicados y poca trazabilidad. Tarevo unifica la operacion diaria en una plataforma moderna, segura y preparada para crecer.

El problema central no es solo vender. El problema es controlar el negocio completo: quien vendio, cuanto se cobro, que medio de pago se uso, que stock quedo, donde esta el producto, que documento tributario corresponde emitir y que usuario hizo cada accion.

## 4. Mercado inicial

Chile.

Segmentos iniciales:

- Tiendas de hogar.
- Ferreterias.
- Minimarkets.
- Librerias y papelerias.
- Bazares.
- Tiendas de mascotas.
- Tiendas de ropa.
- Importadoras.
- Distribuidoras.
- Empresas con sucursales y bodegas.

## 5. Propuesta de valor

Tarevo permite que una empresa administre su negocio desde una sola plataforma:

- Vender en POS.
- Gestionar tickets, pagos y caja.
- Controlar inventario.
- Gestionar bodegas, ubicaciones y traspasos.
- Emitir boletas, facturas y notas cuando corresponda.
- Ver reportes.
- Administrar clientes y proveedores.
- Activar Apps segun el plan.
- Operar con subdominio propio dentro de Tarevo.

## 6. V1 aprobada

La V1 incluye:

### Tarevo Core

- Multiempresa.
- Multiusuario.
- Roles y permisos.
- Subdominios automaticos.
- Portal del cliente.
- Panel SuperAdmin.
- Suscripciones y planes.
- Seguridad y auditoria.

### Tarevo POS

- Ventas.
- Tickets internos.
- Tickets pendientes.
- Tickets anulados.
- Tickets expirados.
- Caja central.
- Estaciones de venta configurables.
- Pago mixto.
- Medios de pago.
- Reporte de pagos.

### Tarevo Inventory

- Productos.
- Categorias.
- Stock.
- Compras.
- Kardex.
- Costos.
- Ajustes.

### Tarevo Warehouse

- Multiples bodegas por empresa.
- Ubicaciones.
- Traspasos.
- Stock en transito.
- Picking basico.
- Recepcion.

### Tarevo DTE Chile

- Boletas.
- Facturas.
- Notas de credito.
- Notas de debito.
- Certificados.
- CAF.
- Adaptador inicial a proveedor DTE externo.

### Reportes

- Ventas.
- Caja.
- Tickets.
- Pagos.
- Inventario.
- Bodega.
- DTE.
- Clientes.

## 7. Fuera de alcance de V1

No entra en V1:

- App movil.
- IA.
- Marketplace publico.
- Shopify.
- Mercado Libre.
- WhatsApp.
- Integracion directa con terminales POS fisicos.
- RFID.
- Business Intelligence avanzado.
- Motor DTE propio directo al SII.

Estas ideas quedan documentadas para roadmap futuro.

## 8. Modelo operativo ideal

Tarevo debe ser self-service:

1. Cliente ve publicidad.
2. Entra a la landing.
3. Escoge plan.
4. Crea cuenta.
5. Escoge subdominio.
6. Paga.
7. Tarevo crea la empresa.
8. Tarevo activa Apps, limites y permisos.
9. Cliente inicia onboarding.
10. Cliente empieza a vender.

## 9. Diferenciadores clave

- Separacion entre ticket, pago y DTE.
- Estaciones de venta configurables.
- Caja central.
- Ciclo de vida completo del ticket.
- Tarevo Warehouse como App premium.
- Almacenamiento por plan.
- Subdominios automaticos.
- SuperAdmin robusto.
- Arquitectura preparada para crecer sin pagar servicios innecesarios al inicio.

## 10. Metricas de exito

- Tiempo para crear cuenta.
- Tiempo para crear empresa.
- Tiempo hasta la primera venta.
- Tickets procesados por dia.
- DTE emitidos por mes.
- Retencion mensual.
- MRR.
- Incidentes de seguridad.
- Tiempo promedio de respuesta del POS.
- Uso de almacenamiento por empresa.
