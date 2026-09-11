# Monday Men's League — Season Recaps

Single-page season recaps for the Monday Men's League at Newton Commonwealth Golf Course. One folder per season, published as static files on Cloudflare Workers.

- **Live site:** https://golf-league-recaps.jdgprojects.dev
- **2026 recap:** https://golf-league-recaps.jdgprojects.dev/2026
- **GitHub account:** jdg0928
- **Local path:** `~/repos/personal/p-golf-league-recap`

---

## Repository structure

```
p-golf-league-recap/
├── .gitignore
├── README.md
├── wrangler.jsonc          Cloudflare config. Points at ./public
├── source/                 Drafts and full-size artwork. Tracked, not published
│   ├── 2026-season-recap.md
│   ├── 2026-season-notes.md
│   └── (original header and OG PNGs)
└── public/                 Everything in here is served on the web
    └── 2026/
        ├── index.html      The recap page. Self-contained, no dependencies
        └── og-image-2026.jpg
```

Only `public/` is published. Anything in `source/` stays in version history but is never uploaded to Cloudflare, which keeps deploys small.

Each page is a single self-contained HTML file. Images are embedded as base64, so there are no linked assets to break. The only external request is to Google Fonts.

---

## Hosting

Registrar and DNS are both Cloudflare, so `jdgprojects.dev` is already a zone in the account and no nameserver changes are needed.

| Setting | Value |
|---|---|
| Platform | Cloudflare Workers, static assets |
| Project name | `golf-league-recaps` |
| Build command | (empty) |
| Deploy command | `npx wrangler deploy` |
| Assets directory | `./public` |
| Default URL | `golf-league-recaps.<subdomain>.workers.dev` |
| Custom domain | `golf-league-recaps.jdgprojects.dev` |

The `name` in `wrangler.jsonc` must match the project name in the Cloudflare dashboard.

Pushing to `main` triggers a rebuild automatically. There is no build step; Cloudflare uploads `public/` as-is.

**Why paths, not subdomains.** Seasons live at `/2026`, `/2027`, and so on rather than at `recap-2026.jdgprojects.dev`. One project, one DNS record, one certificate, and old seasons never break. A per-year subdomain would mean a new Worker and new DNS entry every August.

---

## Publishing a new season

1. Copy `public/2026` to `public/<year>`.
2. Replace `index.html` with the new page.
3. Replace the OG image and rename it to `og-image-<year>.jpg`. Keep the year in the filename. If the reference breaks, it fails loudly; a generic name would silently serve last year's artwork.
4. Update the `og:` and `twitter:` meta tags in the new `index.html`, including `og:url`.
5. Commit and push. Cloudflare redeploys on its own.
6. Re-scrape the URL in the Facebook Sharing Debugger and LinkedIn Post Inspector to clear cached previews.

OG image spec: 1200 x 630, JPEG, under about 300 KB.

---

## Where the data comes from

All figures come from Golf Genius. The public league pages render through JavaScript widgets, so a plain page fetch returns nothing useful. Request the widget endpoints directly instead:

```
https://www.golfgenius.com/leagues/[league-id]/widgets/[widget-name]?page_id=[page-id]&shared=false
```

| Widget | Returns | Notes |
|---|---|---|
| `player_stats` | Per-player eagles, birdies, pars, bogeys, doubles, triples | Works directly |
| `season_points` | Standings, rounds played, gross and net averages, low rounds | Works directly |
| `course_statistics` | Hole-by-hole yardage, par, scoring average, difficulty rank | Does **not** work directly |

`course_statistics` requires clicking **Update Chart** in the browser before it renders, so a fetch returns an empty table. Capture it manually from the page with the filters set to **All Rounds** and **All Golfers**.

Contest winners and prize records are not in Golf Genius. They come from the weekly league email and the prize tracking spreadsheet.

---

## Editorial conventions

Decisions worth keeping consistent year to year:

- **Full names everywhere.** First and last name on every reference, including repeat mentions. Counter to AP style, but this is an informal document.
- **Scope.** Scoring and leaderboard figures cover all league players. Only the Season Points Race and the weekly contests are limited to the contest division, since only entrants are eligible for prizes.
- **Net scoring stays in the background.** It is what makes a wide handicap range work, but it is not a headline.
- **Holes, not rounds.** A player's triple-bogey count is a number of holes. Say so.
- **"Holes played," not "holes walked."** Spell out terms that are not common abbreviations in golf. No "h" for holes.
- **Tee times.** Write "the 5:40 tee time," not "the 5:40 group."
- **Flag course anomalies.** Construction, temporary pars, and unusual pin positions distort scoring averages. Note them and exclude affected holes from difficulty rankings rather than presenting the artifact as a finding.
- **Footer tagline.** *Great people · Good golf · Same Mondays → [next year]*

---

## Prizes

Contest prizes come from 35x70 Golf Co., run by Katy and Dan Winters. Primary contest winners receive store credit good for a polo or hoodie. Secondary prize winners receive a caddie towel. The Weekly Reload pays a sleeve of Titleist ProV1 or V1x.

Their logo is embedded in the page and links to https://35x70golfco.com.

---

*Last updated September 2026*
