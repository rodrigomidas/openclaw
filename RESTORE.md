# Restaurar OpenClaw Rodrigo Agent

Este repo contiene archivos seguros de identidad, memoria inicial y configuración conceptual del agente.

## No contiene secretos

No debe contener:

- API Keys
- tokens de Telegram
- tokens de GitHub
- `.env`
- `auth-profiles.json`
- sesiones locales
- bases SQLite
- logs

## Restaurar archivos del agente

Desde la raíz del repo:

```bash
cp IDENTITY.md ~/.openclaw/agents/main/agent/ 2>/dev/null || true
cp USER.md ~/.openclaw/agents/main/agent/ 2>/dev/null || true
cp SOUL.md ~/.openclaw/agents/main/agent/ 2>/dev/null || true
cp BOOTSTRAP.md ~/.openclaw/agents/main/agent/ 2>/dev/null || true
cp MEMORY.md ~/.openclaw/agents/main/agent/ 2>/dev/null || true
