# ADR-0007: Better Auth (identidad) + autorización propia

- **Estado:** Aceptada
- **Fecha:** 2026-07-28

## Contexto

App financiera y multi-tenant donde conviene poseer los datos de identidad de los usuarios (compliance,
Ley 941). Stack all-TS con Drizzle ya elegido y tres clientes, incluido Expo (web + móvil).

## Decisión

**Better Auth** como capa de autenticación: self-hosted, dueño de sus tablas (`user`, `session`,
`account`, `verification`) vía adapter de Drizzle. La **autorización** —administradora como tenant,
scope de consorcio, roles (admin, empleado, contador, propietario, inquilino, encargado)— vive en
tablas propias del dominio, ligadas al `user` por `user_id`.

## Justificación

Self-hosted / MIT → propiedad de la data. Adapter de Drizzle y plugin de Expo (soporta nativo y web)
de primera parte. 2FA, passkeys y social login incluidos. Ecosistema en consolidación (el equipo tomó
el mantenimiento de Auth.js). Mantener la autorización en código propio permite dominar la lógica de
negocio y no forzar la jerarquía de tres niveles sobre un modelo plano de "organizations".

## Alternativas descartadas

- Clerk / Auth0 (hosted) — descartado por lock-in, costo por usuario activo y por alojar la identidad
  fuera de la propia infraestructura.
- Plugin `organization` de Better Auth para la jerarquía — descartado por no calzar con los tres
  niveles (plataforma → administradora → consorcio).
- Passport + JWT propio de punta a punta — descartado por el riesgo de implementar mal la parte
  sensible de seguridad.

## Consecuencias

- La integración con NestJS es community-maintained (requiere desactivar el body parser de Nest).
- Mayor responsabilidad propia sobre la seguridad que con un proveedor hosted.
- El tenant que alimenta la RLS sale de la tabla de membresías propia, no de Better Auth.
