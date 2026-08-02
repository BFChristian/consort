# ADR-0008: Módulo de IA — analítica determinística + LLM solo para prosa

- **Estado:** Aceptada
- **Fecha:** 2026-07-28

## Contexto

El módulo de IA opera sobre plata ajena (fondos de terceros). No puede introducir errores de cálculo ni
presentar predicciones como certezas. La confianza del usuario depende de que los números sean siempre
correctos.

## Decisión

Dos capas estrictamente separadas:

1. **Capa de analítica determinística** (código, no IA) computa los hechos y produce un objeto de
   *drivers* estructurados: qué rubro cambió, cuánto, y por qué.
2. **El LLM solo redacta prosa** a partir de esos drivers ya calculados. Nunca suma, resta ni estima.

Todo output de IA lleva un disclaimer visible de que fue generado con IA y puede contener errores.

## Justificación

Los números son correctos por construcción; la superficie de error del LLM se reduce a la redacción.
Es una separación exigible a nivel de arquitectura de backend, no una consideración de UX.

## Alternativas descartadas

- Dejar que el LLM calcule o estime sobre los datos — descartado por riesgo inaceptable con fondos de
  terceros.
- "IA que decide / predice" presentada como certeza — descartado: la IA asiste, el humano confirma.

## Consecuencias

- La capa de analítica expone un contrato de *drivers* estructurado como entrada del LLM.
- Ese contrato se piensa desde el diseño del modelo de datos.
