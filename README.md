# Tarevo Documentation

Repositorio oficial de documentacion de Tarevo.

Tarevo es una plataforma SaaS de gestion comercial para PYMEs, enfocada inicialmente en Chile, con arquitectura preparada para crecer hacia otros paises.

## Estado del proyecto

- Producto: Tarevo
- Nombre tecnico: Tarevo Platform
- Dominio objetivo: `gettarevo.com`
- Mercado inicial: Chile
- Estado: Sprint 0 - Documentacion, marca, arquitectura e infraestructura
- Codigo fuente futuro: `tarevo-platform`

## Regla principal

Ninguna linea de codigo debe desarrollarse sin una decision documentada o un PRD asociado.

## Principio financiero

Tarevo debe crecer con disciplina de costos. La arquitectura debe estar preparada para escalar, pero no se deben contratar servicios pagos, integraciones complejas o suscripciones externas antes de que exista una necesidad real o clientes que justifiquen el gasto.

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

## Documentos principales

- `00-Constitution/Tarevo-Constitution.md`
- `01-Product/Product-Vision.md`
- `01-Product/Module-Scope-V1.md`
- `02-Business/PRD-General-Chile.md`
- `03-Architecture/Architecture-Principles.md`
- `04-Infrastructure/INF-001-Produccion.md`
- `05-Database/Conceptual-Data-Model.md`
- `06-Security/SEC-001-Security-Architecture.md`
- `08-ADL/ADL.md`
- `09-Journal/2026-07-09.md`
- `10-Backlog/V1-Initial-Backlog.md`
- `10-Backlog/Codex-Implementation-Prompts.md`
- `11-Roadmap/Roadmap.md`
- `12-Brand/Brand-Foundation.md`

## Como debe trabajar Codex

Codex nunca debe recibir una instruccion generica como "haz Tarevo".

Debe recibir tareas cerradas, por ejemplo:

```text
Lee Tarevo Constitution, ADL, INF-001, SEC-001, PRD-General-Chile y Module-Scope-V1.
Implementa solamente el modulo de autenticacion segura.
No hardcodees secretos.
No hagas una version demo.
Respeta la arquitectura multiempresa y los permisos.
Documenta cualquier decision tecnica nueva en ADL antes de implementarla.
```

## Principio operativo

El chat sirve para discutir ideas. GitHub es la fuente oficial de la documentacion aprobada.
