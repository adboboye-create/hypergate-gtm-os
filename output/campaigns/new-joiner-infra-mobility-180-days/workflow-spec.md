# Workflow spec: New in role, infrastructure and mobility, regulated organisations (180 days)

**Status:** STRUCTURE-APPROVED 2026-11-20 · copy pending · no sends until legal, partner-region and facts.md sign-off and the 9 customer domains are filled

Built with `/build-workflow-spec`, section by section, each section approved by the user on 2026-11-20. It describes the play already built in Clay (workspace 1206365, workbook `wb_0too2hqE6A9WA6UQCp8`), with the changes the approved sections call for. Method: [workflow-anatomy.md](../../../knowledge-base/playbooks/workflow-anatomy.md). Related idea: #11 "New hire" in [campaign-strategy.md](../campaign-strategy.md) (Tier 2). Separate from [intune-migration-file-shares](../intune-migration-file-shares/workflow-spec.md).

**Read first**
- **Weakest signal type.** The signal matrix scores new-joiner signals 1 out of 3 for urgency, with "no evidence it triggers purchases" ([signal-matrix.md](../../../context/icp/signal-matrix.md) U6). Campaign strategy suggests stacking it with a stronger signal. This spec doesn't stack it yet.
- No sends until legal signs off the [compliance brief](../../../context/docs/compliance-cold-outreach.md), Hypergate sales answers the [partner-region memo](../../../context/docs/partner-region-policy.md), Hypergate approves [facts.md](../../../context/messaging/facts.md), and the 9 customer domains in the Exclusions table are filled.

---

## 1. Mother intent [ENGINE]

**A person started their current job in the last 6 months at a regulated organisation with 201 to 5,000 staff, in a role that owns infrastructure, architecture or mobility.**

- Catalog match: *New hires in target dept* ([workflow-anatomy.md](../../../knowledge-base/playbooks/workflow-anatomy.md), Leadership & People Movement). Source: Clay Find People, filtered on the start date of the current role.
- Why now (INFERRED): someone new in a role reviews the estate they've inherited. No evidence that this triggers purchases ([signal-matrix.md](../../../context/icp/signal-matrix.md) U6).
- Lead product: Hypergate Authenticator, native Kerberos SSO to the organisation's own AD with no cloud broker ([value-proposition.md](../../../context/positioning/value-proposition.md) §1, §2). Files is a secondary mention only; there's no file-share signal in this play.
- Titles and personas:
  - Mobility Manager → champion ([personas.md](../../../context/icp/personas.md) §1).
  - Infrastructure Architect, Enterprise Architect, Systems Engineer → influencer ([personas.md](../../../context/icp/personas.md) §3).
  - Data Protection Officer → held: no persona ties DPOs to buying mobile SSO.

## 2. Inclusion / exclusion [ICP]

### Include

| Filter | Value | Source / note |
|---|---|---|
| Person country (compliance follows the person) | **Contact:** United Kingdom, Switzerland, France, United States (email and LinkedIn). **LinkedIn only:** Canada. **Held:** Germany, Austria (rows stay, `Ready to Contact?` false). Anything else is out | [compliance-cold-outreach.md](../../../context/docs/compliance-cold-outreach.md) §1, §12. DE and AT are opt-in for B2B email; CA needs a published address (CASL); CH is pending legal |
| Company HQ | Recorded, not a gate | The ICP has no HQ must-have ([icp.md](../../../context/icp/icp.md) §1) |
| Size | 201 to 5,000 staff (Clay buckets 201-500, 501-1,000, 1,001-5,000) | INFERRED working range: the ICP has no minimum (icp.md open question 1). The cap leaves out organisations the size of some named customers (Jefferies about 7,800 staff, customers.md §2). Widen if volume is thin |
| Industry | Banking, Financial Services, Insurance, Government Administration, Public Policy, Public Safety, Oil and Gas, Law Practice, Legal Services | Core and adjacent ICP industries ([icp.md](../../../context/icp/icp.md) §1). Law added 2026-11-20 |
| Trigger | Started the current role 6 months ago or less (month-level start date). Internal moves count | "New in role" is the mother intent; no paid internal-move check |
| Recipient | Mobility Manager (champion, contacted first); Infrastructure Architect, Enterprise Architect, Systems Engineer (influencer). Data Protection Officer held. **Max 2 contacts per company**, champion first | [personas.md](../../../context/icp/personas.md) §1, §3 |
| Title excludes | Intern, Student, Apprentice, Trainee, Working Student, Recruiter, Talent Acquisition, People Partner, Account Executive, Account Manager, Business Development, Presales, Marketing, Help Desk, Service Desk, Desktop Support, Support Technician, Freelance, Contractor, Interim, Retired. Plus the `Assistant or Intern` formula must be false | As in the Intune spec, section 2 |

### Exclude

| Who | Why / how |
|---|---|
| Hypergate customers and the 28 listed partners | Exclusions table, matched on domain only. The 9 customer domains are blank: no sends until filled |
| Open deals and the real customer list | From Zoho CRM once connected (`{{customer_blocklist}}`, `{{active_pipeline}}`) |
| Staffing agencies and recruiters | Company industry "Staffing and Recruiting" fails |
| Anyone contacted by any Hypergate workflow in the last 90 days | Suppression window |
| Emails at a different domain than the company | Review view, never sent |
| Public-sector organisations (Government Administration, Public Policy, Public Safety) | Held from **email** until legal answers compliance gate G7-C6 (open tenders). LinkedIn allowed |

## 3. Sources [ENGINE]

| What | Source | Cost | Note |
|---|---|---|---|
| Trigger | Clay Find People: titles similar to Infrastructure Architect, Enterprise Architect, Systems Engineer, Mobility Manager, Data Protection Officer; the title excludes above; company size 201-500, 501-1,000, 1,001-5,000; the industries above; started current role 6 months or less; person in United Kingdom, Switzerland, France, United States, Canada, Germany, Austria | Free | Re-run as a new pull; Clay keeps existing rows. Use the free preview count as the volume check |
| Exclusions | `Exclusion & Block list` table, single-row lookup on `Domain` | Free | |
| Company data | `Companies` table, fed by Send table data (only people not excluded and not flagged intern), deduped on domain, then **Enrich company** (run condition: domain not empty) | 1 credit per company (measured 2026-11-19) | |
| Company industry and description | Enrich company `Industry` and `Description` | Included above | Industry feeds G2, G6, G7, C1. Description feeds A1 |
| AI column (A1) | Use AI on job title + company industry + company description, JSON output. Model GPT-4.1 Mini on Clay's managed OpenAI account | 0.2 credits per row (measured 2026-11-20, 3-row proof) | The search payload has no headline, so the headline input was dropped (2026-11-20). Grok 4.1 was rejected by Clay ("Model does not support Use AI") and refunded |
| Work email | Waterfall: Icypeas, Kitt, Enrow, LeadMagic, Findymail, each validated by Findymail. Run condition: `Ready to Contact?` = true AND G3 = `email` | About 2.7 net credits per email found (measured 2026-11-19) | Store `Email Source` and `Email Found On` (compliance G7-C2) |
| LinkedIn | Manual, from a LinkedIn queue view | Free | LinkedIn's User Agreement bans automation tools (compliance §12.3) |

## 4. Signals table [ENGINE]

Every read is a formula (free) except A1 (Use AI). Regexes ignore case.

| # | Signal | Role | How it's read | Output |
|---|---|---|---|---|
| T1 | New in role | trigger | `Start Date` (YYYY-MM) is on or after the month of today minus 180 days. Blank = false | boolean |
| G1 | Size fits | trigger (gate) | Companies `Size` bucket lower bound ≥ 200 and ≤ 5,000 | boolean |
| G2 | Industry fits | trigger (gate) | Company industry contains one of: Banking, Financial Services, Insurance, Government Administration, Public Policy, Public Safety, Oil and Gas, Law Practice, Legal Services | boolean |
| G3 | Market | trigger (gate) | Person country GB, CH, FR, US → `email`; CA → `linkedin_only`; DE, AT → `held`; anything else → `out` | enum |
| G4 | Not excluded | trigger (gate) | Exclusions lookup on domain finds nothing AND not contacted by any Hypergate workflow in 90 days | boolean |
| G5 | Not junior | trigger (gate) | `Assistant or Intern` is false | boolean |
| G6 | Not an agency | trigger (gate) | Company industry is not "Staffing and Recruiting" | boolean |
| G7 | Public sector | trigger (gate, email only) | Company industry is Government Administration, Public Policy or Public Safety | boolean |
| G8 | Picked | trigger (gate) | At most 2 per company: `mobility` first, then `infrastructure`, newest start date next (formula across a Companies lookup) | boolean |
| R1 | Role group | router | Title regex, first match wins: `\b(mobility\|mobile device\|mdm\|emm\|euc\|end user computing\|endpoint)\b` → `mobility`; `\b(architect\|systems engineer\|infrastructure)\b` → `infrastructure`; `\b(data protection\|dpo\|privacy)\b` → `dpo`; else `other` | enum |
| A1 | Role focus (AI) | trigger (gate) | Use AI on title + company industry + company description. Pass: `mobile_endpoint`, `identity_access`, `infrastructure_it`. `not_relevant` → dropped. `unclear` → held | JSON enum + evidence |
| C1 | Segment | context-clause | Industry → `banking` (Banking, Financial Services), `insurance`, `public_sector` (Government Administration, Public Policy, Public Safety), `energy` (Oil and Gas), `law` (Law Practice, Legal Services) | enum |
| C2 | Start month | context-clause | Month name of `Start Date` | text |
| E1 | Email sendable | trigger (email channel) | Email found and validated, its domain equals the company domain, `Email Source` and `Email Found On` filled | boolean |

C1 and C2 never route. No count routes, so there are no count clusters. R1 values: `mobility` and `infrastructure` route, `dpo` is held, `other` is dropped.

### A1: the AI column

- **Type:** Use AI (not Claygent), JSON output, GPT-4.1 Mini (Clay-managed OpenAI). Inputs: job title, company name, company industry, company description.
- **Run condition:** T1, G1, G2, G4, G5, G6 true, AND G3 is `email` or `linkedin_only`, AND R1 is not `dpo`.
- **Output fields:**
  - `role_focus`, one of:
    - `mobile_endpoint`: owns phones, tablets, EMM/MDM or endpoints;
    - `identity_access`: owns Active Directory, identity, authentication or SSO;
    - `infrastructure_it`: corporate IT infrastructure (servers, Windows, network), no identity or mobile mention;
    - `not_relevant`: industrial or OT systems, data protection, applications, anything else;
    - `unclear`.
  - `evidence`: a short quote from the title, headline or description supporting the answer. Empty if `unclear`.
- **Proof:** run on 3 rows you can judge before running the rest.
- **`unclear` means held, never sent.**

### Gates

- **`Ready to Contact?`** = T1, G1, G2, G4, G5, G6, G8 all true, AND G3 is `email` or `linkedin_only`, AND R1 is `mobility` or `infrastructure`, AND A1 `role_focus` is `mobile_endpoint`, `identity_access` or `infrastructure_it`.
- **`Ready for Email?`** = `Ready to Contact?` AND G3 = `email` AND G7 is false AND E1.
- **Held (always false):** G3 = `held` (DE, AT), R1 = `dpo`, A1 = `unclear`. Public sector (G7) is held from email only.

## 5. Routing matrix with angles [ENGINE]

One axis (R1), 2 sending cells.

| Cell | Deterministic read | What it tells us (inferred situation) | The angle it earns |
|---|---|---|---|
| A. Mobility | `Ready to Contact?` = true, R1 = `mobility` | They started in the last 6 months in a role that owns the organisation's phones, EMM or endpoints, at a regulated organisation. A new owner of the fleet is likely reviewing how the mobile estate is set up. We don't know whether they run on-prem AD or Android Enterprise; that can't be seen from outside ([icp.md](../../../context/icp/icp.md) §5) | Android Enterprise has no built-in Kerberos SSO, so on managed Android, staff type their AD password into each app. Hypergate Authenticator gives phones native Kerberos sign-in to their own Active Directory, configured from the EMM they already run, with no extra servers and no cloud broker. Framed as a question about their setup ([value-proposition.md](../../../context/positioning/value-proposition.md) §1; [facts.md](../../../context/messaging/facts.md) Variant B) |
| B. Infrastructure | `Ready to Contact?` = true, R1 = `infrastructure` | They started in the last 6 months as an infrastructure or enterprise architect or a systems engineer, and the AI confirms the role is corporate IT (identity, AD, servers), not industrial systems. Someone new in that seat is likely reviewing the identity and infrastructure estate, which this year includes Microsoft's NTLM phase-out | Microsoft is phasing out NTLM (NTLMv1 SSO blocked by default since 13 Oct 2026), and on Android and iOS, NTLM was often the actual path to on-prem SharePoint, file shares and intranet apps. Android has no built-in Kerberos client. Hypergate gives phones native Kerberos to their own domain controllers, with no Entra ID or Application Proxy in the path ([value-proposition.md](../../../context/positioning/value-proposition.md) §2; [market.md](../../../context/docs/research/market.md) §1.2; [signals.md](../../../context/docs/research/signals.md) S5) |
| Held: DE / AT | G3 = `held` | Opt-in markets for B2B email (and LinkedIn messages, per German and Italian sources) | None; stays false until there's an opt-in route |
| Held: DPO | R1 = `dpo` | No persona ties data protection officers to buying mobile SSO | None; stays false |
| Held: AI unclear | A1 = `unclear` | The AI couldn't tell what the role owns | None until a person reviews the row |
| Email held: public sector | G7 = true | Open legal question on contacting public bodies (G7-C6) | Cells A or B still apply on LinkedIn; email waits for legal |

Dropped (no cell): R1 = `other`, A1 = `not_relevant`, or any trigger gate false.

**Branch coverage**
- Both cells have `{{first_name}}`, `{{company_name}}`, `{{job_title}}`, `{{start_month}}` and `{{segment}}`.
- Neither cell knows their EMM, whether they use Android Enterprise, or whether their AD is on-prem. So neither angle may assert those; both ask.
- No proof point in either cell: facts.md has no approved customer names.
- Canadian rows run the same cells, LinkedIn only.

**Niche-native test**
- A names the exact Android Enterprise gap (no Kerberos SSO) and the fix through the EMM they already run.
- B ties NTLM's retirement to mobile access to on-prem resources.

A generic MDM or SSO vendor couldn't send either unchanged.

**For `/campaign-copy`:** cell B's NTLM date is in the research ([market.md](../../../context/docs/research/market.md) §1.2) but not yet in [facts.md](../../../context/messaging/facts.md). Add it there as a claim pending Hypergate approval before writing copy.

## 6. Variables contract [ENGINE]

| Variable | Source field | Exists in cells |
|---|---|---|
| `{{first_name}}` | People `First Name` (from the search) | A, B |
| `{{company_name}}` | People `Company`, cleaned by a formula that strips these endings only at the end of the name: Inc, Inc., LLC, Ltd, Ltd., Limited, plc, PLC, AG, SA, S.A., SAS, GmbH, Corp, Corp., Corporation, Group, Holding, Holdings (and a trailing comma) | A, B |
| `{{job_title}}` | People `Job Title` (current title, from the search) | A, B |
| `{{start_month}}` | C2: month name of `Start Date` | A, B (context only) |
| `{{segment}}` | C1 | A, B (context only) |
| `{{proof_point}}` | [facts.md](../../../context/messaging/facts.md) | None until Hypergate approves one |
| `{{e1l1}}`, `{{e1l2}}`, … | Copy-line formulas defined by `/campaign-copy`, each guarded by `Ready to Contact?` | A, B |
| `{{sender_signature}}` | Static sequencer setting: sender name, legal entity, postal address, unsubscribe and privacy-notice link (compliance §12.3). Unknown until the sending entity is decided | A, B |

**Internal only, never in copy:**
- `start_date`, `person_country`, `market` (G3), `role_group` (R1);
- `role_focus` and `evidence` (A1);
- `email_source`, `email_found_on`;
- `linkedin_profile`, `company_domain`, `employee_count`.

## 7. Cadence and channel [ENGINE]

- **Periodicity: monthly.** Re-run the free search with the 6-month start-date window. Dedupe people on `LinkedIn Profile` and companies on domain. The 90-day suppression (G4) decides re-contact.
- **Volume check before paying:** compare the free preview count with last month's. The first pull (2026-11-19, before the law, FR and US additions) gave 77 people at 70 companies. Monthly volume after the changes is unknown.
- **Channel:** email plus LinkedIn, on the [gtm-system.md](../../../context/docs/gtm-system.md) §8 skeleton:
  - day 1: Email 1;
  - day 2: LinkedIn connection request, no note;
  - day 4: Email 2;
  - day 7: LinkedIn DM, only if connected;
  - day 10: Email 3.
- **LinkedIn only:** Canada; public-sector rows until legal answers; anyone without a sendable email (E1 false).
- **Nothing at all:** held rows (DE, AT, DPO, AI unclear).
- **LinkedIn is manual.**
- **Reply on any channel:** stop all steps for that contact, pause the other contact at the same company, and go to reply handling ([gtm-system.md](../../../context/docs/gtm-system.md) §9).
- **No reply:** mark "no response" and suppress for 90 days.

---

## Definition of done

- [x] Mother intent: one sentence, signal-led, matched to the catalog
- [x] Inclusion: ICP box + trigger definition + recipient, tagged [ICP]
- [x] Exclusion: who's out and why
- [x] Sources: trigger + every enrichment
- [x] Signals table: every read deterministic (or an AI column with a hard enum), every role declared
- [x] Count clusters: none route (declared)
- [x] Routing matrix with the angle column complete
- [x] Branch coverage checked per cell
- [x] Variables contract: every variable mapped to its source field
- [x] Engine/ICP markers on every section
- [x] Cadence & channel declared

**Next:** bring the Clay build in line with sections 2 to 4 (list in the work log, 2026-11-20). Then `/campaign-copy` for cells A and B, after adding the NTLM claim to facts.md.
