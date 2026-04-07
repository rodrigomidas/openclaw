# Sheet Schema — Deal Tracker

## Tab: Opportunities

### Columns (in order)

| # | Column | Type | Dropdown? | Formula? |
|---|--------|------|-----------|----------|
| 1 | Opportunity ID | Text | No | No |
| 2 | Client | Text | No | No |
| 3 | Main Contact | Text | No | No |
| 4 | Contact Email | Text | No | No |
| 5 | Contact WhatsApp | Text | No | No |
| 6 | Proposal Name | Text | No | No |
| 7 | Proposal Link | URL | No | No |
| 8 | Source Proposal Used | Text | No | No |
| 9 | Brief Date | Date | No | No |
| 10 | Proposal Sent Date | Date | No | No |
| 11 | Send Channel | Text | Yes | No |
| 12 | Current Stage | Text | Yes | No |
| 13 | Temperature | Text | Yes | No |
| 14 | Budget | Number | No | No |
| 15 | Expected Value | Number | No | No |
| 16 | Last Contact Date | Date | No | No |
| 17 | Last Contact Summary | Text | No | No |
| 18 | Next Follow-up Date | Date | No | No |
| 19 | Next Recommended Action | Text | Yes | No |
| 20 | Expected Next Step | Text | No | No |
| 21 | Objections / Risks | Text | No | No |
| 22 | Priority | Text | Yes | No |
| 23 | Days Since Last Contact | Number | No | Yes |
| 24 | Follow-up Status | Text | No | Yes |
| 25 | Updated At | Date | No | No |
| 26 | Notes | Text | No | No |

### Dropdown Values

**Send Channel**: Email, WhatsApp, Email + WhatsApp, Reunión, Otro

**Current Stage**: Brief recibido, Propuesta en preparación, Propuesta enviada, Follow-up 1, Follow-up 2, Reunión agendada, En negociación / ajustes, Ganada, Perdida, Congelada

**Temperature**: Caliente, Tibia, Fría, Congelada

**Next Recommended Action**: Esperar, Enviar follow-up 1, Enviar follow-up 2, Proponer reunión, Revisar propuesta, Reenviar propuesta, Cerrar loop, Marcar como perdida, Mantener en pausa

**Priority**: Alta, Media, Baja

### Formulas

**Days Since Last Contact** (col 23, e.g. W2):
```
=IF(P2="","",TODAY()-P2)
```

**Follow-up Status** (col 24, e.g. X2):
```
=IF(OR(L2="Ganada",L2="Perdida",L2="Congelada"),"Cerrado",
IF(R2="","Esperando respuesta",
IF(R2<TODAY(),"Vencido",
IF(R2=TODAY(),"Vence hoy","Al día"))))
```

### Conditional Formatting

| Condition | Color |
|---|---|
| Follow-up Status = Vencido | Red |
| Follow-up Status = Vence hoy | Orange |
| Follow-up Status = Al día | Green |
| Follow-up Status = Cerrado | Gray |
| Temperature = Caliente | Red/Orange |
| Temperature = Tibia | Yellow |
| Temperature = Fría | Light blue |
| Temperature = Congelada | Gray |
| Priority = Alta | Red |
| Priority = Media | Yellow |
| Priority = Baja | Green/Gray |

## Tab: Stage Rules

| Stage | Default Next Action | Default Delay (days) | Suggested Tone | Notes |
|---|---|---|---|---|
| Brief recibido | Preparar propuesta | 0 | Ejecutivo | mover rápido |
| Propuesta en preparación | Enviar propuesta | 0 | Ejecutivo | cerrar versión |
| Propuesta enviada | Enviar follow-up 1 | 4 | Suave | si no responden |
| Follow-up 1 | Enviar follow-up 2 | 5 | Directo | subir claridad |
| Follow-up 2 | Cerrar loop | 5 | Ejecutivo | no perseguir demasiado |
| Reunión agendada | Esperar reunión | 0 | Ejecutivo | preparar brief |
| En negociación / ajustes | Revisar propuesta | 3 | Directo | avanzar o destrabar |
| Ganada | Cerrar | 0 | — | fuera de seguimiento |
| Perdida | Cerrar | 0 | — | aprendizaje |
| Congelada | Mantener en pausa | 14 | Suave | revisar después |

## Tab: Message Templates

| Template Name | Stage | Tone | Channel | Template |
|---|---|---|---|---|
| FU1 suave email | Propuesta enviada | Suave | Email | Hola {{name}}, te escribo para saber si pudiste revisar la propuesta... |
| FU2 directo email | Follow-up 1 | Directo | Email | Hola {{name}}, retomo la propuesta para entender si vale la pena moverla... |
| FU1 suave whatsapp | Propuesta enviada | Suave | WhatsApp | Hola {{name}}, ¿cómo vas? Quería confirmar si pudiste revisar... |
| Cierre elegante | Follow-up 2 | Ejecutivo | Email | Hola {{name}}, cierro el loop sobre la propuesta que te compartí... |
