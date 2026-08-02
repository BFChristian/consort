# ADR-0002: Backend NestJS

- **Estado:** Aceptada
- **Fecha:** 2026-07-28

## Contexto

Dominio grande y creciente (consorcios, unidades, coeficientes, liquidaciones, cobranzas, proveedores,
módulo de IA, motor de alertas, multi-tenancy), mantenido por un solo dev durante meses. Stack
TypeScript de punta a punta. Se busca estructura sostenible en el tiempo por encima de velocidad
inicial.

## Decisión

NestJS como framework de backend, en arquitectura de **monolito modular**.

## Justificación

Impone estructura (módulos, inyección de dependencias) que sostiene el crecimiento del dominio y evita
que el código degenere con un solo dev. La multi-tenancy entra limpia como guard + interceptor que
setea el tenant por request. Integra colas (`@nestjs/bullmq`) y OpenAPI (`@nestjs/swagger`) de fábrica.
Skill de backend TS de alta demanda, valioso como pieza de portfolio.

## Alternativas descartadas

- Fastify / Hono pelado — descartado porque el ahorro de ceremonia no compensa la falta de estructura
  en un dominio de este tamaño.
- Backend dentro de Next.js (server actions / API routes) — descartado porque dos de los tres clientes
  son Expo (no aprovechan server actions) y un dominio con colas, RLS y jobs no entra cómodo en las
  API routes de Next.

## Consecuencias

- Curva inicial más empinada y más boilerplate para casos simples.
- A cambio, estructura clara y modular; se parte a microservicios solo si algún módulo lo exige.
