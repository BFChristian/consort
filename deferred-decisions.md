# Decisiones diferidas

Decisiones reconocidas pero pospuestas. Cada una se reabre con su feature, o antes del primer deploy
según el caso. Se registran para que no se pierdan del radar.

| Tema | Dirección tentativa | Se reabre cuando |
|------|---------------------|------------------|
| Pagos | MercadoPago | Llega la feature de cobranzas. Core del negocio. |
| Generación de PDF | (a decidir) | Llega la feature de liquidación. |
| Push notifications | Expo Push / FCM | Llega el motor de notificaciones (fase 2). |
| OCR | Visión de LLM vs. Document AI / Textract | Llega el pipeline de IA / onboarding. |
| Hosting + servicios manejados | Neon/Supabase, Upstash, Railway/Fly/Render | **Antes del primer deploy** (deadline más cercano). |
| Observabilidad | Sentry + Pino | Cuando haya qué observar. |
| UI del cliente Expo | NativeWind (± Tamagui) | Con el scaffold del cliente Expo. |

## Nota sobre observabilidad

El *audit log* propio (quién cambió qué y cuándo, relevante para una app financiera) es una cosa
distinta de la observabilidad técnica: es diseño de datos, no una herramienta externa. Se piensa junto
al modelo de datos.

## Descartado por prematuro

State management global, i18n, feature flags y secrets manager dedicado — se resuelven solos o se
deciden mucho más adelante; no se documentan como decisión todavía.
