# Market Estimate Flow — OpenClaw Rodrigo (Musk)

Cómo Musk produce una **estimación de probabilidad calibrada** para un mercado.
Es el corazón del enfoque analítico: el edge de Musk (si existe) está en dar una
probabilidad mejor calibrada que el mercado, en mercados de JUICIO (política,
macro, geopolítica, eventos) — no en el cripto 5m (eficiente, latency-arb).

READ_ONLY. Es una estimación/simulación, no una operación real.

## Método de pronóstico calibrado (superforecasting)

Cuando Rodrigo (o el pipeline) me pide estimar la probabilidad de un mercado, NO
tiro un número al aire. Sigo estos pasos y muestro el razonamiento (1 línea c/u):

1. **CRITERIO**: ¿qué EXACTAMENTE tiene que pasar para que resuelva SÍ? Releo la
   pregunta con cuidado (fechas, umbrales, condiciones). Muchos errores vienen de
   malinterpretar el criterio de resolución.
2. **TASA BASE (vista externa)**: ¿con qué frecuencia ocurren eventos de esta
   clase de referencia? Empiezo por la tasa base, NO por el caso específico. (Ej:
   "un top favorito gana un mundial de 48 equipos ~15-25% de las veces", no "es
   favorito, entonces alto".)
3. **EVIDENCIA (vista interna)**: ajusto la tasa base con información específica y
   ACTUAL (busco con web search si puedo). Un argumento a favor y uno en contra.
   Ajusto con moderación — la vista interna tiende a sobre-ajustar.
4. **TIEMPO**: ¿cuánto falta para la resolución? ¿favorece SÍ o NO?
5. **CHEQUEO DE COHERENCIA**: mi número DEBE coherir con mi razonamiento. No uso
   0% ni 100% (nada es imposible ni seguro). Si la evidencia es débil, me quedo
   cerca de la tasa base — evito el exceso de confianza.

Termino SIEMPRE con una línea exacta y parseable:

PROBABILIDAD_SI: XX%

## Reglas

- Estimación INDEPENDIENTE: si es posible, no miro el precio de mercado antes de
  estimar (para no anclarme). El objetivo es comparar mi juicio contra el mercado.
- No inventar datos; distinguir observado de inferido; declarar incertidumbre.
- Si no puedo verificar info actual, lo digo y me apoyo más en la tasa base.
- Obedece POLYMARKET_READONLY.md, SECURITY.md, AGENT_POLICY.md. Es simulación.
