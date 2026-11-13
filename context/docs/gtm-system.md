# Hypergate outbound GTM system

Version 1, 2026-11-13. Built on [icp.md](../icp/icp.md) and [personas.md](../icp/personas.md), and on the research those files cite (`context/docs/research/`). The method follows [workflow-anatomy.md](../../knowledge-base/playbooks/workflow-anatomy.md): mother intent, then ICP filter, then secondary enrichment, then narrative routing.

**How to read this**

- **Tools.** The GTM stack is not confirmed yet (CLAUDE.md "Tools"). Each tool is tagged:
  - **[kit]**: already in this repo.
  - **[proposed]**: a recommendation that needs team sign-off.
  - **[open]**: no choice made yet.
- **Settings vs facts.** Numbers marked *setting* are starting values to tune from results. They are not facts about Hypergate.
- **Decisions.** Every decision is written as **Question → answer → what happens next**.

## Overview

```
0 Context OS ─► 1 Signals ─► 2 Find companies ─► 3 Enrich ─► 4 ICP fit check
                                                                   │
        ┌──────────────────────────────────────────────────────────┘
        ▼
5 Route by segment ─► 6 Find people ─► 7 Find + verify emails ─► 8 Sequence (email + LinkedIn)
                                                                   │
        ┌──────────────────────────────────────────────────────────┘
        ▼
9 Reply handling ─► 10 CRM ─► 11 Weekly feedback loop ─► back to 0
```

One Clay workbook per mother intent (signal). All workbooks share the same fit check, people, email and CRM steps, so a new signal reuses the whole downstream pipeline.

---

## 0. Context OS

**What happens:** every step reads its rules from these files, and nothing is hard-coded in a tool. The ICP must-haves, segments, personas, proof and exclusions all live in the files listed here.

| File | Used by step |
|---|---|
| `context/icp/icp.md` | 1 (signals), 4 (fit gates, not-a-fit), 5 (readiness tiers, proof) |
| `context/icp/personas.md` | 6 (titles), 8 (pains), 9 (objections) |
| `context/docs/research/` | Every fact used in copy (CLAUDE.md rule 1) |
| `context/messaging/`, `context/brand-kit/` | 8 (copy). **Empty today: they must be built before step 8** |
| `knowledge-base/playbooks/` | Method for 1 to 8 (signal matrix, workflow anatomy, copy laws, Clay iron laws) |
| `knowledge-base/learnings/` | Written by step 11, read by step 1 when planning |
| `output/campaigns/<slug>/workflow-spec.md` | One per workflow. Step 5 routing and step 8 copy live here |

**Tool:** this repo plus Claude Code [kit]. Skills in order: `/signal-matrix` → `/campaign-strategy` → `/build-workflow-spec` → `/campaign-copy`, then `/campaign-contract` → `/design-clay-table-json` → `/import-clay-table`, then `/campaign-qa` before launch.

**Decisions**

- Does `context/icp/signal-matrix.md` exist?
  - No → run `/signal-matrix` first. Steps 1 and 5 need it to turn signals into Clay inputs with exact data sources.
  - Yes → go to step 1.
- Are `context/messaging/` and `context/brand-kit/` filled?
  - No → steps 1 to 7 can run and fill tables, but step 8 is blocked.
  - Yes → step 8 can run.
- Has a workflow spec reached STRUCTURE-APPROVED?
  - No → no copy, no Clay build.
  - Yes → build.

---

## 1. Buying signals (mother intents)

**What happens:** each signal from icp.md §3 becomes one always-on workflow with a fixed source and schedule. Signal = why now. Signals come before any company list (Approach 2 in workflow-anatomy, "Intent first → ICP"), because the ICP must-haves can't be seen from outside (icp.md §5).

| # | Signal (icp.md §3) | Source and how to detect | Tool | Run every (*setting*) | Tier (icp.md §5) |
|---|---|---|---|---|---|
| W1 | Acronis Cyber Files / Files Connect EOL | Job posts naming "Acronis Files"; Acronis forum threads; old Acronis case studies (SG S9) | Clay jobs search [kit]; `crawl4ai` / `agent-browser` for forums and case studies [kit] | Weekly until 2026-12-31, then monthly | Ready now |
| W2 | NTLM on mobile paths | Job posts with "NTLM", "Kerberos migration", "IAKerb"; developer posts with "SPNEGO" (SG S5) | Clay jobs search [kit] | Weekly | Ready now |
| W3 | EMM migration | Job posts "Intune migration", "migrate from Workspace ONE / MobileIron / BlackBerry UEM" (SG S8) | Clay jobs search [kit] | Weekly | Warming |
| W4 | Frontline / shared-device rollout | Zebra and Samsung customer news; rugged-device tenders (SG S3) | `crawl4ai` on vendor press pages [kit]; tender source [open] | Monthly | Warming |
| W5 | Android Enterprise / BYOD | Job posts "Android Enterprise", "work profile", "COPE", "fully managed" (SG S1, S2) | Clay jobs search [kit] | Weekly | Warming |
| W6 | Sovereignty / no cloud broker | Public cloud-exit policies; DACH/EU tenders mentioning "on-premises" and "mobile device management" (SG S4) | `crawl4ai` [kit]; EU TED and Swiss simap tenders [open, not yet searched, SG "Gaps"] | Monthly | Warming |
| W7 | Lookalikes of named customers | Peers of the logo-wall customers: police forces, state chancelleries, EU institutions, public insurers, utilities (CU §2) | Clay lookalike / company search [kit] | Quarterly | Fit only |

**Decisions**

- Is the signal detectable in a named source? (Kit rule: "Must verify tech is detectable", workflow-anatomy L1.)
  - No → it is not a workflow. Log it in learnings.
  - Yes → run a test pull before building.
- Does the test pull return enough accounts that pass step 4?
  - Unknown → run once, count, then decide.
  - Too few to sustain a sequence → merge it as a secondary enrichment into another workflow (workflow-anatomy L3).
  - Enough → build it as a workflow.
- Is today past 2026-12-31 for W1?
  - Yes → change the angle from "updates stop" to "running unsupported since 1 Jan". Same audience.
  - No → keep the deadline angle.
- Is the signal one of S6/S7 (RC4, certificate mapping)?
  - Yes → not a workflow, because their deadlines have passed (icp.md §3). Use as enrichment only.

---

## 2. Finding companies

**What happens:** each workflow turns its signal hits into company rows, one row per domain, in that workflow's Clay Companies table.

**Tool:** Clay Companies table [kit]. Built with `/build-clay` or `/design-clay-table-json` + `/import-clay-table`, run through `tools/rex` [kit].

**Decisions**

- Does the signal hit (job post, article, tender) resolve to a company domain?
  - No → drop the row and record it as "unresolved" for data-quality counts.
  - Yes → normalise the domain and continue.
- Is the domain already in the global account list (any workflow, CRM, or suppression)?
  - Customer, partner, or open deal → suppress (see step 10). Do not enrich.
  - In another active workflow → attach the new signal to the existing account and do not create a second row. Signal stacking happens on the account.
  - Contacted within the suppression window (*setting*) → hold. Re-enter only if the new signal is a different, higher tier.
  - New → continue to step 3.
- Is it a parent company or a subsidiary?
  - Subsidiary with its own IT → treat it as its own account.
  - Unknown → keep the parent and flag for manual review.

**Suppression list seeds:**

- The 9 logo-wall customers (CU §1).
- The 28 listed partners (CO §7).
- EMM vendors that are partners: Microsoft, Ivanti, SOTI, 42Gears, Samsung, Omnissa, BlackBerry, Techstep, Kace, PushManager (CO §4).
- Competitors from competitors.md §2.

---

## 3. Enrichment

**What happens:** add the 2 to 4 secondary signals that decide fit (step 4) and routing (step 5). The kit rule is to stack no more than 4 (workflow-anatomy L3).

| Enrichment | Feeds | Source | Tool |
|---|---|---|---|
| Industry, country, headcount | Step 4 firmographic gate, step 5 proof and language | Clay company enrichment | Clay [kit] |
| On-prem AD evidence: careers / job text mentions "Active Directory", "Kerberos", "on-prem", "PKI/NDES/SCEP" (SG S4, S7 detection) | Step 4 must-have 1 | Job posts, careers pages | Claygent prompt built with `/prompt-builder` [kit] |
| EMM in use: job text names Intune, Workspace ONE, MobileIron/Ivanti, BlackBerry UEM, SOTI, Knox (CO §4) | Step 4 must-have 2, step 5 angle | Job posts | Claygent [kit] |
| Device and OS clues: Zebra, Samsung, Android Enterprise, BYOD, iOS only | Step 4 not-a-fit check, step 5 | Job posts, vendor news | Claygent [kit] |
| Second signal: any other W1 to W7 hit on the same domain | Step 5 priority | Shared account list | Clay lookup across tables [kit] |
| Partner region: country matched to the partner table (CO §7) | Step 5 routing | Static lookup in this repo | Clay formula [kit] |

**Decisions**

- Does a paid column prove itself on one row that should qualify and one that should be rejected? (`/import-clay-table` rule.)
  - No → fix the prompt or source before running on more rows.
  - Yes → run, within budget (`/calculate-costs`).
- Does the Claygent answer include a source URL?
  - No → store as "unknown", never "yes". This is the clean data rule.
  - Yes → store the answer with its URL.

---

## 4. ICP fit check

**What happens:** each account gets one of four results: **Pass**, **Pass-provisional**, **Hold** or **Fail**. Gates run in order and stop at the first Fail.

**Tool:** Clay formula columns over the step 3 enrichments [kit]. The fit result is a single column with a reason.

| Gate | Question | Answers → next |
|---|---|---|
| G1 Exclusions (icp.md "Not a fit") | Cloud-only identity? Acronis Cyber Files **Cloud** only? iOS-only fleet? Everything SaaS? | Any yes with a source → **Fail**, store the reason. Weaker-fit flags (iOS only, already on Entra App Proxy or Okta) → continue, but tag `weaker_fit` |
| G2 On-prem / hybrid AD (must-have 1) | Evidence of on-prem or hybrid AD? | Yes → continue. Unknown → go to G5 |
| G3 Managed fleet (must-have 2) | Evidence of an EMM, and is it on the supported list (CO §4)? | Supported EMM → continue. Unsupported EMM → **Hold**, flag for manual check. Unknown → go to G5 |
| G4 Industry (icp.md §1) | Core, proven-adjacent, or other? | Core or adjacent → continue. Other → only allowed with a Ready-now signal, else **Hold** |
| G5 Unknown handling | Are G2 or G3 unknown? | Both known → **Pass**. One or both unknown and a Ready-now signal (W1, W2) → **Pass-provisional**: the first email asks to confirm fit. Unknown with only a Warming or Fit-only signal → **Hold** and re-check when a new signal arrives |

Size is **not** a gate. There is no evidence for a minimum (icp.md open question 1). Record headcount anyway so step 11 can find a threshold.

**Decisions after the gates**

- Fail → keep the row with its reason and never send. The not-a-fit reasons feed step 11.
- Hold → no outreach. The account re-enters at step 4 when a new signal attaches to it.
- Pass or Pass-provisional → step 5.

---

## 5. Routing by segment

**What happens:** each passing account gets one route, made of three parts: trigger (angle and product), proof (industry), and channel owner (direct or partner). Routes and their angles are fixed in the workflow spec (`/build-workflow-spec`, cell = route).

**Tool:** Clay formula columns [kit], driven by `output/campaigns/<slug>/workflow-spec.md`.

**Part A, trigger.** When an account has several signals, the highest tier wins (icp.md §5). Within the same tier, W1 beats W2 because its date is fixed.

| Trigger | Product lead | Angle source | Proof to attach |
|---|---|---|---|
| W1 Acronis EOL | Files | SG S9 | None exists (icp.md §5). Use the migration guide (SG S9) |
| W2 NTLM | Authenticator; SDK if in-house app evidence | SG S5. Framed as "already breaking" (icp.md §3) | None tied to NTLM |
| W3 EMM migration | Files + Authenticator | SG S8 ("Intune lacks a built-in solution for accessing SMB/CIFS") | York Regional Police (integration, CU §3.3) |
| W4 Frontline | Authenticator | SG S3 | Maersk Drilling (CU §3.2) |
| W5 Android Enterprise / BYOD | Authenticator | SG S1, S2 | Jefferies (quotes are about the work profile, CU §3.1) |
| W6 Sovereignty | Authenticator, Files | SG S4 | Logos only (CU §2) |
| W7 Lookalike | Authenticator | Core gap: "Android Enterprise has no built-in Kerberos SSO" | Closest logo by sector (CU §2) |

**Part B, proof by industry.** This overrides the Part A proof when there is a closer match:

- Police → York Regional Police.
- Bank → Jefferies.
- Offshore, energy or shift work → Maersk Drilling.
- Anything else → the Part A proof.

**Part C, channel owner**

- Is the country covered by a listed partner (CO §7)?
  - No → direct outreach.
  - Yes → **[open] policy decision for Hypergate sales** (options memo: [partner-region-policy.md](partner-region-policy.md)):
    - Option 1: send direct and notify the partner.
    - Option 2: hand the account to the partner.
    - Option 3: co-branded outreach.
  - Until decided → direct, logged as partner-region in the CRM so it can be re-routed.
- Language? The site and 2026 posts exist in EN, DE, FR and IT (CO §9, SG S13).
  - DE/AT/German-speaking CH → German.
  - FR/French-speaking CH → French.
  - IT/Italian-speaking CH → Italian.
  - Else → English.
  - **Rule:** non-English copy needs a native reviewer before launch. If none is available, send English.

---

## 6. Finding people

**What happens:** find up to 3 people per account (*setting*), one per persona role. Route-specific titles come first.

**Tool:** Clay People table via Find People, with a Claygent fallback for accounts with thin LinkedIn data (the `/build-clay` two-path design) [kit]. Apollo is an alternative source [proposed; connector present, not authorised].

| Role (personas.md) | Titles to search | Route tweaks |
|---|---|---|
| Champion (contact first) | Mobility / EMM / MDM / EUC engineer or manager, Security Administrator, mobile device management lead | W1: add file services / infrastructure. W4: add field operations IT |
| Influencer | Identity / Active Directory / PKI engineer, platform security engineering | W2: add Android / mobile app development lead (SDK) |
| Economic buyer (test thread) | Head of EUC / mobility, CISO, CIO. **Hypotheses only** (personas.md §2) | One per account, tagged `eb_test`, so step 11 can learn who engages |

**Decisions**

- Champion found?
  - Yes → they are the primary contact.
  - No → the influencer becomes primary.
  - Neither → the account goes back to Hold. Do not email the economic buyer alone.
- Is the person still in the role? (Check the start date or the latest profile data.)
  - No or unknown → drop them, or re-search once.
- Is the person already in the CRM?
  - Yes → follow the CRM status (step 10). Never contact twice across workflows.

---

## 7. Finding and verifying emails

**What happens:** find a work email with a waterfall, then verify it. Every contact that reaches the sequencer has a verified email or is LinkedIn-only.

**Tool:** Clay email waterfall [kit]. Verification with LeadMagic, then BounceBan only on rows LeadMagic marks invalid or unverified (the `/campaign-qa` pattern) [kit]. Sending-domain health with `/inbox-placement-test` (EmailBison + MailReach) [kit, if EmailBison is chosen].

**Decisions**

- Email found?
  - No → LinkedIn-only track.
  - Yes → LeadMagic.
- LeadMagic result:
  - Valid → send.
  - Invalid or unverified → BounceBan.
- BounceBan result:
  - Deliverable → send.
  - Risky or catch-all → LinkedIn-only, or a low-volume test batch (*setting*). Track the bounce rate separately.
  - Undeliverable → LinkedIn-only.
- Is the domain a public-sector or government domain?
  - Yes → flag for the compliance rule below.
  - No → normal handling.
- **Compliance gate [awaiting legal sign-off].** Research brief: [compliance-cold-outreach.md](compliance-cold-outreach.md). It is research for legal review, not legal advice. Until legal signs off: no sends.
  - **Germany, Austria and Italy require consent for B2B email.** German and Italian sources extend this to LinkedIn messages. In these core markets there is no cold email and no cold sales DM.
  - Switzerland, France, the UK, the US and Canada are "yes with conditions". The conditions are in the brief.
  - Every other EU country is unresearched, so treat it as No.
  - The brief proposes an `outreach_regime` column in Clay, set from the account's country, plus gates G7-C1 to C8 that replace this line once legal approves.
  - Every row must also store the email's source and collection date, which the GDPR Art. 14 notice needs.
  - LinkedIn's User Agreement bans automated messaging tools. This limits the LinkedIn tool choice in step 8.

---

## 8. The sequence (email and LinkedIn)

**What happens:** one sequence per route, written with `/campaign-copy` from the approved spec. Facts in copy come only from research files. Copy rules: `knowledge-base/playbooks/copy-iron-laws.md`, `copy-bans.yaml`, `linkedin-dm-frameworks.md`, and no em dashes (CLAUDE.md rule 3).

**Tools:**

- Email sequencer **[open]**. The kit supports Instantly, PlusVibe or EmailBison (`/campaign-qa`).
- LinkedIn **[open]**. Manual via Sales Navigator to start [proposed]. Add an automation tool only after the team chooses one.
- Pre-launch: `/campaign-qa` against the spec [kit].

**Skeleton** (day numbers are a *setting*; the final cadence is set in each spec):

| Day | Channel | Content |
|---|---|---|
| 1 | Email 1 | Signal line (route trigger) + core gap + one question. Pass-provisional accounts: the question confirms fit (e.g. on-prem AD, which EMM) |
| 2 | LinkedIn | Connection request, no pitch |
| 4 | Email 2 | Proof (step 5 Parts A/B) or, if none, how it works: "no extra servers or middleware" (VO §4) |
| 7 | LinkedIn DM | One forward-looking question tied to the trigger (`/campaign-copy` DM rule) |
| 10 | Email 3 | Objection pre-empt for the persona (personas.md), short close |

**Decisions**

- Email verified?
  - Yes → full sequence.
  - No → LinkedIn steps only.
- Connection accepted?
  - Yes → send the DM on day 7.
  - No by day 7 → skip the DMs and stay on email.
- Any reply on any channel?
  - Yes → stop all steps for that contact and go to step 9.
  - No → continue.
- Reply from one contact at an account?
  - Yes → pause the other contacts at that account until step 9 decides.
- Sequence finished with no reply?
  - Yes → mark "no response" and suppress for the window (*setting*). Re-enter only on a new, higher-tier signal.
- Does a dynamic line lack its data?
  - Yes → use the spec's fallback line (`/campaign-copy` "FALLBACK, never BASE").

---

## 9. Reply handling

**What happens:** every reply is classified the same business day. Each class leads to exactly one action.

**Tool:** the sequencer's unified inbox [open]. Claude can draft a class and a suggested reply, but a person sends every reply (CLAUDE.md rule 4).

| Reply class | Action | Then |
|---|---|---|
| Positive / meeting | Book the meeting. Hand to the account owner with the signal, route and thread | CRM: Meeting booked |
| Referral ("talk to X") | Add X as a contact, open a warm thread that names the referrer | CRM: contact added; the referrer's title feeds the economic-buyer learning |
| Objection | Match it to personas.md objections and answer with the research pointer listed there. New objection → log it verbatim | CRM: In conversation; the objection text goes to step 11 |
| Not now / timing | Ask for the timing, set a follow-up task | CRM: Nurture; re-enter on the date or on a new signal |
| Wrong person | Ask who owns it; mark the contact | CRM: contact role = wrong; re-run step 6 at the account |
| Not a fit (no AD, no Android, cloud-only) | Thank them and close | CRM: Disqualified + reason. Reason → icp.md "Not a fit" review in step 11 |
| Already a customer or partner contact | Stop, apologise, alert the account owner | Fix suppression: a data defect, logged in step 11 |
| Partner-region conflict | Stop, follow the step 5 Part C policy | CRM: partner-owned |
| Unsubscribe / angry | Remove from everything immediately | Global suppression in CRM and sequencer |
| Out of office | Pause until the return date, then resume | No status change |
| Bounce | Mark the email invalid; try LinkedIn | Counts toward the verification quality metric |

---

## 10. The CRM

**What happens:** the CRM is the single source of truth for who exists, who was contacted, and why. Clay and the sequencer read suppression from it and write outcomes to it.

**Tool: Zoho CRM** (chosen 2026-11-13). The Zoho CRM connector on the Claude account must be authorised in claude.ai connector settings before Claude can read or write it. Once authorised, the first job is to pull Hypergate's real customer and partner list into suppression (open decision 4).

| Object | Required fields |
|---|---|
| Account | Domain (unique key), country, industry, headcount, fit result + reason + source URLs, tier, route, partner region, status (Prospect / Customer / Partner / Competitor / Disqualified) |
| Contact | Email, verification result, LinkedIn URL, persona role, `eb_test` flag, status |
| Signal | Type (W1 to W7), date seen, source URL, linked account |
| Activity | Campaign name (`{Workflow} - {Angle} - {Version}`, workflow-anatomy), step, reply class |
| Deal | Opened from a positive reply; source signal and route are copied onto the deal for attribution |

**Decisions**

- Does the account already exist (matched by domain)?
  - Yes → update it, never duplicate.
  - No → create it.
- Is the account status Customer, Partner or open Deal?
  - Yes → suppressed in every workflow (step 2).
- Did a meeting happen?
  - Yes → open a Deal with the source signal and route.
  - No → stays in its activity status.
- Who owns the account after a meeting?
  - **[open]**: Hypergate sales owner or partner (see step 5 Part C).

---

## 11. Weekly feedback loop

**What happens:** every week, results flow back into the Context OS files, so the next week's targeting, gates and copy change based on evidence.

**Tool:** Claude Code in this repo [kit]. Inputs:

- A CRM export.
- A sequencer export.
- The Clay tables (`/export-tables`, `/calculate-costs`, `/workspace-cost-audit`).

**Weekly numbers, per workflow and per route:**

- Signal hits.
- Accounts that pass step 4, broken down by gate result.
- Contacts found.
- Verified email rate.
- Sends.
- Replies by class.
- Meetings.
- Clay cost per meeting.

**Where each learning goes**

| Learning | Written to |
|---|---|
| Results, what worked, what failed | `knowledge-base/learnings/YYYY-Www.md` (new file each week) |
| Titles that replied, referred or booked (especially `eb_test`) | `context/icp/personas.md`: answers open question 1 (who signs) |
| New objections, verbatim | `context/icp/personas.md` objection tables (replace "inferred" with "heard") |
| Not-a-fit reasons from replies and Fails | `context/icp/icp.md` "Not a fit" |
| Headcount of accounts that booked meetings | `context/icp/icp.md` §1: replaces "no stated minimum" once there is data |
| Signals that produce meetings vs nothing | `context/icp/icp.md` §3 urgency and §5 tiers (evidence replaces INF) |
| Suppression misses, bounces, unresolved domains | Data-quality section of the learnings file; fix at source |
| Next week's priorities | `weekly-priorities/YYYY-Www.md` |
| Every change made | `work-log/YYYY-Www.md` (CLAUDE.md rule 5) |

**Decisions**

- Did a workflow produce zero Pass accounts for 3 weeks running (*setting*)?
  - Yes → pause it, or demote it to enrichment.
- Does a route get replies but no meetings?
  - Yes → change copy: a new spec version, same structure.
- Does a route get no replies at all?
  - Yes → check deliverability first (`/inbox-placement-test`), then the angle.
- Is the bounce rate above the sender threshold (*setting*)?
  - Yes → stop sends on that route and fix step 7.
- Did a fact in copy turn out wrong?
  - Yes → fix the research file first, then every spec that cites it.

---

## Check against the four pillars

| Pillar | How the design meets it | Status | Gap to close |
|---|---|---|---|
| **Clean data** | One row per domain (step 2). CRM is the source of truth for suppression (step 10). Claygent answers stored only with a source URL, else "unknown" (step 3). Two-step email verification (step 7). Fit reason stored for every Fail (step 4). Data defects logged weekly (step 11) | Partial | CRM not chosen, so there is no live suppression yet. The customer list is only the 9 public logos, while the 2024 figure was "over 50 paying customers" (CO §9): Hypergate's real customer list is needed before the first send |
| **Always-on signals** | Seven signal workflows on fixed schedules (step 1). New signals attach to existing accounts and can lift Held accounts back in (steps 2, 4) | Partial | No signal has been test-pulled yet, so volumes are unknown. Tender sources (TED, simap) not searched. W1 has a hard end date, so it is time-boxed, not always-on |
| **Composable workflows** | Signal workflows plug into one shared pipeline (steps 2 to 10). Routes are spec cells, so new routes are added without new infrastructure. Kit skills cover each build step | Strong | Shared tables across workbooks (the cross-table account lookup in step 3) must be proven in Clay on real rows |
| **Tight feedback loops** | Weekly loop writes every learning type to a named file (step 11). Replies classified same-day with defined actions (step 9). Attribution from signal to deal (step 10) | Partial | The loop can only run once a sequencer and CRM are chosen and exporting. Win/loss data (icp.md open question 3) needs the Deal object |

## Open decisions (blocking, in order)

1. **Stack:**
   - CRM: **Zoho CRM**, decided 2026-11-13. Its connector needs authorising.
   - Email sequencer: EmailBison recommended, if it confirms EU-only hosting and a DPA covering EU transfer clauses (SCCs), Swiss data law and its full subprocessor list in writing. Otherwise Instantly. See `tools/sequencer-comparison.md`.
   - LinkedIn tool: open.
2. **Compliance:** lawful basis, opt-out wording and sender entity for cold email in DACH/EU and to public bodies (step 7). Research brief for legal: `context/docs/compliance-cold-outreach.md`, with 18 questions for legal. No sends until signed off. **Impact:** DE, AT and IT are opt-in, so outreach in core DACH markets needs an opt-in route (LinkedIn connect without a pitch, phone in DE, inbound) rather than cold email. Hypergate also needs a privacy notice for prospects, and possibly an EU representative under GDPR Art. 27.
3. **Partner policy** in partner regions (step 5 Part C, step 10). With Hypergate sales: [partner-region-policy.md](partner-region-policy.md).
4. **Customer list** from Hypergate for suppression (step 2). Pull it from Zoho CRM once the connector is authorised.
5. **Messaging and brand-kit files** (step 0), which `/campaign-copy` needs.
6. **Signal matrix** (`/signal-matrix`) and test pulls for W1 to W7 (step 1).
7. **Native reviewers** for DE/FR/IT copy (step 5).

## Build order

1. Close open decisions 1 to 4.
2. `/signal-matrix`.
3. Test-pull W1 and W2: Ready now, and W1 runs out on 2026-12-31.
4. `/build-workflow-spec` for W1.
5. Fill messaging/brand-kit, then `/campaign-copy`.
6. Clay build.
7. `/campaign-qa`.
8. Launch.
9. Run the first weekly loop.
10. Repeat steps 3 to 8 for W3 to W7.
