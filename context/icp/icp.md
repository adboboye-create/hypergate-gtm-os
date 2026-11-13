# Hypergate ICP

Built only from `context/docs/research/` (checked 2026-11-13). Every row cites its source.

Source keys: **CO** [company.md](../docs/research/company.md), **CU** [customers.md](../docs/research/customers.md), **CP** [competitors.md](../docs/research/competitors.md), **MK** [market.md](../docs/research/market.md), **SG** [signals.md](../docs/research/signals.md), **VO** [voice.md](../docs/research/voice.md). § = section in that file. **INF** = marked INFERRED in the source, so treat it as a hypothesis.

## One-line ICP

An organisation on on-prem or hybrid Active Directory that manages Android (or iOS) devices through an EMM and needs those devices to reach Kerberos-authenticated apps, intranet or file shares without a cloud identity broker in the path. (SG "Root condition"; CO §1, §3; CP §1)

## 1. Firmographic

| Attribute | ICP | Source |
|---|---|---|
| Core industries | Government and public sector, banking, insurance, law firms | CO §1; CU §1 |
| Proven adjacent | Police (York Regional, States of Jersey), defence and aerospace, critical infrastructure, municipal utility (Linz AG), offshore drilling (Maersk) | CU §2, §3, §4; SG S4 |
| Size | No stated minimum. Named customers range from about 240 to 306 staff (States of Jersey Police) up to 640,000 (USPS). The three case-study customers have about 2,200 to 7,800 staff | CU §2 |
| Geography | Existing logos in US, Canada, DE, AT, CH, LU, Jersey, DK. Site and 2026 posts in EN/DE/FR/IT (INF: DACH, FR, IT, CH are priority). US East Coast base, West Coast push since CES 2025 (INF). Partners cover about 20 regions | CU §2; CO §7, §9; SG S13 |
| Workforce | Mobile or frontline staff who need internal systems: travelling bankers, rig shift crews, police officers | SG "Triggers" table |
| Regulatory context | DORA Art. 9(4)(d) strong authentication (EU finance, since 17 Jan 2025); NIS2 Art. 21(2)(i)/(j) access control and MFA; FINMA Circ. 2023/1; Swiss CI attack reporting. None of them requires Kerberos, so treat them as background pressure, not proven triggers | MK §3, §4 |

## 2. Technographic

**Must have**

| Requirement | Source |
|---|---|
| On-prem or hybrid AD, with domain controllers / KDC reachable from devices (directly or over any VPN/tunnel) | CO §1, §3 |
| Mobile fleet managed by an EMM that supports managed config. Supported EMMs: Intune, Ivanti (MobileIron), SOTI MobiControl, 42Gears, Samsung Knox, Workspace ONE, BlackBerry UEM, Techstep, Kace, PushManager | CO §3, §4 |
| Internal resources on Kerberos / Windows integrated auth: intranet, legacy web apps, SMB/CIFS or NetApp shares | CO §2, §3; CU §3.1 |
| Android 7+ or iOS 13+. Guaranteed on Android Enterprise Recommended devices and all Samsung Galaxy | CO §3 |

**Strong-fit markers**

| Marker | Source |
|---|---|
| Android Enterprise in use: work profile (BYOD), fully managed, kiosk, multi-user shared devices | CO §2.1; SG S1 |
| Zebra rugged devices (validated: TC21/26/52/57/72/77, ET51) or Samsung fleets on Knox | SG S3 |
| Mobile access to SharePoint, file shares or web apps still runs on NTLM | SG S5 |
| A mobile file tool being retired or lost in a migration: Acronis Cyber Files / Files Connect, Docs@Work, BlackBerry Work, Workspace ONE Content, SOTI Hub | SG S8, S9 |
| In-house Android apps that authenticate to on-prem Windows servers (SDK prospects) | SG S5; CO §2.3 |
| Multi-forest or air-gapped AD | CO §3 |
| Business apps that use Chrome Custom Tabs or a webview (Edge, Chrome, SAP Fiori, ServiceNow, Salesforce, Workday, Jira, Confluence) | CO §5 |

**Incumbents to expect** (each needs a gateway server or cloud broker, so they are not an automatic disqualifier): Entra ID broker plus Application Proxy, Okta, Ivanti Docs@Work plus Sentry, BlackBerry BEMS Docs, Workspace ONE Content Gateway. (CP §2, §3)

## 3. Intent signals

Urgency ratings are from SG "Detection summary" and are INF.

| Signal | What to look for | Urgency | Source |
|---|---|---|---|
| S9 Acronis Cyber Files EOL | Acronis Cyber Files / Files Connect users. Security updates stop 2026-12-31. Acronis Cyber Files Cloud is a different product and does not count | High | SG S9 |
| S5 NTLM removal | NTLMv1 SSO has been enforced since the 13 Oct 2026 update (KB5066470), so this is already live, not upcoming. Network NTLM goes off in the next major Windows Server release; Microsoft gives no date, and "2027" is Hypergate's projection | High | SG S5; MK §1.1, §1.2 |
| S8 EMM migration | Moves to Intune, or away from Workspace ONE (Omnissa ownership change), Ivanti EPMM (Jan 2026 CVEs, INF) or BlackBerry | Medium | SG S8 |
| S3 Frontline / shared-device rollout | New Zebra or Samsung fleets, shift-based shared devices | Medium | SG S3 |
| S4 Sovereignty / no cloud broker | Cloud-exit policies, air-gapped sites, classification rules | Medium | SG S4 |
| S1/S2 Android Enterprise adoption | Late moves off Device Admin, Android added next to iOS, BYOD launches | Ongoing, long tail | SG S1, S2 |
| S10 Passwordless rollout | WHfB, FIDO2, cloud Kerberos trust on Windows while Android has no Kerberos client | Not rated | SG S10 |
| S12 Mobile lockout tickets | Password expiry and lockouts on phones driving helpdesk load | Not rated | SG S12 |
| S6/S7 RC4 removal, cert mapping | AD hardening work. Deadlines have passed | Low for new logos | SG S6, S7 |

No evidence in the research for: funding rounds, executive hires, job posts or tenders naming Hypergate as triggers (SG "no evidence found").

## 4. Persona

Full detail is in [personas.md](personas.md).

| Role | Who | Evidence strength |
|---|---|---|
| Champion | Mobility / EMM / security admin who runs the device fleet | Medium: named customer contact (CU §3.3) plus the technical blog's audience (VO §9, INF) |
| Economic buyer | **Unknown.** The research does not say who signs | Weak: open question |
| Influencer | Identity / AD / platform security engineering, in-house Android developers, business project lead | Medium: named contacts (CU §3.1, §3.2) plus Microsoft change pressure (SG S5 to S7) |

## 5. Engagement readiness

**Read this first.** These tiers are a working hypothesis to test:

- There is no win/loss or conversion data behind them.
- The case studies don't say what event started any purchase (SG "Gaps").
- Tier = the urgency rating in section 3, never upgraded.
- Most must-haves (on-prem AD, Kerberos apps, NTLM use) can't be seen from outside. Every "how to find it" idea below comes from SG and is INF, so expect to confirm fit on the first call rather than before it.

**Ready now: a time-bound trigger with a product to match**

| Trigger | Evidence that puts an account here | How to find it (SG, INF) | Product | Proof we can show | Caveat |
|---|---|---|---|---|---|
| Acronis Cyber Files / Files Connect (on-prem) | Account confirmed running it | Job posts naming "Acronis Files", Acronis forum threads, old Acronis case studies (SG S9) | Files | No Files case study (CU "Gaps"). Hypergate migration guide in EN/DE/FR (SG S9) | Updates stop 2026-12-31. Cyber Files **Cloud** does not count |
| NTLM on mobile paths | Mobile access to SharePoint, file shares or web apps runs on NTLM; or in-house Android apps use NTLM | Job posts with "NTLM", "Kerberos migration", "IAKerb"; developer posts with "SPNEGO"; helpdesk posts on mobile 401 loops (SG S5) | Authenticator; SDK for in-house apps (CO §2.3) | No customer story ties a purchase to NTLM (SG "Gaps") | Pitch it as already breaking (enforced since 13 Oct 2026). The next step has no Microsoft date (MK §1.1, §1.2) |

**Warming: a structural trigger, no hard date**

| Trigger | Evidence | How to find it (SG, INF) | Product | Proof we can show |
|---|---|---|---|---|
| EMM migration (rated Medium in SG, so not Ready now) | Moving to Intune, or away from Workspace ONE, Ivanti or BlackBerry | Job posts "Intune migration" / "migrate from Workspace ONE / MobileIron / BlackBerry UEM" (SG S8) | Files (Intune has no built-in SMB access, SG S8), Authenticator | York Regional Police shows the MobileIron integration, not a migration (CU §3.3) |
| Frontline / shared-device rollout | New Zebra or Samsung fleet on shift work | Zebra/Samsung customer news, rugged-device tenders (SG S3) | Authenticator | Maersk Drilling (CU §3.2) |
| Android Enterprise / BYOD adoption | Late move off Device Admin, Android added next to iOS | Job posts "Android Enterprise migration", "work profile", BYOD launches (SG S1, S2) | Authenticator | Jefferies, 2019. Its quotes are about the Android work profile, not about Hypergate (CU §3.1) |
| Sovereignty / no cloud broker | Cloud-exit policy, air-gapped sites | Public-sector policy news, DACH/EU tenders that mention "on-premises" (SG S4) | Authenticator, Files | Logos only (Bayerische Staatskanzlei, European Court of Auditors). No story (CU §2) |

**Fit only:** meets the must-haves, no signal seen. The only proof is the logo wall, and none of the case studies has numbers (CU "Gaps").

**Not ready:** fails a must-have. See "Not a fit".

**Routing:** Hypergate "is distributed through our partner network, where available" (CO §7). Where a listed partner covers the region, check partner routing first.

## Not a fit

| Profile | Why | Source |
|---|---|---|
| Cloud-only identity, no on-prem or hybrid AD | Hypergate talks to on-prem DCs/KDC. Cloud IdPs ship their own mobile SSO brokers | CO §3; CP §3.1, §3.4 |
| No EMM / unmanaged devices | Configuration is delivered as managed config through an MDM | CO §3 |
| No Kerberos or Windows-auth resources (everything is SaaS) | Nothing on-prem to sign in to. Play listing names Kerberos and ADFS; SAML is not mentioned | CO §3 |
| Devices below Android 7 or iOS 13 | Unsupported | CO §3 |
| Acronis Cyber Files **Cloud** users | Still an active product, so no EOL trigger | SG S9 |
| Weaker fit: iOS-only fleet | Apple ships a free Kerberos SSO extension. Hypergate's iOS add-ons are mainly AD password features | CP §3.9 (INF); CO §2.1 |
| Weaker fit: already standardised on Entra App Proxy or Okta and fine with a cloud broker | Hypergate's main differentiator is "no cloud broker" | CP §1, §3.1 (INF) |

## Open questions

1. Minimum company size or device count, deal size, pricing unit (per user or per device): unknown (CO §8).
2. Economic buyer title and budget line: not in the research.
3. Which segment wins most often: there is no win/loss data, and today's customer count is unknown (CO §9, "Gaps").
4. Whether the six logo-only customers are current, and which product they use (CU "Gaps").
5. Healthcare, retail and logistics fit: only mentioned in the Knox post (SG S3). Imprivata is adjacent in healthcare (CP §3.11).
6. Whether DORA, NIS2 or FINMA actually trigger purchases (MK §3, §4).
7. Hypergate's FAQ says iOS only has Kerberos "through constrained delegation". This conflicts with Apple's documentation (CP §3.9).
8. Which Papers entity signs customer contracts (CO §14).
