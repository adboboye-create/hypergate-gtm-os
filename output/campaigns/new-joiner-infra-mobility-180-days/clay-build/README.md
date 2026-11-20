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

The links need a login to the Clay workspace. Workbook and table links are built from the IDs Clay returned; if one doesn't open, use the folder link.

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
| AI answer | infrastructure_it 37, mobile_endpoint 6, not_relevant 3, unclear 1 (held) | Proven on 3 rows first in both pulls; 1 prompt fix after a spot check |
| Candidates | 43 | |
| **Ready to Contact?** (max 2 per company) | **42**: cell A (mobility) 7, cell B (infrastructure) 35 | 1 dropped by the 2-per-company rule |
| **Ready for Email?** | **18** (cell B 16, cell A 2) | Of the 33 Ready to Contact in email markets: 7 public sector (email held until legal answers), 8 without a sendable email (1 email-domain mismatch in review, 1 held for a likely false positive, the rest not found or not looked up) |
| LinkedIn only | 23 | Canada 9 plus public-sector and no-email rows |
| Held / Dropped | 38 / 7 | Held: Germany, Austria, DPOs, AI unclear |

### Fill rates

| Measure | Rate |
|---|---|
| Company enrichment | 78 of 79 (99%) |
| Work email found | 59 of 75 rows looked up (79%) |
| Work email found among AI-checked rows | 33 of 47 (70%) |
| AI role check passes | 43 of 47 (91%) |
| Emails found that are usable for email | 18 of 59 (31%). 18 were found in Germany and Canada on the first run, before the market gate existed, and can't be emailed |

### Cost (Clay credits)

"Spent" counts every paid run from the work log, including force re-runs and the 8 deleted duplicate rows. Clay's cells only keep each cell's latest run, so a cost read from the table today shows less.

| Step | Spent | Per unit |
|---|---|---|
| Enrich company | 85 (75 first run, 1 re-proof, 9 new companies) | 1 per company. About 7 credits went on duplicate companies before dedupe |
| Email waterfall (find + Findymail verify) | about 156.5 (152 first run, 1.5 re-proof, 3 new) | about 2.7 per email found; lookups that find nothing are refunded |
| AI role check (GPT-4.1 Mini) | 9.8 (47 rows, 2 prompt-fix re-runs, 1 row after the intern fix) | 0.2 per row |
| AI on Grok 4.1 (rejected by Clay) | 0 | refunded |
| Search, lookups, formulas, Send to Companies | 0 | free |
| **Total** | **about 251** | **about 6.0 per Ready to Contact person, about 14 per Ready for Email person** |

The cost per contactable person is high because the first run (2026-11-19) enriched duplicate companies and found emails before the market and role gates existed: 18 emails went to people we can't email, and lookups ran on DPOs. The second pull, with every gate in place, cost about 14 credits (9 enrich, 1.4 AI, 3 email) for 7 new cell A contacts, 2 of them email-ready.

### What this shows

- The gate works: 59 rows have an email, but only 18 are sendable.
- Cell A now has 7 contacts, after the mobility titles were added.
- One AI answer looks wrong: "MDM & RDM Analyst" passed as mobile_endpoint, but "RDM" suggests master data, not mobile devices. Its email hasn't been looked up; the row needs a decision (prompt rule or manual hold).
- Nothing has been sent. Blockers: legal sign-off, partner-region decision, facts.md approval, the 9 customer domains, copy (pending), sequencer choice.

Full history: `work-log/2026-W47.md` (entries from 2026-11-20).
