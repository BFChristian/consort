# ADR-0011: Convención de dinero y tiempo

- **Estado:** Aceptada
- **Fecha:** 2026-07-28

## Contexto

Cálculo financiero (expensas, coeficientes, intereses por mora) y fechas con impacto legal y contable.
JavaScript usa floats por defecto y maneja fechas sin timezone explícito — dos fuentes clásicas de bugs
en este dominio.

## Decisión

**Dinero:** nunca floats. `numeric` en PostgreSQL y `decimal` en la capa TS (p. ej. decimal.js /
dinero.js). Los montos se representan como enteros de la mínima unidad (centavos) o decimal explícito,
nunca como `number` de punto flotante.

**Tiempo:** timezone explícita `America/Argentina/Buenos_Aires`. Timestamps almacenados en UTC en la
base; conversión a la TZ local solo en los bordes (presentación / entrada).

## Justificación

Evita errores de redondeo sobre fondos de terceros y bugs de fecha por timezone (incluidos los
estacionales). Es barato de fijar como convención ahora y carísimo de retrofitear una vez que hay datos.

## Alternativas descartadas

- `number` de JS para montos — descartado por error de punto flotante.
- Fechas sin TZ / hora local implícita — descartado por ambigüedad y bugs de conversión.

## Consecuencias

- Todo campo monetario y temporal sigue la convención desde la primera tabla.
- Los schemas de Zod reflejan estos tipos (decimal como string validado, fechas en UTC).
