# Atlas Documentation

Repositorio oficial de documentacion de Atlas.

Atlas es una plataforma SaaS de gestion comercial para PYMEs, enfocada inicialmente en Chile, con arquitectura preparada para crecer hacia otros paises.

## Estado del proyecto

- Producto: Atlas
- Nombre tecnico: Atlas Platform
- Mercado inicial: Chile
- Estado: Sprint 0 - Documentacion y arquitectura
- Codigo fuente futuro: `atlas-platform`

## Regla principal

Ninguna linea de codigo debe desarrollarse sin una decision documentada o un PRD asociado.

## Estructura

```text
00-Constitution/
01-Product/
02-Business/
03-Architecture/
04-Infrastructure/
05-Database/
06-Security/
07-Design-System/
08-ADL/
09-Journal/
10-Backlog/
11-Roadmap/
12-Brand/
13-Legal/
```

## Documentos iniciales

- `00-Constitution/Atlas-Constitution.md`
- `01-Product/Product-Vision.md`
- `03-Architecture/Architecture-Principles.md`
- `04-Infrastructure/INF-001-Produccion.md`
- `06-Security/SEC-001-Security-Architecture.md`
- `08-ADL/ADL.md`
- `09-Journal/2026-07-09.md`
- `10-Backlog/V1-Initial-Backlog.md`
- `11-Roadmap/Roadmap.md`

## Como debe trabajar Codex

Codex nunca debe recibir una instruccion generica como "haz Atlas".

Debe recibir tareas cerradas, por ejemplo:

```text
Lee Atlas Constitution, ADL, INF-001 y SEC-001.
Implementa solamente el modulo de autenticacion segura.
No hardcodees secretos.
No hagas una version demo.
Respeta la arquitectura multiempresa y los permisos.
```

## Principio operativo

El chat sirve para discutir ideas. GitHub es la fuente oficial de la documentacion aprobada.
