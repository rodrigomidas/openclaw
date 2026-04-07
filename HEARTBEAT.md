# HEARTBEAT.md

## Auto-commit
- Run `cd /Users/OpenClaw/.openclaw/workspace && git add -A && git diff --cached --quiet || git commit -m "auto: heartbeat backup $(date +%Y-%m-%d_%H:%M)"` every heartbeat
- If a git remote is configured, also `git push` after commit
