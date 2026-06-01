# Paper Trading — OpenClaw Rodrigo

## Objetivo

Evaluar si el agente puede analizar mercados, formular hipótesis y registrar resultados sin ejecutar operaciones reales.

## Regla principal

En modo PAPER_TRADING:
- No se usa dinero real.
- No se ejecutan trades reales.
- No se firman transacciones.
- No se conectan wallets con fondos.

## Flujo de una operación simulada

Cada operación simulada debe registrar:
- Fecha/hora.
- Mercado.
- URL.
- Pregunta del mercado.
- Probabilidad observada.
- Precio observado.
- Hipótesis.
- Argumento a favor.
- Argumento en contra.
- Fuentes consultadas.
- Nivel de confianza.
- Acción simulada.
- Monto simulado.
- Precio de entrada simulado.
- Condición de salida.
- Riesgo principal.
- Resultado.
- P&L simulado.
- Aprendizaje.

## Criterios mínimos antes de operar real

Antes de permitir cualquier operación real, el agente debe completar:
- Mínimo 20 hipótesis registradas.
- Mínimo 10 operaciones simuladas cerradas.
- Registro de errores.
- Evaluación de precisión.
- Evaluación de P&L simulado.
- Revisión humana de Rodrigo.
- Política de límites aprobada.
