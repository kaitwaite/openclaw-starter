# TOOLS.md — Technical Reference

_Resource IDs, endpoints, scripts, and configuration. Update this when anything changes._

---

## Google Authentication
- Token path: ~/.openclaw/workspace-[name]/google_token.json
- Scopes: [list the scopes your agent needs]

---

## Google Calendars

| Calendar | ID | Access |
|----------|----|--------|
| [Calendar name] | [calendar ID] | Read + Write |
| [Calendar name] | [calendar ID] | Read only |

---

## Google Docs and Sheets

| Resource | ID | Purpose |
|----------|----|---------|
| [Doc name] | [doc ID] | [what it's for] |

---

## Email

| Field | Value |
|-------|-------|
| Send from | [agent email] |
| CC on every email | [your email] |
| Identity | Always sign as [agent name], never impersonate [your user] |

---

## Contacts

| Person | Email | Notes |
|--------|-------|-------|
| [Your user] | [email] | Primary |

---

## Weather API
Source: Open-Meteo (no API key required)
Location: [your city] · lat [latitude] · lon [longitude]

```
curl "https://api.open-meteo.com/v1/forecast?latitude=[LAT]&longitude=[LON]&daily=temperature_2m_max,temperature_2m_min,precipitation_sum,weathercode&temperature_unit=fahrenheit&timezone=[YOUR_TIMEZONE]&forecast_days=2"
```

---

## Scripts

| Script | Purpose |
|--------|---------|
| scripts/google_auth.py | Authenticate Google Workspace |
| scripts/test_google.py | Verify Google API connectivity |

---

## Telegram

| Field | Value |
|-------|-------|
| Bot token | [from BotFather — never commit this] |
| Chat ID | [your chat ID] |
| Primary user handle | [@yourusername] |
