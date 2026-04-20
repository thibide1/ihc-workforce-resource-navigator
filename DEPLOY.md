# Workforce Resource Navigator — Deployment Guide

**Track A static app.** Self-contained. Zero backend. Drop into any static host.

---

## What's in the deploy bundle

```
workforce-resource-navigator/
├── index.html              ← landing page (tools.json inlined)
├── alpine.min.js           ← vendored Alpine.js (no CDN dependency)
├── tools.json              ← canonical tool registry (edit here, re-inline)
├── assets/css/
│   ├── tokens-shared.css   ← IHC Design System v2 shared tokens
│   └── tokens-ihc-2026.css ← IHC 2026 brand tokens
├── tools/
│   └── re-entry-storytelling/
│       ├── index.html      ← Re-Entry Storytelling beta app
│       ├── alpine.min.js   ← Alpine vendored for the beta
│       └── docs/
│           └── From-Paper-to-Pathway-v1.pdf  ← white paper (learn-more link)
├── README.md
└── DEPLOY.md               ← this file
```

All paths inside the bundle are **relative**. The app works at any URL prefix. Drop the folder anywhere.

---

## Deploy path 1 — WordPress File Manager (canonical Track A path)

Per CLAUDE.md Web App Foundation §Track A. Recommended for `investhamiltoncounty.com`.

```bash
# From the repo root:
cd hamilton-implementation/apps
zip -r workforce-resource-navigator.zip workforce-resource-navigator \
    -x "workforce-resource-navigator/DEPLOY.md" \
       "workforce-resource-navigator/README.md"
```

1. Log into WordPress admin
2. Go to **File Manager** (WP File Manager plugin)
3. Navigate to `/wp-content/uploads/apps/`
4. Upload `workforce-resource-navigator.zip`
5. Extract in place → creates `/wp-content/uploads/apps/workforce-resource-navigator/`
6. Access at:
   **`https://investhamiltoncounty.com/wp-content/uploads/apps/workforce-resource-navigator/`**
7. (Optional) Add WordPress rewrite rule for a clean URL like `/tools/` or `/navigator/`:
   ```apache
   # .htaccess addition
   RewriteRule ^navigator/?$ /wp-content/uploads/apps/workforce-resource-navigator/ [L]
   RewriteRule ^navigator/(.*)$ /wp-content/uploads/apps/workforce-resource-navigator/$1 [L]
   ```

---

## Deploy path 2 — Render static site (zero-config)

Faster to stand up than WordPress. Good for testing at a non-production URL first.

1. Create a new Git repo containing just this folder (or push this folder to an existing repo)
2. In Render dashboard: **New → Static Site**
3. Connect the repo
4. Build command: (leave empty)
5. Publish directory: `hamilton-implementation/apps/workforce-resource-navigator`
6. Deploy
7. Render gives you a URL like `wrn-ihc.onrender.com` (free tier) — share with Mike

`render.yaml` example (commit this at repo root if you go this route):
```yaml
services:
  - type: web
    name: workforce-resource-navigator
    runtime: static
    buildCommand: ""
    staticPublishPath: ./hamilton-implementation/apps/workforce-resource-navigator
    headers:
      - path: /*
        name: X-Frame-Options
        value: SAMEORIGIN
      - path: /*
        name: X-Content-Type-Options
        value: nosniff
      - path: /*
        name: Referrer-Policy
        value: strict-origin-when-cross-origin
```

---

## Deploy path 3 — Any static host

Works identically on Netlify, Vercel, Cloudflare Pages, GitHub Pages, or a plain nginx directory. The bundle has no build step, no server requirements, no environment variables.

**Drag-and-drop (Netlify):**
1. https://app.netlify.com/drop
2. Drag the `workforce-resource-navigator` folder onto the drop zone
3. Done — Netlify gives you a live URL

---

## After deploy — verification checklist

Open the deployed URL and confirm:
- [ ] Header renders with purple→blue gradient + "Workforce Resource Navigator" title
- [ ] Category chips appear and filter the tool grid (click them)
- [ ] "From Paper to Pathway" card shows with the "New" badge and "Open tool" button
- [ ] Three placeholder tools show with "Coming soon" badges
- [ ] Click "Open tool" on Re-Entry — the intake beta loads in the same browser tab
- [ ] Click "Read more" on Re-Entry — the white paper PDF opens
- [ ] Crisis bar appears at the bottom with 988, 211, ILS numbers
- [ ] Mobile responsive (resize browser or open on phone)
- [ ] No browser console errors (F12 → Console)

If Alpine doesn't initialize, you'll see a blank main area and `x-cloak` holding. That would mean `alpine.min.js` didn't load — verify the file is at the expected path after upload.

---

## After deploy — headers & privacy

Track A static apps don't run server code, but every hosting platform lets you set response headers. Recommended set (Track A privacy floor per CLAUDE.md Web App Foundation):

```
X-Frame-Options: SAMEORIGIN
X-Content-Type-Options: nosniff
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: camera=(), microphone=(), geolocation=(), interest-cohort=()
Strict-Transport-Security: max-age=31536000; includeSubDomains
Content-Security-Policy: default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline' https://fonts.googleapis.com; font-src 'self' https://fonts.gstatic.com
```

(The `'unsafe-inline'` is required for Alpine.js attribute processing; it's the standard Alpine CSP.)

WordPress: set via a security-headers plugin or `.htaccess`.
Render: set via `render.yaml` (shown above).
Netlify/Vercel: set via `_headers` file or `vercel.json`.

---

## Updating after deploy

**To add a new tool:**
1. Edit `tools.json` in this folder (local)
2. Re-inline tools.json into index.html:
   ```bash
   cd hamilton-implementation/apps/workforce-resource-navigator
   python3 <<'PY'
   import json
   data = json.load(open('tools.json'))
   tools_json = json.dumps(data, ensure_ascii=False)
   html = open('index.html').read()
   start = html.find('const DATA = {')
   depth = 0
   i = start + len('const DATA = ')
   while i < len(html):
       if html[i] == '{': depth += 1
       elif html[i] == '}':
           depth -= 1
           if depth == 0:
               end = i + 2  # include '};'
               break
       i += 1
   open('index.html', 'w').write(html[:start] + 'const DATA = ' + tools_json + ';' + html[end:])
   PY
   ```
3. Re-zip
4. Re-upload (overwrite in place)

**To update the Re-Entry beta** (e.g., question wording changes):
1. Edit `tools/re-entry-storytelling/index.html`
2. Re-zip + re-upload that subfolder only

---

## What to tell stakeholders

This is a **consumer-facing landing page**. It is:
- Free to use for anyone
- On-device for tools that collect data (no server storage)
- Privacy-forward (no tracking, no cookies, no account)
- Always labeled as general information, not legal advice

It is **not**:
- An IHC program management tool
- A replacement for facilitated Re-Entry Storytelling sessions
- A medical, legal, or clinical service

The full Track B production Re-Entry Storytelling platform (per Components 04–14) is a separate deployment — this landing page references the self-serve beta track of Re-Entry as one of many future consumer tools.

---

**Deploy question or issue?** Reference `hamilton-implementation/apps/workforce-resource-navigator/README.md` or contact Mike.
