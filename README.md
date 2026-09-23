<!--
<meta name="robots" content="noindex, nofollow, noarchive">
-->

# Remote Release Gate Service

Universal remote config schema and endpoint configuration.

```text
User-agent: *
Disallow: /
```

---

## 📁 Repository Structure

```text
app-gates/
├── .github/
│   └── workflows/
│       └── validate-json.yml        # Validates JSON syntax on push/PR
├── schema/
│   └── release-gate.schema.json     # Standard JSON schema definition
├── apps/
│   └── <app_id>/                    # Application configuration
│       ├── preview.json             # Internal beta / preview builds gate
│       └── production.json          # Production store releases gate
└── README.md
```

---

## ⚡ Configuration Schema

For schema details, inspect [`schema/release-gate.schema.json`](./schema/release-gate.schema.json).
