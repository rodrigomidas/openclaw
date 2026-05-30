# MEMORY.md — Musk 🦞

Last updated: 2026-04-07

## Who I Am
- **Name**: Musk
- **Role**: Copiloto estratégico y operativo de Rodrigo en MIDAS
- **Emoji**: 🦞
- **Model anterior**: gpt-5.4 → ahora claude-opus-4-6
- **Idioma por defecto**: español

## Who Rodrigo Is
- Rodrigo Reyes — fundador/CEO de MIDAS
- MIDAS: empresa de datos y audiencias en Colombia (mercado latam de 1st party data)
- Gmail/Workspace: rodrigo@m1das.media
- Telegram ID: <CONFIGURAR_LOCALMENTE>
- Timezone: America/Bogota (pero host está en America/New_York)

## Skills Instalados
1. **proposal-engine** — brief → propuesta comercial slide-by-slide
2. **deal-followup** — seguimiento de propuestas enviadas, pipeline de 10 etapas
3. **deal-tracker-sheets** — opera el Google Sheet del pipeline + workflows n8n

## Google Sheet del Pipeline
- Nombre: 🦞 Musk - Proposal Engine Sheet - 2026
- URL: https://docs.google.com/spreadsheets/d/1yAkR3u7VLiOmJASEj7norb2wP46lC1kv2oP-Jjpk0j0/edit
- Tabs: Opportunities, Stage Rules, Message Templates
- 26 columnas definidas (ver skill deal-tracker-sheets)

## n8n
- Instancia: https://m1das.app.n8n.cloud
- Workflow N.1: https://m1das.app.n8n.cloud/workflow/rMyurCfEagq1B2Dr
- Workflow N.2: https://m1das.app.n8n.cloud/workflow/nMEYKgO7wfLXgYS3
- 3 workflows diseñados pendientes de implementar:
  1. PE - Create or Update Opportunity (webhook upsert)
  2. PE - Daily Follow-up Digest (cron → Gmail draft)
  3. PE - Draft Follow-up by Opportunity (webhook → Gmail draft)
- Estado: Rodrigo estaba configurando Workflow 1 nodo por nodo (quedó en el nodo Google Sheets después del Webhook)

## Pipeline Stages Aprobados
1. Brief recibido → 2. Propuesta en preparación → 3. Propuesta enviada → 4. Follow-up 1 → 5. Follow-up 2 → 6. Reunión agendada → 7. En negociación / ajustes → 8. Ganada → 9. Perdida → 10. Congelada

## Caso Real: Seguros Bolívar — Póliza de Movilidad
- Producto: seguro vehicular (Póliza de Movilidad)
- Audiencia: URBEX, 35-55 años, capacidad media-alta
- Canal: Meta remarketing (Custom Audience)
- Budget: COP $3MM/mes, $980/match = ~3,061 usuarios
- Landing: https://digital.experienciasbolivar.segurosbolivar.com/seguro-para-carros
- Se creó un .pptx editado (puede haberse perdido en el wipe)
- Propuesta previa de referencia: Unidrogas + RappiPay

## Integraciones Pendientes
- Google Drive: no conectado
- Gmail: investigado, faltan dependencias (gcloud, tailscale, gogcli) — ruta: openclaw webhooks gmail setup
- n8n ↔ Google Sheets: en proceso de conexión

## Auditoría de Seguridad (19 mar 2026)
- macOS 13.7.8, FileVault ON, firewall habilitado
- OpenClaw 2026.3.13, gateway loopback only
- 0 critical, 2 warnings menores

## Lecciones
- 2026-04-07: Se perdió todo el workspace (skills, memoria, identidad). Se reconstruyó desde conversación exportada de Telegram. **Siempre mantener backup externo (git remote).**

## Preferencias de Rodrigo
- Le gusta ir directo y rápido
- Prefiere opciones numeradas para decidir
- Quiere poder recibir archivos en otros dispositivos (Drive + Telegram)
- Tono comercial: balanceado
- No CRM pesado — Google Sheets es suficiente por ahora
