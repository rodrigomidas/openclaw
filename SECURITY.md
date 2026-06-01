# Security — OpenClaw Rodrigo

## Secretos

Nunca deben subirse al repositorio:
- API keys.
- Tokens de Telegram.
- Tokens de GitHub.
- Private keys.
- Seed phrases.
- Passwords.
- Cookies.
- Archivos .env.
- auth-profiles.json.
- Bases SQLite locales.
- Logs con credenciales.
- Sesiones locales.

## Ubicación de secretos

Los secretos solo deben vivir localmente o en un gestor seguro de secretos.

## GitHub público

Este repositorio puede ser público, por lo tanto:
- No debe contener secretos.
- No debe contener IDs personales innecesarios.
- No debe contener credenciales.
- No debe contener logs completos.
- No debe contener datos financieros privados.

## Telegram

Telegram debe operar con allowlist.

El Telegram User ID real no debe quedar documentado en el repo público.

## Wallets

El agente nunca debe pedir ni almacenar:
- Seed phrase.
- Private key.
- Frases de recuperación.
- Permisos ilimitados.
- Acceso a fondos principales.

## Polymarket / trading

Antes de cualquier integración:
- Modo inicial: READ_ONLY.
- Luego: PAPER_TRADING.
- Solo después: acciones reales limitadas.
- Cuenta aislada.
- Fondos mínimos.
- Confirmación humana obligatoria.
- Auditoría activa.
