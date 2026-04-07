# n8n Workflows v1 — Deal Tracker

## n8n Instance

- URL: https://m1das.app.n8n.cloud
- Existing Workflow N.1: https://m1das.app.n8n.cloud/workflow/rMyurCfEagq1B2Dr
- Existing Workflow N.2: https://m1das.app.n8n.cloud/workflow/nMEYKgO7wfLXgYS3

## Workflow 1: PE - Create or Update Opportunity

**Trigger**: Webhook POST → `proposal-engine/opportunity-upsert`

### Nodes

1. **Webhook - Opportunity Payload** (POST, path: `proposal-engine/opportunity-upsert`, auth: None, respond via Respond node)
2. **Lookup - Opportunity ID** (Google Sheets → Opportunities tab → lookup by Opportunity ID column)
3. **If - Row Exists** (check if lookup returned a row)
4. **Update - Existing Opportunity** (Google Sheets → update row using rowNumber from lookup)
5. **Append - New Opportunity** (Google Sheets → append new row)
6. **Respond - Upsert Result** (return `{"status": "created"|"updated"}`)

### Flow

```
Webhook → Lookup → IF
  ├─ TRUE  → Update → Respond
  └─ FALSE → Append → Respond
```

### Required Fields for Creation

- Opportunity ID
- Client
- Proposal Name
- Current Stage

### Do NOT Write

- Days Since Last Contact (formula)
- Follow-up Status (formula)

---

## Workflow 2: PE - Daily Follow-up Digest

**Trigger**: Cron daily 8:00 AM (weekdays)

### Nodes

1. **Cron** (8:00 AM daily)
2. **Read - Opportunities** (Google Sheets → read all rows from Opportunities)
3. **Filter - Due Followups** (Code node → filter Vencido/Vence hoy, exclude Ganada/Perdida/Congelada, sort by Priority → Temperature)
4. **If - Anything To Draft** (check count > 0)
5. **Gmail - Draft Digest** (create draft with subject: `Deal Follow-up Digest - {date}`, body: formatted list)

### Filter Code

```javascript
const rows = $input.all().map(i => i.json);
const filtered = rows.filter(r => {
  const status = (r["Follow-up Status"] || "").trim();
  const stage = (r["Current Stage"] || "").trim();
  return (
    (status === "Vencido" || status === "Vence hoy") &&
    !["Ganada", "Perdida", "Congelada"].includes(stage)
  );
});
const priorityRank = { "Alta": 1, "Media": 2, "Baja": 3 };
const tempRank = { "Caliente": 1, "Tibia": 2, "Fría": 3, "Congelada": 4 };
filtered.sort((a, b) => {
  const pa = priorityRank[a["Priority"]] || 99;
  const pb = priorityRank[b["Priority"]] || 99;
  if (pa !== pb) return pa - pb;
  const ta = tempRank[a["Temperature"]] || 99;
  const tb = tempRank[b["Temperature"]] || 99;
  return ta - tb;
});
const lines = filtered.map((r, idx) =>
  `${idx + 1}) ${r["Client"]} — ${r["Proposal Name"]}\n   Stage: ${r["Current Stage"]}\n   Priority: ${r["Priority"]}\n   Status: ${r["Follow-up Status"]}\n   Next action: ${r["Next Recommended Action"]}`
);
const body = filtered.length
  ? `Deal Follow-up Digest\n\n${lines.join("\n\n")}`
  : `Deal Follow-up Digest\n\nNo hay follow-ups vencidos ni para hoy.`;
return [{ json: { count: filtered.length, body } }];
```

---

## Workflow 3: PE - Draft Follow-up by Opportunity

**Trigger**: Webhook POST → `proposal-engine/draft-followup`

### Nodes

1. **Webhook - Draft Followup** (POST, path: `proposal-engine/draft-followup`)
2. **Lookup - Opportunity** (Google Sheets → Opportunities → by Opportunity ID)
3. **Read - Templates** (Google Sheets → Message Templates → all rows)
4. **Build - Draft Followup** (Code node → match template by stage/tone/channel, replace {{name}})
5. **Gmail - Create Draft** (to: contact email, subject: `Seguimiento propuesta - {client} - {proposal}`, body: from step 4)
6. **Respond to Webhook** (`{"status": "draft_created"}`)

### Build Code

```javascript
const items = $input.all();
const opportunity = items[0].json;
const templates = items.slice(1).map(i => i.json);
const stage = opportunity["Current Stage"] || "";
const channel = opportunity["Send Channel"] || "Email";
let tone = "Suave";
if (stage === "Follow-up 1") tone = "Directo";
if (stage === "Follow-up 2") tone = "Ejecutivo";
const template = templates.find(t =>
  t["Stage"] === stage && t["Tone"] === tone && t["Channel"] === "Email"
) || templates[0];
let message = template?.["Template"] || "";
message = message.replace("{{name}}", opportunity["Main Contact"] || "equipo");
return [{
  json: {
    to: opportunity["Contact Email"] || "",
    subject: `Seguimiento propuesta - ${opportunity["Client"]} - ${opportunity["Proposal Name"]}`,
    body: message,
    opportunityId: opportunity["Opportunity ID"]
  }
}];
```
