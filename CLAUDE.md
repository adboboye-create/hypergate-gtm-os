# Hypergate GTM Context OS

## Company

Hypergate (https://hypergate.com) sells Kerberos single sign-on and on-prem file access for managed Android and iOS devices: "a fast, secure and accessible Kerberos Single Sign-On (SSO) solution for Android and iOS" (source: https://hypergate.com/, checked 2026-11-13).

- Products: Hypergate Authenticator (SSO plus self-service AD password reset) and Hypergate Files (SMB/CIFS and NetApp shares on mobile), plus a developer SDK. Both work with the customer's EMM and Active Directory, without extra servers or a cloud broker. Source: `context/docs/research/company.md`.
- Core claim: Android Enterprise has no built-in Kerberos SSO, and Hypergate fills that gap (source: https://hypergate.com/authenticator-sso/, checked 2026-11-13).
- Buyers: "government entities, banking institutions, insurance companies, and law firms" running on-premise or hybrid Active Directory (source: https://hypergate.com/, checked 2026-11-13).
- Owner: "Hypergate is developed and maintained by Papers AG, a software security company located in Zug, Switzerland." (source: https://hypergate.com/about-us/, checked 2026-11-13). The Google Play listing names Papers Group AG, so which entity signs customer contracts is unconfirmed.
- Traction: last public figures are self-reported from January 2024 ("over 50 paying customers", four Fortune 500 companies, more than 30,000 daily active users). Source: `context/docs/research/company.md`. Current figures, pricing, funding and team size: unknown (flagged).
- Full research: `context/docs/research/` (company, customers, competitors, market, signals, voice).

## How this folder works

Root files: `CLAUDE.md` (this file), `README.md` (what the repo is), `.gitignore`, `.env` (secrets, empty, never committed). Local only and ignored by Git: `.claude/settings.local.json`, `.treg/`.

- `.claude/skills/`: reusable Claude skills for repeat GTM tasks, one folder per skill (see Skills below). Read when a task matches a skill.
- `context/icp/`: ideal customer profiles and buyer personas. Read before any targeting, list building or copy.
  - `context/icp/icp.md`: five-layer ICP (firmographic, technographic, intent signals, persona, engagement readiness), not-a-fit list and open questions.
  - `context/icp/personas.md`: champion (mobility/EMM admin), economic buyer (unconfirmed) and influencer (identity/security engineering), with pains, triggers and objections.
  - `context/icp/signal-matrix.md`: signal matrix v0.1 (work in progress): industry segments x personas with angles, scored signals, top five signals to build first, workflow tracker.
- `context/positioning/`: positioning, category, competitors and differentiators. Read before any messaging or competitive work.
  - `context/positioning/value-proposition.md`: job, pain, gain and proof for each persona.
  - `context/positioning/positioning.md`: category, target customer, today's alternative, unique value, proof, positioning statement.
  - `context/positioning/competitors.md`: competitor table, where Hypergate wins and loses, how to respond.
- `context/messaging/`: approved value props, proof points and message house. Read before writing any copy.
  - `context/messaging/messaging.md`: core message, four pillars with proof, angle per persona, words to use and avoid. Draft, not yet approved; no `facts.md` yet.
- `context/brand-kit/`: voice, tone, visual rules and assets. Read before producing anything customer facing.
  - `context/brand-kit/brand.md`: tone of voice and key phrases from Hypergate's own copy. Visual rules not researched.
- `context/docs/`: GTM system design, decision memos and customer stories.
  - `context/docs/case-studies.md`: every customer story found (3 published, 6 logo only, 3 unverified).
  - `context/docs/gtm-system.md`: end-to-end outbound GTM system (12 steps, tools, open decisions, build order).
  - `context/docs/partner-region-policy.md`: decision memo for Hypergate sales on outbound in partner regions.
  - `context/docs/compliance-cold-outreach.md`: research brief for legal on cold email and LinkedIn rules by country (not legal advice).
- `context/docs/research/`: raw research and source material with links. Read when you need to verify or cite a fact.
  - `company.md`, `customers.md`, `competitors.md`, `market.md`, `signals.md`, `voice.md`.
- `knowledge-base/playbooks/`: step by step how-tos for repeatable motions, from the starter kit. Read before running a known motion.
  - `copy-frameworks.md`, `copy-iron-laws.md`, `copy-bans.yaml`, `linkedin-dm-frameworks.md`: copy rules and frameworks.
  - `signal-matrix-framework.md`, `workflow-anatomy.md`: targeting and workflow method.
  - `clay/`: `iron-laws.md`, `expert.md`, `formulas.md`, `prompts.md`, `actions-data-credits.md`.
  - `templates/facts-template.md`: template for `context/messaging/facts.md`.
- `knowledge-base/learnings/`: what worked, what failed and why. Read before planning a new campaign. Empty so far.
- `meetings/`: meeting notes and transcripts, named YYYY-MM-DD-topic.md. Read when context from a conversation is needed. Empty so far.
- `output/campaigns/`: finished and draft campaign deliverables, one folder per campaign. Read when reusing or iterating on past work.
  - `output/campaigns/campaign-strategy.md`: 19 ranked outbound campaign ideas from `/campaign-strategy`, with mother intent, tier, signal source, angle, volume band and difficulty.
- `tools/`: scripts and notes on tool integrations. Read before automating anything.
  - `tools/sequencer-comparison.md`: EmailBison vs Instantly vs PlusVibe, with recommendation.
  - `tools/rex/`, `tools/crawl4ai/`, `tools/agent-browser/`: see Tools below.
- `weekly-priorities/`: one file per ISO week (YYYY-Www.md) with the week's goals. Read at the start of every session.
  - `2026-W46.md`.
- `work-log/`: one file per ISO week, matching the priorities file, with timestamped entries. Write to it after every change.
  - `2026-W46.md`.

## Rules

1. Cite a source (URL or file path) for every company fact.
2. Never invent numbers. If a figure is unknown, write "unknown" and flag it.
3. No em dashes in any copy.
4. Ask before sending or publishing anything.
5. Log every change in this week's work log (`work-log/YYYY-Www.md`).

## Skills

From `bolaji-ships/gtm-starter-kit`. Method docs they read live in `knowledge-base/playbooks/`.

- Research to copy, in order: `/campaign-strategy`, `/signal-matrix`, `/build-workflow-spec`, `/campaign-copy`. Draw the system with `/miro-gtm-flowchart`.
- Clay builds (use `tools/rex`): `/build-clay`, `/prompt-builder`, then `/campaign-contract`, `/design-clay-table-json`, `/import-clay-table`, `/save-clay-schema`.
- Clay costs and data: `/calculate-costs`, `/workspace-cost-audit`, `/export-tables`. Pre-launch check: `/campaign-qa`.
- Research and deliverability: `/crawl4ai`, `/agent-browser`, `/inbox-placement-test`.

## Tools

- GTM stack: to confirm with the team.
- `tools/rex/`: unofficial Python SDK for working inside Clay with your own browser session. Start with `GETTING_STARTED.md`.
- `tools/crawl4ai/`, `tools/agent-browser/`: install guides; both are installed separately.
