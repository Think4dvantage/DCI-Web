# Project Overview — DCI Web (Deltaclub Interlaken relaunch)

## What This Is

This repo drives the **relaunch of the Deltaclub Interlaken (DCI) website**
(`deltaclub-interlaken.ch`) and the alignment of its online communication across the
website and the "Delta Club Interlaken DCI" WhatsApp Community. DCI is a paragliding /
hang-gliding club in the Interlaken region. The legacy site is WordPress 6.2.9 (Neve +
Elementor + The Events Calendar + wpDiscuz); see `context/current-site-inventory.md`.

Audiences and their needs are defined in `context/personas.md` (anchor persona:
**Member Core**). The communication model is defined in `context/communication-strategy.md`
(**Website = durable source of truth; WhatsApp = real-time**).

## Status

**Planning / discovery.** Personas and communication strategy are captured. The relaunch
platform, hosting, and feature scope are decided in the relaunch interview and recorded in
`context/features.md`. No services are deployed from this repo yet.

## Deployed Services

| Service | Image | Purpose | Traefik Route |
|---|---|---|---|
| _(none yet — set after platform decision)_ | | | |

## Constraints that pre-shape the build

- **Continuity is the overriding principle** — see `07-continuity.md`. The repo is
  **public**, all accounts are **role-based/impersonal**, secrets live in a club password
  manager, and nothing is "done" until a stranger could take it over. No secrets and **no
  personal data** in the repo (the `old page/` export is gitignored).
- **Hosting is external, NOT the homelab** — this project is an explicit exception to
  `05-user-profile.md`'s self-hosted/Docker/Traefik/`lg4.ch` philosophy. CMS on managed
  hosting; sub-services on a VPS. The infra conventions in `02-infra-conventions.md` /
  `03-cicd-conventions.md` (Traefik/homelab) do **not** govern this project.
- LF line endings; secrets never committed (only `.env.example`).
- The **Board & Content Volunteers** persona (non-technical maintainers) makes low-friction
  authoring a hard requirement on whatever platform is chosen.

## CI/CD Overview

| Pipeline | Trigger | What it does |
|---|---|---|
| _(TBD after platform decision)_ | | |

Runner: `[self-hosted, lg4]` for homelab deploys (per `03-cicd-conventions.md`).

## Repository Layout (current)

```
DCI-Web/
├── .ai/                 # AI source of truth (this blueprint + DCI context)
│   ├── instructions/    # Conventions (infra, CI/CD, constraints, user profile)
│   ├── context/         # personas.md, current-site-inventory.md,
│   │                    #   communication-strategy.md, features.md, architecture.md
│   └── prompts/         # Workflow prompts (specify → clarify → plan → …)
├── old page/            # Legacy WordPress export (WXR) — migration source
└── Personas.txt         # Legacy persona notes (superseded by .ai/context/personas.md)
```

Deployment artifacts (`docker-compose.yml`, `.github/workflows/`, `.env.example`) are
added once the platform is chosen.
