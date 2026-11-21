# DAFRAX Tools

Personal tools portal hosted at `https://dafrax.github.io/tools/` with a client-side session gate and catalog dashboard.

## Structure

- `index.html` - login gate and dashboard UI.
- `tools.json` - single source of truth for active tools.
- `PocketPilot.html` - pocket allocation and redistribution calculator.
- `financial-freedom-calc.html` - financial freedom calculator.

## Local Development

The dashboard loads `tools.json` with `fetch`, so open it through a local static server rather than `file://`:

```bash
python3 -m http.server 8000 --directory tools
```

Open `http://localhost:8000/` and use the demo password `DAFRAX-DEMO`.

## GitHub Pages

Commit changes to the repository `main` branch. GitHub Pages serves the directory at:

`https://dafrax.github.io/tools/`

All catalog URLs are relative to `/tools/`, so the existing tool URLs remain unchanged.

## Security Limitation

This portal uses a client-side password gate because GitHub Pages is static hosting. The demo password is present in publicly downloadable JavaScript and is not a secret. The gate only discourages casual visitors; it is not genuine authentication or access control. Do not place private data, credentials, tokens, or API keys in this repository. Authentication state uses `sessionStorage` and ends with the browser session; favorites, theme, and recently used tools use `localStorage` and are not security controls.

## Add a Tool

Add an object to `tools.json`:

```json
{
  "id": "unique-tool-id",
  "name": "Tool Name",
  "description": "Short description.",
  "category": "Developer",
  "url": "./tool.html",
  "icon": "code",
  "tags": ["developer", "utility"],
  "status": "active"
}
```

Use one of the supported categories: `Network`, `Developer`, `Security`, `Utilities`, `Productivity`, or `Other`. Set `status` to `inactive` to hide a tool without deleting its metadata. Keep IDs unique and verify the relative URL manually.

## Favorites and Recent Tools

Favorites and recent tool IDs are stored in the visitor's browser using `localStorage`. Favorites are filtered against the current catalog, and recently used tools are limited to the latest ten entries. Clearing browser storage clears these preferences.
