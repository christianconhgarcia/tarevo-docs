# Tarevo POS - Arquitectura de impresion

Documento: ARCH-POS-PRINT-001  
Version: 1.0  
Estado: Aprobado como arquitectura actual y hoja de ruta  
Ultima actualizacion: 2026-08-26

## 1. Objetivo

Definir la arquitectura oficial de impresion de Tarevo POS para Windows, macOS y Android, incluyendo conexion local con impresoras, seguridad, configuracion por computador, instaladores, renderizado de tickets y comportamiento ante fallos.

Este documento es la fuente de verdad funcional para nuevas implementaciones de impresion. No se debe crear una segunda arquitectura de impresion paralela sin actualizar esta decision.

## 2. Principio general

Tarevo POS es una aplicacion web. El navegador no debe depender de `window.print()` ni del dialogo de impresion del sistema para los flujos operativos del POS.

La arquitectura separa tres responsabilidades:

1. Tarevo genera el contenido y decide que imprimir.
2. Una capa local del dispositivo conecta el POS con el hardware.
3. La impresora ejecuta el trabajo.

La capa local varia segun plataforma:

```text
Tarevo POS
   |
   +-- Windows  -> Tarevo Print Connector / QZ Tray -> impresora
   |
   +-- macOS    -> Tarevo Print Connector / QZ Tray -> impresora
   |
   +-- Android  -> Tarevo POS App + bridge nativo   -> SDK/servicio de impresora
```

Windows y macOS comparten la misma integracion QZ. Android no usa QZ Tray.

## 3. Estado actual validado

### 3.1 Windows

La impresion silenciosa fue validada en produccion el 2026-08-26.

Prueba validada:

```text
Chrome / Tarevo POS
      -> QZ Tray 2.2.6
      -> firma backend SHA512
      -> certificado Tarevo confiado localmente
      -> impresora Windows
```

Se comprobo que una impresion puede salir sin:

- dialogo del navegador;
- `window.print()`;
- ventana `Allow` de QZ en cada trabajo.

La prueba inicial se realizo con una HP Smart Tank 710-720. El objetivo final incluye impresoras termicas de 58 mm y 80 mm, impresoras de etiquetas y A4.

### 3.2 Configuracion POS implementada

El POS tiene una opcion `Configuracion` debajo de `Caja` y una seccion `Impresion`.

Actualmente permite:

- ver estado de QZ;
- ver version de QZ;
- conectar/actualizar;
- listar impresoras instaladas;
- seleccionar impresora de tickets;
- seleccionar impresora de etiquetas;
- seleccionar impresora A4;
- seleccionar papel 58 mm u 80 mm;
- activar impresion automatica al finalizar una venta;
- guardar la preferencia futura de apertura de cajon;
- imprimir una prueba real mediante QZ.

Las preferencias se guardan por navegador/computador y tenant en `localStorage`:

```text
tarevo_pos_printing_preferences:<tenant>
```

La seleccion de impresora nunca debe tratarse como configuracion global de la empresa, porque cada computador puede tener hardware diferente.

### 3.3 Autoimpresion despues de venta

La impresion del ticket se ejecuta solo despues de que la API confirma que la venta fue completada.

Regla obligatoria:

```text
venta confirmada
   -> estado de venta exitoso
   -> intento best-effort de impresion
```

Un fallo de QZ, de la impresora o de la conexion local NO puede revertir una venta ni marcar una venta confirmada como fallida.

El usuario puede recibir un aviso de que la impresion fallo, pero la venta permanece registrada correctamente.

## 4. Arquitectura QZ para Windows y macOS

### 4.1 Flujo

```text
Tarevo POS
   |
   | solicitud de impresion
   v
QZ Tray local
   |
   | trabajo firmado
   v
Windows/macOS printing stack
   |
   v
Impresora
```

QZ Tray es el puente local entre el navegador y las impresoras instaladas en el sistema operativo.

### 4.2 Firma y confianza

Tarevo usa una arquitectura de confianza propia para impresion silenciosa.

El frontend nunca contiene la clave privada.

Flujo de seguridad:

```text
POS pide certificado publico
   -> GET /api/v1/printing/qz/certificate

QZ necesita firma de una solicitud
   -> POS envia payload al backend
   -> POST /api/v1/printing/qz/sign
   -> backend firma con SHA512
   -> POS devuelve firma a QZ
```

La clave privada se mantiene exclusivamente en backend mediante la variable de entorno:

```text
QZ_PRIVATE_KEY_B64
```

Nunca debe:

- enviarse al frontend;
- registrarse en logs;
- almacenarse en GitHub;
- incluirse en instaladores;
- enviarse a clientes.

El certificado publico de Tarevo se utiliza para establecer confianza local en QZ.

### 4.3 Particularidad actual de Coolify

En produccion se observo que Coolify materializo el valor de `QZ_PRIVATE_KEY_B64` con exactamente un `=` adicional al comienzo dentro del contenedor.

Ejemplo observado:

```text
=LS0tLS1...
```

El backend normaliza exclusivamente ese caso conocido y despues exige:

- base64 valido;
- PEM valido;
- clave privada cargable por OpenSSL;
- clave privada RSA.

No se debe ampliar esta normalizacion de forma permisiva ni aceptar material criptografico corrupto.

## 5. Tarevo Print Connector - Windows

### 5.1 Objetivo

Tarevo debe ofrecer un instalador autoservicio para preparar un computador Windows sin intervencion del soporte tecnico.

Nombre de producto visible:

```text
Tarevo Print Connector
```

QZ Tray es una dependencia tecnica interna. El cliente normal no necesita conocer detalles como WebSocket, SHA512 o certificados.

### 5.2 Instalador previsto

Archivo objetivo:

```text
TarevoPrintConnector.exe
```

El instalador debe poder:

1. instalar QZ Tray;
2. instalar/copiar el certificado publico `override.crt` de Tarevo;
3. configurar QZ para iniciar con Windows;
4. abrir QZ al finalizar;
5. verificar que la instalacion quedo disponible;
6. opcionalmente crear acceso directo o entrada de soporte;
7. dejar preparado un mecanismo futuro de actualizacion.

La clave privada de Tarevo nunca se incluye en el instalador.

### 5.3 Descarga autoservicio desde POS

`Configuracion > Impresion` debe incluir un bloque visible de Tarevo Print Connector.

Estado esperado cuando no esta disponible:

```text
Tarevo Print Connector
Estado: No instalado / No detectado
[ Descargar para Windows ]
```

Estado esperado cuando esta funcionando:

```text
Tarevo Print Connector
Estado: Conectado
Version: x.y.z
[ Buscar actualizacion ]
```

La URL del frontend debe ser estable y no depender del nombre de archivo de una version concreta. Objetivo conceptual:

```text
https://gettarevo.com/downloads/print-connector
```

La URL podra redirigir a la version vigente.

## 6. Tarevo Print Connector - macOS

### 6.1 Arquitectura

macOS usara la misma arquitectura QZ que Windows:

```text
Tarevo POS
   -> QZ Tray para macOS
   -> sistema de impresion macOS
   -> impresora
```

No se debe crear un segundo protocolo de impresion solo para macOS mientras QZ cubra correctamente el caso.

### 6.2 Instalador previsto

Archivo objetivo:

```text
TarevoPrintConnector.pkg
```

Debe instalar/configurar:

- QZ Tray para macOS;
- certificado publico de confianza Tarevo;
- inicio automatico cuando corresponda;
- arranque inicial y verificacion.

El frontend debe detectar el sistema operativo y ofrecer la descarga apropiada:

```text
Windows -> .exe
macOS   -> .pkg
```

### 6.3 Firma/notarizacion

Para pruebas internas puede existir un instalador no firmado, con las advertencias normales del sistema operativo.

Para distribucion profesional en macOS se debe evaluar Apple Developer ID, firma y notarizacion para evitar una experiencia de instalacion deficiente.

## 7. Android y POS todo-en-uno

### 7.1 Por que Android es diferente

No se debe intentar reutilizar QZ Tray en Android.

Muchos terminales POS Android con impresora termica integrada no exponen esa impresora al panel estandar de impresion de Android. Por eso una web abierta directamente en Chrome puede no detectar una impresora que si funciona desde una aplicacion nativa del fabricante.

La solucion oficial propuesta es una app Android de Tarevo.

### 7.2 Arquitectura Android

```text
Tarevo POS App (Android)
      |
      +-- WebView -> https://pos.gettarevo.com
      |
      +-- bridge nativo seguro
              |
              +-- SDK/servicio del fabricante
              +-- ESC/POS cuando aplique
              +-- impresora termica integrada
```

El POS web sigue siendo la fuente unica de la experiencia de venta.

La app Android agrega acceso al hardware.

### 7.3 Actualizaciones

Una actualizacion normal del POS web NO requiere nueva APK.

Ejemplos de cambios que se actualizan por deploy web:

- interfaz;
- productos;
- checkout;
- descuentos;
- logica de ventas;
- textos;
- configuracion;
- reportes.

Una nueva APK solo es necesaria cuando cambia la capa nativa, por ejemplo:

- nuevo SDK de impresora;
- soporte para otra marca/modelo;
- nuevo bridge web-nativo;
- lector de codigo de barras nativo;
- NFC;
- camara/escaneo;
- correccion de bug nativo.

### 7.4 Adaptadores de impresora Android

La arquitectura debe permitir adaptadores por fabricante sin contaminar el flujo de venta.

Ejemplo conceptual:

```text
AndroidPrintingAdapter
   +-- Sunmi
   +-- iMin
   +-- PAX
   +-- ESC/POS generico
   +-- otros SDK segun demanda
```

Antes de soportar un terminal concreto se debe registrar marca, modelo, version Android y SDK/servicio de impresion disponible.

## 8. Abstraccion comun de impresion

El POS debe evolucionar hacia una interfaz comun independiente de plataforma:

```text
PrintingProvider
   +-- QzPrintingProvider        (Windows/macOS)
   +-- AndroidNativeProvider    (Android App)
```

La logica de negocio no debe conocer detalles de QZ, SDK Sunmi, PAX o similares.

Responsabilidades comunes:

- obtener estado;
- listar/identificar impresora;
- imprimir ticket;
- imprimir etiqueta;
- imprimir documento A4 cuando aplique;
- abrir cajon cuando la plataforma lo soporte;
- reportar error sin alterar la venta.

## 9. Tipos de impresion

### 9.1 Tickets termicos

Estado actual: HTML/pixel mediante QZ.

Objetivo futuro: usar impresion nativa/RAW cuando convenga para mejorar velocidad y nitidez.

Tecnologias previstas:

- ESC/POS para tickets/cajon en impresoras compatibles;
- ZPL para ciertas impresoras de etiquetas;
- TSPL para ciertas impresoras de etiquetas.

No se debe forzar una migracion completa a RAW hasta que el renderer y las pruebas de hardware esten maduros.

### 9.2 Etiquetas

El POS ya permite seleccionar una impresora de etiquetas independiente. La logica final de etiquetas se desarrollara con renderer y lenguaje de impresora apropiado por modelo.

### 9.3 A4

Los documentos A4 deben priorizar contenido vectorial/PDF generado por Tarevo y enviado a la impresora seleccionada. Se debe evitar rasterizar innecesariamente documentos administrativos.

## 10. Ticket: renderer, margenes y vista previa

### 10.1 Un solo renderer

La vista previa y la impresion deben usar la misma fuente de verdad.

No se debe mantener una plantilla para preview y otra diferente para imprimir.

Arquitectura objetivo:

```text
ReceiptRenderer
   +-- Vista previa
   +-- QZ / Windows / macOS
   +-- Android native bridge
```

### 10.2 Configuracion local futura

`Configuracion > Impresion` debe incorporar ajustes locales de ticket, como minimo:

- margen superior;
- margen inferior;
- margen izquierdo;
- margen derecho;
- ancho 58/80 mm;
- escala cuando sea necesaria;
- desplazamiento horizontal/vertical solo si se justifica por hardware.

Estos valores deben tener limites razonables y guardarse por computador/navegador y tenant, igual que la impresora.

### 10.3 Vista previa

La pantalla de impresion debe ofrecer una vista previa del ticket que responda en tiempo real a:

- ancho de papel;
- margenes;
- escala;
- contenido del renderer.

La vista previa se usa para reducir pruebas de papel y corregir impresoras con areas no imprimibles distintas.

Una impresora A4 puede cortar un ticket pensado para termica por sus margenes fisicos; por eso la preview y los margenes configurables son parte del producto y no un workaround puntual.

## 11. Cajon portamonedas

La preferencia `Abrir cajon portamonedas despues de imprimir` puede guardarse actualmente, pero no debe fingirse que funciona si no existe comando nativo implementado.

La apertura real se implementara con ESC/POS o mecanismo equivalente de la impresora/dispositivo.

La apertura del cajon debe ocurrir despues del trabajo de impresion correspondiente y nunca afectar el estado de la venta.

## 12. Comportamiento ante fallos

El POS debe seguir operando cuando:

- QZ no esta instalado;
- QZ esta cerrado;
- Tarevo Print Connector no esta disponible;
- no hay impresora configurada;
- la impresora esta offline;
- la firma backend falla temporalmente;
- el bridge Android no esta disponible.

Regla:

```text
fallo de impresion != fallo de venta
```

Los errores deben mostrarse como mensajes de usuario claros y nunca como stack traces.

## 13. Seguridad

Reglas obligatorias:

- la clave privada permanece en backend;
- los clientes reciben solo certificado publico;
- toda firma QZ se genera en backend;
- algoritmo actual: SHA512;
- no registrar payloads sensibles innecesarios;
- no confiar en nombres de impresora enviados por otros tenants;
- preferencias locales no contienen secretos;
- el bridge Android debe limitar comunicaciones al origen oficial de Tarevo y exponer solo funciones necesarias;
- instaladores no contienen secretos del backend.

## 14. Relacion con ventas

La impresion es un efecto posterior de una venta confirmada, no una transaccion de negocio que pueda invalidar la venta.

La plantilla debe reutilizar la informacion canonica de la venta y evitar mantener un segundo modelo de datos solo para impresion.

Cuando exista reimpresion desde historial, debe usar exactamente el mismo renderer y los mismos servicios de impresion.

## 15. Implementacion actual en tarevo-platform

Componentes relevantes actuales:

```text
apps/pos/src/api/printingService.ts
apps/pos/src/api/printingPreferencesService.ts
apps/pos/src/api/receiptPrintingService.ts
apps/pos/src/components/PrintingSettings.tsx
```

Backend relevante:

```text
apps/api/app/Services/QzSigningService.php
apps/api/app/Http/Controllers/Api/V1/QzPrintingController.php
apps/api/routes/qz.php
apps/api/resources/qz/digital-certificate.txt
apps/api/config/qz.php
```

Endpoints:

```text
GET  /api/v1/printing/qz/certificate
POST /api/v1/printing/qz/sign
```

El endpoint de firma requiere autenticacion, tenant y permiso POS correspondiente.

## 16. Historial de implementacion

Cambios principales en `tarevo-platform`:

- PR #159: fundacion QZ, firma segura backend y diagnostico inicial.
- PR #160: autenticacion correcta del diagnostico QZ.
- PR #161: carga robusta de clave privada y normalizacion estricta del `=` de Coolify.
- PR #162: `Configuracion > Impresion`, preferencias locales por tenant, prueba QZ y autoimpresion best-effort despues de venta confirmada.

La impresion silenciosa de Windows quedo validada en produccion despues de estos cambios.

## 17. Hoja de ruta de impresion

Orden recomendado:

### Fase A - Pulido del ticket

- margenes configurables;
- vista previa;
- renderer unico;
- reimpresion desde historial;
- pruebas con impresoras termicas reales 58/80 mm.

### Fase B - Tarevo Print Connector

- instalador Windows `.exe`;
- instalador macOS `.pkg`;
- descarga autoservicio desde `Configuracion > Impresion`;
- deteccion de instalacion/version;
- actualizacion futura.

### Fase C - Impresion nativa/RAW

- ESC/POS para ticket/cajon;
- ZPL/TSPL para etiquetas donde corresponda;
- mantener PDF/vector para A4.

### Fase D - Android POS App

- WebView seguro de Tarevo POS;
- bridge nativo;
- primer adaptador para el terminal Android prioritario;
- arquitectura de drivers por fabricante;
- instalacion/actualizacion controlada de APK.

## 18. Regla de producto

Para el cliente, la experiencia debe ser simple:

```text
Configuracion
 -> Impresion
 -> instalar Tarevo Print Connector si hace falta
 -> elegir impresora
 -> ajustar ticket
 -> ver vista previa
 -> imprimir prueba
 -> vender
```

Los detalles internos de QZ, certificados, puertos, firma o SDK del fabricante pertenecen al diagnostico tecnico y no deben dominar la interfaz de usuario.