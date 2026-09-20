# App Gates (Universal Remote Config & Kill-Switch System)

A lightweight, app-independent repository for managing remote kill-switches, minimum build version enforcers, and maintenance notices across mobile applications.

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
│   ├── geocam/                      # GeoCam configuration
│   │   ├── preview.json             # Internal beta / preview builds gate
│   │   └── production.json          # Production store releases gate
│   └── <future-app>/                # Add other mobile apps here
└── README.md
```

---

## 🌐 Raw URLs for Apps

Each app fetches its remote gate via GitHub's raw CDN:

### GeoCam (Preview / Beta):
```text
https://raw.githubusercontent.com/<YOUR_USERNAME>/app-gates/main/apps/geocam/preview.json
```

### GeoCam (Production):
```text
https://raw.githubusercontent.com/<YOUR_USERNAME>/app-gates/main/apps/geocam/production.json
```

---

## ⚡ How to Trigger Actions

### 1. Kill-Switch (Lock Down All Active Builds Immediately):
In `apps/<app_slug>/preview.json`:
```json
"killSwitch": {
  "enabled": true,
  "title": "Emergency Recall",
  "message": "This test build has been recalled. Please download the latest APK."
}
```

### 2. Minimum Build Enforcer (Require Update to Build 10+):
```json
"minBuild": {
  "enforced": true,
  "minAllowedBuildNumber": 10,
  "message": "Build 10 or newer is required to continue testing."
}
```

### 3. Revoke a Specific Leaked / Broken Build:
```json
"revokedBuilds": [
  "1.0.0_b2",
  "1.0.0_b4"
]
```

---

## 🛡️ Fast-Cache Bypass
GitHub Raw files are cached by Fastly CDN for ~300 seconds (5 minutes). For instantaneous emergency overrides, client apps append a timestamp parameter:
```text
https://raw.githubusercontent.com/.../preview.json?t=1726829400000
```
