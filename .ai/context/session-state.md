# Session State — resume here

**Last updated:** 2026-07-03 (end of discovery/planning session)
**Phase:** Planning complete. Next action = build **Milestone 0 (overview app)**. No code
written yet.

## TL;DR for the next session
Everything is decided and documented. Pick up by scaffolding the overview app per
`specs/001-relaunch/plan.md` → Milestone 0. First confirm the two small open choices below.

## What this project is
Relaunch of `deltaclub-interlaken.ch` (paragliding club DCI Interlaken) + alignment of the
website with the WhatsApp community. Core purpose: the website is the **reliable live source
of truth for flight-area status** (which launch/landing sites are open + current wind);
WhatsApp is the real-time signal. Full context in the files below.

## Read these (authoritative)
- `.ai/context/personas.md` — 11 personas; Member Core = P0 base, sub-personas inherit it.
- `.ai/context/sitemap-and-vision.md` — page vision, IA, locked architecture, feasibility flags.
- `.ai/context/communication-strategy.md` — Web=truth / WhatsApp=realtime; DE/EN policy.
- `.ai/context/current-site-inventory.md` — legacy WordPress audit.
- `.ai/context/features.md` — locked decisions, continuity, 80/20 rollout, Milestone 0, backlog.
- `.ai/instructions/07-continuity.md` — bus-factor doctrine (public repo, role accounts, handover gate).
- `.ai/instructions/01-project-overview.md` — project overview + hosting/continuity exceptions.
- `specs/001-relaunch/spec.md` — the relaunch spec (WHAT/WHY, FRs, success criteria).
- `specs/001-relaunch/plan.md` — the implementation plan; **Milestone 0 detailed**.

## Locked decisions (summary)
- Primary goal: website = live source of truth for flight-area status.
- **Build order: overview (status) app FIRST**, on the maintainer's homelab, then migrate to
  provider. Rest of relaunch follows.
- CMS: managed **WordPress** (Infomaniak), modernized (block theme, drop Elementor,
  Polylang DE/EN, keep The Events Calendar).
- Anchor: separate **status service** = map + per-site open/closed + wind; live embed widget
  + JSON API consumed by WP per-site pages.
- Wind: **winds.mobi** primary now (lenti.cloud offline) → lenti.cloud primary later; fallback + staleness.
- WhatsApp: **assisted manual cross-post** (no Channel API); website authoritative.
- Design: modern, mobile-first refresh; keep DCI identity.
- Rollout: staging URL → build to ~80% → **club/board approval** → big-bang cutover → 20% live.
- News migration: **evergreen only** (news starts fresh). Gastschulen rewrite: **20%** (Rails keeps running).
- Fundgrube (lost & found): dropped → WhatsApp.
- Hosting: Swiss — **Infomaniak** lead; Metanet/Hostpoint alternates.
- Effort: part-time (evenings/occasional daytime), no hard deadline.
- Continuity: **public repo**, role-based accounts (≥2 board members each), password manager,
  runbooks, ownership registry, onboarding doc, handover-ready acceptance gate.

## Milestone 0 — overview app (the immediate next build)
Stack (from plan.md): **FastAPI + SQLite + Leaflet (Swisstopo tiles) + vanilla JS**,
containerized, deployed on homelab (Docker/Traefik per `.ai` infra conventions), built
**portable** (12-factor) so homelab→Infomaniak is a redeploy.
Delivers FR-001..007: map homepage, per-site status+wind, mobile admin status toggle
(<2 min), wind provider abstraction (winds.mobi + fallback + staleness), `/api/*`, `/embed`,
`/health`. Sites defined in a committed `sites.yaml` (no personal data). Target layout:
`apps/overview/` (see plan.md file structure).

## Open questions to confirm before building M0 (asked, not yet answered)
1. Go-ahead to start building M0? (was awaiting user's "go".)
2. Map tiles: **Swisstopo** (recommended) vs plain OpenStreetMap.
3. Storage: **SQLite** (recommended at this scale) vs Postgres.

## Real-world prerequisites (non-code, parallel — need the user/club)
- Create role accounts (`webmaster@…` etc.) + a club password manager.
- winds.mobi API access details; recover **lenti.cloud** (currently offline) for later.
- Confirm **Infomaniak** WordPress plan.
- **Gastschulen** Rails repo access (still pending) — needed for the later Python rewrite.
- Populate `sites.yaml` with real site coordinates + wind-station references.

## Data hygiene reminders
- `old page/` (WordPress export) contains personal data → **gitignored, never commit**.
- Repo is intended public → no secrets, no personal data in any committed file.
- Migrate off the personal-Gmail WordPress admin to a role account.
