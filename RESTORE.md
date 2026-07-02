# Restaurar el agente OpenClaw / Musk

Cómo volver a un agente funcional desde cero (máquina nueva o pérdida total).
Leer entero antes de ejecutar.

> Para recuperar el PROYECTO COMPLETO (agente + research + backtest + paper
> engine, los 4 repos), el índice maestro es `RECOVERY.md` en el repo
> `github.com/rodrigomidas/polyclaw-musk`. Este archivo cubre solo el agente.

## Mapa de dónde vive el estado (IMPORTANTE)

El estado del agente está repartido en TRES lugares. No confundirlos:

| Ubicación | Qué es | ¿Respaldado? |
|---|---|---|
| `~/Projects/openclaw` (este repo, `origin` = github.com/rodrigomidas/openclaw) | Copia **curada** de políticas/identidad/memoria. Rama canónica: `main`. | ✅ GitHub |
| `~/.openclaw/workspace/` | **Runtime vivo** que el agente lee/edita. Repo git propio. | ✅ github.com/rodrigomidas/openclaw-workspace (privado; solo `.md`, secretos/estado gitignoreados) |
| `~/.openclaw/` (`.env`, `service-env/`, `auth-profiles*`, `openclaw.json`, `identity/`) | **Secretos y config de runtime.** | ❌ Solo local — ver `VAULT_BACKUP.md` |

Los `.md` de políticas (AGENTS, SOUL, PAPER_TRADING, POLYMARKET_READONLY, etc.)
existen en los tres lugares y **pueden divergir**. La fuente de verdad para
políticas es este repo (`main`); el workspace se sincroniza desde acá.

## Restaurar el workspace vivo

`~/.openclaw/workspace/` ya está respaldado en
`github.com/rodrigomidas/openclaw-workspace` (privado; solo `.md` de política,
con `.gitignore` que excluye estado de runtime y secretos). Para restaurarlo:

```bash
git clone https://github.com/rodrigomidas/openclaw-workspace.git ~/.openclaw/workspace
```

Recordá commitear/pushear ahí cuando edites políticas del agente en vivo (no es
automático). Las `skills/` NO están en ese backup: son repos propios
(p.ej. `skills/polyclaw` = github.com/chainstacklabs/polyclaw) que se restauran
clonándolos por separado, y su `.env` se recupera desde el vault.

## Gap conocido (a remediar)

- **Los secretos no se respaldan en git** (correcto por seguridad) pero deben
  respaldarse aparte: ver `VAULT_BACKUP.md`. Sin ellos el agente restaurado
  no arranca (sin API keys, sin token de Telegram, y **sin la llave de la wallet
  de Polygon no hay acceso a fondos**).

## Procedimiento de restauración

### 1. Instalar el runtime OpenClaw
Instalar el binario/paquete de OpenClaw (ver `~/.openclaw/npm/package.json` para
la versión) y correr una vez para que cree la estructura `~/.openclaw/`.

### 2. Restaurar secretos y config de runtime
Seguir `VAULT_BACKUP.md` en orden inverso: restaurar `~/.openclaw/.env`,
`~/.openclaw/service-env/ai.openclaw.gateway.env`, `auth-profiles.json`,
`~/.openclaw/openclaw.json` e `identity/device.json` desde el vault seguro.

### 3. Restaurar políticas e identidad del agente
Clonar este repo y copiar los `.md` al workspace del runtime:

```bash
git clone https://github.com/rodrigomidas/openclaw.git
cd openclaw
# El agente lee de ~/.openclaw/workspace/. Copiar TODAS las políticas:
mkdir -p ~/.openclaw/workspace
cp -v *.md ~/.openclaw/workspace/
# BOOTSTRAP.md vive en el runtime (~/.openclaw/agents/main/agent/), no en este
# repo; si no lo tenés en el vault, se regenera en el primer arranque del agente.
```

### 4. Verificar antes de habilitar trading
- El agente arranca en modo **paper trading** (ver `PAPER_TRADING.md`).
- Confirmar que `POLYMARKET_READONLY.md` y `SECURITY.md` están cargados ANTES
  de habilitar cualquier ejecución con dinero real.
- Revisar `runbook.md` (en polyclaw-musk) para arranque y parada de emergencia.

## Qué NO va en este repo (nunca commitear)

API keys · tokens de Telegram/GitHub · `.env` · `auth-profiles.json` ·
**llave/seed de la wallet** · sesiones locales · SQLite · logs. Ver `.gitignore`.
