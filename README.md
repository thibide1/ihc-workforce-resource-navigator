# Workforce Resource Navigator

**Track A static app** · Invest Hamilton County · 2026

An umbrella app for consumer/resident-facing workforce tools. Each tool is a self-contained module that can be added to or removed from the Navigator without affecting the others.

---

## What's in it (v1)

| Tool | Status | Description |
|------|--------|-------------|
| **From Paper to Pathway** (Re-Entry Storytelling) | Live | Self-serve prep tool for people re-entering the workforce after jail, recovery, or supervision |
| Hamilton County Wage Explorer | Coming soon | Plain-language wages by occupation |
| Training Finder | Coming soon | Credential + funding pathway guide |
| Support Services Directory | Coming soon | Housing · childcare · transportation · legal help |

---

## File structure

```
workforce-resource-navigator/
├── index.html        ← main landing page (self-contained; tools.json inlined)
├── tools.json        ← canonical tool registry (edit here; re-inline for deploy)
├── README.md         ← this file
└── build/            (optional — add per-tool sub-directories as tools ship)
```

---

## Adding a new tool

1. Add an entry to `tools.json` under `tools[]` with required fields:
   - `id` (slug, unique)
   - `name`, `tagline`, `description`
   - `category` (one of the existing category ids; or add a new category)
   - `status` (`live` or `coming-soon`)
   - `audience`, `time_estimate`
   - `what_you_get` (array of strings)
   - `launch_path` (relative URL to the tool's entry point) — required if status is `live`
   - `icon` (emoji), `brand_color`, `badge` (optional)
2. Re-inline `tools.json` into `index.html` (see "Build / Deploy" below).
3. Ship.

Category examples already defined: `reentry`, `job-search`, `training`, `support`. Add more by editing `tools.json → categories[]`.

---

## Build / Deploy

### Local preview
Just open `index.html` in any browser. The `tools.json` is inlined, so it works via `file://` without CORS issues.

### Production (WordPress File Manager)
Per CLAUDE.md Track A deployment pattern:
1. Zip the contents of this folder (everything except README.md)
2. Upload to `/wp-content/uploads/apps/workforce-resource-navigator/`
3. Access at `investhamiltoncounty.com/wp-content/uploads/apps/workforce-resource-navigator/`
4. Optionally: set up WordPress rewrite rule for a cleaner URL

### Re-inlining tools.json after edits
```bash
cd hamilton-implementation/apps/workforce-resource-navigator
python3 -c "
import json
tools_json = json.dumps(json.load(open('tools.json')))
html = open('index.html').read()
# Find the existing 'const DATA = {...};' line and replace its value
import re
html = re.sub(r'const DATA = \{.*?\};', 'const DATA = ' + tools_json + ';', html, count=1, flags=re.DOTALL)
open('index.html', 'w').write(html)
"
```

---

## Privacy posture

- No cookies
- No third-party analytics (no GA, no Pixel)
- No account creation
- Each tool handles its own data per that tool's privacy policy
- This landing page itself holds zero user data

## Brand compliance

- Uses Design System v2 tokens (loaded via `../../../alex-core/design-system/v2/css/`)
- IHC 2026 brand colors only
- Montserrat + Lora fonts (Google Fonts, self-hosted option for production)
- WCAG 2.2 AA target
- Mobile-responsive

---

## Related

- Re-Entry Storytelling program: `hamilton-implementation/programs/re-entry-workforce/`
- Existing beta app this links to: `hamilton-implementation/programs/re-entry-workforce/intake-instrument/app/index.html`
- Alex Suite (the platform this is a peer of): `hamilton-implementation/dashboards/economic-impact/`
- IHC Design System v2: `alex-core/design-system/v2/`
