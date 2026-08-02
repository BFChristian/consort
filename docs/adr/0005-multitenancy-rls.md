# ADR-0005: Multi-tenancy con Row-Level Security (jerarquía de 3 niveles)

- **Estado:** Aceptada
- **Fecha:** 2026-07-28

## Contexto

SaaS con jerarquía de tres niveles: **plataforma → administradora (tenant) → consorcio**. El
aislamiento entre administradoras es crítico: se manejan datos financieros de terceros. Se busca además
habilitar benchmarking cross-tenant anonimizado (foso de datos) sin fragmentar la información.

## Decisión

Aislamiento lógico con `administradora_id` (tenant) en cada tabla de dominio + **Row-Level Security de
PostgreSQL**, sobre un **schema único**. La variable de sesión de tenant se setea por request (guard /
interceptor de NestJS) a partir de la membresía del usuario autenticado.

## Justificación

Un solo schema es mucho más simple de operar y migrar para un dev solo que schema-por-tenant. RLS lleva
el aislamiento a la capa de base de datos (defensa en profundidad ante un bug de query en la app). El
schema único habilita analytics cross-tenant simple.

## Alternativas descartadas

- Schema-por-tenant / DB-por-tenant — descartado por costo operativo y de migraciones, y porque
  complica el analytics cross-tenant.
- Aislamiento solo en la capa de aplicación (sin RLS) — descartado por dejar una única línea de defensa
  ante errores de query.

## Consecuencias

- Toda tabla de dominio lleva `administradora_id` y hereda la política RLS.
- La autorización (rol + scope de consorcio) vive en tablas propias, no en RLS.
- El tenant sale de la tabla de membresías, no de Better Auth (ver [ADR-0007](./0007-auth-better-auth.md)).
