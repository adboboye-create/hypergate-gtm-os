# Hypergate: Buying Signals and Triggers (raw research)

Checked: 2026-11-13

Raw research, not conclusions. Each signal lists: what it is, evidence with source URL, and detection ideas. All detection ideas are INFERRED (our ideas, not stated by any source). Hypergate blog dates come from page metadata (datePublished).

## Sources used

- Hypergate customer stories: https://hypergate.com/blog/success-story-jefferies/, https://hypergate.com/blog/success-story-with-maersk-drilling/, https://hypergate.com/blog/success-story-with-york-regional-police/
- Hypergate blog (technical and announcement posts, 2019 to 2026): https://hypergate.com/blog/ and the individual posts linked below
- Hypergate pages: https://hypergate.com/, https://hypergate.com/mobile-sso-without-cloud-broker/
- Google: https://blog.google/products/android-enterprise/jefferies-case-study/, https://developers.google.com/android/work/device-admin-deprecation, https://blog.google/products/android-enterprise/da-migration/
- Microsoft (via Message Center mirror): https://mc.merill.net/message/MC902778
- Security press on Ivanti EPMM: https://www.helpnetsecurity.com/2026/01/30/ivanti-epmm-cve-2026-1281-cve-2026-1340/, https://www.bleepingcomputer.com/news/security/ivanti-warns-of-two-epmm-flaws-exploited-in-zero-day-attacks/amp/
- NTLM press: https://thehackernews.com/2026/02/microsoft-begins-ntlm-phase-out-with.html, https://www.securityweek.com/microsoft-moves-closer-to-disabling-ntlm/amp/
- VMware/Omnissa background: https://www.techtarget.com/enterprise-software/opinion/VMware-EUC-is-now-Omnissa-What-we-know-so-far

## Root condition behind every signal

Hypergate's core claim: Android Enterprise has no built-in Kerberos SSO. "Android Enterprise ships no built-in Kerberos SSO, so users on fully managed Samsung fleets still type Active Directory passwords into their phones, app by app." (source: https://hypergate.com/blog/samsung-mdm-knox-sso/, checked 2026-11-13). The same problem statement appears in two of three customer stories: "Android Enterprise doesn't support Kerberos Authentication natively, so therefore enablement of Single Sign-On with a local active directory previously was not possible." (source: https://hypergate.com/blog/success-story-with-york-regional-police/, checked 2026-11-13).

So the fit precondition is: managed Android (or iOS) devices + on-prem or hybrid Active Directory + internal apps, intranet or file shares that use Kerberos/Windows authentication. Most signals below are events that make this gap visible or urgent.

## What triggered purchase in the customer stories

| Customer | Trigger in their own story | Source |
|---|---|---|
| Jefferies | Move to Android Enterprise work profile for a BYOD fleet ("85% of their work devices are employee-owned (BYOD)"); travelling bankers needing in-house finance systems; legacy apps on "Windows authentication infrastructure" in a "hybrid cloud environment" | https://hypergate.com/blog/success-story-jefferies/ (checked 2026-11-13) |
| Maersk Drilling | Shared Android devices on 24h shift work; "devices are shared by multiple users"; auto logout after each shift; local AD on rigs for offline auth; "each user was prompted for their credentials for each application" | https://hypergate.com/blog/success-story-with-maersk-drilling/ (checked 2026-11-13) |
| York Regional Police | Officers and civilians "using Android phones for their daily work"; Android Enterprise lacked Kerberos so SSO to local AD "previously was not possible"; existing MobileIron MDM | https://hypergate.com/blog/success-story-with-york-regional-police/ (checked 2026-11-13) |

## Signals

### S1. Adopting Android Enterprise (including migration off Device Admin)

- What: an org moves Android devices onto Android Enterprise (work profile, fully managed, dedicated) and loses the Kerberos SSO that EMM-proprietary Device Admin setups used to give.
- Evidence:
  - Hypergate, 2019: "In 2019 the already depreciated device administrator method for device management will disappear and hence a shift to the newer (and better) Android Enterprise device management is unavoidable." and "Android Enterprise is lacking an important feature which used to work with EMM Proprietary solutions on Device Admin" (source: https://hypergate.com/blog/android-enterprise-is-lacking-an-important-feature/, checked 2026-11-13).
  - Hypergate, 2019: "Because Device Admin is being deprecated and companies have to switch to Android Enterprise the Android world is lacking this important feature." (source: https://hypergate.com/blog/seamless-single-sign-on-stay-secure-on-android-enterprise/, checked 2026-11-13).
  - Hypergate on VMware: "The change from device administrator removes a feature that previously worked with EMM Proprietary solutions like VMware Workspace ONE: Kerberos based Single Sign-on (SSO) or Kerberos Constrained Delegation." (source: https://hypergate.com/blog/vmware_workspace_one_works_with_hypergate/, checked 2026-11-13).
  - Hypergate with MobileIron, 2020: "the lack of Kerberos SSO on Android (Active Directory SSO support) can be a blocker when rolling out Android Enterprise" (source: https://hypergate.com/blog/mobileiron-and-hypergate-enable-sso/, checked 2026-11-13).
  - Google: Device Admin deprecated for enterprise use in Android 9.0, with functions removed in Android 10.0 (source: https://developers.google.com/android/work/device-admin-deprecation, checked 2026-11-13 via search result summary; page not opened directly). Google blog "What you need to know about Device Admin deprecation" (source: https://blog.google/products/android-enterprise/da-migration/, checked 2026-11-13 via search result; not opened).
  - Microsoft Intune ended support for Android device administrator on devices with Google Mobile Services as of December 31, 2024 (source: https://mc.merill.net/message/MC902778, checked 2026-11-13 via search result summary).
- Timing note: INFERRED: the Device Admin deadline has passed (2019 to 2024), so this is now a long-tail signal: laggards still on Device Admin, or non-GMS fleets.
- Detection (INFERRED): job posts mentioning "Android Enterprise migration", "device admin", "work profile", "COPE", "fully managed"; EMM community or LinkedIn posts by IT staff about Android Enterprise rollouts; RFPs for Android device refresh.

### S2. Switching corporate mobile platform to Android, or adding Android next to iOS (incl. BYOD)

- What: an org that was iOS-only (where Apple ships a Kerberos client) adds or switches to Android and finds the SSO gap.
- Evidence:
  - "Administrators have been able to use Kerberos for single sign-on on iOS for years because Apple natively provides a Kerberos client in the operating system, but to date, Android has never natively offered support for Kerberos." (source: https://hypergate.com/blog/vmware_workspace_one_works_with_hypergate/, checked 2026-11-13).
  - "While companies got the advantage of the Kerberos SSO on their iOS devices, Android users where left behind." (source: https://hypergate.com/blog/seamless-single-sign-on-stay-secure-on-android-enterprise/, checked 2026-11-13).
  - Jefferies: BYOD on Android work profile (source: https://hypergate.com/blog/success-story-jefferies/, checked 2026-11-13).
- Detection (INFERRED): device tenders or press about Android handset rollouts (e.g. police forces issuing Android phones to officers); BYOD policy launches; job posts listing both "Intune/Workspace ONE" and "Android Enterprise"; Samsung or Zebra customer announcements.

### S3. Frontline, shift-based or rugged / shared-device rollouts

- What: shared Android devices across shifts (rigs, police, retail, logistics, healthcare) where repeated AD logins hurt productivity.
- Evidence:
  - Maersk Drilling: "devices are shared by multiple users. The devices log out automatically and close all open sessions in the background after each shift, interrupting the workflow." (source: https://hypergate.com/blog/success-story-with-maersk-drilling/, checked 2026-11-13).
  - Zebra validation (2024-06-07), tested on "TC21 TC26 TC52 TC57 TC72 TC77" and tablet "ET51" (source: https://hypergate.com/blog/hypergate-is-zebra-validated-again/, checked 2026-11-13).
  - Samsung Knox post: "Samsung devices dominate corporate Android fleets, and no other Android OEM ships a comparable enterprise stack out of the box." and Knox Manage "shows up so often in retail, logistics and healthcare." (source: https://hypergate.com/blog/samsung-mdm-knox-sso/, checked 2026-11-13).
  - Ingram Micro partnership (2020) ties Hypergate to Android Zero-touch reseller rollouts: "customers can now directly get access to company data just minutes after they received their boxed device." (source: https://hypergate.com/blog/hypergate-and-ingram-micros-partnership/, checked 2026-11-13).
- Detection (INFERRED): press releases or case studies from Zebra, Samsung, Honeywell naming a new customer fleet; job posts for "mobility engineer" with Zebra/Samsung Knox/KME; tenders for rugged handhelds; news of police body-worn/phone programmes; offshore, utilities, logistics companies announcing digital worker programmes.

### S4. On-prem or hybrid Active Directory with Kerberos-protected internal apps, plus a need to avoid cloud identity brokers (sovereignty, air-gap, regulation)

- What: orgs that cannot or will not put Entra ID / Okta in the mobile auth path.
- Evidence:
  - "Sovereignty and classification requirements often prevent the use of a cloud identity provider. Defence, government, and critical infrastructure are commonly required to keep authentication metadata within national or accredited boundaries." (source: https://hypergate.com/mobile-sso-without-cloud-broker/, checked 2026-11-13).
  - "Air-gapped networks, sites without persistent internet connectivity, and environments where a cloud identity provider cannot be a single point of failure all need an authentication model that does not depend on external services." (same source).
  - Digital sovereignty post (2026-01-14) cites: Microsoft France testimony to the French Senate on June 10, 2025, Entra ID outages on February 25 and October 29, 2025, and Schleswig-Holstein moving off Microsoft (source: https://hypergate.com/blog/digital-sovereignty-authentication/, checked 2026-11-13). Hypergate states Schleswig-Holstein "expects to save over 15 million euros in licence costs in 2026" (same source; Hypergate's figure, not verified by us).
  - Maersk rigs keep a local AD "to make sure users can authenticate even when the mobile connection is lost due to bad weather conditions." (source: https://hypergate.com/blog/success-story-with-maersk-drilling/, checked 2026-11-13).
  - Homepage: "Specially designed for on-premise and hybrid environments, our products cater to organizations that prioritize privacy and security." (source: https://hypergate.com/, checked 2026-11-13).
- Detection (INFERRED): public-sector, defence, utilities, banks and insurers in DACH/EU; job posts asking for "Active Directory", "Kerberos", "PKI/NDES/SCEP" alongside an EMM; public sovereignty or "cloud exit" policy announcements (state governments, ministries); tenders mentioning "on-premises" and "mobile device management".

### S5. Microsoft NTLM deprecation (hard deadline October 2026, network NTLM off in next Server LTSC)

- What: mobile access to on-prem SharePoint, file shares and intranet often runs on NTLM; when NTLM is blocked server-side, Android/iOS flows break.
- Evidence:
  - Hypergate (2026-06-25): "On Android and iOS, NTLM was often the actual path to on-prem SharePoint, file shares, and internal web apps." "Microsoft's plan ships no mobile equivalent, so those flows break when NTLM is blocked." "First hard deadline: NTLMv1 enforcement, October 2026" (source: https://hypergate.com/blog/disable-ntlm-mobile-devices/, checked 2026-11-13).
  - Hypergate timeline: Phase 1 auditing on Windows 11 24H2 / Server 2025 (events 4020, 4022, 4032); Phase 2 H2 2026 IAKerb and LocalKDC; "in October 2026 the BlockNTLMv1SSO default flips from Audit to Enforce (KB5066470)"; Phase 3 "next Windows Server LTSC (projected 2027)" network NTLM disabled by default (same source).
  - Independent coverage: Microsoft published a three-phase plan to disable NTLM by default, reported late January / early February 2026 (sources: https://thehackernews.com/2026/02/microsoft-begins-ntlm-phase-out-with.html, https://www.securityweek.com/microsoft-moves-closer-to-disabling-ntlm/amp/, checked 2026-11-13 via search summary). The October 2026 KB5066470 date was not confirmed against Microsoft's own material in our search; treat as Hypergate's claim.
  - Earlier Hypergate post on the same theme (2024-02-02): https://hypergate.com/blog/migrate-from-ntlm-to-kerberos-add-kerberos-support-on-android/ (checked 2026-11-13).
  - App-developer angle (2026-05-13): "Android apps that still authenticate with NTLM need a replacement, and that replacement is Kerberos." Hypergate SDK "com.hypergate:sdk" on Maven Central (source: https://hypergate.com/blog/android-kerberos-sso-ntlm-sdk/, checked 2026-11-13).
- Timing: today (2026-11-13) is just after the October 2026 NTLMv1 date claimed by Hypergate; next stated milestone is the next Windows Server LTSC, "projected 2027" (Hypergate's projection).
- Detection (INFERRED): job posts mentioning "NTLM", "NTLM removal", "Kerberos migration", "IAKerb"; companies with in-house Android apps (Play Store managed apps, developer job posts with "SPNEGO" or "NTLM"); helpdesk/forum posts about 401 loops on mobile after Windows updates; ISVs whose Android apps talk to on-prem Windows servers (SDK prospects).

### S6. Microsoft Kerberos RC4 removal (point of no return July 14, 2026)

- What: service accounts with RC4-only keys stop issuing tickets; mobile SSO to those apps fails with 401 loops that look like NTLM blocks.
- Evidence:
  - Hypergate (2026-07-14): "The July 2026 cumulative update permanently removes the RC4DefaultDisablementPhase rollback key from domain controllers (CVE-2026-20833, KB5073381)." Phases: January 13, 2026 audit; April 14, 2026 AES-only default; July 14, 2026 rollback removed (source: https://hypergate.com/blog/kerberos-rc4-removal-mobile-sso/, checked 2026-11-13).
  - "cyber insurers have started asking about Kerberos encryption posture in 2026 renewal questionnaires." (same source; Hypergate's claim, not verified).
  - Hypergate says its Authenticator "negotiates AES by default" so the device side needs no change (same source). INFERRED: this is more a conversation opener with existing mobile-Kerberos users than a net-new purchase trigger.
- Detection (INFERRED): AD hardening projects in job posts ("Kerberoasting", "RC4", "gMSA"); security advisories from national CERTs referencing KB5073381.

### S7. Strong Certificate Mapping enforcement (KB5014754, full enforcement September 2025)

- What: MDM-issued user certificates without the AD SID break certificate-based Kerberos (PKINIT) on mobile.
- Evidence:
  - Hypergate (2025-04-08): "Kerberos authentication for mobile clients (Android, iOS, etc.) using certificate-based login will break if the certificates aren't updated"; dates "February 11, 2025" (strong mapping default) and "September 10, 2025" (compatibility mode phased out); affects Intune, Ivanti, Workspace ONE, BlackBerry UEM, SOTI MobiControl, Samsung Knox (source: https://hypergate.com/blog/preparing-your-mdm-uem-for-strong-certificate-mapping-enforcement/, checked 2026-11-13).
  - NTLM post repeats: "Strong Certificate Mapping Enforcement, in strict mode since September 2025, rejects certificates that don't." (source: https://hypergate.com/blog/disable-ntlm-mobile-devices/, checked 2026-11-13).
- Timing: deadline passed. INFERRED: mainly relevant to orgs doing certificate-based mobile auth for the first time.
- Detection (INFERRED): job posts for PKI/NDES/SCEP admins tied to an EMM; forum posts about KDC event ID 39/41.

### S8. EMM migration (to Intune or between UEMs)

- What: moving EMM removes vendor-proprietary file access and SSO tools; Intune has no built-in SMB file access.
- Evidence:
  - Hypergate (2025-07-03): "Intune lacks a built-in solution for accessing SMB/CIFS network file shares, posing challenges for organizations needing to maintain secure, on-premises file access." Lists vendor-tied tools that a migration leaves behind: "Ivanti (MobileIron) Docs@Work", "BlackBerry Work", "VMware Workspace ONE Content", "SOTI Hub" (source: https://hypergate.com/blog/simplify-intune-migration-with-hypergate-files-for-on-prem-access/, checked 2026-11-13).
  - "Whether you are currently using Microsoft Intune or planning a migration to it, Hypergate Files is completely EMM-agnostic." (source: https://hypergate.com/blog/mobile-file-access-acronis-cyber-files/, checked 2026-11-13).
  - Context: VMware EUC (Workspace ONE) became Omnissa in 2024 after Broadcom sold it to KKR; Gartner advised customers to anticipate pricing changes (source: https://www.techtarget.com/enterprise-software/opinion/VMware-EUC-is-now-Omnissa-What-we-know-so-far, checked 2026-11-13 via search summary). INFERRED: ownership change can prompt EMM re-evaluation; no data found on actual migration volumes.
  - Ivanti EPMM (formerly MobileIron Core): critical zero-days CVE-2026-1281 and CVE-2026-1340 disclosed January 29, 2026, CVSS 9.8, exploited in the wild, CISA KEV listing (sources: https://www.helpnetsecurity.com/2026/01/30/ivanti-epmm-cve-2026-1281-cve-2026-1340/, https://www.bleepingcomputer.com/news/security/ivanti-warns-of-two-epmm-flaws-exploited-in-zero-day-attacks/amp/, checked 2026-11-13 via search summary). INFERRED: repeated EPMM incidents may push MobileIron shops (York Regional Police's EMM was MobileIron) to migrate, which would reopen the SSO and file-access question. No official Ivanti EPMM end-of-life date found.
- Detection (INFERRED): job posts "Intune migration", "migrate from Workspace ONE/MobileIron/BlackBerry UEM"; LinkedIn posts from EUC teams; tenders for UEM replacement; companies listed as affected by EPMM breaches.

### S9. Acronis Cyber Files end of life (support ends December 31, 2026)

- What: on-prem mobile file access tool going away; Hypergate Files positioned as replacement.
- Evidence:
  - "Acronis Cyber Files reached end-of-life on 31 December 2025. The last security updates stop on 31 December 2026." "Acronis isn't offering an on-premises replacement or a migration path." (source: https://hypergate.com/blog/acronis-cyber-files-is-end-of-life-a-migration-guide-for-mobile-access-to-on-prem-file-servers/, checked 2026-11-13).
  - Applies to "Acronis Cyber Files and its companion, Acronis Files Connect"; "Acronis Cyber Files Cloud is a different, still-active product" (same source).
  - Earlier post (2025-12-17): "For many IT leaders, end-of-life announcements act as a forced checkpoint" (source: https://hypergate.com/blog/mobile-file-access-acronis-cyber-files/, checked 2026-11-13).
  - Hypergate publishes this guide in EN, DE and FR (sitemap: https://hypergate.com/de/blog/acronis-cyber-files-end-of-life-migrationsleitfaden-mobiler-dateizugriff/, https://hypergate.com/fr/blog/acronis-cyber-files-fin-de-vie-guide-migration-acces-mobile/, checked 2026-11-13).
- Timing: about 7 weeks left until December 31, 2026 (as of 2026-11-13). Most time-sensitive signal found.
- Detection (INFERRED): Acronis Files Connect / Cyber Files customer lists (technographic tools, old Acronis case studies, Mac-in-enterprise users), job posts mentioning "Acronis Files", public Acronis forum threads.

### S10. Going passwordless / hybrid identity (Windows Hello for Business, FIDO2, cloud Kerberos trust)

- What: orgs rolling out passwordless on Windows find mobile has no equivalent path to on-prem Kerberos resources.
- Evidence:
  - Hypergate (2026-07-22): cloud Kerberos trust "exists only on Windows and macOS. On Android there is no Kerberos client at all, and Microsoft's own docs say to install a non-Microsoft SSO client." (source: https://hypergate.com/blog/cloud-kerberos-trust-explained/, checked 2026-11-13). We did not verify the Microsoft doc wording directly.
- Detection (INFERRED): job posts mentioning "Windows Hello for Business", "cloud Kerberos trust", "FIDO2 rollout", "passwordless" plus Android/iOS fleets; Entra Private Access or Global Secure Access rollouts.

### S11. Browser or app vendor changes enabling Kerberos on mobile

- What: new support in common apps widens use cases.
- Evidence: "Microsoft Edge for Android has added support for Hypergate Authenticator" starting "version 124.0.2478.50" (2024-05-15) (source: https://hypergate.com/blog/microsoft-edge-now-supports-kerberos-via-hypergate-authenticator/, checked 2026-11-13). Compatibility post for Android 15 and iOS 18 exists (URL from sitemap: https://hypergate.com/blog/hypergate-authenticator-and-files-compatible-with-android-15-and-ios-18/; not opened).
- Detection (INFERRED): orgs standardising on Edge for Android via Intune; new Android OS versions (watch for compatibility announcements).

### S12. Helpdesk load from password resets and lockouts on mobile

- What: password expiry and lockouts on phones drive tickets; Hypergate offers on-device AD password reset.
- Evidence: "Hypergate Authenticator empowers your users to reset their Active Directory password by themself" (homepage, Password Reset feature) (source: https://hypergate.com/, checked 2026-11-13); "Mobile password prompts drive lockouts, and every lockout is a ticket." (source: https://hypergate.com/blog/samsung-mdm-knox-sso/, checked 2026-11-13). All three case studies list reduced support as a benefit, with no numbers (see customers.md).
- Detection (INFERRED): service desk job posts in orgs with large Android fleets; public IT strategy documents citing ticket reduction goals.

### S13. Market and go-to-market signals from Hypergate itself

- Hypergate exhibited at CES 2025 (Las Vegas) to "expand our reach beyond our established partnerships and customer base on the East Coast, opening new doors on the West Coast" (source: https://hypergate.com/blog/2025-marks-hypergates-debut-at-ces/, checked 2026-11-13). INFERRED: US is an active expansion target.
- Gitex Global 2024 attendance (URL from announcement category: https://hypergate.com/blog/hypergate-is-going-to-gitex/; not opened).
- Digitalization Fair 2023 focused on "Enterprise Mobility for the Public Sector" (title from https://hypergate.com/blog/category/announcement/, checked 2026-11-13).
- Partners: EBF (Germany, 2021), Ingram Micro (2020, Zero-touch reseller), MobileIron Marketplace Premier (2019) (sources: https://hypergate.com/blog/hypergate-and-ebf-partnership/, https://hypergate.com/blog/hypergate-and-ingram-micros-partnership/, https://hypergate.com/blog/mobileiron-partnership/, checked 2026-11-13).
- Content languages: EN, DE, FR, IT versions of 2026 posts (sitemap https://hypergate.com/post-sitemap.xml, checked 2026-11-13). INFERRED: DACH, France, Italy and Switzerland are priority markets.

## Signals asked about but with no evidence found

- Funding rounds, new IT leaders (CIO/CISO hires) or expansion as triggers: no Hypergate source ties a purchase to these. INFERRED only: a new head of EUC/mobility or a new CISO could reopen mobile auth decisions.
- Hiring for mobility/EUC roles: no example found of a job post naming Hypergate (web search for "Hypergate" with job/tender terms, 2026-11-13, returned nothing relevant).
- Tenders or procurement records naming Hypergate: none found (same search). Swiss simap.ch and EU TED not searched.

## Detection summary (all INFERRED)

| Signal | Best public data source | Urgency as of 2026-11-13 |
|---|---|---|
| S9 Acronis Cyber Files EOL | Technographics, Acronis forums, job posts | High (support ends 2026-12-31) |
| S5 NTLM removal | Job posts, in-house Android apps, Windows Server upgrade plans | High (next LTSC "projected 2027" per Hypergate) |
| S8 EMM migration | Job posts, Ivanti EPMM incident news, Omnissa renewals | Medium |
| S3 Frontline / rugged rollouts | Zebra/Samsung customer news, device tenders | Medium |
| S4 Sovereignty / on-prem | Public-sector policy news, DACH/EU tenders | Medium |
| S1/S2 Android Enterprise adoption | Job posts, BYOD/device programme news | Ongoing, long tail |
| S6/S7 RC4 and cert mapping | AD hardening job posts | Low for net-new (deadlines passed) |

## Gaps

- Google pages on Device Admin deprecation and Microsoft Message Center MC902778 were seen only via search summaries, not opened; verify before citing in copy.
- KB5066470 October 2026 NTLMv1 enforcement date is Hypergate's claim; not confirmed against Microsoft's own docs.
- Microsoft docs wording "install and configure a non-Microsoft SSO client" (cloud Kerberos / Global Secure Access) not verified on learn.microsoft.com.
- No official Ivanti EPMM end-of-life date found; Ivanti lifecycle pages reportedly require login.
- No data on how many Omnissa or Ivanti customers are migrating to Intune.
- Customer stories do not say what event started the buying process (no dates of purchase, no "we switched from X" detail beyond EMM names).
- No job posts, LinkedIn posts or tenders naming Hypergate found.
- Samsung Knox Marketplace, Omnissa Marketplace, Google Android Enterprise Solutions Directory listings not checked.
- Hypergate figures quoted inside its blog (e.g. Schleswig-Holstein savings, insurer questionnaires) not independently verified.
