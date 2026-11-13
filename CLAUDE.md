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

- `.claude/skills/`: reusable Claude skills for repeat GTM tasks. Read when a task matches a skill.
- `context/icp/`: ideal customer profiles and buyer personas. Read before any targeting, list building or copy.
- `context/positioning/`: positioning, category, competitors and differentiators. Read before any messaging or competitive work.
- `context/messaging/`: approved value props, proof points and message house. Read before writing any copy.
- `context/brand-kit/`: voice, tone, visual rules and assets. Read before producing anything customer facing.
- `context/docs/research/`: raw research and source material with links. Read when you need to verify or cite a fact.
- `knowledge-base/playbooks/`: step by step how-tos for repeatable motions. Read before running a known motion.
- `knowledge-base/learnings/`: what worked, what failed and why. Read before planning a new campaign.
- `meetings/`: meeting notes and transcripts, named YYYY-MM-DD-topic.md. Read when context from a conversation is needed.
- `output/campaigns/`: finished and draft campaign deliverables, one folder per campaign. Read when reusing or iterating on past work.
- `tools/`: scripts and notes on tool integrations. Read before automating anything.
- `weekly-priorities/`: one file per ISO week (YYYY-Www.md) with the week's goals. Read at the start of every session.
- `work-log/`: one file per ISO week, matching the priorities file, with timestamped entries. Write to it after every change.

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
