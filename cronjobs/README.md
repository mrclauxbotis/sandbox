# Cron Jobs

This folder stores cron job definitions used by OpenClaw.

## Active job: USD -> COP

Definition file:
- `usd_cop_every_2h_8am_4pm_cot.job.json`

Schedule:
- Every 2 hours from 8:00 to 16:00 (COT / America/Bogota)
- Cron expression: `0 8-16/2 * * *`

## Re-create command

From OpenClaw, create this job with:

```json
{
  "action": "add",
  "job": {
    "name": "USD/COP cada 2h (8am-4pm COT)",
    "schedule": { "kind": "cron", "expr": "0 8-16/2 * * *", "tz": "America/Bogota" },
    "sessionTarget": "isolated",
    "payload": {
      "kind": "agentTurn",
      "message": "Consulta el tipo de cambio USD a COP usando https://open.er-api.com/v6/latest/USD y toma rates.COP. Responde SOLO en este formato exacto: USD -> COP: <valor en COP>"
    },
    "delivery": { "mode": "announce", "channel": "telegram", "to": "1497039310" },
    "enabled": true
  }
}
```
