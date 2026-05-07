# AI × Journalism Summit 2026 — Mini App

A simple single-page app to help navigate the Hacks/Hackers AI x Journalism Summit (May 13–14, Baltimore).

## Features

- **Browse all 45 sessions** organized by day and time slot
- **Filter by track**: Preview / Play / Adopt / Govern (color-coded)
- **Search** across titles, descriptions, and speakers
- **Star sessions** to build your personal schedule (saved in browser localStorage)
- **Conflict detection**: starred sessions in the same time slot are flagged in red
- **Export your picks**:
  - Copy as text (for pasting into notes)
  - Download as `.ics` (import to Google Calendar / Apple Calendar)
- Click any session card to expand full description and speaker bios

## Files

- `index.html` — the whole app (HTML + CSS + JS in one file)
- `sessions.json` — session data, easy to edit if the program updates

## Deploy to GitHub Pages

```bash
cd ~/projects   # or wherever
mkdir hh-summit-2026 && cd hh-summit-2026
# copy index.html and sessions.json into this folder
git init
git add .
git commit -m "Initial summit app"
gh repo create hh-summit-2026 --public --source=. --push
# Then enable Pages: Settings -> Pages -> deploy from main / root
```

Or just drag the folder into a new repo on GitHub.com and turn on Pages.

## Local preview

Because `index.html` fetches `sessions.json`, you need a tiny local server (file:// won't work due to CORS):

```bash
cd hh-summit-2026
python3 -m http.server 8000
# open http://localhost:8000
```

## Updating the program

When the official program changes, edit `sessions.json`. Each entry needs:

```json
{
  "id": "unique-string",
  "day": "Wed May 13" | "Thu May 14",
  "dayNum": 1 | 2,
  "time": "HH:MM–HH:MM",
  "track": "Preview" | "Play" | "Adopt" | "Govern" | "Plenary",
  "title": "...",
  "description": "...",
  "speakers": [{"name": "...", "role": "..."}]
}
```

`Plenary` is for non-session items (welcome, lunch, reception). They appear muted and can't be starred.

## Notes

- Stars persist via `localStorage`, so they survive page reloads but are per-browser/per-device.
- The .ics export assumes EDT (UTC-4) for May in Baltimore.
- If you open `index.html` directly via `file://` and the sessions don't load, use the local server above.
