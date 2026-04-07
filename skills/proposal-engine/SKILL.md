---
name: proposal-engine
description: >
  Create, adapt, and deliver commercial proposals for MIDAS clients. Use when: a new proposal
  request arrives, an existing proposal needs adaptation for a new client/product, a brief needs
  structuring, a deck needs content generation slide-by-slide, or a delivery email needs drafting.
  Triggers on: "propuesta", "proposal", "brief", "deck", "nueva propuesta", "adaptar propuesta".
---

# Proposal Engine

Convert commercial briefs into reusable, consistent proposals fast.

## Workflow

1. **Structure the brief** — Normalize input into standard brief format (see `references/brief-template.md`).
2. **Find reference proposal** — Identify the closest prior proposal as base. Classify similarity: alta / media / baja.
3. **Build delta map** — Determine what stays, what gets rewritten, what gets removed, what's new.
4. **Rewrite narrative** — Adapt the commercial story to the new client/product/objective/audience.
5. **Ground execution** — Define audience, activation, media mix, costs, process/timeline.
6. **Generate deliverables** — Produce deck content, file naming, delivery email, executive summary.

## Output Levels

- **Level 1**: Structured brief + assumptions + gaps detected
- **Level 2**: Deck structure + delta map vs reference proposal
- **Level 3**: Full slide-by-slide copy + costs + process + risk notes
- **Level 4**: File name + delivery email + internal executive summary
- **Level 5**: Editable .pptx if technically feasible

## Brief Format

Read `references/brief-template.md` for the standard input format.

## Rules

- Always start from the real brief, not assumptions.
- Separate facts / inferences / assumptions explicitly.
- Avoid overpromising segmentation capabilities the data doesn't support.
- Reuse before reinventing — prefer adapting existing decks.
- Respect client tone and structure when a reference exists.
- Ask for clarification only if it materially changes the proposal.

## MIDAS Context

MIDAS is a Latin American data marketplace offering 1st party data and identified audiences from recognized brands. Proposals typically include: strategic vision, objectives, audience/universe, segmentation, activation, media mix, costs, process/timeline, and confidentiality closing.

### Common Proposal Structure

1. Portada
2. Índice
3. Visión
4. Objetivos
5. Universo
6. Segmentación
7. Audiencia(s) propuesta(s)
8. Activación recomendada
9. Media Mix
10. Costos
11. Proceso
12. Cierre / confidencialidad

## Integration

After proposal is sent, create/update opportunity in the deal tracker sheet using `deal-tracker-sheets` skill, then `deal-followup` takes over for follow-up management.
