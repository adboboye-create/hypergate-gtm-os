# Workflow spec: Intune migration leaves file shares behind

**Status:** COPY-APPROVED 2026-11-13 · section 2 contact titles and 180-day rule added 2026-11-17 (user) · Clay-readiness fixes applied 2026-11-17 (sections 2 to 7; trigger, routing cells and copy unchanged) · facts.md claims (F1 to F9) pending Hypergate approval · no sends until legal and partner decisions

Approval note: the user approved sections 1 to 3 and told Claude to "do the best thing" for the rest, so sections 4 to 7 are Claude's recommendations, approved by delegation. Re-open any section before `/campaign-copy` if it needs a change.

Built with `/build-workflow-spec` from idea #1 in [campaign-strategy.md](../campaign-strategy.md) (Tier 1, S3 + D3, Easy). Signal: U1 in [signal-matrix.md](../../../context/icp/signal-matrix.md). Method: [workflow-anatomy.md](../../../knowledge-base/playbooks/workflow-anatomy.md).

**Read first**
- No sends until legal signs off the compliance brief and Hypergate sales answers the partner-region memo ([gtm-system.md, Open decisions 2 and 3](../../../context/docs/gtm-system.md)).
- Claims come only from [facts.md](../../../context/messaging/facts.md) (draft, F1 to F9 pending Hypergate approval). It has no authorized customer names, so no proof point appears in the copy.
- Sections 1 to 7 are the structure. The approved copy (written with `/campaign-copy`) is under "Copy" at the end.

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
| Markets | UK, FR, US, CA, CH (company HQ, gate G2). CH is included pending legal; nothing sends before legal signs off anyway. **CA is LinkedIn-only**: CASL implied consent needs a conspicuously published address, and waterfall-found emails do not qualify, so Canadian contacts never enter the email steps | [compliance-cold-outreach.md §1, §12.1, §12.4](../../../context/docs/compliance-cold-outreach.md) |
| Contact location | The contact's own country must also be GB, FR, US, CH or CA (CA LinkedIn-only). A contact at a US company who sits in Germany is dropped: the compliance regime follows the person as well as the account | [compliance-cold-outreach.md §12.1](../../../context/docs/compliance-cold-outreach.md) |
| Industries | Banking (S1), police (S2), government administration (S3), utilities and critical infrastructure (S4), insurance, law firms. Checked by gate G5 on Clay's industry value, mapping in section 4 ("C3 / G5 industry mapping"). Industry `other` fails | [icp.md §1](../../../context/icp/icp.md); [signal-matrix.md 1a](../../../context/icp/signal-matrix.md) |
| Size | 250+ employees. INFERRED working floor: the ICP has no minimum (icp.md open question 1) and the smallest known customer has about 240 to 306 staff. In Clay searches use the size buckets 201-500 and above (250 is not a bucket), then gate G1 checks `employee_count >= 250` after Enrich Company | [icp.md §1](../../../context/icp/icp.md) |
| Trigger | Job post, last 30 days, description matches the Intune migration pattern (signal T1) | Section 4 |
| Recipient | Champion: head or lead of EUC, endpoint, mobility, workplace or client engineering. Fallback: IT infrastructure manager. Max 2 contacts per account. Exact titles to target and exclude: see "Contact job titles" below | [personas.md](../../../context/icp/personas.md) |

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

**How Clay applies these exclusions.** One Exclusions table, uploaded as a CSV with columns `Company Name | Domain | Type` (Type: `customer`, `partner`, `agency`, `open_deal`), matched on **domain** only (plain `acme.com`).
- Load now: the 9 logo-wall customers ([case-studies.md](../../../context/docs/case-studies.md)), the 28 listed partners ([company.md §7](../../../context/docs/research/company.md)) and any staffing agencies or MSPs found during testing. Leave a domain blank rather than guess it; fill it from the company's own website before the first send.
- Load later: `{{customer_blocklist}}` and `{{active_pipeline}}` from Zoho CRM, once the connector is authorised. Until then the customer list is only the public logos: no sends.
- 90-day suppression: no shared cross-workflow table exists yet, so for now it is checked only within this workflow (a lookup on `last_contacted_at` in this campaign's People table). Replace it with the CRM check when Zoho is connected.

### Contact job titles (added 2026-11-17)

These are the people to find at each account (Clay Find People), not the job post. The post's own title is `{{job_title}}` (signal C2). Matching is case-insensitive on the current title. Pick at most 2 contacts per account, Priority 1 first, then Priority 2 only if Priority 1 finds fewer than 2.

**New joiners only (added 2026-11-17, user decision).** Every contact, Priority 1 and Priority 2, must have joined the account's company in the last 180 days: company start date on or after today minus 180 days. Read it from the start date of the current position in Clay Find People (Clay's "max months in current role" filter set to 6, as in [signal-matrix.md U6](../../../context/icp/signal-matrix.md)), then check it with a formula on the start date. Caveats:
- "Months in current role" can reset on an internal move. If the profile shows an earlier role at the same company, the person did not just join: exclude them. People search does not return work history, so this needs Enrich Person (paid): run it only on contacts that already passed every other gate, then a formula flags any earlier role whose company domain equals the account domain.
- Start dates are month-level and can lag ([signal-matrix.md U6](../../../context/icp/signal-matrix.md)). Missing start date → exclude, never assume.
- This rule is the user's choice, not a sourced finding. There is no evidence yet that new joiners convert better ([signal-matrix.md U6](../../../context/icp/signal-matrix.md): "no evidence it triggers purchases"). It will also leave more accounts with no contact; those go to Hold.

**Target**

| Priority | Titles (any seniority from senior engineer up to head of) | Why | Source |
|---|---|---|---|
| 1. Champion | EUC / End User Computing (engineer, lead, manager, head) | Owns the device fleet and the EMM move | [gtm-system.md §6](../../../context/docs/gtm-system.md); [personas.md §1](../../../context/icp/personas.md) |
| 1. Champion | Mobility / Enterprise Mobility / Mobile Device Management / MDM / EMM (engineer, lead, manager) | Same | [gtm-system.md §6](../../../context/docs/gtm-system.md); [personas.md §1](../../../context/icp/personas.md) |
| 1. Champion | Endpoint (engineer, engineering lead, manager, head of endpoint management) | Same; matches the job-post titles in signal U1 | [signal-matrix.md U1](../../../context/icp/signal-matrix.md) |
| 1. Champion | Client Engineering / Client Platform (engineer, lead, manager) | Same | [signal-matrix.md U1](../../../context/icp/signal-matrix.md) |
| 1. Champion | Intune Engineer / Intune Administrator; Modern Workplace or Digital Workplace (engineer, lead, manager) | Run the Intune side of the move | INFERRED: no source names these titles |
| 1. Champion | Security Administrator, only where the profile headline (from Enrich Person) matches `\b(mobile\|mobility\|mdm\|emm\|intune\|endpoint)\b` | The York Regional Police contact held this title | [personas.md §1](../../../context/icp/personas.md) (CU §3.3) |
| 2. Fallback | IT Infrastructure Manager / Head of IT Infrastructure; File Services, Storage or Windows Server (lead, manager) | Owns the SMB shares that Files connects to; gtm-system adds "file services / infrastructure" for the Files-led route | [gtm-system.md §6](../../../context/docs/gtm-system.md) (W1 route tweak) |

**Exclude** (drop the contact even if a target word also matches)

| Exclude titles containing | Why | Source |
|---|---|---|
| Intern, student, apprentice, trainee, graduate, working student | Not a decision maker or owner | INFERRED |
| Recruiter, talent, HR, people partner | Posted the job; not running the migration | INFERRED (same reason as the agency exclusion above) |
| Sales, account executive, account manager, business development, presales, marketing | Not the buyer persona | INFERRED |
| Help desk, service desk, desktop support, 1st line, 2nd line, support technician | Supports users; does not own the EMM or the shares | INFERRED |
| Freelance, contractor, interim, consultant (when the employer is an agency or MSP) | Not the organisation doing the migration | INFERRED (same reason as the agency exclusion above) |
| CIO, CTO, CISO, IT Director, VP IT | Economic buyer is unconfirmed; gtm-system says not to email the economic buyer alone, and this workflow sends to the champion only | [gtm-system.md §6](../../../context/docs/gtm-system.md); [personas.md §2](../../../context/icp/personas.md) |
| Former, ex-, retired, or a current role that started at a different company than the account | No longer at the account | [gtm-system.md §6](../../../context/docs/gtm-system.md) ("Is the person still in the role?") |

No Priority 1 or Priority 2 contact who joined in the last 180 days → the account goes to Hold, per [gtm-system.md §6](../../../context/docs/gtm-system.md). Never fall back to an excluded title, or to someone who joined more than 180 days ago, to fill the 2 slots.

## 3. Sources [ENGINE]

| What | Source | Note |
|---|---|---|
| Trigger | TheirStack Jobs API, **broad pull**: description contains "intune", posted in the last 30 days (`posted_at_max_age_days = 30`), job country in GB, FR, US, CA, CH. Each returned job becomes **one row in a Jobs table** (write the HTTP response's job list out to rows, or send it into a Clay webhook table). The precise T1 regex then runs **inside Clay as a formula** on `job_description`, so the match is free, repeatable and checkable. Confirm TheirStack's exact request field names and whether it offers a recruiting-agency filter before the build | Same build as SM U1. Free tier 200 credits/month; about $59/month for 1,500 ([signal-matrix.md 2a](../../../context/icp/signal-matrix.md)) |
| Backup trigger | Clay Find Jobs (PredictLeads, Google Jobs) | Max 4 keywords via Google Jobs. Test one row first: T1, G3, R1 and C1 all need the **full** job description. If Find Jobs returns only a snippet, use it as a list of companies to check, not as a trigger |
| Exclusions | Exclusions table from CSV (`Company Name \| Domain \| Type`), matched on domain | See section 2, "How Clay applies these exclusions" |
| Company data | Clay Enrich Company: domain, name, employee count, industry, HQ country | Feeds G1, G2, G5 and C3. Once per company, in a Companies table deduped on domain |
| People | Clay Find People, started from the Companies table view of companies that passed G1 to G5 and Exclusions. Filters: contact job titles (include and exclude, section 2), person country, start date of current role 6 months or less, max 2 results per company | Feeds the recipient |
| Person history | Clay Enrich Person (paid), only on contacts that passed every other gate | Internal-move check (180-day rule) and the Security Administrator headline check |
| Emails | Find-and-verify waterfall, only on rows where `Ready to Contact?` is true and the contact is not Canadian | [gtm-system.md §7](../../../context/docs/gtm-system.md) |

## 4. Signals table [ENGINE]

Every read is a regex, a boolean or a lookup. All regexes are case-insensitive and run on the full job description (`job_description`) unless stated.

| # | Signal | Role | How it's read | Output |
|---|---|---|---|---|
| T1 | Intune migration named | trigger | Regex: `(migrat\w*\|transition\w*\|mov(e\|ing)\|switch\w*\|consolidat\w*\|roll(ing)?\s?out)[^.]{0,80}\bintune\b` OR `\bintune\b[^.]{0,40}(migration\|rollout\|transition\|onboarding)` | boolean |
| G1 | Company size | trigger (gate) | `employee_count >= 250` | boolean |
| G2 | HQ market allowed | trigger (gate) | `hq_country` in {GB, FR, US, CA, CH} | boolean |
| G3 | Not iOS-only | trigger (gate) | Fails only if `\b(ios\|iphone\|ipad)\b` matches AND `\bandroid\b` does not match | boolean |
| G4 | Not an agency post | trigger (gate) | Company domain is not in the Exclusions table with Type `agency` AND Clay industry is not "Staffing and Recruiting" AND company name does not match `\b(recruit\w*\|staffing\|personnel\|talent)\b` | boolean |
| G5 | Industry allowed | trigger (gate) | C3 segment is not `other` (mapping below) | boolean |
| X1 | Not excluded | trigger (gate) | Company domain is not in the Exclusions table (any Type) and not contacted by this workflow in the last 90 days | boolean |
| R1 | Old EMM named | router | Four regexes, counted as distinct matches, **only in sentences that also contain a migration word** (`migrat\w*\|transition\w*\|mov(e\|ing)\|switch\w*\|replac\w*\|from\|sunset\w*\|decommission\w*`); split `job_description` into sentences on `.`, `;` and line breaks first. This stops "experience with Workspace ONE and Intune" from routing to cell B. **Ivanti:** `\bmobileiron\b\|\bivanti\s*(epmm\|uem\|neurons for mdm)\b\|\bepmm\b`. **Workspace ONE:** `\bworkspace\s?one\b\|\bairwatch\b\|\bomnissa\b`. **BlackBerry:** `\bblackberry\s*(uem\|work\|dynamics\|enterprise)\b\|\bbes\s?12\b`. **SOTI:** `\bsoti\b\|\bmobicontrol\b` | enum, see clusters |
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

C1, C2 and C3 never route. They may add one line of colour in copy, and only in the rows where they are present. All T, G, X, R and C reads are Clay formulas (free) except G1, G2 and C3, which read Enrich Company fields.

**C3 / G5 industry mapping** (Clay's LinkedIn industry value, case-insensitive; INFERRED mapping of the ICP segments to Clay values; anything unlisted is `other` and fails G5)

| Clay industry contains | C3 segment |
|---|---|
| Banking, Financial Services, Investment Banking, Capital Markets | `banking` (S1) |
| Law Enforcement, Public Safety | `police` (S2) |
| Government Administration, Public Policy, International Affairs | `government` (S3) |
| Utilities, Oil and Energy, Renewables, Electric Power, Railroad, Transportation/Trucking/Railroad | `utilities_ci` (S4) |
| Insurance | `insurance` |
| Law Practice, Legal Services | `law` |

Check on the first 25 rows that real Clay values land in the right segment; add missing values here.

**`Ready to Contact?`** (one formula, the run condition for every paid person-level step and every copy line): T1 and G1 to G5 and X1 are all true, R1 is set, a Priority 1 or 2 contact was found who joined in the last 180 days with no earlier role at the account, the contact's country is allowed, and (for email steps) the contact is not in CA and the email is verified.

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
| `{{company_name}}` | Clay company enrichment `name`, cleaned by a formula that strips these suffixes only at the end of the name: Inc, Inc., LLC, Ltd, Ltd., Limited, plc, PLC, AG, SA, S.A., SAS, GmbH, Corp, Corp., Corporation, Group, Holding, Holdings (and a trailing comma) | A, B, C, D, E |
| `{{job_title}}` | TheirStack `job_title` (C2) | A, B, C, D, E |
| `{{old_emm}}` | R1 display name: "Ivanti", "Workspace ONE", "BlackBerry", "SOTI" | A, B, C, D |
| `{{old_file_tool}}` | Lookup on R1: ivanti → "Docs@Work", workspace_one → "Workspace ONE Content", blackberry → "BlackBerry Work", soti → "SOTI Hub" (source in section 1) | A, B, C, D |
| `{{file_share_mentioned}}` | C1 boolean | A, B, C, D, E (fallback needed when false) |
| `{{segment}}` | C3 enum | A, B, C, D, E (context only) |
| `{{proof_point}}` | `context/messaging/facts.md` | None until approved |
| `{{e1l1}}` | Formula: Email 1 line 1, picks the approved variant by R1 (Copy section), guarded by `Ready to Contact?` | A, B, C, D, E |
| `{{e1l2}}` | Formula: Email 1 line 2, picks the approved variant by R1, guarded by `Ready to Contact?` | A, B, C, D, E |
| `{{e2l1}}` | Formula: Email 2 line 1, picks the C1 line or the FALLBACK, guarded by `Ready to Contact?` | A, B, C, D, E |
| `{{sender_signature}}` | Static sequencer setting: sender name, legal entity and postal address, approved by legal. **Unknown** until the sending entity is decided (Papers AG or Papers Group AG, [compliance-cold-outreach.md §13 Q1](../../../context/docs/compliance-cold-outreach.md)) | A, B, C, D, E |

Internal only, never in copy: `job_url`, `job_posted_date`, `r1_match_count`, `hq_country`, `employee_count`.

## 7. Cadence & channel [ENGINE]

- **Periodicity:** always-on. TheirStack pull every Monday with a 30-day lookback. Trigger it with a scheduled run of the Jobs table in Clay if the plan allows it; otherwise an outside weekly schedule posts to a Clay webhook (confirm which before the build). Dedupe Jobs on TheirStack job ID, and Companies on domain, so a company enters once per signal; the 90-day suppression (gate X1) decides whether a returning company can be contacted again.
- **Volume check before paying:** run Find People's free preview count on the first week's passing companies. If it is near zero (all the filters stack: Intune post, title, joined in 180 days, 250+ staff, 5 markets), widen titles or the 180-day window before enriching.
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

**Next:** get facts.md approved by Hypergate, choose the email and LinkedIn tools, then export the copy and run `/campaign-qa`.

---

## Copy

Written with `/campaign-copy`. Every claim traces to [facts.md](../../../context/messaging/facts.md) (F1 to F9), which is a draft pending Hypergate approval. No customer names: none are authorized. Variables follow section 6.

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

### LinkedIn. Approved 2026-11-13

**Connection request (day 2):** empty, no note.

**DM (day 7, only if connected):** one sentence, dynamic on R1, no spintax, no link, no signature.
- + R1 = `ivanti` / `workspace_one` / `blackberry` / `soti` (cells A to D): "{{first_name}}, once {{old_emm}} is gone, will phones still need to reach the on-prem file shares, or is that content moving to OneDrive?"
- + R1 = `not_named` (cell E): "{{first_name}}, with the move to Intune, will phones still need the on-prem file shares, or are those heading to OneDrive?"

One DM only, per section 7 cadence. No DM 2.

### Sample: cell A, Email 1 as received

> **Subject:** intune and file shares
>
> Sam,
>
> From the Endpoint Engineer role Acme Bank has open, it reads like devices are moving from Ivanti to Intune.
>
> If phones reach file shares through Docs@Work today, my guess is that piece stays behind with Ivanti, since Intune has no built-in way to reach SMB shares.
>
> Hypergate Files gives phones the same on-prem SMB and Windows shares under Intune, with no extra servers, proxies or middleware.
>
> Is phone access to file shares part of the Intune plan?
>
> {{sender_signature}}

(Sam and Acme Bank are illustrative values, not a real lead.)
