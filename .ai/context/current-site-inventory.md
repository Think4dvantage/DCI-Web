# Current Site Inventory — deltaclub-interlaken.ch

Audit of the legacy WordPress site, from the export at
`old page/deltaclubinterlaken.WordPress.2026-05-25.xml` (WXR 1.2, generated 2026-05-25).
Baseline for the relaunch and migration scope.

## Platform / stack (legacy)

| Aspect | Value |
|---|---|
| CMS | WordPress 6.2.9 |
| Theme | Neve |
| Page builder | Elementor (`elementor_library` present) |
| Events | The Events Calendar (Tribe: `tribe_events`, `tribe_venue`, `tribe_organizer`) |
| Comments | wpDiscuz (`wpdiscuz_form`) |
| Language | German only |
| Base URL | https://deltaclub-interlaken.ch |

## Content counts (from export)

| post_type | count | status |
|---|---|---|
| attachment (media) | 287 | — |
| post (news) | 66 | 198 total published across all types |
| tribe_events | 54 | 6 draft, 3 private |
| page | 42 | |
| nav_menu_item | 30 | |
| tribe_venue | 6 | |
| elementor_library | 3 | |

Categories: Allgemein, Berichte, Events, News, Uncategorized.

## Section / page map

- **Home**
- **Fluggebiet** (flying area) — the reference core:
  - Startplätze (launch): Amisbühl, Bergbo, Breitlauenen, Chalet, Hohwald, Luegibrüggli,
    Niederhorn
  - Landeplätze (landing): Höhematte, Lehn
  - Notlandeplatz: Flugplatz Interlaken
- **Meteo**, **Webcams** — conditions
- **DCI Fundgrube** — a **lost & found** (found items posted hoping the owner claims them),
  implemented with a full ad-style flow (create / edit / show / search / renew / reply).
  Relaunch decision: **drop from website, move to WhatsApp.**
- **Streckenflugcup** — cross-country cup: 2019, 2020, 2021, 2022, 2023
- **Impressionen** — gallery
- **Membership:** "Ich möchte DCI Mitglied werden"
- **Governance/contact:** Vorstand, Impressum, Links; role-targeted contact forms —
  "Nachricht an den Präsidenten", "…Vizepräsidenten", "…betreffend Webseite oder Lufträume"
- **Blog / News**

## News feed character (the #1 content stream)

Dominated by **flight-area status & safety**, e.g.:
- Site open/closed: "Startplatz Luegibrüggli wieder offen", "Startplatz Chalet gesperrt",
  "Deltarampe Niederhorn gesperrt/wieder offen", "Alle Start- und Landeplätze … gesperrt"
- Airspace / aviation: "Luftraumeinschränkungen … Lauberhornrennen", "TMA und CTR Meiringen
  …", "Helikopterflüge …", "Drohnenflug über dem Golfplatz"
- Rules & conduct: "Haltet euch an die Regeln", "Groundhandling Regeln Lehn",
  "Neue Regeln am Weissenstein"
- Covid-era closures/openings
- Club news: T-Shirts, new grill, Chrigel Maurer talks, Hauptversammlung (HV)

**Implication:** this stream is exactly what the WhatsApp channels now carry in real time.
The relaunch must resolve the overlap → Website holds the durable, authoritative status;
WhatsApp carries the real-time ping. See `communication-strategy.md`.

## Events character

Hike & Fly outings, Clubfliegen, **Notschirm falten** (reserve-repack courses), HV/AGM,
grill & social evenings, Frauen (women's) events, Delta SM (Swiss championship),
Saisonabschluss, PWC/comp events.

## WhatsApp Community — "Delta Club Interlaken DCI"

| Channel | Assumed purpose | Confirmed? |
|---|---|---|
| DCI-Events | Event announcements | likely |
| DCI-Flyers | **Unclear** — promo flyers vs active flyers coordinating | ❓ confirm in interview |
| DCI-Vollmondflug/Nachtfliegen | Full-moon / night-flying activity group | likely |
| DCI-FlugKompass | **Unclear** — likely "fly where today / conditions" | ❓ confirm in interview |
| DCI-EventsOrga | Event organizers / board coordination | likely |

## Migration open questions (→ interview)
- Keep the 66-post news archive? Cut-off date?
- ~~Does Fundgrube survive?~~ **Resolved:** lost & found → moved to WhatsApp, dropped.
- **Streckenflugcup:** survives, evolving into a Competition page (XContest club feed +
  DCI's own competitions). Live vs archive TBD.
- Retain `old page/` export in-repo after migration?
