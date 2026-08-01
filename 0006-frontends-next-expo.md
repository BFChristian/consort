# ADR-0006: Admin en Next.js + cliente único en Expo (Camino A)

- **Estado:** Aceptada
- **Fecha:** 2026-07-28

## Contexto

Tres superficies: admin web (densa en datos, desktop-first), cliente web y cliente móvil. El cliente
web y el móvil son el mismo producto para el mismo usuario (propietario / inquilino), con las mismas
features. Un solo dev.

## Decisión

- **Admin** en Next.js (React web).
- **Cliente web + móvil** en un único codebase Expo / React Native que produce web, iOS y Android
  (Camino A).

## Justificación

El admin es una app compleja por derecho propio → Next.js. El portal del cliente está detrás de login,
así que no necesita SEO ni SSR, que es lo único que Next.js aportaría de ventaja ahí; sin esa
necesidad, React Native Web alcanza y colapsa dos superficies en un codebase. Menos código para
mantener estando solo, y aprender RN suma al portfolio y a la empleabilidad.

## Alternativas descartadas

- Next.js para cliente web + Expo para móvil (dos codebases) — descartado por el doble mantenimiento de
  la capa de presentación con un solo dev.

## Consecuencias

- Se aprende el dialecto de RN (`View` / `Text` / `Pressable`, estilos como objeto, sin DOM).
- La web del cliente queda "buena pero no impecable"; aceptable porque es una UI simple.
- Con tres consumidores de la misma API, el contrato tipado deja de ser un lujo.
