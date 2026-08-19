# Resumen - AS-IS

## Dominios y subdominios

![AS-IS](HogarDeLosAlpes-Dominios-ASIS_ContextMap.png)

Las tres relaciones del ASIS cuentan la misma historia desde ángulos distintos: no hay contextos internos, solo un monolito (MonolitoHogarDeLosAlpes) que absorbe todo, y ese monolito siempre aparece como downstream de los tres sistemas externos.

Frente a verificación de proveedores y a la pasarela de pagos usa ACL, es decir, se protege con una capa propia y no deja que el modelo del sistema externo se filtre directamente. Pero frente a partners (aseguradoras, bancos, comercios) es Conformist sin traducción: se adapta tal cual a más de 30 contratos distintos, sin capa de protección ni lenguaje común.

En conjunto, las relaciones describen una compañía técnicamente inmadura y sin poder de negociación frente a sus socios B2B2C: todo el negocio corre acoplado en un único sistema que, además de no poder evolucionar por partes, queda expuesto y rígido ante cada partner porque no tiene una traducción propia que lo aísle.

# Resumen — TO-BE

## Dominios y subdominios

![TO-BE](HogarDeLosAlpes-Dominios-Contextos-TOBE_ContextMap.png)

Los contextos describen una compañía que se organiza deliberadamente en capacidades de negocio autónomas y reutilizables: ContextoGestionDeTrabajos es el eje central —único dueño del Aggregate Trabajo— y expone su lenguaje (OHS/PL) a Marketplace, Operación B2B2C, Pagos, e incluso a las dos líneas de negocio nuevas (Fintech y Suscripciones), que se construyen consumiendo capacidades ya existentes (Trabajos, Marketplace, Acreditación, Calidad y Reputación) en lugar de duplicarlas, mostrando una estrategia de crecimiento por composición sobre una base común.

La mayoría de relaciones internas ya no son Conformist "a ciegas" como en el ASIS, sino CF sobre un Published Language explícito, es decir, contratos publicados y estables entre equipos que pueden evolucionar de forma independiente.

El ACL, en cambio, se usa solo donde persiste riesgo real: frente a los sistemas externos (pagos, verificación, +30 partners) y en los puntos donde un contexto observa a otro con un propósito distinto (Calidad y Reputación sobre Trabajos, Operación B2B2C sobre Acreditación por las homologaciones de partner). Además, separar ContextoAlianzasB2B2C (negociación comercial) de ContextoOperacionB2B2C (ejecución operativa), y aislar ContextoExpansionRegional como capacidad transversal consumida por quien la necesita, muestra una compañía que refleja su estructura organizacional en la arquitectura (Conway) y que diseñó el TOBE explícitamente para soportar su expansión de negocio —fintech, suscripciones, nuevos países— sin repetir la rigidez del monolito original.
