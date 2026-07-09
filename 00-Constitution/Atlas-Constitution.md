# Atlas Constitution

Documento: ATLAS-CONSTITUTION-001  
Version: 1.0  
Estado: Draft aprobado para Sprint 0  
Fecha: 2026-07-09  
Owner: Chris  

## 1. Proposito

Este documento define los principios que guian Atlas. Toda decision de producto, arquitectura, seguridad, infraestructura, diseno y desarrollo debe respetar esta Constitucion.

Si una nueva funcionalidad contradice este documento, debe replantearse antes de entrar al backlog.

## 2. Identidad

- Nombre comercial: Atlas
- Nombre tecnico: Atlas Platform
- Producto: plataforma SaaS de gestion comercial
- Mercado inicial: Chile
- Vision futura: Latinoamerica

Atlas no se presentara principalmente como un ERP tradicional. Comercialmente sera: la plataforma para administrar un negocio.

## 3. Mision

Construir una plataforma SaaS intuitiva, segura y confiable para que las PYMEs administren ventas, inventario, caja, clientes, bodegas, catalogo, reportes y facturacion electronica desde un solo lugar.

## 4. Vision

Convertirse en una plataforma de gestion comercial lider para PYMEs en Latinoamerica, comenzando por Chile, con un nucleo independiente del pais y modulos tributarios desacoplados.

## 5. Principios inmutables

### 5.1 Atlas siempre sera SaaS

Atlas se construira como plataforma cloud. No habra instalaciones por cliente ni versiones separadas del producto.

Implicaciones:

- Un solo codigo base.
- Planes y permisos controlan funcionalidades.
- Las empresas comparten plataforma, pero no datos.

### 5.2 Atlas sera self-service

El cliente debe poder registrarse, pagar, crear su empresa, escoger subdominio, configurar su cuenta y empezar a usar Atlas sin intervencion manual del equipo.

### 5.3 El ERP es el sistema maestro

Atlas sera la fuente oficial de productos, stock, ventas, clientes y operaciones. WooCommerce, catalogo web, marketplaces o apps futuras seran canales, no sistemas maestros.

### 5.4 El nucleo sera independiente del pais

Inventario, POS, caja, clientes, bodega y reportes no deben depender del SII ni de ninguna normativa especifica. La logica tributaria vive en modulos independientes.

### 5.5 Seguridad por diseno

La seguridad no es un modulo posterior. Debe existir desde el primer commit: autenticacion segura, permisos, auditoria, cifrado, backups, rate limiting y manejo correcto de secretos.

### 5.6 Todo sera modular mediante Apps

Atlas se organizara como un ecosistema de Apps:

- Atlas Core
- Atlas POS
- Atlas Inventory
- Atlas Warehouse
- Atlas DTE
- Atlas CRM
- Atlas Reports
- Atlas Catalog

Las integraciones futuras se dejaran preparadas, pero no se desarrollaran hasta que haya demanda real.

### 5.7 Escalabilidad diferida

La arquitectura debe permitir crecer, pero no se agregaran suscripciones, servicios externos o complejidad operativa antes de necesitarlos.

### 5.8 No se hardcodean secretos

Ninguna clave, token, certificado o password puede quedar en codigo, commits, frontend o chat. Todo secreto vive en variables de entorno, GitHub Secrets, Coolify Secrets o sistemas equivalentes.

### 5.9 Todo debe poder auditarse

Toda accion critica debe registrar usuario, empresa, fecha, modulo, IP si aplica, datos anteriores y datos nuevos.

### 5.10 La experiencia del usuario manda

Una funcion complicada debe redisenarse antes de desarrollarse. Atlas debe ser rapido, claro e intuitivo.

### 5.11 El cliente es dueno de sus datos

Atlas debe permitir exportar informacion clave en formatos estandar cuando corresponda.

### 5.12 La V1 sera solida, no gigante

Atlas V1 no intentara incluir todas las ideas futuras. Solo incluira lo necesario para vender, operar y validar el producto en Chile.

## 6. Lemas internos

- Si no simplifica el negocio del cliente, no pertenece a Atlas.
- Si una funcion no ayuda a vender mas, controlar mejor o ahorrar tiempo, no entra en la V1.
- Primero arquitectura, despues programacion.

## 7. Decisiones relacionadas

Ver `08-ADL/ADL.md`.
