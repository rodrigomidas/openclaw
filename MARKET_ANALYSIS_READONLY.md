# Market Analysis Read-Only Flow — OpenClaw Rodrigo

Este documento define el flujo de análisis de mercados en modo solo lectura.

## Objetivo

Permitir que el agente analice un mercado, pregunta, evento o hipótesis usando únicamente información pública, sin conectar cuentas, wallets, claves privadas, fondos ni capacidad de ejecución.

## Modo obligatorio

READ_ONLY

## Entrada esperada

Rodrigo puede enviar:

- Una URL pública de un mercado.
- El nombre de un mercado.
- Una pregunta de investigación.
- Un evento público.
- Una hipótesis para evaluar.

## Permitido

El agente puede:

- Leer información pública.
- Resumir la pregunta del mercado.
- Identificar criterios de resolución.
- Analizar contexto.
- Comparar fuentes.
- Formular hipótesis.
- Estimar incertidumbre.
- Registrar una simulación.
- Sugerir próximos pasos no sensibles.

## Prohibido

El agente no puede:

- Ejecutar trades.
- Conectar cuentas.
- Conectar wallets.
- Firmar transacciones.
- Mover fondos.
- Depositar fondos.
- Retirar fondos.
- Pedir seed phrases.
- Pedir private keys.
- Pedir tokens sensibles.
- Operar cuentas de Rodrigo.
- Automatizar decisiones financieras.

## Flujo de análisis

Para cada mercado o evento, el agente debe responder con esta estructura:

MERCADO:
URL O REFERENCIA:
PREGUNTA PRINCIPAL:
ESTADO:
FECHA / PLAZO RELEVANTE:
CRITERIOS DE RESOLUCIÓN:
CONTEXTO:
DATOS OBSERVABLES:
FUENTES CONSULTADAS:
ARGUMENTO A FAVOR:
ARGUMENTO EN CONTRA:
INCERTIDUMBRE:
RIESGOS:
HIPÓTESIS:
CONFIANZA:
ACCIÓN SIMULADA:
QUÉ FALTARÍA VERIFICAR:
NO ES UNA OPERACIÓN REAL.

## Reglas de calidad

El agente debe:

- Distinguir datos observados de inferencias.
- Citar o mencionar fuentes cuando sea posible.
- No inventar precios, probabilidades ni datos.
- Declarar incertidumbre.
- Evitar exceso de confianza.
- No presentar simulaciones como recomendaciones reales.
- Mantener lenguaje claro y operativo.

## Relación con otros documentos

Este flujo debe obedecer:

- AGENTS.md
- AGENT_POLICY.md
- SECURITY.md
- PAPER_TRADING.md
- POLYMARKET_READONLY.md
- RESEARCH_READONLY_FLOW.md
- AUDIT_LOG.md
- SOUL.md

Si hay conflicto, gana la regla más restrictiva.

