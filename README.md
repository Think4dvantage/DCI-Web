# DCI-Web

Website relaunch + online-communication alignment for **Deltaclub Interlaken (DCI)**, a
paragliding / hang-gliding club. Core purpose: make the website the reliable **live source
of truth for flight-area status** (which launch/landing sites are open + current wind), with
WhatsApp as the real-time signal.

> **Status:** planning complete, build not yet started. Start at
> [`.ai/context/session-state.md`](.ai/context/session-state.md).

## Where things live
- **`.ai/`** — project source of truth (tool-agnostic): personas, communication strategy,
  site vision/IA, legacy-site inventory, conventions, and the continuity/handover doctrine.
- **`specs/001-relaunch/`** — the relaunch [spec](specs/001-relaunch/spec.md) and
  [implementation plan](specs/001-relaunch/plan.md).

## Principles
- **Continuity first** — this repo is public, all accounts are role-based, secrets live in a
  club password manager, and everything is documented so anyone can take over. See
  [`.ai/instructions/07-continuity.md`](.ai/instructions/07-continuity.md).
- **No secrets, no personal data** in the repo. The legacy WordPress export is gitignored.

## Next step
Milestone 0 — the standalone **overview (status) app** (map + wind + per-site status),
built portable and hosted on the maintainer's homelab first. See the plan.
