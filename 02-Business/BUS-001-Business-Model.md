# BUS-001 — Business Model

Version: 0.2  
Estado: Aprobado para Tarevo V1  
Fecha de aprobación comercial: 2026-07-12  
Owner: Chris

## Objetivo

Definir el modelo comercial inicial de Tarevo para Chile y mantener una única fuente oficial para precios, límites y beneficios de los planes.

## Inversión inicial

- Dominio: `gettarevo.com`.
- Costo inicial del dominio: USD 10.46.
- Vigencia inicial: 1 año.

## Filosofía

- Crecer con ingresos, no con deuda.
- Evitar servicios de pago hasta que aporten valor real.
- Preparar la arquitectura para escalar sin sobredimensionar costos.
- No prometer funciones o límites que todavía no puedan operarse de forma segura.

## Planes V1 aprobados

Los precios se expresan en pesos chilenos y no incluyen IVA.

| Recurso | Starter | Pro | Business | Enterprise |
|---|---:|---:|---:|---:|
| Precio mensual | $19.990 + IVA | $39.990 + IVA | $79.990 + IVA | Cotización |
| Empresas incluidas | 1 | 1 | 1 | Según contrato |
| Usuarios | 3 | 10 | 30 | Personalizado |
| Sucursales | 1 | 3 | 10 | Personalizado |
| Bodegas | 1 | 3 | 10 | Personalizado |
| Cajas | 1 | 3 | 10 | Personalizado |
| Almacenamiento | 5 GB | 25 GB | 100 GB | Personalizado |
| POS | Incluido | Incluido | Incluido | Incluido |
| Inventario | Básico | Completo | Completo | Completo |
| Warehouse completo | No | Sí | Sí | Sí |
| Reportes | Básicos | Ampliados | Ampliados | Personalizados según contrato |
| Dominio propio | No | Sí | Sí | Según contrato |
| Subdominio Tarevo | Sí | Sí | Sí | Sí |
| DTE | Límite básico | Límite ampliado | Límite superior | Según contrato |
| Soporte | Estándar | Prioritario | Prioritario | Según contrato |

## Reglas comerciales

- Los límites se controlan mediante entitlements en backend.
- Superar un límite no elimina datos existentes.
- Un downgrade inactiva o restringe recursos excedentes de forma controlada; nunca los elimina automáticamente.
- El cliente conserva acceso de lectura a sus datos según la política de suspensión.
- Los recursos adicionales futuros pueden venderse como complementos: almacenamiento, DTE, usuarios, sucursales, bodegas, cajas y Apps.
- El precio y los límites no deben duplicarse manualmente en distintos módulos del código. Deben provenir de una única configuración de planes.

## Período de gracia

El período de gracia aprobado es de 7 días después del vencimiento.

Después del período de gracia:

- Se bloquean nuevas ventas y otras operaciones definidas por la política de suspensión.
- Los datos se conservan.
- La cuenta se reactiva al confirmar un pago válido.
- Ningún dato se elimina por falta de pago.

## Decisiones todavía pendientes

- Duración final del trial inicial.
- Cantidad exacta de DTE incluida por plan, después de conocer el costo del proveedor.
- Proveedor de pagos.
- Proveedor DTE inicial.
- Precio de almacenamiento adicional.
- Precios anuales y descuentos por prepago.
- Política final de soporte y SLA.
