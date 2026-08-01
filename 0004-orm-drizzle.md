# ADR-0004: ORM Drizzle sobre PostgreSQL

- **Estado:** Aceptada
- **Fecha:** 2026-07-28

## Contexto

La multi-tenancy se enforcea con Row-Level Security de PostgreSQL, que requiere setear una variable de
sesión por transacción (`SET app.current_tenant = ...`) para que las políticas filtren por tenant. El
dev además busca aprender la base de datos, no esconderla.

## Decisión

Drizzle ORM sobre PostgreSQL.

## Justificación

Da control directo sobre la conexión y la sesión, así que setear la variable de RLS en cada request
sale limpio (con Prisma esto se pelea con `$executeRaw` y extensiones del cliente). Es SQL-first y
transparente: se aprende la base y se sabe exactamente qué query corre — deseable con datos
financieros. Tiene adapter nativo de Better Auth.

## Alternativas descartadas

- Prisma — descartado por la fricción para setear la variable de sesión de RLS, pese a mejor DX,
  migraciones más cómodas y mayor popularidad.

## Consecuencias

- Se escribe más cercano al SQL (más control, menos azúcar).
- `tenant_id` y las políticas RLS son ciudadanos de primera desde la primera tabla, no un agregado
  posterior.
