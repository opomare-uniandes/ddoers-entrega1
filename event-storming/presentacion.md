# Hogar de los Alpes — Event Storming (TO-BE)
### Actores, comandos, eventos, modelo de lectura, sistemas externos y lenguaje ubicuo

---

## Flujo 1 — Trabajos Complejos y Novedades
*(Dominio Core)*

**Actores**
- Dueño de Hogar
- Proveedor
- Agente IA de Re-diagnóstico (asistido)

**Sistemas externos**
- Sin sistema externo directo en este flujo: la integración con partners B2B2C se resuelve vía Anti-Corruption Layer (comando Sincronizar Novedad con Partner).

**Modelo de lectura**
- Vista Consolidada del Trabajo Complejo (CQRS)

**Comandos (9)**
- Reportar Novedad en Ejecución
- Confirmar Re-diagnóstico
- Crear Sub-Trabajo
- Recalcular Costos
- Reordenar Plan del Trabajo
- Aceptar Nuevo Alcance y Costo
- Abrir Disputa
- Sincronizar Novedad con Partner (ACL)
- Solicitar Reasignación

**Eventos de dominio (12)**
- Novedad Reportada (evento de integración)
- Re-diagnóstico Sugerido
- Trabajo Re-diagnosticado
- Re-diagnóstico Rechazado
- Sub-Trabajo Creado
- Costos Recalculados
- Plan Reordenado
- Alcance Aceptado
- Disputa Abierta
- Disputa Resuelta
- Novedad Sincronizada con Partner
- Proveedor Reasignado

**Definiciones — Lenguaje ubicuo**
- Bounded Context (Evans): Orquestación de Trabajos, Cotizaciones y Visitas, Marketplace y Matching, y Calidad-Disputas son contextos independientes, cada uno con su propio modelo y base de datos.
- Ubiquitous Language: Novedad, Sub-Trabajo, Alcance y Disputa significan exactamente lo mismo en el código y en la conversación de negocio dentro del contexto.
- Aggregate: "Trabajo" es el aggregate root — único punto de escritura consistente del contexto.
- Saga coreografiada: cada novedad se procesa sin orquestador central; ningún contexto bloquea a los demás.

---

## Flujo 2 — Verificación de Proveedores
*(Dominio Core)*

**Actores**
- Proveedor (persona o empresa)
- Agente IA de Verificación Documental (agente automatizado)

**Sistemas externos**
- Sistema de la Policía (API asíncrona)
- Entidades Certificadoras (API asíncrona)
- Registros Empresariales (API asíncrona, solo empresas)

**Modelo de lectura**
- Vista de Cobertura y Habilitación (CQRS)

**Comandos (10)**
- Registrar Proveedor
- Iniciar Verificación
- Analizar Documentos con IA
- Calcular Riesgo Preliminar
- Consultar Antecedentes Judiciales
- Validar Títulos y Certificados
- Verificar Registro Mercantil y Estado Legal
- Calcular Decisión de Habilitación
- Revisar Caso Manualmente
- Revalidar Proveedor / Técnico

**Eventos de dominio (12)**
- Proveedor Registrado
- Verificación Iniciada
- Documentos Analizados
- Riesgo Preliminar Calculado
- Antecedentes Verificados
- Certificación Verificada
- Empresa Verificada
- Proveedor Habilitado (servicio, zona)
- Caso Escalado a Agente
- Decisión Confirmada
- Revalidación Programada
- Proveedor Revalidado

**Definiciones — Lenguaje ubicuo**
- Bounded Context: Registro de Proveedores y Acreditación de Proveedores son contextos independientes, cada uno con su propio modelo y base de datos.
- Aggregate: "Proveedor" agrupa antecedentes, certificaciones y estado de habilitación bajo un único límite de consistencia.
- Ubiquitous Language: Habilitado, Revalidación y Acreditación se usan de forma consistente, sin sinónimos ambiguos entre equipos.
- Human-in-the-loop: la IA acelera el análisis documental, pero un agente humano confirma la decisión final en casos de alto riesgo.

---

## Flujo 3 — Marketplace B2C
*(Subdominio de Soporte)*

**Actores**
- Dueño de Hogar
- Proveedor
- Agente IA de Diagnóstico (asistido)

**Sistemas externos**
- Sistema de Notificaciones
- Pasarela de Pagos (circuit breaker + reintentos)

**Modelo de lectura**
- Vista Comparativa de Cotizaciones (CQRS)
- Vista de Reputación (CQRS)

**Comandos (12)**
- Describir Problema
- Crear Trabajo
- Publicar Oferta
- Matchear Proveedores
- Enviar Cotización
- Seleccionar Cotización
- Asignar Proveedor
- Reportar Novedad
- Recotizar (compensación)
- Finalizar Trabajo
- Liberar Pago
- Calificar Proveedor

**Eventos de dominio (15)**
- Problema Reportado
- Problema Diagnosticado (evento de integración)
- Trabajo Creado
- Oferta Publicada
- Proveedores Matcheados
- Proveedor Notificado
- Cotización Registrada
- Cotización Seleccionada
- Trabajo Asignado
- Ejecución Iniciada
- Novedad Reportada
- Recotización Solicitada
- Trabajo Finalizado (Outbox)
- Pago Liberado
- Proveedor Calificado

**Definiciones — Lenguaje ubicuo**
- Bounded Contexts independientes: Marketplace y Matching, Orquestación de Trabajos y Liquidación de Trabajos — cada uno con su propio modelo y base de datos.
- Patrón Outbox: los eventos se publican de forma confiable junto con la transacción local (Trabajo Finalizado, Pago Liberado).
- CQRS: la Vista Comparativa de Cotizaciones y la Vista de Reputación se actualizan de forma asíncrona, desacopladas del modelo de escritura.
- Aggregate: "Trabajo" es el aggregate root — agrupa cotización, asignación, ejecución y cierre bajo un mismo límite de consistencia.