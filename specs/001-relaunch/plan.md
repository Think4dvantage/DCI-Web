# Implementation Plan: DCI Website Relaunch (v2)

Companion to `spec.md`. Build order is **overview app first** (Milestone 0, homelab), then
the WordPress relaunch. Effort is part-time (evenings/occasional daytime), no hard deadline —
so milestones are independently shippable and each leaves the system in a working state.

---

## Technical Context

- **Overview (status) app** — new custom service. Default stack per `.ai` architect prompt:
  **Python + FastAPI**, **SQLite**, server-rendered templates + **Leaflet** map, vanilla JS.
  Containerized (`python:3.11-slim`), 12-factor, env-config.
- **CMS** — managed **WordPress** (Infomaniak), modernized: lightweight block theme, drop
  Elementor, **Polylang** (DE/EN), keep **The Events Calendar**.
- **Hosting** — Milestone 0 on the **homelab** (Docker + Traefik, `lg4.ch`); later migrate to
  Infomaniak/VPS. CMS on Infomaniak managed hosting from Milestone 1.
- **Guest-school app** — existing Rails app stays running; Python rewrite is post-cutover.

### Key decisions (research)

| Topic | Decision | Rationale / alternative |
|---|---|---|
| Overview backend | FastAPI | `.ai` default; trivial `/health`; async for wind fetches. |
| Storage | **SQLite** (named volume) | Handful of sites; portable single file; no DB server to run/move. Postgres is overkill at this scale. |
| Map tiles | **Swisstopo** (wmts, free) with OSM fallback | Swiss-official basemap fits the area; no key. OSM as backup/dev. |
| Map client | **Leaflet** (self-hosted assets) | Lightweight, embeddable, no vendor lock-in/key. |
| Wind source | **Provider abstraction**: winds.mobi (primary now) → lenti.cloud (primary later) with fallback chain + cache | Meets FR-006/FR-007; lenti.cloud offline today, so winds.mobi carries v1. |
| Admin auth | Single **role login** (hashed cred in env) behind HTTPS; mobile-friendly form | Meets FR-004 (<2 min flip) without a user system. ≥2 board members share the role cred via password manager (continuity). |
| Site definitions | Seeded from a committed **`sites.yaml`** (no personal data) → loaded to DB | Version-controlled, public-safe, easy to edit. |
| Embedding | `/embed` route (iframe) + `/api/*` JSON | Meets Q5 "live widget + data API"; WP pages consume `/api`. |

## Constitution & Continuity Check

- **Continuity (`07-continuity.md`)**: repo public → `sites.yaml` and code carry **no
  personal data**; admin credential and any API keys via `.env` (gitignored) +
  password manager. Ships with a runbook + ownership-registry entry. ✅
- **Infra conventions (`02`/`03`)** apply to Milestone 0 on homelab: Traefik **list-format**
  labels, Python-stdlib healthcheck, `restart: unless-stopped`, pinned image tags,
  `json-file` logging with rotation, `.env.example` documents every var. ✅
- **Portability**: no homelab-only assumptions beyond additive Traefik labels; SQLite on a
  named volume; all config via env → homelab→Infomaniak is a redeploy. ✅
- **Hosting exception**: CMS + eventual sub-service hosting is external (documented in
  `01-project-overview.md`). ✅

## Data Model (overview app)

| Entity | Fields | Notes |
|---|---|---|
| `site` | id, slug, name, type (launch/landing), lat, lon, wind_station_ref, active | Seeded from `sites.yaml`; geo + station mapping only (rich content lives in WP) |
| `site_status` | site_id, state (open/conditional/closed), reason, updated_at, updated_by | Volunteer-edited; drives map icons + per-site pages |
| `wind_reading` | site_id, direction, speed, gust, observed_at, source, fetched_at | Cached; `source` = winds.mobi/lenti.cloud; staleness computed from observed_at |

## API Contracts (overview app)

- `GET /health` → 200 JSON (service, version, uptime, wind-source status). Unauth.
- `GET /api/sites` → all sites with current status + latest wind + freshness.
- `GET /api/sites/{slug}` → one site (consumed by the WP per-site page).
- `GET /embed` → iframe-able interactive map (status + wind, click-through).
- `GET /` → homepage map (standalone until embedded).
- `POST /admin/status/{slug}` (auth) → set state + reason. Mobile form + JSON.
- Internal scheduler → refresh `wind_reading` per site on an interval, primary→fallback.

## File Structure (overview app — new repo area, e.g. `apps/overview/`)

```
apps/overview/
├── app/                     # FastAPI application
│   ├── main.py              # routes, /health
│   ├── wind/                # provider abstraction: base, windsmobi.py, lenticloud.py, chain
│   ├── models.py            # SQLite models
│   ├── admin.py             # status toggle (auth)
│   ├── templates/           # map homepage, /embed, admin form (DE/EN labels)
│   └── static/              # Leaflet assets, icons, css
├── sites.yaml               # site definitions (NO personal data)
├── Dockerfile               # python:3.11-slim, pinned
├── docker-compose.yml       # homelab: Traefik list-labels, healthcheck, json-file logging
├── docker-compose.dev.yml   # dev overlay: source mount, overview-dev.lg4.ch
├── .env.example             # every var documented (admin cred, wind source URLs, interval)
└── README.md                # runbook: run, deploy, rotate cred, migrate to provider
```

---

## Milestones

### M0 — Overview app on homelab  *(FIRST — the anchor, build now)*
Status service delivering FR-001..FR-007: map homepage with per-site open/closed + wind,
mobile admin status toggle, wind provider abstraction (winds.mobi primary, fallback +
staleness), JSON API, `/embed`. Deployed on homelab via Docker/Traefik. Portable by design.
**Done when:** map shows live status+wind on a phone; a volunteer flips a status in <2 min;
wind survives primary-source outage via fallback; `/health` green; README runbook exists.

### M1 — WordPress foundation on Infomaniak (staging)
Managed WP on Infomaniak at a **non-indexed staging URL**; modern block theme + DCI identity,
mobile-first; Polylang DE/EN; The Events Calendar; core IA/navigation. Role admin account
(retire the personal-Gmail admin).

### M2 — Content + integration
Rich launch/landing site pages at core depth (description, access, favourable/dangerous wind,
rules) consuming `/api/sites/{slug}`; embed the overview map on the homepage via `/embed`;
migrate **evergreen** content + events; membership form + governance pages; monitored contact
(role routing + responders); comments.

### M3 — Continuity hardening (gate for cutover)
`docs/ownership.md`, `docs/onboarding.md`, per-service runbooks; all accounts role-based with
≥2 board holders; secrets in the club password manager; public repo verified clean. Complete
the `07-continuity.md` handover-ready checklist.

### M4 — Approval + big-bang cutover
Club/board reviews staging → approves → DNS cutover to the real domain. Old site retired.

### M5 — The 20% (post-cutover, iterative)
360° panos + video lists per site; social feed (YouTube, then Instagram best-effort);
competition page (XContest embed + DCI comps; Hike & Fly Challenge); mentorship directory;
**migrate overview app homelab→Infomaniak/VPS**; switch wind primary to lenti.cloud when
back; gastschulen rewrite RoR→Python; full bilingual + evergreen backfill.

---

## Verification

- **M0:** `docker-compose config` valid; container healthy (`/health` 200); map renders
  status+wind on mobile; status flip round-trips to map + `/api`; kill the primary wind
  source → fallback still serves wind with correct staleness; no secrets/personal data in
  `apps/overview/` (scan).
- **M1–M2:** staging is noindex; DE/EN switch works on key pages; each site page shows all 5
  content elements + live status/wind from the API; evergreen content + events present.
- **M3:** handover dry-run — a second person deploys the overview app and edits content using
  only the public repo + password manager (SC-006).
- **M4:** board sign-off recorded (SC-007); post-cutover the domain serves the new site with
  evergreen content/events (SC-008).

## Immediate real-world prerequisites (parallel, non-code)
- Create role accounts (`webmaster@…`, etc.) + a club password manager.
- Confirm Infomaniak plan for WP; note winds.mobi API access; recover lenti.cloud (later).
