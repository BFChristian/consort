# Stack reference

Tecnologías cerradas del proyecto. Cada una tiene su ADR con la justificación; acá va la foto rápida.

## Fundacional

| Área | Elección | ADR |
|------|----------|-----|
| Monorepo | Turborepo (`apps/*`, `packages/*`) | [0001](../adr/0001-monorepo-turborepo.md) |
| Backend | NestJS (monolito modular) | [0002](../adr/0002-backend-nestjs.md) |
| Contrato de API | REST + OpenAPI, clientes tipados generados | [0003](../adr/0003-api-rest-openapi.md) |
| ORM / DB | Drizzle ORM sobre PostgreSQL | [0004](../adr/0004-orm-drizzle.md) |
| Multi-tenancy | PostgreSQL + Row-Level Security, schema único | [0005](../adr/0005-multitenancy-rls.md) |
| Admin web | Next.js | [0006](../adr/0006-frontends-next-expo.md) |
| Cliente web+móvil | Expo / React Native (codebase único) | [0006](../adr/0006-frontends-next-expo.md) |
| Auth | Better Auth (identidad) + autorización propia | [0007](../adr/0007-auth-better-auth.md) |
| Validación | Zod (schema compartido) | [0009](../adr/0009-validacion-zod.md) |
| Testing | Vitest + Playwright + Supertest | [0010](../adr/0010-testing-vitest-playwright.md) |
| Dinero y tiempo | Convención (numeric/decimal, TZ explícita) | [0011](../adr/0011-convencion-dinero-tiempo.md) |

## Infraestructura de apoyo

| Área | Elección | Nota |
|------|----------|------|
| Colas / jobs | Redis + BullMQ (`@nestjs/bullmq`) | Liquidaciones, OCR, mails/push, crons |
| Storage | S3-compatible; MinIO en dev | Comprobantes, PDFs, reglamentos |
| Email | Resend | Requerido por Better Auth desde el día uno |
| State de servidor (fronts) | TanStack Query | Cache/refetch/mutaciones en Next y Expo |
| Entorno de dev | Docker Compose | Postgres + Redis + MinIO con un comando |

## Datos externos

| Fuente | Uso |
|--------|-----|
| INDEC — serie de IPC (pública) | Vistas de expensas ajustadas por inflación |

## Diferido (ver [deferred-decisions](../adr/deferred-decisions.md))

Pagos (MercadoPago), generación de PDF, push (Expo Push/FCM), OCR, hosting + servicios manejados,
observabilidad (Sentry + Pino), UI del cliente Expo (NativeWind ± Tamagui).
