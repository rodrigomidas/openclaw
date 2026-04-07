---
name: deal-followup
description: >
  Track commercial proposal status and manage follow-up for MIDAS deals. Use when: a proposal
  was sent and needs follow-up, deciding if it's time for next contact, drafting follow-up messages,
  classifying opportunity temperature, determining next best action, or when a client responds and
  next steps need definition. Triggers on: "follow-up", "seguimiento", "pipeline", "oportunidad",
  "deal status", "qué propuestas están pendientes".
---

# Deal Follow-up

Operate commercial follow-up with discipline. No opportunity dies from neglect.

## Pipeline Stages

1. Brief recibido
2. Propuesta en preparación
3. Propuesta enviada
4. Follow-up 1
5. Follow-up 2
6. Reunión agendada
7. En negociación / ajustes
8. Ganada
9. Perdida
10. Congelada

## Workflow

1. **Read current state** — Determine real pipeline stage of the opportunity.
2. **Measure signal** — Evaluate: days since last contact, response received?, interest shown?, objections?, silence?
3. **Assign temperature** — Caliente / Tibia / Fría / Congelada.
4. **Suggest next action** — Follow-up / Esperar / Reunión / Revisar propuesta / Cerrar oportunidad.
5. **Draft message** — Generate appropriate follow-up by channel, tone, stage, and client relationship.

## Output Levels

- **Level 1**: Recommended status + temperature + urgency
- **Level 2**: Next action + suggested follow-up date + recommended channel
- **Level 3**: Drafted follow-up message + alternative versions by tone (suave / directo / ejecutivo)
- **Level 4**: Strategic recommendation (esperar / insistir / simplificar / agendar / reenviar / cerrar)

## Follow-up Cadence Defaults

| Stage | Default Action | Delay (days) | Tone |
|---|---|---|---|
| Propuesta enviada | Follow-up 1 | 4 | Suave |
| Follow-up 1 | Follow-up 2 | 5 | Directo |
| Follow-up 2 | Cerrar loop | 5 | Ejecutivo |
| En negociación | Revisar propuesta | 3 | Directo |
| Congelada | Revisar | 14 | Suave |

## Message Patterns

Read `references/followup-message-patterns.md` for templates by tone and channel.

## Opportunity Record

Read `references/opportunity-record-template.md` for the standard data model shared with deal-tracker-sheets.

## Rules

- Don't follow up too early if it adds no value.
- Don't let opportunities die from forgetting.
- Prefer brief, concrete, commercial messages.
- Don't sound needy or passive.
- Escalate priority when: several days without response, client showed interest but no next step, timing-sensitive opportunity.

## Integration

Operates on the Google Sheet tracker via `deal-tracker-sheets` skill. After `proposal-engine` sends a proposal, deal-followup takes over.
