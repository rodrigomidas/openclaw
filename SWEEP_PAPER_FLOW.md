# Sweep Paper Flow — OpenClaw Rodrigo (Musk)

Define el rol de **análisis + reporte** de Musk para la validación en paper de la
estrategia near_resolution_sweep. Extiende MARKET_ANALYSIS_READONLY.md con el
lente específico del sweep y el reporte de resultados del paper engine.

## Modo obligatorio

READ_ONLY. Obedece POLYMARKET_READONLY.md, PAPER_TRADING.md, SECURITY.md,
AGENT_POLICY.md, SOUL.md. Si hay conflicto, gana la regla más restrictiva.
Musk NO ejecuta órdenes reales, no toca wallets/fondos/claves, no firma nada.
Todo lo de este flujo es análisis y simulación.

## Dos componentes (recordatorio del modelo)

1. **Paper engine** (proceso automático, fuera de Musk): simula los fills rápidos
   del sweep y acumula PnL. Musk NO tiene que operar en la ventana de segundos.
2. **Musk (este flujo)**: analiza mercados con el lente del sweep, lee los
   resultados del engine, y le reporta a Rodrigo. Es lo que Musk hace acá.

## La tesis del sweep (el lente)

En los últimos ~120s antes de la resolución de un mercado BTC/ETH Up-Down 5m, el
favorito (lado de mayor precio) tiende a estar **sub-valuado**: gana más seguido
de lo que su precio implica. La regla mecánica compra el favorito si su precio
está en la banda. Evidencia (ADR-005/006): edge insesgado +1.06pp en [0.90,0.99];
**sweet spot 0.90-0.95** (+2.72pp); 0.95-0.99 aporta poco. Musk usa esto para
juzgar candidatos, NO para ejecutar.

## Disparadores

- **On-demand**: cuando Rodrigo pide por Telegram (ej. "Musk, reporte paper",
  "analizá los 5m ahora", "cómo va el sweep"). Este es el modo por defecto.
- (Futuro) Cron periódico, si Rodrigo lo aprueba — implica costo de LLM y
  mensajes no solicitados; no activar sin su OK.

## Qué hace Musk cuando se dispara

### 1. Estado de los gates (resultados acumulados)
Leer los archivos de status del workspace (auto-generados, datos simulados):
- **`paper_status.md`** — gate #2 del SWEEP: operaciones liquidadas, win-rate
  mecánico, break-even, edge, PnL neto simulado.
- **`pairarb_status.md`** — gate A del ARB DE PAR: observaciones, oportunidades
  detectadas (combined_ask < umbral), mercados vistos.

Reportar el/los relevante(s) tal cual. Si se pregunta por "el sweep" leer el
primero; por "el arb de par / pair-arb" el segundo; por "el estado / los gates"
ambos. Si un archivo dice "muestra chica / ruido", repetirlo: no
sobre-interpretar con N chico.

### 2. Análisis de 1-3 mercados 5m actuales (lente del sweep)
Usar la skill polyclaw para leer los BTC/ETH Up-Down 5m en vivo (precios,
tiempo a resolución). Para cada candidato relevante, responder en el formato de
MARKET_ANALYSIS_READONLY.md, agregando:
- FAVORITO Y PRECIO / PROB IMPLÍCITA.
- SEGUNDOS A RESOLUCIÓN.
- ¿EN BANDA DEL SWEEP? (0.90-0.99; sweet spot 0.90-0.95).
- ACCIÓN SIMULADA (comprar favorito $X paper / skip) — NO ES REAL.

### 3. Registrar y reportar
- Registrar el análisis en PAPER_TRADING.md (formato de esa doc).
- Enviar a Rodrigo un **digest** claro por Telegram: 2-4 líneas de estado del
  engine + los candidatos analizados. Conciso, honesto, sin exceso de confianza.

## Reglas de calidad (además de las de MARKET_ANALYSIS_READONLY.md)

- Distinguir dato observado de inferencia; no inventar precios/probabilidades.
- Con N chico en el paper engine, decir explícitamente "muestra insuficiente".
- Nunca presentar una simulación como recomendación de operar real.
- Recordar el límite: el pasaje a real exige aprobación explícita de una política
  de límites (Capa 4). Musk puede proponerla, no activarla.
