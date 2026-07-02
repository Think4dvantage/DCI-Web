# Communication Strategy — DCI

How the DCI website and the WhatsApp Community divide responsibility. This is the spine of
the relaunch: it decides what content lives where and removes today's overlap.

## Core model (locked)

> **Website = durable reference / single source of truth.**
> **WhatsApp = real-time signal that links back to the website.**

- Anything a member/visitor should be able to look up later lives on the **website**.
- Anything that is "right now, notice this" is pushed on **WhatsApp** — short, with a link
  back to the authoritative website page.
- When the two could conflict (e.g. site status), the **website is authoritative**; WhatsApp
  is the notification, not the record.

## Content-ownership rules

| Content | Owner (record) | Real-time push |
|---|---|---|
| Flight-area status (open/closed + why) | **Website** (live status board) | WhatsApp alert linking to board |
| Airspace / heli / drone / temporary restrictions | **Website** (status + news) | WhatsApp alert |
| Rules & conduct, site how-to, access | **Website** (Fluggebiet pages) | — |
| Events (dates, details, signup) | **Website** (calendar) | WhatsApp reminder linking to event |
| Event organization / logistics chatter | — | **WhatsApp** (Orga channel) |
| Club news / reports | **Website** (news) | WhatsApp when noteworthy |
| Discussion / banter / Q&A | (optional web forum) | **WhatsApp** primary |
| Night/full-moon flying coordination | — | **WhatsApp** (activity channel) |
| Rankings (Streckenflugcup) | **Website** | WhatsApp on milestones |
| Marketplace (Fundgrube) | **Website** (if kept) | WhatsApp cross-post optional |

## WhatsApp channel → website surface mapping

| Channel | Website counterpart (source of truth) | Integration to decide (interview) |
|---|---|---|
| DCI-Events | Event calendar | reminder links back; auto vs manual |
| DCI-FlugKompass (❓conditions/where-to-fly) | Live status board + meteo/webcams | status change → alert? |
| DCI-Flyers (❓intent) | TBD once intent confirmed | — |
| DCI-Vollmondflug/Nachtfliegen | Event/activity page | — |
| DCI-EventsOrga | (internal; no public web surface) | stays WhatsApp-only |

## Language policy

- **Bilingual DE/EN.** German is primary/complete.
- English on **high-value pages for EN-needed personas**: Fluggebiet/launch-site pages,
  membership, tandem directory, visitor how-to, contact. (Personas: Outside Licensed
  Pilots, Tandem Customers primary.)
- News/status: German first; English optional for safety-critical items.

## Open decisions (→ interview)
- WhatsApp↔website integration mechanism: manual cross-post vs automation (status change →
  auto WhatsApp alert). Note: WhatsApp **Channels** have no official inbound posting API;
  automation likely needs a workaround or a different push channel (e.g. Telegram, email,
  RSS→bot). Flag this trade-off during the interview.
- Confirm intent of **DCI-Flyers** and **DCI-FlugKompass** before finalizing the mapping.
- Whether to keep an on-site discussion/forum or cede all discussion to WhatsApp.
