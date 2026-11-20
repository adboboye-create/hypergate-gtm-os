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

## Results scorecard (read from Clay on 2026-11-20)

### Funnel

| Step | Count | Note |
|---|---|---|
| Free people search, imported | 77 people | Started current role in the last 6 months; UK 44, Canada 15, Germany 10, Switzerland 8 |
| Companies (deduped on domain) | 70 | Enrich company succeeded on 70 of 70 (100%) |
| Not on the never-contact list | 76 of 77 | 1 row has no domain, so it can't be checked and is held back |
| Company passes size, industry, not agency | 71 of 77 people | 6 people's company didn't match in the lookup |
| Role group | infrastructure 49, DPO 26 (held), mobility 1, other 1 | Only 1 mobility title found, so cell A is empty |
| Market | email 52, LinkedIn-only 15 (Canada), held 10 (Germany, Austria) | Compliance follows the person's country |
| Eligible for the AI role check | 40 | All free gates passed, not DPO |
| AI answer | infrastructure_it 36, not_relevant 3, unclear 1 (held) | Proven on 3 rows first; 1 prompt fix after a spot check |
| Candidates | 36 | |
| **Ready to Contact?** (max 2 per company) | **35**, all cell B | 1 dropped by the 2-per-company rule |
| **Ready for Email?** | **16** | Of the 27 Ready to Contact in email markets: 5 public sector (email held until legal answers), 6 without a sendable email (1 email-domain mismatch in review) |
| LinkedIn only | 18 | Canada 8, public sector 5, no sendable email 5 |
| Held / Dropped | 36 / 6 | Held: Germany, Austria, DPOs, AI unclear |

### Fill rates

| Measure | Rate |
|---|---|
| Company enrichment | 70 of 70 (100%) |
| Work email found (first waterfall run) | 57 of 72 rows run (79%) |
| Work email found among AI-checked rows | 31 of 40 (78%), the other 9 recorded "not found" |
| AI role check passes | 36 of 40 (90%) |
| Emails found that are usable for email | 16 of 57 (28%). 18 were found in Germany and Canada before the market gate existed, and can't be emailed |

### Cost (Clay credits, measured per cell)

| Step | Runs | Net credits | Per unit |
|---|---|---|---|
| Enrich company | 70 + 1 re-proof | 71 | 1 per company |
| Email waterfall (find + Findymail verify) | 72 rows + 1 re-proof | 153.5 | about 2.7 per email found (no-data lookups refunded) |
| AI role check (GPT-4.1 Mini) | 42 cells (40 rows + 2 re-runs) | 8.4 | 0.2 per row |
| AI on Grok 4.1 (rejected by Clay) | 3 | 0 | refunded |
| Search, lookups, formulas, Send to Companies | | 0 | free |
| **Total** | | **about 233** | **about 6.7 per Ready to Contact person, about 14.6 per Ready for Email person** |

The cost per contactable person is high because the first run (2026-11-19) found emails before the market and role gates existed: 18 emails went to people we can't email, and lookups ran on DPOs. With the current run conditions, the waterfall only runs on Ready to Contact people in email markets.

### What this shows

- The gate works: 57 rows have an email, but only 16 are sendable.
- The play is cell B only until mobility titles are added to the search.
- Nothing has been sent. Blockers: legal sign-off, partner-region decision, facts.md approval, the 9 customer domains, copy (pending), sequencer choice.

Full history: `work-log/2026-W47.md` (entries from 2026-11-20).
