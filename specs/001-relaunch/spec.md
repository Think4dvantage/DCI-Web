# Feature: DCI Website Relaunch (v2)

## Overview

Relaunch `deltaclub-interlaken.ch` as a **mobile-first, bilingual, handover-proof** club
site whose core purpose is to be the **reliable live source of truth for flight-area
status** — which launch/landing sites are open and the current wind — with the **website as
the durable record** and **WhatsApp as the real-time signal**. Built on a staging URL to
~80% completeness, approved by the club, then cut over big-bang; the remaining detail work
is polished live.

Supporting context (authoritative): `.ai/context/personas.md`,
`.ai/context/sitemap-and-vision.md`, `.ai/context/communication-strategy.md`,
`.ai/context/current-site-inventory.md`, `.ai/instructions/07-continuity.md`.

## User Stories

### P1 — Must Have (ships in the 80% at cutover)

- **Flight-area status at a glance.** As any pilot (Member Core anchor), I want a map
  homepage showing which launch/landing sites are open/closed and the current wind, so I can
  decide whether and where to fly.
  - **Acceptance:** on a phone, within seconds of loading, I can read each site's open/closed
    state + a current wind value; icons are clickable through to the site page.
- **Per-site status.** As a pilot, I want each launch and landing site's live status + wind
  on its own page, so I can check one specific site.
  - **Acceptance:** every site page shows the same status/wind as the map, plus a "last
    updated" indication.
- **Fast status updates.** As a Board & Content Volunteer, I want to change a site's status
  in under 2 minutes from my phone, so information stays current.
  - **Acceptance:** a non-technical volunteer flips a site to closed + reason and it appears
    on the map and site page within a minute.
- **Rich site pages.** As an Outside Pilot or Newbie, I want each site page to explain how to
  get there, favourable vs dangerous wind, applicable rules, and a prose description, so I can
  fly the site safely.
  - **Acceptance:** each site page contains all of: access/how-to-get-there, favourable wind,
    dangerous wind, rules, description.
- **Monitored contact.** As a landowner/authority or member of the public, I want a contact
  that is actually watched and answered quickly, so complaints/questions get a response.
  - **Acceptance:** contact routes to a role inbox with an assigned responder and a stated
    response expectation.
- **Membership + governance.** As a prospective member, I want a "become a member" form and a
  clear explanation of how the DCI is set up.
- **Bilingual.** As an international visitor/tandem customer, I want the site in German with
  English on the high-value pages (flying area, membership, tandem, contact).
- **Handover-proof (continuity).** As the club, I want the whole system documented and
  role-owned so any capable person can take over even if the current maintainer is gone.
  - **Acceptance:** the `07-continuity.md` "handover-ready" checklist passes.

### P2 — Should Have (early in the 20%, post-cutover)

- **News & events.** Evergreen content migrated (rules, guides, timeless posts); dated
  status/news is not migrated (news starts fresh). Event calendar in place.
- **On-site comments** on news/posts.
- **Competition page.** XContest feed of pilots listing DCI as their club + DCI's own
  competitions.
- **Social media feed.** Aggregated DCI-member paragliding posts — YouTube first (Instagram
  is constrained; see Dependencies).
- **Mentorship.** Opt-in veteran directory that hands off to WhatsApp for real contact.
- **Assisted WhatsApp cross-post.** When a volunteer changes status or posts news, the admin
  offers a one-tap pre-filled WhatsApp message + stable link.

### P3 — Nice to Have (later 20%)

- 360° panorama + curated video list per site (rolling content production).
- New **Hike & Fly Challenge** competition (cf. pdcs.ch).
- Switch wind primary from winds.mobi to **lenti.cloud** once it is back online.
- Full bilingual coverage; full news-archive backfill.
- Guest-school registration rewrite (see FR-024; the existing app keeps running until then).

## Functional Requirements

**Status & wind (anchor)**
- FR-001: The homepage presents a map of the flying area with an icon per launch and landing
  site indicating open / conditional / closed.
- FR-002: Each site icon shows a current wind value and links to that site's page.
- FR-003: The system stores a per-site status (state + short reason + last-updated timestamp).
- FR-004: Authorized volunteers can change a site's status quickly from a mobile device.
- FR-005: The same live status and wind appear on each individual site page.
- FR-006: Wind data is sourced with a primary provider and an automatic fallback so wind
  remains available when the primary is down (see Dependencies).
- FR-007: Every status/wind display shows how fresh the data is (last-updated), and clearly
  indicates when wind data is unavailable rather than showing stale values as current.

**Site content**
- FR-010: Each launch and landing site has a dedicated page containing: description, how to
  get there, favourable wind, dangerous wind, and rules.
- FR-011: Site pages support later addition of a 360° panorama and a video list without
  redesign (P3 content).

**Content platform**
- FR-012: News posts and events are authored and displayed; the event calendar is retained.
- FR-013: Content is available in German, with English on the high-value pages.
- FR-014: Non-technical volunteers can perform the common tasks (post news, add an event,
  flip a status) via a simple documented workflow.

**Community & engagement**
- FR-015: A "become a member" form and DCI governance/structure pages exist.
- FR-016: A competition page shows a club-filtered XContest view and DCI's own competitions.
- FR-017: A social feed aggregates DCI-member paragliding content (YouTube; Instagram best-
  effort per constraints).
- FR-018: An opt-in veteran directory lets newbies find mentors, with contact handed to
  WhatsApp.
- FR-019: On-site comments are available on news posts.

**Communication**
- FR-020: The website is the authoritative record for status; WhatsApp is a real-time
  pointer back to it.
- FR-021: The admin can generate a pre-filled WhatsApp message (summary + stable deep link)
  for a status change or news post.

**Continuity (cross-cutting — governed by `07-continuity.md`)**
- FR-022: The repository is public and contains no secrets and no personal data.
- FR-023: Every account/service is role-owned (not personal); ≥2 board members hold access
  to each critical account; credentials live in the club password manager.
- FR-024: Each service ships with a runbook; an ownership registry (`docs/ownership.md`) and
  maintainer onboarding guide (`docs/onboarding.md`) exist and stay current.

**Services**
- FR-025: The guest-school registration capability remains available throughout the relaunch
  and is later re-provided as a maintained sub-service.

## Non-Functional Requirements

- NFR-001 (Mobile-first): primary flows (check status/wind, read a site page) are usable
  one-handed on a phone at a launch site.
- NFR-002 (Continuity): a new capable maintainer can stand up every component using only the
  public repo + the password manager, with no undocumented steps.
- NFR-003 (Privacy/DSG-GDPR): no personal data in the public repo; the legacy export is kept
  private; member/mentor data is opt-in only.
- NFR-004 (Resilience): wind and status degrade gracefully — fallback wind source, explicit
  staleness, never present unavailable data as live.
- NFR-005 (Bilingual): DE complete; EN on flying-area, membership, tandem, contact pages.
- NFR-006 (Findability): visitor-facing pages (site pages, tandem, membership) are
  search-discoverable; the staging build is NOT indexed.
- NFR-007 (Low authoring friction): the common volunteer tasks require no technical skill and
  no page-builder wrangling.

## Success Criteria

- SC-001: A pilot can determine open/closed status + current wind for any site within ~10
  seconds of landing on the homepage, on a phone.
- SC-002: A non-technical volunteer changes a site's status in under 2 minutes end-to-end.
- SC-003: When the primary wind source is offline, wind still displays via the fallback with
  no manual intervention.
- SC-004: Every launch/landing site page includes all five required content elements
  (description, access, favourable wind, dangerous wind, rules).
- SC-005: The public repo passes a scan showing zero secrets and zero personal data.
- SC-006: A person who has never worked on the project can, from the repo + password manager
  alone, deploy the status service and edit content — validated by a dry-run handover.
- SC-007: The club/board formally approves the staging site before cutover.
- SC-008: After cutover, the old site's high-value evergreen content (site pages, timeless
  guides/rules, events) is present on the new site; dated news is intentionally not carried
  over.

## Key Entities

| Entity | Key Attributes | Notes |
|---|---|---|
| Site (launch/landing) | name, type, geo-coordinates, description, access, favourable wind, dangerous wind, rules, linked wind station | Core of the map + site pages |
| Site status | site, state (open/conditional/closed), reason, updated-at, updated-by | Volunteer-edited; drives icons |
| Wind reading | site/station, direction, speed/gust, timestamp, source | From primary or fallback source |
| Event | title, date/time, venue, description, signup | The Events Calendar |
| News post | title, body, date, language, comments | Bilingual |
| Member application | applicant details | Handled per privacy rules; not in public repo |
| Veteran (mentor) | opt-in profile, contact-via-WhatsApp | Opt-in only |
| Account/asset (ownership) | asset, type, role owner, credential location | `docs/ownership.md` |

## Out of Scope

- **Fundgrube (lost & found):** moved to WhatsApp; not rebuilt on the website.
- **Self-hosting on the homelab:** this project uses managed hosting + a VPS; the `.ai`
  Traefik/homelab infra conventions do not apply.
- **Full rebrand:** identity/logo are retained; only a modern mobile-first refresh.
- **Automated posting into WhatsApp Channels:** not possible via API; handled by assisted
  manual cross-post.

## Assumptions

- Managed hosting is procured for the CMS; a VPS is procured for sub-services.
- The club provides role-based email accounts and a shared password manager.
- The board will review and approve the staging site before cutover.
- Existing content is largely reused (WordPress → modernized WordPress), minimizing migration.
- Most launch sites have an associated public wind station reachable via the chosen sources.

## Dependencies

- **Wind data:** own page **lenti.cloud** (currently offline) as intended primary;
  **winds.mobi API** as fallback (and interim primary until lenti.cloud returns).
- **XContest** DCI club page/ranking (no open API — embed/link expected).
- **YouTube** (feasible) and **Instagram** (Graph API + app review; likely curated account
  or paid widget rather than open hashtag search).
- **WhatsApp** community/channels (no inbound Channel API).
- **The Events Calendar** and bilingual plugin (Polylang) on WordPress.
- **Existing guest-school registration app** (`gastschulen.deltaclub-interlaken.ch`) —
  keeps running until re-provided; repo access pending.
- **Hosting/VPS providers** — to be selected (Swiss/EU preferred).

## Edge Cases

- Both wind sources unavailable → show explicit "wind unavailable", never a stale value as
  current.
- Site has no associated wind station → show status only, label wind as not available.
- Status left stale → "last updated" makes staleness visible; consider a staleness warning.
- WhatsApp says one thing, website another → website is authoritative by policy.
- Staging site accidentally indexed or shared → must be noindex + access-gated.
- Legacy export or member data slips toward the public repo → gitignore + review gate.
- Volunteer without technical skills must still complete common tasks unaided.

## Resolved decisions

- **News migration:** evergreen only (rules, guides, timeless posts). Dated status/news is
  not migrated — news starts fresh on the new site.
- **Guest-school rewrite:** in the 20% (post-cutover). The existing Rails app keeps running
  and is linked at cutover; rewrite follows once repo access is available.
