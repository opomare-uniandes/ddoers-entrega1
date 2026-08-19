# Hogar de los Alpes — Dominios y subdominios

## Propósito

Esta carpeta contiene el modelo estratégico de dominios y subdominios de
**Hogar de los Alpes**. El modelo fue construido a partir de las capacidades,
reglas y objetivos del negocio descritos en el caso de estudio y documentado
con el DSL de **Context Mapper**.

El artefacto principal es [`HogarDeLosAlpes-Dominios.cml`](./HogarDeLosAlpes-Dominios.cml).
Su alcance corresponde al espacio del problema: describe capacidades de
negocio, pero no define contextos acotados, microservicios, equipos ni unidades
de despliegue.

## Contenido de la carpeta

| Recurso | Descripción |
|---|---|
| [`HogarDeLosAlpes-Dominios.cml`](./HogarDeLosAlpes-Dominios.cml) | Fuente oficial del modelo: dominios, *vision statements*, subdominios y tipos. |
| [`diagramas/`](./diagramas/) | Vistas gráficas del portafolio de dominios y del detalle de sus subdominios. |
| [`generar-diagramas.mjs`](./generar-diagramas.mjs) | Generador reproducible de los diagramas mediante Node.js y Graphviz. |

## Enfoque de modelado

La descomposición se realizó por **capacidades, conocimiento y reglas de
negocio**. No se utilizaron como límites el organigrama, las tecnologías, el
monolito actual ni una posible lista futura de microservicios.

Para clasificar cada subdominio se consideró:

1. si diferencia a Hogar de los Alpes frente al mercado;
2. si concentra conocimiento complejo o altamente variable;
3. si impacta directamente la estrategia o propuesta de valor; y
4. si una solución estándar del mercado sería suficiente.

## Resultado

El modelo contiene:

- **3 dominios de negocio** con su respectivo `domainVisionStatement`;
- **25 subdominios**, todos con clasificación y *vision statement* propio;
- **9** subdominios `CORE_DOMAIN`;
- **13** subdominios `SUPPORTING_DOMAIN`; y
- **3** subdominios `GENERIC_SUBDOMAIN`.

![Resumen de dominios y subdominios](./diagramas/HogarDeLosAlpes-Dominios-Resumen.png)

## Dominios identificados

### Servicios para el Hogar

**Estado:** vigente y principal.<br>
**Composición:** 16 subdominios: 5 núcleo, 9 soporte y 2 genéricos.

**Vision statement:** conectar hogares y organizaciones aliadas con
proveedores confiables para diagnosticar, coordinar y resolver necesidades del
hogar de extremo a extremo, con seguridad, trazabilidad y adaptación a cada
mercado.

Este dominio materializa la propuesta de valor actual. Marketplace y B2B2C se
mantienen como subdominios porque, aunque presentan clientes y reglas
diferentes, comparten los conceptos centrales de trabajo, proveedor acreditado
y ejecución física en el hogar.

### Servicios Financieros para Proveedores

**Estado:** emergente.<br>
**Composición:** 5 subdominios: 2 núcleo, 2 soporte y 1 genérico.

**Vision statement:** impulsar la inclusión y el crecimiento financiero de los
proveedores mediante una billetera, pagos y crédito responsable sustentado en
su historial verificable de trabajos.

Se modela como dominio independiente porque constituye una línea de negocio
con clientes, regulación, riesgos y ciclos de vida propios. Su diferenciación
consiste en aprovechar el historial de trabajos y cumplimiento para construir
*scoring* y ofrecer crédito responsable.

### Servicios Recurrentes para el Hogar

**Estado:** futuro.<br>
**Composición:** 4 subdominios: 2 núcleo y 2 soporte.

**Vision statement:** ofrecer a los hogares servicios recurrentes confiables
mediante suscripciones flexibles que aseguren continuidad, coordinación y
calidad con proveedores acreditados.

Se modela como dominio separado porque la suscripción introduce una propuesta
comercial y un ciclo de vida distintos de un trabajo puntual: planes,
frecuencias, renovaciones, pausas, cancelaciones y cobros periódicos.

## Criterios de clasificación

### Núcleo — `CORE_DOMAIN`

Incluye las capacidades que concentran diferenciación, complejidad y
conocimiento propio: diagnóstico, orquestación de trabajos, *matching*,
operación B2B2C, acreditación, *scoring* financiero, crédito y oferta de
servicios recurrentes.

La **acreditación de proveedores** es núcleo porque la confianza en quien
ingresa al hogar es parte central de la promesa de la compañía. La habilitación
depende del tipo de proveedor, el servicio, la zona, las credenciales, el
*partner* y las revalidaciones aplicables.

### Soporte — `SUPPORTING_DOMAIN`

Agrupa capacidades necesarias para operar, con reglas propias, que no
constituyen por sí solas la ventaja principal. Incluye registro, catálogo,
cotizaciones, evidencias, garantías, reputación, liquidación, facturación,
localización, billetera y gestión administrativa de suscripciones.

**Liquidación de Trabajos** permanece separada de **Procesamiento de Pagos**:
la primera contiene reglas de retención, liberación y distribución de fondos;
la segunda representa la integración con medios y proveedores de pago.

### Genérico — `GENERIC_SUBDOMAIN`

Incluye capacidades importantes pero estandarizadas para las que existen
productos y prácticas maduras: autenticación y autorización, procesamiento de
pagos y cumplimiento financiero.

**Autenticación y Autorización** se conserva como un único subdominio genérico.
La autenticación verifica la identidad de usuarios, proveedores, agentes y
*partners*; la autorización controla las capacidades disponibles para cada
actor. Ambas responsabilidades forman una capacidad IAM cohesionada y
normalmente soportada por protocolos y productos estándar.

## Decisiones de alcance

- **IA no es un dominio:** es un habilitador aplicado a diagnóstico,
  acreditación, *scoring*, priorización, riesgo y fraude.
- **Plataforma no es un dominio:** es una agrupación tecnológica u
  organizacional, no una propuesta de valor.
- **El monolito no es un dominio:** corresponde a una forma de implementación.
- **Los países no son dominios:** introducen variaciones de moneda, regulación
  y operación dentro de las capacidades existentes.
- **Un subdominio no equivale automáticamente a un microservicio:** este modelo
  no determina límites de despliegue.

## Validación y regeneración

El CML fue validado con Context Mapper 6.12.0 sobre OpenJDK 17, sin errores ni
advertencias en el panel **Problems** de Visual Studio Code.

![Validación del modelo con Context Mapper DSL](./evidencias/ContextMapper-Validacion-DSL.jpg)

La captura anterior evidencia simultáneamente el archivo CML abierto con
resaltado del DSL, el indicador **Context Mapper DSL** en la barra de estado y
el panel **Problems** sin errores ni advertencias.

Para revisarlo:

1. abrir `HogarDeLosAlpes-Dominios.cml` en Visual Studio Code;
2. confirmar que el lenguaje activo sea **Context Mapper DSL**;
3. revisar las declaraciones `Domain`, `Subdomain`,
   `domainVisionStatement` y `type`; y
4. comprobar que el panel **Problems** no reporte errores.

Para regenerar los diagramas se requiere Node.js y Graphviz disponibles en el
`PATH`:

```bash
node generar-diagramas.mjs
```

Los diagramas son vistas estratégicas derivadas del CML; no representan
Context Maps de DDD.

## Trazabilidad con la rúbrica

| Criterio | Evidencia |
|---|---|
| Todos los dominios y subdominios usando Context Mapper | 3 declaraciones `Domain` y 25 declaraciones `Subdomain`. |
| *Vision statement* para todos los dominios | 3 de 3 dominios declaran `domainVisionStatement`. |
| Tipo para todos los subdominios | 25 de 25 subdominios declaran `type` con un valor permitido. |
