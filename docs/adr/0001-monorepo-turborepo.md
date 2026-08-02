# ADR-0001: Monorepo con Turborepo

- **Estado:** Aceptada
- **Fecha:** 2026-07-28

## Contexto

Un solo desarrollador. Tres superficies (API NestJS, admin Next.js, cliente Expo) más código
compartido: schemas de validación, tipos y el cliente de API generado desde el spec OpenAPI. Se
necesita compartir ese contrato con el mínimo overhead de coordinación.

## Decisión

Monorepo gestionado con Turborepo. `apps/*` para las tres superficies, `packages/*` para lo compartido
(schemas Zod, tipos, cliente tipado, config de tooling).

## Justificación

Un único lugar donde vive el contrato tipado, consumido por backend y ambos fronts sin sincronizar
repos. Builds incrementales y cacheados. Un solo flujo de CI. Para un dev solo, elimina el costo de
versionar y publicar paquetes entre repos separados.

## Alternativas descartadas

- Repos separados (back y fronts) — descartado por la fricción de compartir el contrato tipado y la
  duplicación de tooling.
- Nx — descartado por mayor complejidad y curva frente a lo que necesita un solo dev.

## Consecuencias

- Requiere disciplina de límites entre `apps/*` y `packages/*`.
- Tooling compartido (tsconfig, lint, format) centralizado en `packages/*`.
- Los fronts consumen el cliente tipado desde un package, no desde código duplicado.
