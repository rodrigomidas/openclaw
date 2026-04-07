# Brief Template — Proposal Engine

## Standard Input

```
Cliente:
Producto:
Objetivo:
Audiencia:
Canal:
Presupuesto:
Timing:
Referencia previa: (link o nombre de propuesta base)
Restricciones:
Output esperado: (formato, idioma, nivel de detalle)
```

## Example — Seguros Bolívar / Póliza de Movilidad

```
Cliente: Seguros Bolívar
Producto: Póliza de Movilidad (seguro vehicular)
Objetivo: Generar tráfico calificado al landing page, mejorar baseline de performance con audiencias identificadas de 1st Party Data
Audiencia: 35-55 años, capacidad adquisitiva media-alta, interés en asegurar carro o moto
Canal: Remarketing en Meta (Custom Audience)
Presupuesto: COP $3.000.000/mes
Timing: ASAP
Referencia previa: Seguros Bolívar - MIDAS - Propuesta Renta Voluntaria V1.0
Restricciones: URBEX como única fuente de audiencia. No se puede distinguir carro vs moto explícitamente.
Output esperado: Presentación .pptx con mismo diseño/tipografía que propuesta previa, en español
```

## Notes

- If URBEX is the data source, available variables include: edad, tenencia de inmuebles, avalúo catastral, barrio/ubicación, metraje, créditos activos/pagados, perfil patrimonial inferido.
- When data doesn't support explicit claims (e.g., car vs bike ownership), use softer language: "usuarios con alta afinidad hacia productos de protección asociados a movilidad".
- Cost formula for URBEX: budget / match cost = audience size (e.g., $3MM / $980 = ~3,061 users).
