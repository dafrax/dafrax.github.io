# DAFRAX Tools

Personal tools portal hosted at `https://dafrax.github.io/tools/` with a catalog dashboard.

## Structure

- `index.html` - public dashboard UI.
- `tools.json` - single source of truth for active tools.
- `PocketPilot.html` - pocket allocation and redistribution calculator.
- `financial-freedom-calc.html` - financial freedom calculator.
- `financial-freedom-simulator.html` - goal-based financial freedom simulator.
- `financial-freedom-simulator-master-prompt.md` - simulator implementation specification.

## Local Development

The dashboard loads `tools.json` with `fetch`, so open it through a local static server rather than `file://`:

```bash
python3 -m http.server 8000 --directory tools
```

Open `http://localhost:8000/` to view the dashboard.

## GitHub Pages

Commit changes to the repository `main` branch. GitHub Pages serves the directory at:

`https://dafrax.github.io/tools/`

All catalog URLs are relative to `/tools/`, so the existing tool URLs remain unchanged.

## Security Limitation

This dashboard is public because GitHub Pages is static hosting. It does not provide authentication or access control. Do not place private data, credentials, tokens, or API keys in this repository. Favorites, theme, and recently used tools use `localStorage` only for browser preferences and are not security controls. For genuinely private tools, serve them from a private origin protected by Tailscale, Cloudflare Access, or a server-side authentication layer.

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
