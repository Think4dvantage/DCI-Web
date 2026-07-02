# Personas — DCI Interlaken

Source of truth for stakeholder personas of the DCI website + WhatsApp community.
Supersedes the legacy `Personas.txt` at repo root.

## Model: base persona + sub-personas

Personas split into two groups:

1. **DCI Members** — share a common base persona, **Member Core**, which captures what
   *every* member wants in unison. The other member personas (Newbie, Competitive, Veteran,
   Board & Content Volunteers) are **sub-personas**: they **inherit all Member Core needs**
   and add their own specialization. Design for Core first; layer sub-persona needs on top.
2. **External personas** — non-members (visiting pilots, landowners/authorities, tandem
   customers/firms, aspiring pilots, public). They do **not** inherit Member Core.

```
DCI Member (base = Member Core)  ── P0
├── Member Newbie                ── P1   inherits Core + "explain the why" + mentorship
├── Board & Content Volunteers   ── P1   inherits Core + maintainer/publisher role (internal)
├── Member Competitive           ── P2   inherits Core + competition/ranking/recognition
└── Member Veteran               ── P2   inherits Core + be-asked-for-insight + peer contact

External personas (do not inherit Core)
├── Outside Licensed Pilots      ── P1   EN
├── Landowners & Authorities     ── P1
├── Sport Newbies (aspiring)     ── P2   EN-ish
├── Tandem Customers             ── P2   EN
├── Tandem Firms                 ── P2
└── Pedestrians / Public         ── P2
```

**Priority tiers** — P0: design anchor, validated first · P1: strategically critical,
explicitly designed for · P2: served, not optimized for.

**served-by** = primary channel under the comms model (Website = durable source of truth;
WhatsApp = real-time). See `communication-strategy.md`. **lang** = DE/EN needed.

---

# DCI Members

## P0 — Member Core  *(base persona for all members)*

**Summary:** Dues-paying local pilot who flies Interlaken often. The site is built for
them first. Joined to avoid per-flight landing taxes and/or to support the club. **Every
member sub-persona below is a Member Core plus a specialization.**

**Jobs-to-be-done (shared by ALL members)**
- Know **what's open/closed right now and why** (launch/landing sites, airspace, heli/drone,
  temporary restrictions) — the single most important job.
- Feel part of a community: fly with others, attend events, discuss ideas, be visible in
  the DCI feed / social media.
- Trust that the club is actively working to keep as many launch/landing sites available as
  possible (property purchase/rental, stakeholder negotiation).

**Pains:** status info scattered/stale; duplicate/contradictory info between website and
WhatsApp.
**served-by:** Website = authoritative **live status board** + rules + site pages + event
archive. WhatsApp = real-time nudges that link back to the site. **lang:** DE.
**Key content/features:** live flight-area status board · Fluggebiet site pages · event
calendar · news feed · member discussion · (marketplace = Fundgrube).

> The live status board is *this base persona's* feature and the anchor of the whole
> Web-as-reference / WA-as-realtime model.

---

## P1 — Member Newbie  *(sub-persona of Core)*

**Inherits:** all Member Core needs.
**Adds:**
- Needs the **"why"** — detailed explanations of each site's conditions, hazards, rules,
  and the reasoning behind closures.
- Wants to **connect with veteran pilots** to confirm their learning.

**Pains:** rules stated without rationale; no clear path to a mentor.
**served-by:** Website (deep reference pages) + WhatsApp (asking veterans). **lang:** DE
(some EN if learning from abroad).
**Key content (on top of Core):** richly explained Fluggebiet pages · glossary/rules ·
mentorship path.

---

## P1 — Board & Content Volunteers  *(sub-persona of Core — internal role)*

**Inherits:** all Member Core needs (they are members too).
**Adds (the maintainer role that keeps the whole site alive):**
- Publish/flip a site-status change in **under 2 minutes**, from a phone.
- Create events, post news, moderate discussion — without wrestling a heavy page builder.

**Pains:** current WP + Elementor is heavy; posting a simple "Startplatz X gesperrt" is more
work than it should be.
**served-by:** Website admin/authoring surface (+ possibly triggers a WhatsApp alert).
**lang:** DE.
**Key content:** simple authoring UI · status toggle · event entry · role permissions.

> Drives the **CMS / authoring-tool decision** in the relaunch.

---

## P2 — Member Competitive  *(sub-persona of Core)*

**Inherits:** all Member Core needs.
**Adds:** compete for the club vs other clubs; fly in a DCI team; appear on top-lists; be
singled out for good performance; earn prizes/recognition at events.
**Pains:** rankings not visible/current; achievements not surfaced.
**served-by:** Website (Streckenflugcup rankings, results) + WhatsApp (banter). **lang:** DE.
**Key content (on top of Core):** Streckenflugcup rankings · team pages · results/awards.

---

## P2 — Member Veteran  *(sub-persona of Core)*

**Inherits:** all Member Core needs.
**Adds:** be asked for insight on current situations; connect regularly with fellow veterans.
**served-by:** WhatsApp (insight/discussion) + Website (recognition). **lang:** DE.
**Key content (on top of Core):** discussion surface · a way to be tapped for input ·
veteran recognition.

---

# External personas *(do not inherit Member Core)*

## P1 — Outside Licensed Pilots (visitors)

**Summary:** Licensed pilot from outside the region, planning to fly Interlaken.
**Jobs:** find launch sites — how to get there, what to look for, required conditions,
decision resources.
**Pains:** local knowledge is tacit / German-only / not visitor-oriented.
**served-by:** Website (self-serve site pages, maps, access, conditions). **lang:** **EN
needed** (+DE) — high-value bilingual target.
**Key content:** Fluggebiet pages with access/parking/conditions · maps · webcams/meteo ·
visitor etiquette & landing-tax info.

## P1 — Landowners & Authorities

**Summary:** Gemeinden, Grundeigentümer, Behörden, farmers, neighbors. The club's mission of
keeping sites open depends on these relationships.
**Jobs:** find **who to contact** and that the club is responsible/reachable; lodge a
complaint/request and get a response; see the club takes rules seriously.
**Pains:** no obvious, credible public contact point; unclear who is accountable.
**served-by:** Website — public "Who we are / Rules / Contact" surface, **separate from the
member feed.** **lang:** DE (EN optional).
**Key content:** public about/responsibility page · rules & conduct · role-targeted contact
(Präsident/Vize/Webseite) · complaints channel.

## P2 — Sport Newbies (aspiring pilots)

**Jobs:** find reliable info on how to start; learn which schools relate to DCI.
**served-by:** Website. **lang:** DE (+EN).
**Key content:** "how to become a pilot" page · related/partner schools.

## P2 — Tandem Customers

**Jobs:** find trustworthy DCI member companies offering tandem flights.
**served-by:** Website. **lang:** **EN needed** (+DE) — largely tourists.
**Key content:** directory of DCI tandem member firms · trust signals.

## P2 — Tandem Firms

**Jobs:** get referrals for tandem requests; gain trust via local-club endorsement.
**served-by:** Website (listing/referral). **lang:** DE/EN.
**Key content:** firm listing · referral/endorsement mechanism.

## P2 — Pedestrians / Public

**Jobs:** understand the sport; have a contact point for complaints/requests/questions.
**served-by:** Website. **lang:** DE.
**Key content:** intro-to-the-sport page · public contact point (overlaps Landowners &
Authorities).

---

## Notes
- **Fundgrube (marketplace)** is a *feature* for members (Core/Newbie), not its own persona.
  Fate in relaunch TBD (interview).
- **EN-needed personas:** Outside Licensed Pilots, Tandem Customers (primary); Sport Newbies,
  Tandem Firms (secondary). Scope bilingual content around their high-value pages.
