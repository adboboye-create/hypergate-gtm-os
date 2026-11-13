# Workflow spec: Intune migration leaves file shares behind

**Status:** STRUCTURE-APPROVED 2026-11-13 · E1, E2, E3 approved · LinkedIn pending · facts.md claims pending Hypergate approval

Approval note: the user approved sections 1 to 3 and told Claude to "do the best thing" for the rest, so sections 4 to 7 are Claude's recommendations, approved by delegation. Re-open any section before `/campaign-copy` if it needs a change.

Built with `/build-workflow-spec` from idea #1 in [campaign-strategy.md](../campaign-strategy.md) (Tier 1, S3 + D3, Easy). Signal: U1 in [signal-matrix.md](../../../context/icp/signal-matrix.md). Method: [workflow-anatomy.md](../../../knowledge-base/playbooks/workflow-anatomy.md).

**Read first**
- No sends until legal signs off the compliance brief and Hypergate sales answers the partner-region memo ([gtm-system.md, Open decisions 2 and 3](../../../context/docs/gtm-system.md)).
- `context/messaging/facts.md` does not exist yet. Every customer name, number or proof point stays a `{{placeholder}}` until it is approved there.
- This file holds structure only. No copy. Copy is written by `/campaign-copy`, which reads this file.

---

## 1. Mother intent [ENGINE]

**An organisation has posted a job in the last 30 days that names a move of its mobile fleet to Microsoft Intune.**

- Catalog match: *Hiring specific roles* ([workflow-anatomy.md, Mother Intent Catalog](../../../knowledge-base/playbooks/workflow-anatomy.md)). The trigger is read from the text of the job post, not the job title.
- Why it matters: "Intune lacks a built-in solution for accessing SMB/CIFS network file shares", and the file tools tied to the old EMM ("Ivanti (MobileIron) Docs@Work", "BlackBerry Work", "VMware Workspace ONE Content", "SOTI Hub") stay behind with it (source: https://hypergate.com/blog/simplify-intune-migration-with-hypergate-files-for-on-prem-access/, via [signals.md S8](../../../context/docs/research/signals.md)).
- Lead product: Hypergate Files. "Hypergate Files is completely EMM-agnostic" (source: https://hypergate.com/blog/mobile-file-access-acronis-cyber-files/, via [signals.md S8](../../../context/docs/research/signals.md)).
- Why only moves *to Intune*: the source fact is about Intune. A move between two other EMMs (for example Workspace ONE to Ivanti) does not carry it, so it is out of this workflow.

## 2. Inclusion / exclusion [ICP]

### Include

| Filter | Value | Source |
|---|---|---|
| Markets | UK, FR, US, CA, CH. CH is included pending legal; nothing sends before legal signs off anyway | [compliance-cold-outreach.md §1, §12.4](../../../context/docs/compliance-cold-outreach.md) |
| Industries | Banking (S1), police (S2), government administration (S3), utilities and critical infrastructure (S4), insurance, law firms | [icp.md §1](../../../context/icp/icp.md); [signal-matrix.md 1a](../../../context/icp/signal-matrix.md) |
| Size | 250+ employees. INFERRED working floor: the ICP has no minimum (icp.md open question 1) and the smallest known customer has about 240 to 306 staff | [icp.md §1](../../../context/icp/icp.md) |
| Trigger | Job post, last 30 days, description matches the Intune migration pattern (signal T1) | Section 4 |
| Recipient | Champion: head or lead of EUC, endpoint, mobility, workplace or client engineering. Fallback: IT infrastructure manager. Max 2 contacts per account | [personas.md](../../../context/icp/personas.md) |

### Exclude

| Who | Why |
|---|---|
| Hypergate customers (logo wall in [case-studies.md](../../../context/docs/case-studies.md) plus `{{customer_blocklist}}` from Zoho CRM, blocked until the connector is authorised) | Never cold-email a customer |
| Hypergate's 28 listed partners ([company.md §7](../../../context/docs/research/company.md)) | Partners, not prospects |
| Job posts placed by staffing agencies, recruiters or MSPs | The poster is not the organisation doing the migration |
| Accounts with an open deal (`{{active_pipeline}}`) | Sales already owns them |
| iOS-only fleets: post mentions iOS or iPhone and never mentions Android (signal G3) | Apple ships Kerberos SSO for free; weak fit ([icp.md Not a fit](../../../context/icp/icp.md)) |
| HQ in DE, AT, IT or any EU country not cleared | Opt-in markets. Route to the partner or the no-pitch LinkedIn path, not this email workflow ([compliance-cold-outreach.md §12.4](../../../context/docs/compliance-cold-outreach.md)) |
| Accounts contacted in the last 90 days by any Hypergate workflow | Suppression window |

## 3. Sources [ENGINE]

| What | Source | Note |
|---|---|---|
| Trigger | TheirStack Jobs API, regex over the full job description, `posted_at_max_age_days = 30`, country filter, through a Clay HTTP API column | Same build as SM U1. Free tier 200 credits/month; about $59/month for 1,500 ([signal-matrix.md 2a](../../../context/icp/signal-matrix.md)) |
| Backup trigger | Clay Find Jobs (PredictLeads, Google Jobs) | Max 4 keywords via Google Jobs |
| Company data | Clay company enrichment: domain, name, employee count, industry, HQ country | Feeds G1, G2 and the industry context |
| People | Clay Find People with the champion titles above | Feeds the recipient |
| Emails | Find-and-verify waterfall | [gtm-system.md §7](../../../context/docs/gtm-system.md) |

## 4. Signals table [ENGINE]

Every read is a regex, a boolean or a lookup. All regexes are case-insensitive and run on the full job description (`job_description`) unless stated.

| # | Signal | Role | How it's read | Output |
|---|---|---|---|---|
| T1 | Intune migration named | trigger | Regex: `(migrat\w*\|transition\w*\|mov(e\|ing)\|switch\w*\|consolidat\w*\|roll(ing)?\s?out)[^.]{0,80}\bintune\b` OR `\bintune\b[^.]{0,40}(migration\|rollout\|transition\|onboarding)` | boolean |
| G1 | Company size | trigger (gate) | `employee_count >= 250` | boolean |
| G2 | HQ market allowed | trigger (gate) | `hq_country` in {GB, FR, US, CA, CH} | boolean |
| G3 | Not iOS-only | trigger (gate) | Fails only if `\b(ios\|iphone\|ipad)\b` matches AND `\bandroid\b` does not match | boolean |
| G4 | Not an agency post | trigger (gate) | Company domain is not in the agency/MSP list AND company name does not match `\b(recruit\w*\|staffing\|personnel\|talent)\b` | boolean |
| R1 | Old EMM named | router | Four regexes, counted as distinct matches. **Ivanti:** `\bmobileiron\b\|\bivanti\s*(epmm\|uem\|neurons for mdm)\b\|\bepmm\b`. **Workspace ONE:** `\bworkspace\s?one\b\|\bairwatch\b\|\bomnissa\b`. **BlackBerry:** `\bblackberry\s*(uem\|work\|dynamics\|enterprise)\b\|\bbes\s?12\b`. **SOTI:** `\bsoti\b\|\bmobicontrol\b` | enum, see clusters |
| C1 | File shares named in the post | context-clause | Regex: `\b(smb\|cifs\|file\s?shares?\|network\s?(drive\|share)s?\|netapp\|file\s?server)\b` | boolean |
| C2 | Job title | context-clause | TheirStack `job_title`, as posted | text |
| C3 | Segment | context-clause | Clay industry mapped to S1 to S4, insurance, law, other | enum |

**R1 clusters (count of distinct old-EMM matches)**

| Count | Output value | Meaning |
|---|---|---|
| 1, Ivanti regex | `ivanti` | Leaving Ivanti EPMM / MobileIron for Intune |
| 1, Workspace ONE regex | `workspace_one` | Leaving Workspace ONE / AirWatch for Intune |
| 1, BlackBerry regex | `blackberry` | Leaving BlackBerry UEM for Intune |
| 1, SOTI regex | `soti` | Leaving SOTI MobiControl for Intune |
| 0 or 2+ | `not_named` | No single old EMM can be named with certainty, so copy names none |

C1, C2 and C3 never route. They may add one line of colour in copy, and only in the rows where they are present.

## 5. Routing matrix with angles [ENGINE]

One axis (R1), five cells. No second axis: file-share mention (C1) changes a line, not the narrative.

| Cell | Deterministic read | What it tells us (inferred situation) | The angle it earns |
|---|---|---|---|
| A. Ivanti | T1 = true, R1 = `ivanti` | They are moving devices from Ivanti EPMM (MobileIron) to Intune. If phones reach file shares today, it is probably through Docs@Work, which is part of the Ivanti stack and does not move to Intune | When Ivanti goes, Docs@Work goes with it. Hypergate Files keeps phone access to the same SMB shares under Intune, against the shares they already run |
| B. Workspace ONE | T1 = true, R1 = `workspace_one` | They are moving from Workspace ONE (AirWatch) to Intune. Phone access to shares probably runs through Workspace ONE Content, which stays behind | Workspace ONE Content does not come along to Intune. Hypergate Files gives the same shares on phones under Intune, with any EMM after that |
| C. BlackBerry | T1 = true, R1 = `blackberry` | They are moving from BlackBerry UEM to Intune. File access on phones probably runs through BlackBerry Work, which stays behind | BlackBerry Work stays with BlackBerry. Hypergate Files puts the same file shares on phones under Intune |
| D. SOTI | T1 = true, R1 = `soti` | They are moving from SOTI MobiControl to Intune. Shared files on devices probably come through SOTI Hub, which stays behind | SOTI Hub stays with SOTI. Hypergate Files gives the same shares on devices under Intune |
| E. Not named | T1 = true, R1 = `not_named` | They are moving to Intune. We do not know from where, so we do not know which file tool they use today | Intune has no built-in access to SMB file shares. Is phone access to file shares on the migration plan? Hypergate Files covers it on any EMM |

**Branch coverage**
- Cells A to D can use `{{old_emm}}` and `{{old_file_tool}}`. Cell E cannot: its angle names no old product.
- The tool names come from the Hypergate source in section 1, not from the job post. Copy must not say the prospect *uses* the tool, only that it stays with the old EMM (infer what they are doing, not what they own).
- `{{job_title}}` exists in every cell. `{{file_share_mentioned}}` exists in every cell but is often false: copy needs a fallback line for false.
- No proof point exists in any cell until `facts.md` approves one. York Regional Police shows a MobileIron integration, not an Intune migration, so it is not proof for cell A ([icp.md §5](../../../context/icp/icp.md)).

**Niche-native test:** each angle names the exact file tool that the move to Intune leaves behind. A generic file-sharing or SSO vendor could not send it unchanged.

## 6. Variables contract [ENGINE]

| Variable | Source field | Exists in branches |
|---|---|---|
| `{{first_name}}` | Clay Find People `first_name` | A, B, C, D, E |
| `{{company_name}}` | Clay company enrichment `name`, cleaned (no "Inc", "AG", "Ltd") | A, B, C, D, E |
| `{{job_title}}` | TheirStack `job_title` (C2) | A, B, C, D, E |
| `{{old_emm}}` | R1 display name: "Ivanti", "Workspace ONE", "BlackBerry", "SOTI" | A, B, C, D |
| `{{old_file_tool}}` | Lookup on R1: ivanti → "Docs@Work", workspace_one → "Workspace ONE Content", blackberry → "BlackBerry Work", soti → "SOTI Hub" (source in section 1) | A, B, C, D |
| `{{file_share_mentioned}}` | C1 boolean | A, B, C, D, E (fallback needed when false) |
| `{{segment}}` | C3 enum | A, B, C, D, E (context only) |
| `{{proof_point}}` | `context/messaging/facts.md` | None until approved |

Internal only, never in copy: `job_url`, `job_posted_date`, `r1_match_count`, `hq_country`, `employee_count`.

## 7. Cadence & channel [ENGINE]

- **Periodicity:** always-on. TheirStack pull every Monday with a 30-day lookback; dedupe by company domain so a company enters once per signal.
- **Channel:** email plus LinkedIn, on the skeleton in [gtm-system.md §8](../../../context/docs/gtm-system.md): Email 1 (day 1), LinkedIn connection with no pitch (day 2), Email 2 (day 4), LinkedIn DM (day 7, only if connected), Email 3 (day 10).
- **No verified email:** LinkedIn steps only.
- **Reply on any channel:** stop all steps for that contact, pause other contacts at the account, go to reply handling ([gtm-system.md §9](../../../context/docs/gtm-system.md)).
- **No reply:** mark "no response", suppress for 90 days. Re-enter only on a new, higher-tier signal.
- **Volume:** Low to Medium, under 25 to 100 accounts a month (INFERRED band from [campaign-strategy.md](../campaign-strategy.md)). Real count unknown until the first TheirStack pull.

---

## Definition of done

- [x] Mother intent: one sentence, signal-led, matched to the catalog
- [x] Inclusion: ICP box + trigger definition + recipient, tagged [ICP]
- [x] Exclusion: who's out and why
- [x] Sources: trigger + every enrichment
- [x] Signals table: every read deterministic, every role declared
- [x] Count clusters declared for R1
- [x] Routing matrix with the angle column complete
- [x] Branch coverage checked per cell
- [x] Variables contract: every variable mapped to its source field
- [x] Engine/ICP markers on every section
- [x] Cadence & channel declared

**Next:** `/campaign-copy` on this file. Before copy: create `context/messaging/facts.md` (template in `knowledge-base/playbooks/templates/facts-template.md`).

---

## Copy

Written with `/campaign-copy`. Every claim traces to [facts.md](../../../context/messaging/facts.md) (F1 to F8), which is a draft pending Hypergate approval. No customer names: none are authorized. Variables follow section 6.

**Campaign:** Intune migration leaves file shares behind. **Register:** signal play, technical peer voice. **Spelling:** American until Hypergate confirms.

### Email 1 (day 1, new thread). Approved 2026-11-13

**Subject** (static, same for the whole thread): `{intune and file shares|file shares after intune|file shares on intune}`

**Body**

```
{{first_name}},

{{e1l1}}

{{e1l2}}

Hypergate Files {gives|brings} phones the same on-prem SMB and Windows shares under Intune, with no extra servers, proxies or middleware.

{Is phone access to file shares part of the Intune plan?|Are file shares on phones part of the Intune plan?|Is file-share access from phones in scope for the Intune move?}

{{sender_signature}}
```

**{{e1l1}}: mother intent (dynamic, exhaustive on R1, no fallback)**
- + R1 = `ivanti` / `workspace_one` / `blackberry` / `soti` (cells A to D): "From the {{job_title}} role {{company_name}} has open, it reads like devices are moving from {{old_emm}} to Intune."
- + R1 = `not_named` (cell E): "From the {{job_title}} role {{company_name}} has open, it reads like devices are moving to Intune."

**{{e1l2}}: what stays behind (dynamic, exhaustive on R1, no fallback)**
- + A, R1 = `ivanti`: "If phones reach file shares through Docs@Work today, my guess is that piece stays behind with Ivanti, since Intune has no built-in way to reach SMB shares."
- + B, R1 = `workspace_one`: "If file shares on phones run through Workspace ONE Content today, that probably doesn't make the move, because Intune has no built-in way to reach SMB shares."
- + C, R1 = `blackberry`: "Could be off, but if BlackBerry Work is how phones open file shares today, it stays with BlackBerry, and Intune has no built-in way to reach SMB shares."
- + D, R1 = `soti`: "If devices get shared files through SOTI Hub today, that likely stays with SOTI, since Intune has no built-in way to reach SMB shares."
- + E, R1 = `not_named`: "Intune has no built-in way to reach SMB file shares, so my guess is phone access to them needs its own answer in the move."

Facts used: F1, F2, F4. Word counts: A 72, B 70, C 71, D 69, E 66.

### Email 2 (day 4, same thread). Approved 2026-11-13

**Subject:** `Re:` + the Email 1 subject (unchanged).

**Body**

```
{{first_name}},

{{e2l1}}

With Hypergate Files, they open them in Word, Excel or the PDF app {with no extra viewer|without a separate viewer}, and there's a version built for Intune.

{It works with SMB2/SMB3 shares and NetApp backends.|It supports SMB2/SMB3 shares and NetApp backends.}

{Worth a look before the cutover?|Would that be useful before the cutover?|Worth seeing before the cutover?}

{{sender_signature}}
```

**{{e2l1}}: file shares in the post (dynamic on C1, with fallback)**
- + C1 `file_share_mentioned` = true: "The {{job_title}} posting names file shares as part of the work, so I'm guessing phone users will need them after the move too."
- FALLBACK: "If staff open files from the network shares on their phones today, they'll probably expect the same after the move to Intune."

Facts used: F5, F6, F7. Word counts: 58 (C1 true), 57 (fallback).

### Email 3 (day 10, same thread). Approved 2026-11-13

**Subject:** `Re:` + the Email 1 subject (unchanged).

**Body** (static, spintax on every line)

```
{{first_name}},

{Last note from me on this.|I'll leave it here after this one.|One last note on this.}

{If you're unsure it fits your devices and shares, Hypergate tests it with you on your own setup.|If fit is the question, Hypergate tests it with you on your own devices and shares.}

{If file access on phones sits with someone else on the team, who should I ask?|If someone else owns file access on phones, who would that be?}

{{sender_signature}}
```

Facts used: F9. Word counts: 41 to 46.
