# ADR-0003: API REST + OpenAPI con clientes tipados generados

- **Estado:** Aceptada
- **Fecha:** 2026-07-28

## Contexto

Tres clientes TypeScript (admin Next.js, cliente Expo web y móvil) consumen la misma API. A futuro
habrá webhooks de pago (MercadoPago) y posibles integraciones con organismos (AFIP/ARCA), que hablan
HTTP estándar, no un protocolo cerrado.

## Decisión

Contrato REST documentado con OpenAPI vía `@nestjs/swagger`. Del spec se generan **clientes tipados**
para los dos fronts (p. ej. `openapi-typescript` u `orval`).

## Justificación

Da tipado end-to-end (el objetivo que tentaba a tRPC) pero sobre un estándar agnóstico de lenguaje y a
prueba de futuro: webhooks, integraciones externas y una eventual API pública hablan REST nativo. Un
OpenAPI bien armado además es buena carta de presentación en portfolio.

## Alternativas descartadas

- tRPC — descartado por fricción con NestJS y por atar el sistema a un mundo cerrado solo-TS (mal fit
  para webhooks y API pública).
- GraphQL — descartado por complejidad (resolvers, N+1, caching) que las necesidades de datos de los
  clientes no justifican.

## Consecuencias

- Se agrega un paso de generación de clientes tipados al pipeline del monorepo.
- El spec OpenAPI es un artefacto de primer nivel; el diseño de entidades piensa en paralelo qué
  expone la API y con qué forma.
