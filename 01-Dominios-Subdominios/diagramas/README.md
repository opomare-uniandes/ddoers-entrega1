# Diagramas estratégicos

Estas imágenes son vistas complementarias derivadas de
`../HogarDeLosAlpes-Dominios.cml`:

- `HogarDeLosAlpes-Dominios-Resumen`: portafolio de los tres dominios, vision
  statements y resumen cuantitativo.
- `HogarDeLosAlpes-ServiciosParaElHogar`: subdominios del negocio vigente.
- `HogarDeLosAlpes-ServiciosFinancierosParaProveedores`: subdominios del
  negocio financiero emergente.
- `HogarDeLosAlpes-ServiciosRecurrentesParaElHogar`: subdominios del negocio
  futuro de suscripciones.

Cada diagrama se entrega en PNG y SVG. Los archivos DOT regenerables se
encuentran en `fuentes/`.

## Convención visual

- Rojo claro: subdominio núcleo (`CORE_DOMAIN`).
- Azul claro: subdominio de soporte (`SUPPORTING_DOMAIN`).
- Verde claro: subdominio genérico (`GENERIC_SUBDOMAIN`).

## Regeneración

Desde el directorio padre:

```bash
node generar-diagramas.mjs
```

Requiere Node.js y Graphviz (`dot`) disponibles en el `PATH`.

## Alcance

Estos son mapas estratégicos de dominios y subdominios. No son Context Maps de
DDD y no sustituyen los futuros diagramas AS-IS/TO-BE de bounded contexts,
relaciones, mecanismos de integración y equipos.
