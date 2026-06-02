# Market Preview Analysis — OpenClaw Rodrigo

Este documento define qué debe hacer el agente cuando solo puede observar una vista previa, metadata, snippet, screenshot o lectura parcial de un mercado.

## Modo obligatorio

READ_ONLY

## Regla principal

Si el agente solo tiene acceso parcial al mercado, debe decirlo explícitamente y no hacer análisis profundo.

Frase obligatoria:

Lectura parcial: solo pude observar metadatos o vista previa, no el mercado completo.

## Permitido

El agente puede:

- Extraer únicamente lo visible.
- Listar datos observados.
- Marcar datos no verificados.
- Pedir información faltante.
- Preparar una checklist de datos necesarios.
- Sugerir fuentes públicas para completar el análisis.

## Prohibido

El agente no puede:

- Inventar datos faltantes.
- Inferir criterios de resolución.
- Inferir liquidez, volumen o probabilidades si no son visibles.
- Asumir que la lista visible está completa.
- Recomendar operaciones reales.
- Ejecutar trades.
- Conectar cuentas.
- Conectar wallets.
- Firmar transacciones.
- Mover fondos.

## Formato obligatorio

LECTURA:
DATOS VISIBLES:
DATOS NO VERIFICADOS:
QUÉ FALTA PARA ANÁLISIS COMPLETO:
FUENTES SUGERIDAS:
PRÓXIMO PASO SEGURO:
NO ES UNA OPERACIÓN REAL.

