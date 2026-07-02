# Project State — Musk (contexto para el agente)

Estado del proyecto de trading. Read-only: nada de esto habilita acciones reales.
Todo lo cuantitativo es simulado.

## Fase actual

**Validación en paper.** No hay trading real, ni wallet fondeada, ni capital en
riesgo. Dos "gates" (validaciones) corren en background recolectando datos:

- **Gate #2 (SWEEP)**: estrategia near-resolution sweep — comprar el favorito de
  un mercado 5m cerca de la resolución. Edge validado offline: ~+1.06% sobre
  volumen. Fino pero real; direccional. Status: `paper_status.md`.
- **Gate A (ARB DE PAR)**: comprar YES+NO por combinado < $1 y hacer MERGE por
  $1/par (market-neutral). Análisis offline: selectivo da ~+5.3%. Candidato a
  estrategia primaria. Status: `pairarb_status.md`. (Detector en vivo midiendo
  la tasa de oportunidad real.)

## Qué sé (validado)

- El sweep es un edge estructural fino; el momentum del subyacente y el timing
  NO lo mejoran (testeado). Sus levers son ejecución/sizing/escala, no "pensar
  mejor".
- El arb de par selectivo es más rentable y market-neutral; ahí la inteligencia
  (selección + ejecución dual-leg) sí paga.
- Cohorte: mercados BTC/ETH/SOL/XRP/DOGE Up-Down de 5 minutos.

## Qué NO hago (hasta aprobar una política de límites)

Trading real, conectar wallet, firmar, mover fondos, ejecución automatizada de
órdenes reales. El pasaje de paper a real requiere aprobación explícita de
Rodrigo de una política de límites (la "Capa 4": caps de exposición, drawdown,
kill switch). Ver POLYMARKET_READONLY.md.

## Mi rol

Analizar mercados (formato de MARKET_ANALYSIS_READONLY.md), leer los status de
los gates y reportarle a Rodrigo. No soy el recolector (eso son scripts en
background); soy el analista/reporte encima.
