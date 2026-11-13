# Campaign strategy: Hypergate

Status: v0.1, 2026-11-13. Built with `/campaign-strategy` from CLAUDE.md, everything in `context/` and `knowledge-base/playbooks/workflow-anatomy.md`. No external research was run for this file.

**Read first**
- Every idea is a hypothesis. There is no win/loss, call or send data behind any of it (icp.md §5).
- **No sends** until legal signs off the compliance brief and Hypergate sales decides the partner policy (gtm-system.md, Open decisions 2 and 3).
- Cold email is not an option in DE, AT and IT (opt-in only), and EU countries not yet researched are treated the same. Cold email may be possible in FR, UK, US, CA (narrowly) and CH (pending legal) (compliance-cold-outreach.md §1, §12.4). Each idea lists its markets.
- Customer names in copy (Jefferies, Maersk Drilling, York Regional Police) need sign-off in `context/messaging/facts.md`, which does not exist yet.

Source keys: **SM** context/icp/signal-matrix.md, **ICP** context/icp/icp.md, **PS** context/icp/personas.md, **CS** context/docs/case-studies.md, **CMP** context/positioning/competitors.md, **MSG** context/messaging/messaging.md, **CB** context/docs/compliance-cold-outreach.md, **R/x** context/docs/research/x.md.

---

## Summary

**Target audience (given):** organisations on on-prem or hybrid AD that manage Android (or iOS) devices through an EMM. Priority segments are banking, police, government administration and utilities, in DACH and the EU first (ICP one-line; SM "Decisions taken").

**Core value proposition:** phones sign in to Active Directory the way Windows PCs do. Native Kerberos goes straight to the customer's own domain controllers, with no extra servers and no cloud broker. SMB and NetApp file access and an SDK come on top (MSG "Core message").

**Key differentiators:** native Kerberos on Android, which Android Enterprise does not ship. No gateway server and no Entra ID or Okta in the path. Works with 10 EMMs. One vendor for SSO, AD password reset and file access (positioning.md "Unique value").

---

## Customer discovery analysis

| Company | Industry | Size | Key metric | Problem solved | Source |
|---|---|---|---|---|---|
| Jefferies | Investment bank, US | 5,000 (Hypergate) to 7,787 (Wikipedia) | None; qualitative: fewer tickets, device set up in minutes | Android work profile BYOD users reaching legacy Windows-auth apps | CS |
| Maersk Drilling (now Noble) | Offshore drilling, DK | 2,500+ | None; qualitative: less support, better productivity | Shared shift devices; a login per app; local AD offline | CS |
| York Regional Police | Police, CA | 1,600 officers + 600 civilians | None; qualitative: reduced support | No Kerberos on Android Enterprise; MobileIron in place | CS |
| Logos only: Bayerische Staatskanzlei, Linz AG, European Court of Auditors, Suva, States of Jersey Police, USPS | Government, utility, EU body, insurer, police, postal | About 300 to 640,000 | None | Not stated | CS |

**Patterns**
- Industries: public sector dominates, with 5 of the 9 logos (R/customers §2). Then banking, insurance, energy and drilling, and postal.
- Size: about 300 to 640,000 staff. No floor is stated (ICP §1).
- Roles named in stories: security administrator, VP platform security engineering, business performance project manager (PS). There is no economic buyer.
- Common problems: no Kerberos on Android, a password prompt per app, shared and shift devices, an existing EMM that has to keep working.

**Targeting challenges**
1. **Compliance reorders geography.** The ICP puts DACH first, but DE and AT are opt-in for B2B email (CB §1). Cold email should start in UK, FR, US and CH (pending legal). DACH runs on opt-in routes: LinkedIn connection requests with no pitch, partners, content and, in DE only, phone pending legal (CB §12.4).
2. **Frontline is a real segment, not only the named sectors.** Maersk (shift crews) and USPS (postal) fall outside "government, banks, insurers, law firms", and Hypergate's Knox post names retail, logistics and healthcare (R/signals S3). The rugged and shared-device ideas below test this.
3. **iOS-only fleets are a weak fit.** Apple ships Kerberos SSO for free (CMP). Exclude them, or lead them with Files.

**Best customers for lookalikes:** York Regional Police (police on Android plus an EMM), Maersk Drilling (shift crews on shared devices), Jefferies (bank on Android work profile).

---

## Ranked campaign ideas

**Ranking method.** Each idea is scored on signal strength (S: how strongly the filter shows a need now) and data ease (D: can it be pulled reliably and programmatically). Both are scored 1 to 3 and the list is sorted by S+D, then by S. All scores are INFERRED judgements. Where SM already scored a signal, the scores follow SM 2a.

**Volume per month** counts accounts, not people. It is an INFERRED estimate in three bands: **Low** is under 25, **Medium** is 25 to 100, **High** is over 100. No list has been pulled yet, so real counts are unknown until the 30-day test pulls (SM open question 5). Known anchors are cited where they exist.

**Difficulty:** Easy means one data source and standard Clay columns. Medium means two or more sources, or a human check. Hard means a manual list, blocked data or a new channel.

| # | Campaign | Level | Mother intent | Tier | Segment / persona | Signal and data source | Angle | Volume / month | Difficulty | S | D |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Intune migration leaves file shares behind | Focused | Hiring specific roles | Tier 1: precise trigger, same build as #4 and #5 | S1 to S5 / EMM admin | Job post naming "Intune migration" or a move off Workspace ONE, MobileIron or BlackBerry, plus "file share", "SMB" or "SharePoint". TheirStack Jobs API regex via Clay HTTP (SM U1) | Intune has no built-in SMB access, and EMM file tools stay behind with the old EMM. Files works on any EMM (R/signals S8) | Low to Medium | Easy | 3 | 3 |
| 2 | Public tenders for MDM, UEM or smartphones | Niche | Niche-specific play (public procurement) | Tier 1: free data, three segments, one build | S2, S3, S4 / EMM admin, then head of IT | TED API, simap.ch, oeffentlichevergabe.de; CPV 32250000 and 48781000 plus MDM keywords (SM N1) | When the EMM or fleet changes, sign-in and file shares come along, whatever the EMM (SM 1b S3) | Low to Medium | Medium: open tenders go to the bidding partner or integrator; contact the buyer after award (SM top-5 caveat; CB G7-C6) | 3 | 3 |
| 3 | NTLM is already breaking on phones | Focused | Hiring specific roles; Regulatory changes | Tier 1: strongest timing, near-zero extra cost | S1 to S5 / identity and AD engineer | Job post with "NTLM", "Kerberos", "IAKerb", "AD hardening" (TheirStack, SM U4) | NTLMv1 SSO has been enforced since 13 Oct 2026, and Microsoft ships no mobile equivalent (R/market §1.2; R/signals S5) | Low (SM U4: research found no such posts yet) | Easy | 3 | 2 |
| 4 | EMM change or Android Enterprise rollout | Focused | Hiring specific roles | Tier 1: highest volume, every segment | S1 to S5 / EMM admin | Job post naming Android Enterprise, work profile, an EMM name or an EMM migration (TheirStack, Clay Find Jobs; SM U1) | Kerberos sign-in through the EMM you already run, with no gateway server (SM 1b) | Medium to High | Easy | 2 | 3 |
| 5 | Acronis Cyber Files ends 31 December | Niche | Competitor customers (one-time list) | Tier 1: only hard deadline, about 7 weeks left | All / EMM admin, file server owner | Acronis case studies (6 names, 2016 to 2019) and job posts with "Acronis Files" (SM U7). Exclude Cyber Files **Cloud** | Security updates stop 31 Dec 2026 and Acronis offers no on-prem successor. Hypergate has a migration guide in EN, DE and FR (R/signals S9) | One-time list, Low | Hard: thin data, no technographic source | 3 | 1 |
| 6 | Lookalike: police forces on Android (York Regional Police) | Niche | Lookalike of customers | Tier 1: proven story and quote, named list in SM 1c | S2 / EMM admin, security admin | Police forces with Android or Samsung fleets: SM 1c list (Met, West Midlands, Police Scotland and others), Samsung Knox stories, force press releases | Officers get one sign-in inside the MobileIron or Intune setup you already run (CS York; SM 1b S2) | Low (finite list) | Medium | 2 | 2 |
| 7 | Lookalike: banks on Android work profile (Jefferies) | Niche | Lookalike of customers | Tier 2: strong fit, old public evidence (2019) | S1 / EMM admin, identity engineer | Google Android Enterprise customer stories and SM 1c S1 list (BBVA, HSBC, Standard Chartered, Yorkshire BS and others) | Bankers on work profile still type AD passwords into each internal app (SM 1b S1) | Low | Medium | 2 | 2 |
| 8 | Lookalike: shift crews on shared devices (Maersk Drilling) | Niche | Lookalike of customers; Niche-specific play | Tier 2: good story, needs a human check per hit | S4, S7 / EMM admin, operations lead | Zebra, Samsung Knox and HMD customer stories (SM N5); SM 1c S4 list (SBB, DB, E.ON Next, PPC Romania and others) | One sign-in per shift, not per app, and it still works offline against a local AD (CS Maersk) | Low | Medium | 2 | 2 |
| 9 | Workspace ONE renewal window | Focused | Companies using specific software | Tier 2: real timing, unconfirmed segment match | S1 to S5 / EMM admin | Bloomberry Workspace ONE renewal dates; 56 renewals were due within 3 months at the time of the check, globally (SM U2) | Before you renew or move, check what your SSO and file shares depend on. Hypergate moves with you (R/voice §4 "Vendor freedom") | Low (anchor: 56 per quarter, all segments) | Medium: Bloomberry access, coverage per segment unknown | 2 | 2 |
| 10 | Passwordless on Windows, nothing on phones | Focused | Hiring specific roles | Tier 2: same build as #3, unproven pull | S1 to S5 / identity engineer | Job post with "Windows Hello for Business", "cloud Kerberos trust", "FIDO2" plus an EMM term (TheirStack) | Cloud Kerberos trust covers Windows and macOS. On Android there is no Kerberos client at all (R/signals S10) | Low to Medium | Easy | 2 | 2 |
| 11 | New hire: new head of EUC, mobility, IT or CISO | Focused | New leadership (past 90 days) | Tier 2: easy data, weakest signal | S1 to S5 / new leader | Clay Find People, months in role 3 or fewer, plus titles; Sales Navigator "changed jobs" (SM U6) | New leaders review the mobile estate. A quick win: stop phones asking for AD passwords (INFERRED) | Medium | Easy | 1 | 3 |
| 12 | SDK: Android apps still on NTLM | Niche | Hiring specific roles | Tier 3: strong pain, very low volume, no SDK proof | ISVs and in-house app teams / Android developer | Android developer job posts naming "NTLM", "SPNEGO", "Kerberos" (TheirStack) | Swap NTLM for Kerberos in your app with one SDK on Maven Central (R/company §2.3) | Low | Medium | 2 | 1 |
| 13 | Device rollout news | Focused | New product launches / niche news | Tier 2: timely, needs a human check | S2, S3, S4 / EMM admin | Google News RSS (DE and EN queries), vendor story libraries (SM U5) | You just put Android phones in staff hands. Make sure they sign in to the intranet without a password (SM 1b) | Low | Medium | 2 | 1 |
| 14 | Sovereignty or cloud-exit decisions | Niche | Regulatory changes | Tier 2: on-message, mostly in opt-in markets | S3 / head of IT, identity engineer | Google News RSS: "digitale Souveränität Verwaltung", "Microsoft Ausstieg", "openDesk" (SM N2) | A sovereign workplace needs mobile sign-in on your own AD, without Entra ID or Okta (SM 1b S3) | Low | Medium; DE administrations are opt-in only | 2 | 1 |
| 15 | Champion migration | Focused | Champion/user migration | Tier 3: blocked until the CRM export | All / past champion | Hypergate customer contacts from Zoho CRM, then Clay job-change tracking (SM U8) | You rolled out Hypergate at your last employer; same gap here? | Low | Hard: blocked | 2 | 1 |
| 16 | Golden ICP: Swiss cantonal stack | Niche | Niche-specific play | Tier 2: finite list, best market for compliance, manual research | Swiss cantonal banks, cantonal police, cantonal administrations / EMM admin | Public lists of cantons and cantonal banks; simap.ch tender history; careers pages naming the EMM | Swiss vendor, your own AD, no cloud broker. Each email names one finding from the 10-minute research | Low (finite list, count to pull) | Medium | 1 | 2 |
| 17 | Creative Ideas: 3 uses from their website | Broad | Niche-specific play | Tier 2: works on any base list, weak trigger | Base list in cold-email markets / EMM admin | Company website and careers pages (mobile workforce, intranet, apps such as SAP Fiori or ServiceNow), Claygent | "I had 3 ideas for {{company}}", each tied to a workforce or app named on their site | Medium to High | Medium | 1 | 2 |
| 18 | Creative (non-ICP): EMM integrators and MSPs | Focused | Niche-specific play (channel) | Tier 2: depends on the partner policy | Integrators and MSPs that sell Intune, Knox, Workspace ONE or Ivanti in regions with thin partner cover / practice lead | Microsoft, Samsung Knox and Omnissa partner directories; integrator service pages; compared with Hypergate's 28 listed partners (R/company §7) | Your clients on Android Enterprise hit the Kerberos gap. Add a fix that needs no servers (INFERRED) | Low to Medium | Medium: partner-policy decision first | 1 | 2 |
| 19 | Speakers and exhibitors at mobility events | Focused | Companies attending an event | Tier 3: speculative | S1 to S4 / EMM admin | Public speaker and exhibitor pages of EMM and public-sector digital events (Hypergate has attended CES, Gitex and Digitalization Fair, R/signals S13) | Reference their talk topic, then the gap it leaves on Android (INFERRED) | Low | Medium | 1 | 2 |

Ideas #1, #3, #4 and #10 are one TheirStack build with four regex sets. #2 and #13 can share Google News or TED plumbing. Building the jobs engine first unlocks four ideas (SM "Compounding insight").

---

## Campaign overviews

Value prop categories: **R** = mitigate risk, **T** = save time, **M** = save money. Cold-email markets mean FR, UK, US, CA (published addresses only) and CH (pending legal). Opt-in markets (DE, AT, IT, other EU) use LinkedIn with no pitch, partners or content (CB §12.1).

1. **Intune migration leaves file shares behind** (T, R). Hook: "Saw you're moving {{company}} to Intune." Name the old EMM's file tool from the job post (Docs@Work, BlackBerry Work, Workspace ONE Content, SOTI Hub, R/signals S8). Bridge: Intune has no built-in SMB access. Offer: Files on any EMM, opening files in native apps. Proof: none for Files (CS gap), so lead with the mechanism, not a story. CTA: "Is file-share access on the migration plan?" Differs from #4: Files-led, migration-specific. Markets: cold email where allowed; DE/AT route to the partner (EBF and Anyplace IT are listed for DE).
2. **Public tenders** (R). Public tenders are public, so the opening line can cite the notice. Open tender: route the account to the bidding integrator or partner. After award: approach the buyer and the winner with "your new EMM will need Kerberos on Android". Proof: York quote, public-sector logos. Variables: tender title, CPV, EMM named, award date. Markets: mostly DE, CH, LU and AT, so partner-led or phone first (CB G7-C6, Q9).
3. **NTLM is already breaking on phones** (R). Hook: the job post's own words about NTLM or Kerberos. Line: "NTLMv1 SSO has been enforced since the 13 Oct update. On Android, NTLM was often the path to SharePoint and file shares." CTA: "Do you know which mobile flows still hit NTLM?", which links to the readiness check offer below. Microsoft gives no date for network NTLM going off, so do not state one (ICP §3).
4. **EMM change or Android Enterprise rollout** (T). Hook: role and EMM from the job post. Bridge: Android Enterprise ships no Kerberos SSO. Route by EMM: MobileIron goes to the York story, Knox to the Knox-complementary line (CMP), Intune to the "no cloud broker" line. CTA: soft question about intranet sign-in on the new fleet.
5. **Acronis Cyber Files ends 31 December** (R, T). Short and dated. "Acronis Cyber Files security updates stop on 31 December. Acronis offers no on-prem replacement." Offer: Hypergate's migration guide in EN, DE or FR by language. The guide is the opt-in vehicle in DACH. Exclude Cyber Files Cloud. One-time list, so run it now and never again.
6. **Lookalike: police** (R, T). "York Regional Police gave 1,600 officers one sign-in on Android inside MobileIron." Needs facts.md approval. Personalise with the force's device news from SM 1c. UK forces are cold-email eligible with an LIA on file; DE forces are opt-in, and many DE and AT forces are on iPhone (weak fit, SM 1c note).
7. **Lookalike: banks** (R, T). Personalise with the bank's own Android Enterprise story (BBVA, Standard Chartered). Hook: "your bankers already use work profile." Proof: Jefferies, but do not use the Mehta quotes, which are about work profile (CS). Note DORA Art. 9(4)(d) as background only, never as the trigger (SM killed list).
8. **Lookalike: shift crews** (T). Hook: the customer story they published with Zebra or Samsung. Line: "Do your crews sign in again in every app after each shift change?" Proof: Maersk benefits, no numbers. Personas: EMM admin plus the operations lead (value-proposition.md §4).
9. **Workspace ONE renewal window** (M, R). Timing: renewal date from Bloomberry. Angle: vendor freedom, so SSO and file access are not tied to the EMM. Do not attack Omnissa; it is a partner (CMP). CTA: "Worth checking before the renewal?"
10. **Passwordless on Windows, nothing on phones** (R). Hook: their WHfB or FIDO2 rollout. Line: cloud Kerberos trust covers Windows and macOS, and Android has no Kerberos client. Note: the Microsoft doc wording is unverified (R/signals Gaps), so quote Hypergate's post, not Microsoft.
11. **New hire** (T, R). Acknowledge the new role and their previous company. A new leader inherits the mobile estate. Ask if phones still prompt for AD passwords. Stack on #4 to raise relevance (SM 2b). Weakest signal on its own, with no evidence it triggers purchases (SM U6).
12. **SDK** (T). A developer-to-developer tone. Quote the job's NTLM requirement and point to `com.hypergate:sdk` and the sample app. CTA: "Want the sample app link?" No proof exists, so keep it purely technical.
13. **Device rollout news** (T). Congratulate the rollout from the press release, then raise the intranet sign-in question. Human check per hit (SM U5).
14. **Sovereignty decisions** (R). Cite the public decision. Line: mobile sign-in on your own AD, no Entra ID or Okta. Mostly DE administrations, so route via partner, Dataport-style IT providers or content (CB §12.4).
15. **Champion migration** (T). Warm note to the past champion. Blocked until the Zoho CRM connector is authorised (gtm-system.md Open decision 4).
16. **Golden ICP: Swiss cantonal stack** (R). A rep spends 10 minutes per account: simap tender history, careers pages naming the EMM, any device news. The email names that finding plus "Swiss software, your AD, no cloud broker." Low daily volume and individually written, to fit the CH reading (CB CH_INDIVIDUAL).
17. **Creative Ideas** (T). Claygent reads the site and careers pages and returns 3 ideas, for example "field inspectors reach the intranet without a password", "case files from the SMB share in native Word" or "SAP Fiori without a second login". Each idea must map to a supported app or feature (R/company §5). CTA: "Would any of these be worth a look?"
18. **Creative (non-ICP): integrators and MSPs** (M). Pitch a margin line for their Android Enterprise clients, with no server for them to run. Exclude Hypergate's 28 listed partners. Hold until sales answers the partner-policy memo.
19. **Event speakers and exhibitors** (T). Reference the session topic and ask a follow-up question about Android. Run only once a specific event list is chosen.

---

## No-AI campaigns

**Acronis Cyber Files ends 31 December** (#5)
- Why it works without AI: the deadline is the personalisation, and every name on the list has the same problem.
- Structure: three lines. The date and what stops. Acronis offers no on-prem replacement. "Want the migration guide?"

**Intune has no file-share access** (#1, static version)
- Why it works without AI: the list filter, an Intune migration job post, already says everything.
- Structure: "Moving to Intune? It has no built-in SMB access, and {{old EMM}}'s file app stays behind. Hypergate Files works on any EMM. Worth a look before cutover?" The only variable is the old EMM name.

---

## Front-end offers

1. **Mobile NTLM readiness check.** A short guided check using Microsoft's phase 1 NTLM auditing (events 4020, 4022 and 4032 on Server 2025 and Windows 11 24H2, R/signals S5) to list which mobile flows still use NTLM. It is value before any purchase, and it fits the most specific Hypergate voice (R/voice §8). Fits #3, #10 and #12.
2. **Acronis migration guide.** Hypergate already publishes it in EN, DE and FR (R/signals S9). It is the consent-capturing vehicle for opt-in markets (CB §12.4). Fits #5 and #1.
3. **"We test your app with you."** Hypergate's FAQ offers to "test it together with you" for apps not on the list (R/voice §6). A free compatibility test on one internal app shows value inside a pilot. A free trial is reported only by a Capterra snippet (low confidence, R/company §8), so confirm the trial terms with Hypergate before offering one.

---

## Killed or parked

- **Ivanti EPMM CVEs as the trigger:** every customer is hit at once, and the story turns into scaring them about a partner (SM killed list).
- **DORA, NIS2 or FINMA as the trigger:** static with no timing. Use them as narrative lines only (SM killed list).
- **LinkedIn engagement scraping:** LinkedIn's user agreement bans scraping and automation (CB §12.3 item 6).
- **G2 and Capterra reviewers:** blocked, and avoided by this skill's rules.

---

## What to do next

1. **First workflow:** the TheirStack jobs engine, starting with #1 and #3 on the same build. They score highest, the data is easy and cheap, and the engine unlocks #4 and #10 too. Run `/build-workflow-spec` on #1.
2. **In parallel, one-time:** build the #5 Acronis list now because of the 31 Dec deadline. Hold the sends until legal sign-off, and offer the guide instead of a pitch.
3. **Before any send:** legal sign-off (CB §13), the partner-policy decision, the suppression list from Zoho CRM, and `facts.md` approval for customer names.
