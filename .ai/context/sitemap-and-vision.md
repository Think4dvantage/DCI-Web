# Site Map & Relaunch Vision — DCI Web

The user's vision for the relaunched site, captured verbatim-in-intent and structured into
an information architecture. Companion to `personas.md` and `communication-strategy.md`.

## Locked architecture (from relaunch interview)

- **Hosting:** end state = Swiss managed hosting for the CMS + a VPS for sub-services
  (lead provider **Infomaniak**; alternates **Metanet**/**Hostpoint**). **Exception:** the
  **overview/status app is built FIRST and runs on the maintainer's homelab** initially
  (so the `.ai` homelab infra conventions apply to that component's v1), then migrates to
  the provider. It must be built **portable** (12-factor, containerized) so the move is a
  redeploy. **Effort:** part-time, evenings/occasional daytime, no hard deadline.
- **CMS:** Managed **WordPress**, modernized — drop Elementor for a lightweight block
  theme, bilingual **DE/EN** via Polylang, keep The Events Calendar. Zero content migration.
- **Anchor feature:** map-first flight-area status (open/closed per site + live wind),
  built as a **separate status service** on the VPS, embedded in WP as a **live interactive
  widget** + a **JSON data API** that per-site pages consume. (Not a static image.)
- **Wind data:** primary = own page **lenti.cloud** (currently offline); fallback =
  **winds.mobi API**. Provider abstraction so it degrades gracefully.
- **Guest-school registration** (`gastschulen.deltaclub-interlaken.ch`): existing Ruby on
  Rails app → **rewrite to Python**, in scope, as a VPS sub-service.
- **WhatsApp:** website is source of truth; **assisted manual cross-post** (admin generates
  a one-tap pre-filled WhatsApp message + stable link). No API into WhatsApp Channels.
- **Design:** modern, **mobile-first** refresh; **keep** existing DCI identity/logo.
- **Primary goal:** the website is the reliable live source of truth for flight-area status.

## Information architecture (navigation)

- **Home** — simplified flying-area overview: map with per-site open/closed icons + current
  wind values. Mobile-first (pilots check at launch). Entry to everything.
- **Flying Area** (Fluggebiet) — a page per **launch** and **landing** site. Rich detail:
  - 360° photo of the site (self-hosted pano viewer, e.g. Pannellum)
  - list of videos showing the site (curated YouTube links)
  - prose description
  - how to get there (access/parking)
  - favourable wind / dangerous wind
  - rules
  - live status + wind for that site (from the status service data API)
- **DCI Members** —
  - become-a-member form
  - how the DCI is set up (governance / structure explanation)
  - **newbie ↔ veteran mentorship**: realistically an opt-in veteran directory; real contact
    handed off to WhatsApp (matching mechanism TBD)
- **News** — posts + reference information (migrate/prune legacy archive).
- **Social Media Feed** — aggregated **DCI-member** posts from Instagram / YouTube with
  paragliding content, filtered by tag/hashtag. Serves Member Core's "be seen" job.
- **Competition** — **XContest** feed of pilots listing DCI as their club + DCI's own
  competitions (evolves Streckenflugcup). Idea: add a **Hike & Fly Challenge** (cf.
  https://www.pdcs.ch/ ).
- **Contact** — actively **monitored, fast-answer**. Role-targeted routing
  (Präsident/Vize/Webseite) with assigned responders + response expectation.

## In / out of scope (from interview)

**In:** rich site pages · status map service · bilingual DE/EN · Streckenflugcup /
competition page · on-site comments/discussion · gastschulen rewrite (RoR→Python) ·
social feed · mentorship (light) · monitored contact.

**Out / moved:** **Fundgrube** = a **lost & found** (found items posted hoping someone
claims them) → move to **WhatsApp**, drop from website.

## Feasibility flags (research items, not blockers)

| Item | Risk | Realistic approach |
|---|---|---|
| **Instagram aggregation** | Simple feed API is dead; hashtag search needs Business Graph API + app review, fragile | YouTube via API is fine; Instagram via a curated club account or a paid widget service, not free hashtag scraping |
| **XContest club feed** | No open API; DCI has a club page/ranking | Embed/link the XContest club ranking rather than a custom native feed |
| **360° photos + video lists** | Not tech — content production | Pano viewer is trivial to self-host; work is capturing panos + curating videos per site |
| **Newbie↔veteran matching** | Filtering/verifying "the right people" is unclear | Opt-in veteran directory → WhatsApp handoff; keep matching light |
| **"Contact answered fast"** | Mostly process, not tech | Routing + assigned responders + response-time expectation, plus the form |
| **Mentorship / member privacy** | Member data exposure | Opt-in only; no scraping members into a directory |

## Open interview items (still to decide)
- Phasing / MVP-first vs big-bang, and timeline/effort budget.
- Competition data source specifics (XContest embed vs scrape; new Hike&Fly Challenge rules).
- Social feed provider choice + budget for a widget service.
- Mentorship matching mechanism.
