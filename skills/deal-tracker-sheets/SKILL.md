---
name: deal-tracker-sheets
description: >
  Operate the MIDAS commercial pipeline Google Sheet — create/update opportunities, validate
  structure, prepare payloads for n8n workflows, and manage the deal tracker. Use when: creating
  a new opportunity row, updating deal status, preparing webhook payloads, validating sheet
  structure, or designing n8n automation for the pipeline sheet. Triggers on: "tracker", "sheet",
  "pipeline sheet", "actualizar oportunidad", "nueva oportunidad", "n8n workflow".
---

# Deal Tracker Sheets

Operate the Google Sheet that powers the MIDAS commercial pipeline.

## Sheet Info

- **Name**: 🦞 Musk - Proposal Engine Sheet - 2026
- **URL**: https://docs.google.com/spreadsheets/d/1yAkR3u7VLiOmJASEj7norb2wP46lC1kv2oP-Jjpk0j0/edit
- **Tabs**: Opportunities, Stage Rules, Message Templates

## Schema

Read `references/sheet-schema.md` for full column definitions, formulas, dropdowns, and formatting rules.

## n8n Workflows

Read `references/n8n-workflow-v1.md` for the 3 workflow designs:
1. PE - Create or Update Opportunity (webhook upsert)
2. PE - Daily Follow-up Digest (cron → Gmail draft)
3. PE - Draft Follow-up by Opportunity (webhook → Gmail draft)

## Payload Examples

Read `references/row-payload-examples.json` for sample webhook payloads.

## Operations

### Create Opportunity
1. Validate required fields: Opportunity ID, Client, Proposal Name, Current Stage.
2. Build payload from brief/proposal data.
3. Send to n8n webhook or append directly.

### Update Opportunity
1. Lookup by Opportunity ID.
2. Update only changed fields.
3. Always update `Updated At`.

### Read Pipeline Status
1. Read all active rows (exclude Ganada/Perdida/Congelada).
2. Flag overdue follow-ups (Next Follow-up Date < today).
3. Sort by Priority → Temperature → Follow-up date.

## Opportunity ID Format

`XX-YYYY-NNN` where:
- XX = client abbreviation (e.g., SB = Seguros Bolívar)
- YYYY = year
- NNN = sequential number

## Rules

- Never write to formula columns (Days Since Last Contact, Follow-up Status).
- Always validate required fields before creating rows.
- Use exact dropdown values for stage/temperature/priority/channel.
