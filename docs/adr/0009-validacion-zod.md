# ADR-0009: Validación con Zod (schema compartido)

- **Estado:** Aceptada
- **Fecha:** 2026-07-28

## Contexto

Monorepo con package compartido y contrato tipado end-to-end. Se busca una sola fuente de verdad de las
reglas de validación, reutilizable entre el backend y los dos fronts (Next y Expo).

## Decisión

Zod como librería de validación runtime. Los schemas viven en un `package` compartido; en NestJS se
integran vía pipe (p. ej. `nestjs-zod`, que además alimenta el OpenAPI).

## Justificación

Un schema de Zod valida en runtime y **deriva el tipo estático** (una sola definición). Al vivir en el
package compartido, lo reusan backend, OpenAPI y ambos fronts sin redefinir reglas por superficie —
imposible de lograr con validación atada a clases del backend.

## Alternativas descartadas

- class-validator (nativo de NestJS) — descartado porque los decoradores quedan atados a clases del
  backend y no viajan al package compartido ni al Expo. Sería defendible solo si el backend fuera una
  isla.

## Consecuencias

- Fricción menor y de una sola vez al integrar Zod en Nest (salirse del camino de decoradores).
- El package de schemas Zod es un artefacto central del monorepo.
