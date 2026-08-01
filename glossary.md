# Glosario de dominio

Lenguaje ubicuo del proyecto. El objetivo es que cada concepto se llame **igual** en el schema, la API
y la UI. Documento vivo: se actualiza cuando se cierra una decisión o se agrega un concepto.

## Estructura del consorcio

- **Consorcio (de propietarios)** — el edificio o conjunto sometido a propiedad horizontal. Unidad
  central del dominio. Una administradora gestiona N consorcios.
- **Administradora** — la empresa que administra consorcios. Es el **tenant** del SaaS (el cliente que
  paga). No confundir con *administrador* (la persona).
- **Administrador** — la persona física/jurídica inscripta que administra. En CABA debe estar en el
  RPA (ver Ley 941).
- **Unidad funcional (UF)** — cada unidad independiente del consorcio: departamento, cochera, baulera,
  local. Puede tener superficie propia y uno o más coeficientes.
- **Coeficiente (de copropiedad)** — porcentaje de participación de una UF en los gastos y decisiones.
  El conjunto suma 100%. **Puede haber múltiples coeficientes por UF**: distintos rubros se prorratean
  con coeficientes distintos (p. ej. ascensor no siempre lo paga la planta baja). El modelo soporta
  varios coeficientes por unidad, no uno solo.

## Expensas y liquidación

- **Expensas** — la contribución mensual de cada UF a los gastos del consorcio.
  - **Ordinarias** — gastos corrientes y periódicos.
  - **Extraordinarias** — gastos no recurrentes (obras, reparaciones mayores).
- **Liquidación (de expensas)** — el proceso y documento mensual que junta los gastos del período, los
  clasifica, aplica el coeficiente correspondiente a cada rubro, suma fondo de reserva e intereses, y
  emite el detalle individual por UF.
- **Rubro / categoría de gasto** — clasificación de un gasto (limpieza, ascensor, sueldos, ABL,
  reparaciones, etc.). Taxonomía cerrada y normalizada (habilita analytics y benchmarking).
- **Fondo de reserva** — fondo acumulado del consorcio para imprevistos.
- **Prorrateo** — reparto de un gasto entre las UF según el coeficiente que aplique a ese rubro.

## Cobranzas

- **Estado de cuenta** — saldo y movimientos de una UF (deudas, pagos, intereses).
- **Cobranza** — gestión del cobro de las expensas a las UF.
- **Mora** — atraso en el pago.
- **Interés por mora** — recargo aplicado sobre el saldo impago.

## Gobierno y personas

- **Propietario** — dueño de una UF.
- **Inquilino** — quien alquila una UF. En inglés "tenant" — **ver nota de ambigüedad abajo**.
- **Consejo de propietarios / de administración** — órgano de control de la administración.
- **Asamblea** — reunión de propietarios que decide sobre el consorcio.
  - **Ordinaria** / **Extraordinaria**.
- **Acta** — documento que registra lo resuelto en asamblea.
- **Encargado** — personal del edificio. Su liquidación de sueldos cae bajo convenio (SUTERH /
  FATERYH); es un subdominio propio, candidato a integración/tercerización antes que a construcción.
- **Proveedor** — quien provee bienes/servicios al consorcio (se identifica por CUIT).

## Regulatorio (Argentina · CABA)

- **Ley 941** — régimen de CABA que crea el RPA y obliga al administrador a inscribirse y presentar
  DDJJ anual.
- **RPA** — Registro Público de Administradores de Consorcios (CABA).
- **DDJJ** — declaración jurada (anual, ante el RPA).
- **Cuenta bancaria del consorcio** — cada consorcio debe tener su propia cuenta. Impacta el modelo y
  la conciliación.
- **INDEC / IPC** — Índice de Precios al Consumidor (serie pública del INDEC). Se usa para las vistas de
  expensas ajustadas por inflación.

## Términos técnicos de tenancy

- **Plataforma** — nivel raíz del SaaS (todas las administradoras).
- **Tenant** — en el SaaS, equivale a **administradora**. Unidad de aislamiento de datos.
- **RLS (Row-Level Security)** — mecanismo de PostgreSQL que enforcea el aislamiento por tenant a nivel
  de fila.

## Nota de ambigüedad: "tenant"

La palabra **tenant** tiene dos sentidos que no hay que cruzar:

- **Tenant (SaaS)** = **administradora**. Es el eje de aislamiento de datos (RLS).
- **Tenant (inmobiliario)** = **inquilino**. Es un rol de persona sobre una UF.

En el código y el schema, **tenant siempre refiere a la administradora**. Para el sentido inmobiliario
se usa siempre **inquilino** (nunca "tenant"). Evita colisiones de naming.
