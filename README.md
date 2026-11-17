# Fudgett

Fudgett is a mobile-first recipe cost calculator: the user enters ingredients and quantities, and the app calculates the proportional cost of the quantities actually used, plus cost per serving.

## Current implementation

- Recipe calculator with g, kg, ml, l and pieces.
- Proportional cost calculation from package price and package size.
- Partial totals when some ingredient prices are missing; missing prices are never invented.
- CSV catalog import with fields: `ingredient,store,price,pack_qty,unit`; optional `updated_at,url`.
- Saved recipes with edit and delete actions.
- Pantry inventory with quantities and optional expiry dates.
- Local data persistence in browser storage.
- Full JSON backup export and restore.
- PWA manifest and service worker for previously visited pages / offline shell.
- Responsive layout, including compact mobile navigation.
- Basic privacy, terms and offline information pages.

## Important launch limitations

1. **No live supermarket catalog integration is active.** The app does not scrape supermarket websites or claim live prices. Prices are used only after a CSV catalog is imported.
2. **No cloud account or cross-device sync is configured.** Data is saved on the current browser/device. Users should export a JSON backup. Clearing browser data or switching device can otherwise lose local data.
3. The privacy and terms pages are starter drafts, not final legal advice. Add the controller's legal details and have the documents reviewed before public commercial launch.
4. The app currently uses external Google Fonts and Font Awesome CDN assets. A production hardening pass should self-host assets and add a Content Security Policy.
5. GitHub Pages is static hosting. A backend (e.g. Supabase) is needed for accounts, cloud sync, shared data, server-side catalog updates, rate limiting and stronger operational security.

## CSV catalog format

Example header:

```csv
ingredient,store,price,pack_qty,unit,updated_at,url
```

- `price`: price of the whole package in EUR.
- `pack_qty`: quantity contained in that package.
- `unit`: `g`, `kg`, `ml`, `l` or `pz`.
- `updated_at`: ISO date or timestamp.
- `url`: optional source page.

Example: a 500 g pasta package priced at €1.49 is stored as `Pasta,Coop,1.49,500,g,2026-11-17,`.

## Hosting

The site is configured for GitHub Pages under the repository subpath. The service worker uses relative paths so it can run under `/fudget/`.
