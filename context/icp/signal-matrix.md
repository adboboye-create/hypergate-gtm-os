# Hypergate signal matrix

**Status: work in progress, v0.1 (2026-11-13). Top-five build order approved by the user on 2026-11-13.** Built with `/signal-matrix`. It is a set of hypotheses to validate with Hypergate sales and leadership, not a final plan. There is no win/loss or call data behind any of it yet.

**Answers:** what are we selling, to whom, and how do we find them right now?

**Inputs read:** [icp.md](icp.md), [personas.md](personas.md), everything in [context/docs/research/](../docs/research/). **Method:** [signal-matrix-framework.md](../../knowledge-base/playbooks/signal-matrix-framework.md), [workflow-anatomy.md](../../knowledge-base/playbooks/workflow-anatomy.md).

**Source keys** (same as icp.md): **CO** company.md, **CU** customers.md, **CP** competitors.md, **MK** market.md, **SG** signals.md, **VO** voice.md. § = section. Two new research passes on 2026-11-13 are cited by URL inline: example organisations (**EX**) and data source checks (**DS**). "Snippet" = seen in a search result summary only; re-check before use.

**INFERRED** = not supported directly by the research. Every angle, score and volume judgement in this file is INFERRED unless a source is given.

## Decisions taken (2026-11-13, with the user)

| Decision | Choice | Why |
|---|---|---|
| Rows | Segments by industry | Every customer maps to one. Filterable in Clay (industry, size, country). Triggers go to Matrix 2 |
| Columns | The three personas in personas.md | Requested. Economic buyer is unconfirmed, so that column is the weakest |
| Priority cells | Banking, police, government administration, utilities and critical infrastructure | Strongest mix of fit, signals and reach (scores below). Insurance rides on banking as a keyword swap |
| Geography | DACH + EU first, US/UK/Canada second | Site languages EN/DE/FR/IT, most logos, partner network and sovereignty angle (CO §7, §9; CU §2) |
| Example search | Real organisations only for the 4 priority cells | Cost. Other rows carry Clay filter definitions |

## What we sell (one paragraph)

Hypergate Authenticator gives managed Android (and iOS) devices Kerberos single sign-on against on-prem or hybrid Active Directory, with self-service AD password reset, configured through the customer's EMM and with no extra servers or cloud broker (CO §2.1, §3). Hypergate Files gives mobile access to SMB/CIFS and NetApp shares, opening files in native apps (CO §2.2). An SDK lets in-house Android apps answer with Kerberos instead of NTLM (CO §2.3). Root pain: "Android Enterprise ships no built-in Kerberos SSO" (SG "Root condition"). Single core technology, two products plus SDK, so Matrix 1 carries a lead product and an upsell per row (hypotheses).

---

# Matrix 1: Segments x personas

## 1a. Segment definitions and priority

Scores: **Fit** = product-market fit, **Density** = number of programmable signals, **Reach** = can we get data and contacts in this market. All three are INFERRED judgements from the research cited.

| # | Segment | Target definition (filterable) | Lead / upsell | Fit | Density | Reach | Priority |
|---|---|---|---|---|---|---|---|
| S1 | Banking and capital markets | Retail, private, cantonal and investment banks, Landesbanken, building societies. DACH + EU first, then UK/US. INFERRED size floor: 1,000+ employees (ICP sets no minimum, CU §2 customers start at about 240). Must run an EMM | Authenticator / Files | High (Jefferies CU §3.1; homepage names banks CO §1) | High | High (rich data, Apollo/LinkedIn) | **High** |
| S2 | Police and public safety | National, state, cantonal and regional police forces; issuing smartphones to officers; EMM-managed | Authenticator / Files | High (York Regional Police story and quote CU §3.3; Jersey logo CU §2) | Medium | Medium | **High** |
| S3 | Government administration | State, cantonal, federal and city administrations, ministries, EU institutions and agencies, and public-sector IT service providers (for example Dataport, HZD, LDI RLP) | Authenticator + Files together | High (Bayerische Staatskanzlei, European Court of Auditors logos CU §2; sovereignty page SG S4) | Medium (tenders are public) | Medium | **High** |
| S4 | Utilities and critical infrastructure | Energy, grid, water, rail and transport operators, Stadtwerke, offshore. Field or shift staff on shared or rugged Android (Zebra, Samsung) | Authenticator / Files | Medium (Linz AG logo CU §2; Maersk story CU §3.2) | Medium | Medium | **Medium-High** |
| S5 | Insurance | Primary insurers, accident and health insurers, reinsurers. Same filters as S1 | Authenticator / Files | Medium-High (Suva logo CU §2; homepage names insurers CO §1) | High (same signals as S1) | High | Medium |
| S6 | Law firms | Large firms (INFERRED: 300+ lawyers) with on-prem file servers. US AmLaw, UK top firms, DACH large firms | Files / Authenticator | Medium (unnamed "big American law firm" only, CU §2) | Low | Medium | Medium-Low |
| S7 | Frontline industries | Logistics, postal, retail, manufacturing, healthcare with shared Zebra/Samsung fleets and on-prem AD | Authenticator / Files | Medium (USPS logo CU §2; Zebra validation SG S3). Microsoft shared device mode and Imprivata compete (CP §3.1, §3.11) | Medium | High | Medium-Low |
| S8 | Defence and aerospace | Defence ministries, armed forces IT, defence contractors with classified or air-gapped AD | Authenticator | Medium (sovereignty claim SG S4; one unverified story CU §2) | Low | Low | Low |

## 1b. Angle per cell

Angles describe the buyer's situation in their terms. They are all INFERRED hypotheses: no buyer has confirmed any of them. The economic buyer is unconfirmed (personas.md §2), so treat that column as the weakest. The evidence each angle leans on is in brackets.

| Segment | Champion: mobility / EMM admin | Economic buyer (unconfirmed): CIO, CISO or head of EUC | Influencer: identity / AD engineering, app developers |
|---|---|---|---|
| **S1 Banking** | Bankers on Android work profile still type their AD password into each internal app. Kerberos sign-in through the EMM you already run, no gateway server [Jefferies CU §3.1; VO §4] | DORA Art. 9(4)(d) asks for strong authentication. Keep mobile sign-in on your own AD instead of a cloud broker [MK §3.2; CP §1. DORA as a buying trigger is unproven, ICP open question 6] | NTLMv1 SSO is enforced since 13 Oct 2026 and network NTLM is next. Mobile paths to SharePoint and file shares often still run on NTLM [MK §1.1, §1.2; SG S5] |
| **S2 Police** | Officers on Android get one sign-in to the intranet and police apps, inside the MobileIron or Intune setup you already run [York CU §3.3] | Officer sign-in stays on your own AD, with no cloud identity provider in the path [SG S4; CP §1] | Kerberos to local AD on Android Enterprise, which Android does not do natively. AES by default after the RC4 removal [CU §3.3; SG S6] |
| **S3 Government** | When the EMM or device platform changes, intranet sign-in and file-share access come along, whatever the EMM [SG S8; VO §4 "eliminating vendor lock-in"] | A sovereign workplace needs mobile sign-in that stays on your own AD, without Entra ID or Okta [SG S4; VO §4] | Moving off NTLM while staying on-prem: Entra Kerberos and cloud trust do not cover Android [SG S10, S5] |
| **S4 Utilities / CI** | Shift crews on shared Android devices sign in once per shift, not once per app, and it still works offline against a local AD [Maersk CU §3.2] | Strong authentication on field devices without adding servers, as NIS2 and Swiss CI rules raise the bar [MK §3.1, §4.2. Relevance INFERRED] | Validated on Zebra TC and ET devices and all Samsung Galaxy; deployed through Knox or your EMM [SG S3; CO §3] |
| S5 Insurance | Field and claims staff on Android reach internal web apps without retyping AD passwords [INFERRED from S1] | Same as S1. DORA covers insurers [MK §3.2 lists 21 entity types; insurer coverage not quoted, INFERRED] | Same as S1 (NTLM) |
| S6 Law firms | Lawyers open matter files from on-prem shares in native Word and PDF apps on their phone [CO §2.2; CU §2 law firm line] | Client files stay on your own servers, with nothing synced to a cloud [VO §4. INFERRED] | In-house or DMS-linked apps still on NTLM [SG S5] |
| S7 Frontline | One sign-in per shift on shared Zebra or Samsung devices [SG S3] | Every lockout is a ticket; self-service AD password reset on the device [SG S12; VO §4] | Microsoft shared device mode needs MSAL-built apps and Entra; legacy Kerberos web apps do not fit it [CP §3.1] |
| S8 Defence | Works in air-gapped and multi-forest AD with no external service [CO §3; SG S4] | Classification rules keep authentication metadata inside accredited boundaries [SG S4] | Native Kerberos to existing domain controllers, no middleware [CO §3] |

## 1c. Example organisations (priority cells only)

Real organisations from public sources, checked 2026-11-13 (EX). None is a known customer. Evidence shows a mobility situation, **not** confirmed fit: on-prem AD and Kerberos apps cannot be seen from outside (icp.md §5), so qualify on the first call. Fit judgements are INFERRED. Dates matter: older items are flagged.

**Anchors (existing customers, CU §2):** Jefferies (S1), York Regional Police, States of Jersey Police (S2), Bayerische Staatskanzlei, European Court of Auditors (S3), Linz AG, Maersk Drilling/Noble (S4), Suva (S5), USPS (S7).

### S1 Banking and capital markets

| Organisation | Country | Evidence | Source |
|---|---|---|---|
| BBVA | ES | 100,000+ Android devices on Android Enterprise, work profile, zero-touch (Sep 2025) | https://blog.google/products-and-platforms/products/android-enterprise/bbva-android-enterprise/ |
| ABANCA | ES | BlackBerry UEM, about 1,750 Samsung Android plus iPhones, COPE (undated) | https://www.casestudies.com/company/blackberry/case-study/blackberry-uem-is-a-wise-investment-for-abanca |
| CaixaBank | ES | 22,000+ Android devices to staff (2019, old) | https://blog.google/products/android-enterprise/banks-find-investing-android-pays |
| HSBC | UK | Supports only Android Enterprise Recommended devices (2019, old) | same as CaixaBank |
| Standard Chartered | UK | BYOD on Android work profile (2019, old) | same as CaixaBank |
| Yorkshire Building Society | UK | Android handsets for intranet and corporate apps (2019, old) | same as CaixaBank |
| DZ BANK | DE | MobileIron EMM after the WGZ merger (reseller page, snippet) | https://ebf.com/en/references/dz-bank/ |
| Bausparkasse Schwäbisch Hall | DE | MobileIron UEM since 2014, about 3,300 field staff (snippet) | https://ivanti.com/resources/library/ivi/2504/14b365796302/?ext=pdf |
| Swissquote | CH | Endpoint Engineer job covering Android Enterprise and Intune (posting now gone, snippet) | https://www.efinancialcareers.co.uk/jobs-Switzerland-Gland-Endpoint_Engineer.id24698792 |

Gap: no Kantonalbank, Austrian bank or Landesbank with mobility evidence found. Requires Clay research with filters: industry = Banking, country in (CH, AT, DE), employees 1,000+, then the U1 hiring signal.

### S2 Police and public safety

| Organisation | Country | Evidence | Source |
|---|---|---|---|
| Policie České republiky | CZ | Jun 2025 framework tender for Enterprise Mobility Management for its "Mobile Secure Platform" (snippet) | https://op.europa.eu/en/web/public-procurement/procurement-details/-/procurement/afba8ffb-b8d4-44fd-8d07-738120f0964d |
| Metropolitan Police | UK | Approval to buy 29,737 Samsung A32 phones with Intune (snippet) | https://www.london.gov.uk/programmes-strategies/mayors-office-policing-and-crime-mopac/mopac-governance-and-decision-making/mopac-decisions/pcd-1323-smart-phone-role-out |
| West Midlands Police | UK | Android Enterprise plus Knox Suite on 8,500+ devices (snippet) | https://www.samsungknox.com/en/success-stories/west-midlands-police |
| Police Scotland | UK | Samsung devices to about 10,500 officers plus 5,892 more, done Jun 2022 (snippet) | https://www.spa.police.uk/publication-library/digitally-enabled-policing-programme-work-stream-update-7-december-2022/mobile-working-project |
| City of London Police | UK | Samsung A40 phones with cloud management (2021, snippet) | https://policeprofessional.com/?p=131799 |
| Bundespolizei | DE | About 1,000 Samsung Galaxy S10 EE on Knox MDM (2019, old, snippet) | https://news.samsung.com/de/samsung-stattet-bundespolizei-mit-galaxy-s10-aus |
| Polizei Baden-Württemberg | DE | 1,000 Android smartphones for police systems on the street (2019, old, snippet) | https://im.baden-wuerttemberg.de/de/service/presse-und-oeffentlichkeitsarbeit/pressemitteilung/pid/1000-smartphones-fuer-die-polizei-baden-wuerttemberg |
| Polizei Sachsen | DE | About 2,300 Samsung Galaxy A8 (2019, old, PDF unread) | https://medienservice.sachsen.de/medien/news/226350/download_pdf |
| Waterloo Regional Police | CA | BlackBerry UEM with Samsung and Knox (2018, old, snippet) | https://insights.samsung.com/2018/10/25/waterloo-regional-police-goes-mobile-first-with-samsung-and-blackberry |
| Toronto Police Service | CA | 700 Samsung Galaxy S8+, iOS added later (2018, old, snippet) | https://mobilesyrup.com/2018/06/15/toronto-police-connected-officers-use-ios-and-samsung-devices-in-2019/ |

Note: Austrian federal police, Polizei NRW, Sachsen-Anhalt and Brandenburg are on iPhone (EX). Hypergate supports iOS, but Apple ships its own Kerberos extension (CP §3.9), so they are weaker fits (INFERRED). Landespolizei Mecklenburg-Vorpommern pulled all service phones after a June 2025 hack on its MDM server (iPhone, snippet: https://www.nordkurier.de/regional/mecklenburg-vorpommern/weiter-warten-auf-neue-polizeihandys-nach-hackerangriff-4766880). It is an event to watch, not an Android fit.

### S3 Government administration

| Organisation | Country | Evidence | Source |
|---|---|---|---|
| LDI Rheinland-Pfalz | DE | Jun 2026 tender to replace an outdated on-prem MDM, citing data protection and sovereignty; estimate EUR 5M; deadline 17 Jul 2026 (closed). AirWatch since 2013 per a 2019 audit | https://www.patterno.de/en/ausschreibungen/tender/mobile-device-management-loesung-fuer-den-landesbetrieb-mainz-cy162nwx5r3t177kjzrphc4v |
| HZD "HessenSmartphone" | DE | BlackBerry UEM/Dynamics, iOS and Android, 10,000+ phones; tender allows an EMM switch (Jun 2024, snippet) | https://ted.europa.eu/de/notice/556196-2024/pdf |
| Centre des technologies de l'Etat (CTIE) | LU | Framework to extend Ivanti EPMM (MobileIron) licences (Apr 2026) | https://www.patterno.de/en/ausschreibungen/tender/ivanti-endpoint-manager-lizenzen-fuer-it-des-staates-luxembourg-g6ffuv5o1r03km0wwa2395lw |
| Land Schleswig-Holstein (with Dataport) | DE | Cabinet decision for a sovereign workplace and Microsoft exit (Apr 2024); AD central today; smartphones in scope (snippet) | https://www.schleswig-holstein.de/DE/landesregierung/themen/digitalisierung/linux-plus1/Projekt/projekte.html |
| Sächsische Informatikdienste (SID) | DE | 2026 tender described as UEM with prequalification (scope unread) | https://ted.europa.eu/de/notice/53332-2026/pdf |
| ZIT-BB Brandenburg | DE | Aug 2026 framework for about 5,000 tablets and 2,500 smartphones (PDF unread) | https://ted.europa.eu/en/notice/569806-2026/pdf |
| Landeshauptstadt Stuttgart | DE | Smartphone framework agreement, Jul 2025 (snippet) | https://ted.europa.eu/de/notice/469381-2025/pdf |
| Pensionsversicherungsanstalt | AT | Jun 2026 framework to lease smartphones and tablets; MDM not mentioned | https://www.patterno.de/en/ausschreibungen/tender/leasing-von-smartphones-und-tablets-fuer-die-wien-ckl18lvpz0nnc09r2ey0w0qn |
| eu-LISA | EU | Ex-ante notice for mobile provision, interest deadline 30 Apr 2026; MDM scope unclear (snippet) | https://www.eulisa.europa.eu/sites/default/files/documents/ex-ante-notice-lisa-2026-lvp-0008.pdf |
| Shared Services Canada | CA | Samsung Android approved for federal staff next to BlackBerry (2017, old, snippet) | https://www.theglobeandmail.com/report-on-business/ottawa-opens-door-to-samsung-smartphones-marking-an-end-to-blackberrys-reign/article35840810/ |

### S4 Utilities and critical infrastructure

| Organisation | Country | Evidence | Source |
|---|---|---|---|
| Deutsche Bahn (DB Systel) | DE | Staff Samsung, Nokia and Apple devices migrating to Intune; guides Dec 2025 to Jun 2026 (snippet) | https://mobileworkplace.deutschebahn.com/anleitungen/DB-Smartphone-und-Tablet-migration |
| SBB | CH | Samsung Galaxy for 30,000 staff with Knox Configure and Android Enterprise (snippet) | https://www.samsungknox.com/en/success-stories/sbb |
| EnBW | DE | Several thousand Nokia Android One phones from Mar 2019, MDM enrolment (old) | https://www.hmd.com/de_at/case-study-enbw |
| Swissgrid | CH | "Beschaffung Mobile Devices" tender via simap.ch, 23 Feb 2026 (scope unread) | https://ted.europa.eu/en/notice/126946-2026/pdf |
| Stadtwerke Potsdam | DE | Jun 2026 hardware framework with a smartphone and tablet lot (snippet) | https://www.patterno.de/en/ausschreibungen/tender/rahmenvertrag-hardware-smartphones-tablets-fuer-stadtwerke-potsdam-vbjksninu4hkwiqv9uua84qx |
| Stadtwerke Dinslaken | DE | Securing an employee mobile fleet, about 400 staff; EMM not named (snippet) | https://www.casestudies.com/company/checkpoint-software/case-study/how-stadtwerke-dinslaken-secures-its-fleet-of-employee-mobile-devices |
| Stadtwerke Unna | DE | Central EMM for field devices, open to Android (old, snippet) | https://www.cio.de/article/3653509/stadtwerke-unna-legen-mobilgeraete-an-die-leine-2.html |
| E.ON Next | UK | Field service on Zebra ET65 rugged Android tablets (snippet) | https://www.zebra.com/gb/en/resource-library/success-stories/eon-next-energises-field-service-with-zebras-durable-dependable-and-high-speed-et65-android-tablets.html |
| PPC Romania | RO | 1,500 Samsung Galaxy devices for its mobile workforce via Knox (2026, snippet) | https://www.samsungknox.com/de/blog/msp-we-are-project |
| SNCF | FR | Frontline teams on Android (snippet) | https://blog.google/products-and-platforms/products/android-enterprise/sncf-case-study/ |

Gap: no DACH/EU offshore or water operator with mobility evidence found (EX).

### Non-priority rows (S5 to S8): Clay filters instead of names

| Segment | Requires Clay research with filters |
|---|---|
| S5 Insurance | Industry = Insurance; country in DACH, then EU/UK; employees 1,000+ (INFERRED floor); then U1/U4 job signals |
| S6 Law firms | Industry = Law Practice; employees 500+ (INFERRED); US, UK, DE; then U1 jobs with "file server", "Intune", "Android" |
| S7 Frontline | Industry in (Logistics, Postal, Retail, Hospital and Health Care, Manufacturing); then U5 (Zebra/Samsung customer stories) |
| S8 Defence | Not workable with programmable signals today (reach Low). Partner-led (HiTech Defense, iSEC7 per CO §7) |

---

# Matrix 2: Signals

## 2a. Signal scorecard

The four tests come from workflow-anatomy.md ("Choosing a Mother Intent"). Each is scored 1 (weak), 2 (fair) or 3 (strong); total out of 12. **All scores are INFERRED judgements.** Status uses the Iron Law forcing question: could a Clay operator build this now with zero ambiguity?

| ID | Type | Signal (observable event) | Mother intent (catalog) | Data source | Detection tool / Clay action | Key filters | Reason | Volume | Data | Story | Total | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| **N1** | Niche (public sector) | Public tender for MDM / UEM / EMM software or a smartphone fleet | Niche-specific play (public procurement); Regulatory changes | TED Search API, free, no key (`POST api.ted.europa.eu/v3/notices/search`); simap.ch unofficial JSON API; oeffentlichevergabe.de daily OCDS export [DS] | Clay HTTP API column on TED, or Apify actors (simap, Germany tenders) into Clay | CPV 32250000 (mobile telephones), 48781000 (system management software), plus full-text "Mobile Device Management", "MDM", "UEM", "Enterprise Mobility", "Ivanti", "BlackBerry", "Workspace ONE". NUTS: DE, AT, CH, LU, then EU | 3 | 2 | 3 | 3 | **11** | VERIFIED |
| **U1** | Universal | Job post naming an EMM change or Android Enterprise work: "Intune migration", "MobileIron", "Ivanti EPMM", "Workspace ONE", "BlackBerry UEM", "SOTI", "Android Enterprise", "work profile" | Hiring specific roles | TheirStack Jobs API (regex over full job description) [DS]; Clay Find Jobs (PredictLeads, Google Jobs; max 4 keywords via Google Jobs) [DS]; Apify StepStone, LinkedIn Jobs, jobs.ch/jobup.ch actors [DS] | TheirStack via Clay HTTP column (free 200 credits/month; about $59/month for 1,500) [DS]; Clay Find Jobs | Description regex on the terms above; titles: Mobility Engineer, EUC, Endpoint, MDM, Client Engineer; posted last 30 days; countries DACH first | 2 | 3 | 3 | 3 | **11** | VERIFIED |
| **U4** | Universal | Job post naming NTLM removal or Kerberos hardening: "NTLM", "Kerberos", "IAKerb", "RC4", "AD hardening", "Windows Hello for Business", "cloud Kerberos trust" | Hiring specific roles | TheirStack Jobs API (same build as U1) [DS] | Same Clay HTTP column as U1, second regex | Same as U1; stack with an EMM term in the same post for fit | 3 | 1 (EX found no posts naming Kerberos or NTLM) | 3 | 3 | **10** | VERIFIED (PARTIAL: low volume) |
| **U7** | Universal | Organisation runs Acronis Cyber Files / Files Connect (on-prem). Security updates stop 2026-12-31 (SG S9) | Competitor customers (one-time list) | Acronis case studies (casestudies.com, Acronis resource center: ANWB, Morse Group, Toro Rosso, SGS Packaging, Malmberg, TTS Group, 2016 to 2019) [DS]; job posts with "Acronis Files" (TheirStack) | One-time scrape plus TheirStack regex. No technographic provider confirmed for Acronis Files [DS] | Exclude Acronis Cyber Files **Cloud** users (still active, SG S9) | 3 | 1 | 1 | 3 | **8** | VERIFIED (PARTIAL): a one-time list build, not a repeatable workflow |
| **U5** | Universal | Public news of a smartphone or rugged-device rollout to staff (police, utilities, frontline) | New product launches / niche news | Google News RSS (`news.google.com/rss/search?q=...&hl=de&gl=DE&ceid=DE:de`, `when:7d`), free, undocumented [DS]; vendor story libraries: Samsung Knox, Zebra, Google Android Enterprise blog, BlackBerry [DS] | Clay HTTP column on RSS; Apify or crawl4ai for story libraries | DE queries: "Smartphones Polizei", "Diensthandys Android", "mobiles Arbeiten Stadtwerke"; EN: "police smartphones rollout", "frontline Android devices" | 2 | 1 | 2 | 3 | **8** | VERIFIED (PARTIAL): needs a human check per hit |
| **U2** | Universal (compound) | Organisation runs a specific EMM: MobileIron/Ivanti, Workspace ONE, BlackBerry, SOTI, Intune. Bloomberry shows Workspace ONE renewal windows | Companies using specific software | TheirStack technology pages (MobileIron 1,475 companies, SOTI MobiControl 417, AirWatch 303) [DS]; Bloomberry (Workspace ONE 2,428 companies, 56 renewals due within 3 months) [DS]; Enlyft (Intune 51,756, AirWatch 8,989, MobileIron 5,004) [DS]; HG Insights and Sumble native in Clay (coverage of these products not confirmed) [DS] | Clay HG Insights "Companies by product usage" (8 credits per company per technology) or Sumble; TheirStack via HTTP | Use only to stack on N1, U1 or U4, never alone. Global counts, not per segment | 1 | 3 | 2 | 2 | **8** | VERIFIED (COMPOUND) |
| **U6** | Universal (compound) | New CIO, CISO, Head of IT, Head of EUC/Mobility in the last 90 days | New leadership (past 90 days) | Clay Find People with "max months in current role" = 3 plus title; Sales Navigator "changed jobs in past 90 days" [DS] | Clay Find People | Titles above; month-level dates, data can lag [DS] | 1 (no evidence it triggers purchases, SG "no evidence found") | 2 | 3 | 2 | **8** | VERIFIED (COMPOUND) |
| **N2** | Niche (S3 government) | Public sovereignty or cloud-exit decision by an administration (for example Schleswig-Holstein, SG S4) | Regulatory changes | Google News RSS (DE: "digitale Souveränität Verwaltung", "Microsoft Ausstieg", "openDesk") [DS] | Clay HTTP column on RSS | DE, AT, CH, FR, DK; last 30 days | 2 | 1 | 2 | 3 | **8** | VERIFIED (PARTIAL) |
| **N5** | Niche (S4 utilities, S7 frontline) | Rugged or shared Android fleet rollout (Zebra, Samsung, HMD) | Niche-specific play | Zebra success stories, Samsung Knox case studies, HMD case studies [DS]; plus N1 tenders with hardware lots (for example Stadtwerke Potsdam) | Apify or crawl4ai scrape into Clay | Utilities, transport, logistics; DACH/EU | 2 | 1 | 2 | 3 | **8** | VERIFIED (PARTIAL) |
| U8 | Universal | Former contact at a customer moves to a new company (champion migration) | Champion/user migration | Hypergate CRM customer contacts | Clay people enrichment on a CRM export | Needs the customer contact list (not in research) | 2 | 1 | 1 | 3 | 7 | BLOCKED: needs CRM export |

### Killed signals (and why)

| Signal | Why killed |
|---|---|
| Fundraising | Banks, public sector and utilities do not raise VC. Hypergate itself has no funding trail (CO §10). Framework: fundraising only in VC markets |
| Headcount growth | Large, stable organisations; growth says nothing about Kerberos or EMM needs (INFERRED) |
| BuiltWith web technographics | EMM, AD and file-share tools are back-end and invisible to website scans [DS] |
| DORA, NIS2, Swiss CI rules as a mother intent | Static: they apply to everyone in scope at once and give no timing. No evidence they trigger purchases (ICP open question 6). Keep them as narrative lines only |
| Ivanti EPMM CVEs (Jan 2026) as a mother intent | Every EPMM customer is affected at once, and the story drifts toward scaring people about their vendor (framework guardrail: guess their situation, do not diagnose problems). Use at most as background when U2 shows MobileIron |
| RC4 removal, strong certificate mapping | Deadlines passed (SG S6, S7); low value for new logos |
| Reddit / Microsoft Q&A posts | Posters are anonymous, so no company-level signal; Reddit commercial use needs a contract [DS]. Fine for content research only |

## 2b. Signals by segment (play and product)

Same Clay build for every segment in a row; only keywords, product and angle change. Blank = does not apply.

| Type | Signal | S1 Banking | S2 Police | S3 Government | S4 Utilities / CI |
|---|---|---|---|---|---|
| Niche | N1 Tenders for MDM / UEM / smartphones | | TED/simap, CPV + "Polizei", "police", "MDM". Lead: Authenticator. Example: Czech police EMM tender | TED/simap/oeffentlichevergabe, CPV + "MDM", "UEM". Lead: Authenticator + Files. Examples: LDI RLP, HZD, CTIE, SID, ZIT-BB | TED/simap, CPV + "Stadtwerke", "Energie", "Bahn". Lead: Authenticator. Examples: Swissgrid, Stadtwerke Potsdam |
| Universal | U1 Jobs: EMM change / Android Enterprise | Titles: Endpoint, Client, Mobility Engineer at banks. Lead: Authenticator (Files if "file share" or "Intune migration"). Example: Swissquote | Same regex, police employers (karriere portals via Apify). Lead: Authenticator | Same regex, public IT providers (Dataport, HZD, ITZBund, cantonal IT). Lead: Files on Intune migration | Same regex, utility and rail employers. Lead: Authenticator |
| Universal | U4 Jobs: NTLM / Kerberos hardening | AD / identity engineer posts. Lead: Authenticator; SDK if in-house Android apps | Same | Same | Same |
| Universal | U7 Acronis Cyber Files users | Lead: Files | Lead: Files | Lead: Files | Lead: Files |
| Universal | U5 Device rollout news | Rare for banks | "Smartphones für die Polizei", force press releases. Lead: Authenticator | "Diensthandys Verwaltung". Lead: Authenticator | "Stadtwerke mobiles Arbeiten", Zebra/Samsung stories. Lead: Authenticator |
| Niche | N2 Sovereignty / cloud exit | | | Lead: Authenticator + Files ("no cloud broker") | Municipal utilities owned by those administrations (INFERRED) |
| Niche | N5 Rugged / shared fleet stories | | Samsung Knox police stories (for example West Midlands) | | Zebra, Samsung, HMD stories. Lead: Authenticator |
| Universal (compound) | U2 EMM in use | Stack on U1/U4 | Stack on N1 | Stack on N1 | Stack on N1/U1 |
| Universal (compound) | U6 New IT leader | Stack on U1 | Stack on N1 | Stack on N1 | Stack on U1 |

**Compounding insight:** 6 of the 9 verified or partial signals are universal (U1, U2, U4, U5, U6, U7). U1 and U4 are the same TheirStack build with two regex sets. N1 is one TED build that serves three segments (police, government, utilities) by swapping keywords. So two core builds (TheirStack jobs, TED tenders) cover all four priority segments.

---

# Top signals to build first

| Rank | Signal | Why first |
|---|---|---|
| 1 | **N1 Public tenders (TED + simap + oeffentlichevergabe)** | Highest score (11). Free data with no key. Serves three of four priority segments with one build. Real 2026 examples match Hypergate's pitch closely: LDI RLP is replacing an on-prem MDM citing sovereignty; HZD allows an EMM switch; Luxembourg extends Ivanti EPMM. **Caveat (INFERRED):** contact with a buyer during an open tender can be restricted, so route open tenders to the bidding partner or integrator, and approach the buyer after award or ahead of the next cycle. Check procurement rules with Hypergate |
| 2 | **U1 Jobs naming an EMM change or Android Enterprise** | Score 11. Highest volume, works in every segment with keyword swaps, and the EMM-migration story is in Hypergate's own content (SG S8, "Intune lacks a built-in solution for accessing SMB/CIFS network file shares"). Cheap to test on TheirStack's free tier |
| 3 | **U4 Jobs naming NTLM or Kerberos hardening** | Strongest timing story (NTLMv1 SSO enforced since 13 Oct 2026, MK §1.2) and the most specific Hypergate voice (VO §8). Low volume, but near-zero extra cost because it is the same build as U1 with a second regex |
| 4 | **U7 Acronis Cyber Files users (one-time list)** | The only hard deadline (updates stop 2026-12-31, about 7 weeks away) and Hypergate already has migration guides in EN/DE/FR (SG S9). Score is only 8 because data is thin, so build it once now as a list, not as a workflow |
| 5 | **U2 EMM installed base as a stacking layer** | Not a trigger by itself, but it routes the story: which EMM they run decides which angle and partner to use. Bloomberry's Workspace ONE renewal window adds timing. Confirm HG Insights coverage in a Clay sandbox first |

---

# Matrix 3: Workflow tracker

All rows are "Planned". Columns from the framework; empty columns get filled as campaigns launch.

| W # | Status | Workflow name | Mother intent | Segments | Persona | Channel | Clay URL | Copy URL | Total leads |
|---|---|---|---|---|---|---|---|---|---|
| W1 | Planned | Public tenders: MDM / UEM / smartphones | N1 | S2, S3, S4 | | | | | |
| W2 | Planned | Hiring: EMM change / Android Enterprise | U1 | S1 to S4 (+S5) | | | | | |
| W3 | Planned | Hiring: NTLM / Kerberos hardening | U4 | S1 to S4 (+S5) | | | | | |
| W4 | Planned | Acronis Cyber Files end of life (list) | U7 | All | | | | | |
| W5 | Planned | Device rollout news | U5 | S2, S3, S4 | | | | | |
| W6 | Planned | Sovereignty / cloud exit decisions | N2 | S3 | | | | | |
| W7 | Planned | Rugged / shared fleet stories | N5 | S4 (+S7) | | | | | |
| W8 | Blocked | Champion migration | U8 | All | | | | | |

Other tracker columns (Campaigns, Campaign Status, Launch Date, Campaign Name, Industry, Company Size, Enrichment 1 to 5, # Iteration, Changelog, Steps, Total Emails, Progress, Bounce) are left for launch.

---

# Open questions and checks before building

1. **Economic buyer:** who signs and from which budget (personas.md §2). The economic-buyer angles stay hypotheses until then.
2. **Procurement rules:** can Hypergate or its partners contact a buyer while a tender is open, per country? Affects how W1 runs.
3. **HG Insights / Sumble coverage:** do they detect Ivanti EPMM, Workspace ONE, BlackBerry UEM, SOTI? Test in a Clay sandbox before paying 8 credits per lookup [DS].
4. **Snippet-only evidence:** re-check the "snippet" examples and unread tender PDFs (SID Sachsen, ZIT-BB, Swissgrid, Polizei Sachsen) on the source portals before any outreach.
5. **Volume:** no per-segment counts exist yet. Run U1 and N1 on the free tiers for 30 days to get real numbers before scoring volume again.
6. **Partner routing:** where a listed partner covers the region (CO §7), decide whether signals go to the partner or to Hypergate.
7. **DACH banking gap:** no Kantonalbank, Austrian bank or Landesbank example found; run the S1 filters in Clay.
8. **iOS-only fleets** (Austrian and several German police forces): pursue or deprioritise, given Apple's built-in Kerberos extension (CP §3.9)?
