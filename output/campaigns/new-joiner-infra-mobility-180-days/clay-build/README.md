# Clay build: New in role, infrastructure and mobility (180 days)

Spec: [../workflow-spec.md](../workflow-spec.md) (STRUCTURE-APPROVED 2026-11-20, copy pending). Build guide: [new-joiner-infra-mobility-180-days-clay-build-guide.md](new-joiner-infra-mobility-180-days-clay-build-guide.md). Diagram: [new-joiner-infra-mobility-180-days-clay-flow.png](new-joiner-infra-mobility-180-days-clay-flow.png).

## Clay links

| What | Link |
|---|---|
| Workspace folder | https://app.clay.com/workspaces/1206365/home/f_0too2hlcYvMge63yz2T |
| Workbook "Hypergate · New joiner infra and mobility (180 days)" | https://app.clay.com/workspaces/1206365/workbooks/wb_0too2hqE6A9WA6UQCp8 |
| Table: Exclusion & Block list | https://app.clay.com/workspaces/1206365/workbooks/wb_0too2hqE6A9WA6UQCp8/tables/t_0topxuyxz6fadCao9d7 |
| Table: People (main table) | https://app.clay.com/workspaces/1206365/workbooks/wb_0too2hqE6A9WA6UQCp8/tables/t_0torupffE645kbSrVwk |
| Table: Companies | https://app.clay.com/workspaces/1206365/workbooks/wb_0too2hqE6A9WA6UQCp8/tables/t_0tose66FtiXahD5gC9D |
| Workflow: Hypergate · Load new joiners to Audiences (manual trigger, run as routine `workflow:wf_0tp0mx49VhNtGBKNhnM`) | https://app.clay.com/workspaces/1206365/terracotta/tc-workflows/wf_0tp0mx49VhNtGBKNhnM |
| Audience segment: Hypergate · Ready to Contact, no email yet (`audseg_0tp0n0q4kjc8CvDpV3j`, dynamic) | Audiences > People > segments |
| Workflow: Hypergate · Email second try (segment trigger, Wiza, Findymail verify, 2 branches, write-back) | https://app.clay.com/workspaces/1206365/terracotta/tc-workflows/wf_0tp0n2d6yAhMeMQvwXd |

## Audiences and Workflows (added 2026-11-24)

Why each surface: [clay-tables-audiences-workflows.md](../../../../context/docs/clay-tables-audiences-workflows.md).

```mermaid
flowchart LR
  T[People table<br/>search, gates, AI, routing] -->|routine: Load new joiners| A[(Audiences: 87 people<br/>+ Hypergate fields)]
  A --> S{{Segment: Ready to Contact,<br/>email market, not public sector,<br/>no email, no lookup result}}
  S -->|person enters| W1[Find email<br/>Wiza, LinkedIn profile]
  W1 --> C1{Email found?}
  C1 -->|yes| V[Verify<br/>Findymail]
  C1 -->|no| N1[Write: not found]
  V --> C2{Verified?}
  C2 -->|yes| Y[Write: email found]
  C2 -->|no| N2[Write: not verified]
  Y & N1 & N2 -->|Email Lookup filled| X[Leaves segment]
```

- Audiences people fields added: Hypergate Ready to Contact (boolean), Hypergate Market, Hypergate Public Sector (boolean), Hypergate Cell, Hypergate Status, Hypergate Email Lookup, Hypergate Clay Row ID. Matched on LinkedIn URL, so a re-load updates rather than duplicates.
- The segment started with 6 people: Ready to Contact, email market, not public sector, but the table's 5-provider waterfall found no email.
- Workflow run on all 6 (2026-11-24): 1 email found and verified (written to Audiences), 3 found but not verified by Findymail (not written), 2 not found. All three branches used; the segment drained to 0. Cost: 12 data credits and 8 action credits in total. Published: it now runs by itself for anyone who enters the segment (for example after the next search pull is loaded).
- Write-back of fixed text needs a code node (Label: ...) feeding the write step; a reference with no variable passes validation but writes nothing.
- The verified email found by the workflow is in Audiences only. The People table still shows that person as LinkedIn only.
- Third pull (2026-11-24): after reloading all 126 people, 2 new people entered the segment. The live trigger did not start runs within about 5 minutes, so the published version was run on them by hand (`runs test --audience-segment --live`): 1 not found, 1 not verified. Whether segment entry caused by another workflow's write fires the trigger is unconfirmed.

The links need a login to the Clay workspace. Workbook and table links are built from the IDs Clay returned; if one doesn't open, use the folder link.

## Current totals (read from Clay on 2026-11-24, all rows, after the third pull)

| Measure | Count |
|---|---|
| People | 126 (87 + 39 from the third pull: UK 12, CH 11, DE 7, FR 6, CA 3) |
| Companies | 111 |
| Ready to Contact | 53 (cell A Mobility 8, cell B Infrastructure 45) |
| Ready for Email | 26 |
| Status | Held 61 · Ready to send 26 · LinkedIn only 24 · Dropped 12 · Review: email domain 3 |
| Spend on 2026-11-24 | About 68 credits for the third pull (Enrich company 32, AI about 5, email waterfall about 31) and 15 for the Audiences email workflow (8 runs), 83.2 in total, read from the workspace balance |

The 2026-11-20 scorecard below is kept as history; its totals are superseded by this table.

## Results scorecard (read from Clay on 2026-11-20, all rows)

Two pulls: the first (2026-11-19) with infrastructure, architect, DPO and mobility-manager titles, 77 people; the second (2026-11-20) added 9 mobility titles and appended 10 new people (only people the search hadn't returned before).

> **Correction (2026-11-20):** an earlier version of this scorecard said 70 companies and 70 Enrich company credits. Those figures were read from the Companies table's first view, which is filtered ("ICP Pass"). Over all rows, the first run created 77 company rows with no dedupe (7 domains twice or more) and enriched 75 of them. Dedupe on `Company Domain` was switched on afterwards, which removed 8 duplicate rows.

### Funnel

| Step | Count | Note |
|---|---|---|
| Free people search, imported | 87 people | UK 50, Canada 17, Germany 12, Switzerland 8 |
| Companies (deduped on domain) | 79 | Enriched 78 of 79; 1 row has no domain |
| Not on the never-contact list | 86 of 87 | 1 row has no domain, so it can't be checked and is held back |
| Company passes size, industry, not agency | 80 of 87 people | 7 fail (one company is 10,001+ staff; the rest have no company match) |
| Role group | infrastructure 49, DPO 26 (held), mobility 11, other 1 | Mobility went from 1 to 11 after the title change |
| Market | email 58, LinkedIn-only 17 (Canada), held 12 (Germany, Austria) | Compliance follows the person's country |
| Eligible for the AI role check | 47 | All free gates passed, not DPO |
| AI answer | infrastructure_it 37, mobile_endpoint 5, not_relevant 4, unclear 1 (held) | Proven on 3 rows first in both pulls; 2 prompt fixes after spot checks (architects in any industry; MDM next to data words = master data) |
| Candidates | 42 | |
| **Ready to Contact?** (max 2 per company) | **41**: cell A (mobility) 6, cell B (infrastructure) 35 | 1 dropped by the 2-per-company rule |
| **Ready for Email?** | **18** (cell B 16, cell A 2) | Of the 32 Ready to Contact in email markets: 7 public sector (email held until legal answers), 7 without a sendable email (1 email-domain mismatch in review, the rest not found) |
| LinkedIn only | 22 | Canada 9 plus public-sector and no-email rows |
| Held / Dropped | 38 / 8 | Held: Germany, Austria, DPOs, AI unclear |

### Fill rates

| Measure | Rate |
|---|---|
| Company enrichment | 78 of 79 (99%) |
| Work email found | 59 of 75 rows looked up (79%) |
| Work email found among AI-checked rows | 33 of 47 (70%) |
| AI role check passes | 42 of 47 (89%) |
| Emails found that are usable for email | 18 of 59 (31%). 18 were found in Germany and Canada on the first run, before the market gate existed, and can't be emailed |

### Cost (Clay credits)

"Spent" counts every paid run from the work log, including force re-runs and the 8 deleted duplicate rows. Clay's cells only keep each cell's latest run, so a cost read from the table today shows less.

| Step | Spent | Per unit |
|---|---|---|
| Enrich company | 85 (75 first run, 1 re-proof, 9 new companies) | 1 per company. About 7 credits went on duplicate companies before dedupe |
| Email waterfall (find + Findymail verify) | about 156.5 (152 first run, 1.5 re-proof, 3 new) | about 2.7 per email found; lookups that find nothing are refunded |
| AI role check (GPT-4.1 Mini) | 10.0 (47 rows, 3 prompt-fix re-runs, 1 row after the intern fix) | 0.2 per row |
| AI on Grok 4.1 (rejected by Clay) | 0 | refunded |
| Search, lookups, formulas, Send to Companies | 0 | free |
| **Total** | **about 251** | **about 6.1 per Ready to Contact person, about 14 per Ready for Email person** |

The cost per contactable person is high because the first run (2026-11-19) enriched duplicate companies and found emails before the market and role gates existed: 18 emails went to people we can't email, and lookups ran on DPOs. The second pull, with every gate in place, cost about 14 credits (9 enrich, 1.4 AI, 3 email) for 6 new cell A contacts (after the master-data fix), 2 of them email-ready.

### What this shows

- The gate works: 59 rows have an email, but only 18 are sendable.
- Cell A now has 6 contacts, after the mobility titles were added.
- One AI answer was wrong ("MDM & RDM Analyst" passed as mobile_endpoint). A prompt rule now treats MDM next to data words as master data; the row re-ran as not_relevant and is dropped.
- The email waterfall now skips public-sector rows, whose email is held until legal answers.
- Nothing has been sent. Blockers: legal sign-off, partner-region decision, facts.md approval, the 9 customer domains, copy (pending), sequencer choice.

Full history: `work-log/2026-W47.md` (entries from 2026-11-20).
