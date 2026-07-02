# Feature History & Backlog — DCI Web

## Current Version: v0.1 (planning)

### Shipped Milestones

| Milestone | What shipped |
|---|---|
| v0.1 | Discovery: legacy-site audit, sharpened personas, communication strategy, and relaunch vision captured in `.ai/context/` |

---

## Locked decisions (relaunch interview)

- Primary goal: website = reliable **live source of truth** for flight-area status.
- Hosting: **managed hosting** (CMS) + **VPS** (sub-services). NOT self-hosted — exception
  to the `.ai` homelab profile.
- CMS: **managed WordPress, modernized** (drop Elementor, block theme, Polylang DE/EN, keep
  The Events Calendar).
- Anchor: **status service** (map + wind + per-site status) on VPS → live widget + JSON API.
- Wind: **lenti.cloud** primary → **winds.mobi** fallback.
- WhatsApp: **assisted manual cross-post** (source of truth = website).
- Design: **modern mobile-first refresh, keep DCI identity.**
- Gastschulen app: **rewrite RoR → Python** (VPS sub-service), in scope.
- Fundgrube (lost & found): **dropped** → WhatsApp.

---

## Backlog (unordered — to be phased in the plan)

**Anchor / status**
- Status service: per-site open/closed model + admin toggle (<2 min flip from phone)
- Interactive map homepage (clickable icons → site pages), mobile-first
- Wind provider abstraction: lenti.cloud primary, winds.mobi fallback, per-site mapping
- JSON data API consumed by per-site WP pages + the map widget

**Content / CMS**
- WordPress modernization: remove Elementor, lightweight block theme, DCI identity
- Bilingual DE/EN (Polylang) on high-value pages
- Rich launch/landing site pages: 360° pano · video list · prose · access · favourable vs
  dangerous wind · rules · live status/wind
- News migration/prune (66-post archive, cut-off TBD)
- Event calendar (keep The Events Calendar)
- On-site comments/discussion (wpDiscuz replacement)

**Community / engagement**
- DCI members area: become-a-member form + governance/how-DCI-works pages
- Newbie↔veteran mentorship (opt-in veteran directory → WhatsApp handoff)
- Social media feed: YouTube (feasible) + Instagram (constrained — curated/paid widget)
- Competition page: XContest club feed (embed/link) + DCI competitions; evolve
  Streckenflugcup; candidate **Hike & Fly Challenge** (cf. pdcs.ch)
- Monitored Contact: role routing (Präsident/Vize/Webseite) + assigned responders + SLA

**Comms**
- Assisted WhatsApp cross-post tooling (pre-filled message + stable deep-links)

**Services**
- Gastschulen registration rewrite RoR → Python (VPS)

---

## Feasibility / research items
- Instagram aggregation path (Business Graph API + review vs curated account vs paid widget)
- XContest club-feed integration (embed/scrape/link)
- Social-feed widget budget
- Mentorship matching mechanism + member-privacy (opt-in)
- 360°/video content production plan per site

## Continuity (cross-cutting, overriding — see `instructions/07-continuity.md`)

- Repo **public**; zero secrets / zero personal data.
- All accounts **role-based/impersonal**; ≥2 board members per critical account.
- Credentials in a club password manager; rotation + handover documented.
- Deliverables: `docs/ownership.md` (registry), `docs/onboarding.md`, per-service runbooks,
  and a non-technical "common tasks" guide.
- **Immediate action:** gitignore `old page/` (contains personal data) before any public
  push. It is currently untracked — must stay uncommitted.
- Migrate off the personal-Gmail WordPress admin to a role account.
- "Handover-ready" is an **acceptance gate** for cutover (see 07-continuity.md checklist).

## Rollout strategy (locked)

Pareto, staged-then-big-bang:
1. Build the new site on a **throwaway/staging URL** (not public, not indexed).
2. Reach **~80%** (the high-value core — see split below).
3. Get **club/board approval** to move (governance gate; Board persona).
4. **Big-bang cutover** (DNS) to replace the old site at the real domain.
5. Iterate the remaining **20% detail work live**, post-launch.

### Proposed 80% (pre-approval, ships at cutover)
- Modernized WordPress (block theme, DCI identity, mobile-first)
- Full top-level IA/navigation + all main pages
- Status service: map homepage + per-site open/closed + wind + JSON API
  (winds.mobi as primary at first — lenti.cloud is offline)
- Rich site pages for ALL launch/landing sites at CORE depth
  (status, wind, prose, access, favourable/dangerous wind, rules)
- Evergreen content migrated (rules/guides/timeless) + events; dated news starts fresh
- Bilingual: full DE + EN on high-value pages
- Monitored Contact (role routing + responders)
- Become-a-member form + governance pages
- On-site comments

### Proposed 20% (post-cutover, iterative)
- 360° panos + curated video lists per site (rolling content production)
- Social media feed (Instagram feasibility work; YouTube first)
- Competition page (XContest embed + DCI competitions; Hike & Fly Challenge)
- Newbie↔veteran mentorship directory
- Gastschulen rewrite RoR→Python (old app keeps running meanwhile)
- Switch wind primary to lenti.cloud once back online
- Full bilingual coverage + news-archive backfill

## Resolved
- 80/20 split confirmed. News migration = evergreen only. Gastschulen rewrite = 20%.
- **Hosting:** Swiss. Lead = **Infomaniak** (privacy-focused EU provider); alternates
  **Metanet** / **Hostpoint**. For CMS (managed) + eventually the sub-services.
- **Effort:** part-time — evenings + occasional daytime; no hard deadline.
- **Build order:** the **overview (status) app FIRST**, initially self-hosted on the
  maintainer's homelab container host, then migrated to the provider. The rest of the
  relaunch follows.

## Milestone 0 — Overview app (first deliverable, before the WordPress relaunch)
- Standalone status service: map + per-site open/closed + wind (winds.mobi primary until
  lenti.cloud is back), admin status toggle, JSON data API, embeddable widget.
- **Initial hosting = homelab** → the `.ai` infra conventions (`02-infra`, `03-cicd`,
  Traefik list-labels, healthchecks) **apply for v1**.
- **Hard requirement: portability** — 12-factor, containerized, env-config, no homelab-only
  assumptions — so the homelab→Infomaniak/VPS move is a redeploy, not a rewrite.

## Open decisions
- (none blocking) — VPS/product tier at Infomaniak to be picked when Milestone 0 migrates.
