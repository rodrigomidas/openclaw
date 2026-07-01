# Backup de secretos del agente

Los secretos NO van en git. Pero si no se respaldan aparte, una pérdida de
máquina deja al agente irrecuperable — y **la llave de la wallet perdida = fondos
perdidos**. Este doc es el procedimiento; **no contiene ningún secreto**.

> **Prioridad absoluta:** la llave privada / seed de la wallet de Polygon. Sin
> backup off-machine de eso, no hay recuperación de los fondos. Hacelo YA aunque
> no hagas el resto.

## Inventario — qué respaldar (todo bajo `~/.openclaw/`)

| Archivo | Contiene |
|---|---|
| `~/.openclaw/.env` | API keys, tokens (Telegram/GitHub/LLM), posiblemente la llave de wallet |
| `~/.openclaw/service-env/ai.openclaw.gateway.env` | env del gateway (tokens de servicio) |
| `~/.openclaw/service-env/ai.openclaw.gateway-env-wrapper.sh` | wrapper del gateway |
| `auth-profiles.json` (y `~/.openclaw/backups/auth-profiles.backup.*.json`) | perfiles de auth |
| `~/.openclaw/openclaw.json` (+ `.last-good`) | config principal del runtime |
| `~/.openclaw/identity/device.json` | identidad del dispositivo |

Verificá dónde está realmente la llave de la wallet (puede estar en `.env`, en
`auth-profiles.json`, o en un keystore aparte del SDK de Polymarket). Respaldá
ese archivo explícitamente.

## Método recomendado (archivo cifrado off-machine)

No guardar en texto plano ni en el repo. Cifrar y subir a un lugar seguro
(gestor de contraseñas con adjuntos, o almacenamiento cifrado):

```bash
# 1. Empaquetar los secretos (ajustá rutas según el inventario de arriba)
tar czf openclaw-secrets.tar.gz \
  -C ~ .openclaw/.env \
  .openclaw/service-env \
  .openclaw/openclaw.json .openclaw/openclaw.json.last-good \
  .openclaw/identity/device.json \
  .openclaw/backups

# 2. Cifrar (elegí UNO):
#    age (recomendado): age -p -o openclaw-secrets.tar.gz.age openclaw-secrets.tar.gz
#    gpg:                gpg -c openclaw-secrets.tar.gz
# 3. Borrar el .tar.gz sin cifrar:
rm openclaw-secrets.tar.gz
# 4. Subir openclaw-secrets.tar.gz.age a: gestor de contraseñas / vault / bóveda
#    cifrada off-machine. Guardá la passphrase en un lugar DISTINTO.
```

Adicional: exportar la **seed de la wallet** a papel/metal (backup físico) es la
práctica estándar para fondos que no querés perder.

## Restaurar

```bash
# desde el vault, con la passphrase:
age -d openclaw-secrets.tar.gz.age | tar xzf - -C ~   # (o gpg -d | tar xzf -)
```

Luego seguir `RESTORE.md` desde el paso 3.

## Cadencia

Re-hacer este backup cada vez que cambie un token, se rote una API key, o se
cambie la wallet. Como mínimo, verificarlo trimestralmente restaurándolo en un
directorio de prueba (un backup no verificado no es un backup).
