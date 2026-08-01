# ADR-0010: Testing con Vitest + Playwright

- **Estado:** Aceptada
- **Fecha:** 2026-07-28

## Contexto

El dev testea y CI corre tests. Monorepo TypeScript con API NestJS y dos fronts. Se busca una sola
config coherente en todo el repo.

## Decisión

- **Vitest** como test runner para unit e integration.
- **Playwright** para E2E del admin.
- **Supertest** para tests de integración de la API en NestJS.

## Justificación

Vitest es más rápido y ESM-nativo, con una config que sirve a todo el monorepo. Playwright es robusto y
estándar para E2E web. Supertest es el estándar para probar controladores de Nest.

## Alternativas descartadas

- Jest — descartado por config más pesada y soporte de ESM más engorroso frente a Vitest.

## Consecuencias

- El pipeline de CI corre lint + build + test.
- Convención de ubicación de tests por app y por package.
