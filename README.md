# Documentación del proyecto

Plataforma SaaS de administración de consorcios (Argentina · CABA como contexto regulatorio primario).

## Índice

- **Arquitectura**
  - [Overview del sistema](./docs/architecture/overview.md) — mapa de contenedores y cómo se hablan.
  - [Stack reference](./docs/architecture/stack-reference.md) — tecnologías cerradas y rol de cada una.
- **Decisiones (ADR)**
  - [Índice de ADRs](./docs/adr/README.md)
  - [Decisiones diferidas](./docs/adr/deferred-decisions.md) — reconocidas pero pospuestas.
- **Dominio**
  - [Glosario](./docs/domain/glossary.md) — lenguaje ubicuo del dominio.

## Convención de documentación

Decision-first: se registra **qué** se decidió y **por qué** (breve). Las alternativas descartadas
aparecen como una línea cada una, no como discusión. El modelo de datos (ERD, diccionario de datos)
se documenta una vez diseñadas las entidades del core.
