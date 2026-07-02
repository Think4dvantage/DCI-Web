# Continuity & Handover — Bus-Factor Doctrine

**Overriding goal:** any capable person must be able to take over DCI's web + comms with
**no tribal knowledge and no dependency on any individual** — including if the current
maintainer disappears overnight. Continuity outranks convenience.

This principle governs the whole DCI-Web project and applies to every decision.

---

## 1. Public repository

The repo is **public**. Consequences (hard rules):

- **No secrets in the repo, ever** — API keys, passwords, tokens live in the club password
  manager (see §3), referenced by name only. `.env` gitignored; only `.env.example`.
- **No personal data in the repo** — member data, emails, comments, the WordPress export.
  - The legacy export `old page/*.xml` contains personal data (author emails, commenters,
    possibly members). It **must be gitignored** and stored privately. It is currently
    untracked — keep it that way; never commit it to the public repo.
- Assume every commit is world-readable and permanent. Scrub before, not after.

## 2. Impersonal, role-based accounts

Every account, domain, service login, and API integration is owned by a **club role**, not
a person.

- Use role addresses: e.g. `webmaster@deltaclub-interlaken.ch`, `vorstand@…`,
  `praesident@…` — never a personal Gmail. (Current anti-pattern: WP admin is a personal
  `@gmail.com`.)
- Domain registrar, DNS, hosting, VPS, CMS admin, WhatsApp community ownership, social
  accounts, wind-data (lenti.cloud, winds.mobi), XContest club, analytics — all under role
  ownership with credentials in the shared password manager.
- No integration depends on a personal developer account or a personal API key.
- At least **two board members** always have access to every critical account (no
  single point of failure).

## 3. Secrets & credential management

- One club **password manager** (e.g. Bitwarden/Vaultwarden org) is the single source of
  truth for all credentials, shared with the board/role holders.
- The repo references *where* a secret lives and *what role owns it* — never the value.
- Document credential **rotation** and **handover** steps per service.

## 4. Documentation standard (definition of done)

Nothing is "done" until a stranger could run it. Every service/component ships with:

- **README/runbook**: what it is, how to run/deploy it, its dependencies, its env vars,
  how to rotate its secrets, how to recover it.
- Entry in the **ownership registry** (§5).
- Plain-language "how to change the common things" notes for non-technical volunteers
  (e.g. "how to flip a launch site to closed", "how to post news").

## 5. Ownership registry (`docs/ownership.md` — to create)

A committed, always-current inventory (no secret values) of:

| Asset | Type | Role owner | Where credentials live | Notes |
|---|---|---|---|---|
| domain deltaclub-interlaken.ch | domain/DNS | webmaster | pw-manager | registrar X |
| CMS (WordPress) | hosting | webmaster | pw-manager | provider Y |
| status service | VPS service | webmaster | pw-manager | repo Z |
| … | | | | |

Covers: domains, DNS, hosting, VPS, CMS, sub-services (status, gastschulen), WhatsApp
community, social accounts, wind sources, XContest club, analytics, email addresses.

## 6. Onboarding a new maintainer (`docs/onboarding.md` — to create)

A single doc that takes a new volunteer from zero to productive: repo layout, how to get
credential access, how to run each service locally, how to deploy, who to contact.

---

## Definition of "handover-ready" (acceptance gate for the relaunch)
- [ ] Repo public with zero secrets/personal data
- [ ] Every account role-based; ≥2 board members hold access to each critical account
- [ ] All credentials in the club password manager; rotation documented
- [ ] Ownership registry complete and current
- [ ] Each service has a runbook; onboarding doc exists
- [ ] Non-technical "how to do the common tasks" guide exists for volunteers
