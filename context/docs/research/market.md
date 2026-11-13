# Market and regulatory drivers: Hypergate buyers (raw research)

Checked: 2026-11-13

Raw research, not conclusions. Buyers in scope: enterprise IT, identity and mobility teams that need SSO, Kerberos, conditional access and file access on managed Android (and iOS). Quotes are exact. Anything inferred is marked "INFERRED:". Items marked "via search result summary" were not read directly on the source page.

## Sources used

- Microsoft: https://techcommunity.microsoft.com/blog/windows-itpro-blog/advancing-windows-security-disabling-ntlm-by-default/4489526 , https://support.microsoft.com/kb/5066470 , https://support.microsoft.com/en-us/topic/how-to-manage-kerberos-kdc-usage-of-rc4-for-service-account-ticket-issuance-changes-related-to-cve-2026-20833-1ebcda33-720a-4da8-93c1-b0496e1910dc , https://techcommunity.microsoft.com/blog/intunecustomersuccess/intune-ending-support-for-android-device-administrator-on-devices-with-gms-in-de/3915443 , https://learn.microsoft.com/en-us/entra/identity/authentication/concept-fido2-compatibility , https://blogs.microsoft.com/blog/2023/08/09/microsoft-solutions-boost-fortune-500-frontline-productivity-with-next-generation-ai/
- Google: https://developers.google.com/android/work/device-admin-deprecation
- Samsung: https://docs.samsungknox.com/dev/knox-sdk/release-notes/knox-sdk-341/
- EU: https://www.nis-2-directive.com/NIS_2_Directive_Article_21.html (mirror of Directive (EU) 2022/2555 text), https://digital-strategy.ec.europa.eu/en/news/commission-refers-ireland-spain-france-and-netherlands-court-justice-failing-transpose-rules , https://www.digital-operational-resilience-act.com/Article_9.html (mirror of Regulation (EU) 2022/2554 text), https://www.esma.europa.eu/digital-operational-resilience-act-dora , https://www.eba.europa.eu/sites/default/files/2024-12/0133f341-fcf5-48d1-812b-d0a66e2b3e8c/JC%202024%2099_ESAs%20Public%20Statement%20on%20DORA%20application%20%281%29.pdf
- Switzerland: https://www.finma.ch/en/news/2022/12/20221213-mm-anh-rs-op-risks/ , https://www.finma.ch/en/documentation/dossier/dossier-cyberrisiken/cyberrisiken-und-outsourcing-2024/ , https://www.ncsc.admin.ch/25-mp-en
- US: https://zerotrust.cyber.gov/federal-zero-trust-strategy
- Market data: https://gs.statcounter.com/os-market-share/mobile/worldwide , https://gs.statcounter.com/os-market-share/mobile/europe
- Vendor events: https://www.omnissa.com/insights/official-launch-pr/ , https://citrix.com/blogs/2022/11/15/citrix-endpoint-management-is-back-by-popular-demand , https://itbrief.co.uk/story/blackberry-adds-sovereign-control-tools-to-uem-platform
- Hypergate (for how it frames these drivers): https://hypergate.com/blog/kerberos-rc4-removal-mobile-sso/ , https://hypergate.com/?p=23355 , https://hypergate.com/blog/android-kerberos-sso-ntlm-sdk/

## Timeline at a glance

| Date | Event | Who is affected | Source |
|---|---|---|---|
| Android 9 / Android 10 | Device admin deprecated for enterprise, policies removed for DPCs targeting API 29 | Any org still on Android device admin management | https://developers.google.com/android/work/device-admin-deprecation |
| 1 Jan 2024 | FINMA Circular 2023/1 "Operational risks and resilience: banks" in force | Swiss banks | https://www.finma.ch/en/documentation/dossier/dossier-cyberrisiken/cyberrisiken-und-outsourcing-2024/ |
| 1 Jul 2024 | Omnissa (former VMware EUC, incl. Workspace ONE) becomes independent under KKR | Workspace ONE customers | https://www.omnissa.com/insights/official-launch-pr/ |
| 30 Sep 2024 (end FY2024) | US OMB M-22-09 zero trust goals due | US federal agencies | https://zerotrust.cyber.gov/federal-zero-trust-strategy |
| 17 Oct 2024 | NIS2 transposition deadline | EU member states, then essential and important entities | https://digital-strategy.ec.europa.eu/en/news/commission-refers-ireland-spain-france-and-netherlands-court-justice-failing-transpose-rules |
| 31 Dec 2024 | Intune ends support for Android device administrator on GMS devices | Intune customers on DA | https://techcommunity.microsoft.com/blog/intunecustomersuccess/intune-ending-support-for-android-device-administrator-on-devices-with-gms-in-de/3915443 |
| 17 Jan 2025 | DORA applies | EU financial entities | https://www.esma.europa.eu/digital-operational-resilience-act-dora |
| 1 Apr 2025 | Swiss mandatory cyberattack reporting for critical infrastructure (fines from 1 Oct 2025) | Swiss CI operators incl. cantonal and communal administrations | https://www.ncsc.admin.ch/25-mp-en |
| 13 Jan 2026 | Kerberos RC4 hardening phase 1 (audit) | All AD domain controllers | Microsoft KB5073381 |
| 29 Jan 2026 | Microsoft announces plan to disable NTLM by default | All Windows / AD estates | Microsoft Windows IT Pro blog |
| 14 Apr 2026 | Kerberos RC4 phase 2: default becomes AES-SHA1 only | All AD domain controllers | Microsoft KB5073381 |
| 8 Jul 2026 | Commission refers Ireland, Spain, France, Netherlands to CJEU over NIS2 | Those states | Commission news |
| Jul 2026 | Kerberos RC4 phase 3: rollback removed | All AD domain controllers | Microsoft KB5073381 |
| 2nd half 2026 | NTLM phase 2: IAKerb and local KDC (pre-release) | Windows Server 2025 / Windows 11 24H2+ | Microsoft Windows IT Pro blog |
| 13 Oct 2026 | NTLMv1-derived SSO blocked by default (BlockNtlmv1SSO Enforce) | Windows 11 24H2 to 26H2, Windows Server 2025 | Microsoft KB5066470 |
| Next major Windows Server release (date not given) | Network NTLM disabled by default | All Windows / AD estates | Microsoft Windows IT Pro blog |

## 1. Microsoft legacy authentication changes (NTLM, RC4)

### 1.1 NTLM disabled by default (three phases)
- Announced 29 January 2026 (page shows "Updated Oct 22, 2026"). (source: https://techcommunity.microsoft.com/blog/windows-itpro-blog/advancing-windows-security-disabling-ntlm-by-default/4489526, checked 2026-11-13)
- Phase 1, "Building visibility and control": "Available now, enhanced NTLM auditing helps your organization understand exactly where and why NTLM is still being used." (Windows Server 2025, Windows 11 24H2 and later). (same source, checked 2026-11-13)
- Phase 2, "Addressing the top NTLM pain points": solutions "will be available in the second half of 2026", including "IAKerb and local Key Distribution Center (KDC) (pre-release)". (same source, checked 2026-11-13)
- Phase 3, "NTLM disabled by default": "In the next major Windows Server release and associated Windows client releases." ... "Network NTLM will be disabled by default." (same source, checked 2026-11-13)
- Caveat from Microsoft: "Timelines and feature availability outlined in this post are subject to change." (same source, checked 2026-11-13)
- Release date of the next major Windows Server: Not found from Microsoft. An analyst estimate of 2027 or 2028 from Directions on Microsoft appeared in search results only (source: https://www.directionsonmicrosoft.com/reports/ntlm-to-be-disabled-in-future-releases/, via search result summary, checked 2026-11-13).

### 1.2 NTLMv1 SSO blocked by default from October 2026
- "Beginning with the October 2026 Windows security update released on October 13, 2026" ... "Windows uses Enforce mode (1) instead of Audit mode (0)" when BlockNtlmv1SSO is not set. Applies to "Windows 11, versions 26H2, 26H1, 25H2, and 24H2, and Windows Server 2025". (source: https://support.microsoft.com/kb/5066470, checked 2026-11-13)
- Reports of Wi-Fi, Ethernet and VPN (MS-CHAPv2) authentication failures after the October 2026 update appeared in trade press (source: https://www.theregister.com/a/5303503 and https://windowsreport.com/?p=1512685, via search result summary, checked 2026-11-13).

### 1.3 Kerberos RC4 removal (CVE-2026-20833, KB5073381)
- "January 13, 2026 - Initial Deployment Phase": "This phase is to warn customers of new security enforcements that will be introduced in the second deployment phase." (source: https://support.microsoft.com/en-us/topic/how-to-manage-kerberos-kdc-usage-of-rc4-for-service-account-ticket-issuance-changes-related-to-cve-2026-20833-1ebcda33-720a-4da8-93c1-b0496e1910dc, checked 2026-11-13)
- "April 14, 2026 - Enforcement Phase with manual rollback": "This phase changes the default value for DefaultDomainSupportedEncTypes to AES-SHA1 only: 0x18." (same source, checked 2026-11-13)
- "July 2026 - Enforcement Phase": "The Windows updates released in or after July 2026 will remove support for the registry subkey RC4DefaultDisablementPhase." (same source, checked 2026-11-13)
- Hypergate's own framing: the "device side is rarely the problem"; breakage shows up when a service account lacks AES keys and looks like a 401 loop on mobile; Hypergate Authenticator negotiates AES by default. (source: https://hypergate.com/blog/kerberos-rc4-removal-mobile-sso/, dated July 2026, checked 2026-11-13)

INFERRED: Relevance to Hypergate. Microsoft is pushing every AD estate from NTLM toward Kerberos. Android has no built-in Kerberos client (see competitors.md), so Android apps and browsers that fall back to NTLM or typed passwords are the client-side gap. Hypergate already markets this: "As Microsoft phases out NTLM in favor of the more secure Kerberos protocol" (source: https://hypergate.com/?p=23355, checked 2026-11-13) and "NTLMv1 gets blocked in October 2026 (KB5066470)" (source: https://hypergate.com/blog/android-kerberos-sso-ntlm-sdk/, checked 2026-11-13).

## 2. Android management changes

### 2.1 Device admin deprecation (Google)
- Android 9.0: "Device admin is marked deprecated for enterprise use through updates to documentation." Android 10.0: "The above policies will no longer be available to DPCs targeting API level 29." Android 11.0: "USES_POLICY_RESET_PASSWORD is marked as deprecated when invoked by a device admin and stops functioning." (source: https://developers.google.com/android/work/device-admin-deprecation, checked 2026-11-13)

### 2.2 Intune ends Android device administrator support on GMS devices
- Intune "will be ending support for device administrator management on devices with access to Google Mobile Services (GMS), beginning December 31, 2024." After that, no bug or security fixes and "Intune technical support will no longer support these devices." (source: https://techcommunity.microsoft.com/blog/intunecustomersuccess/intune-ending-support-for-android-device-administrator-on-devices-with-gms-in-de/3915443, via search result summary, checked 2026-11-13)
- INFERRED: Organisations that migrated (or still must migrate) to Android Enterprise are re-provisioning devices and app configs, a natural moment to add an AE managed-config app like Hypergate (which states it is "Android Enterprise Recommended" per https://hypergate.com/faq/).

### 2.3 Samsung deprecated its own AD Kerberos SSO
- "Due to low usage, however, we are deprecating this SSO feature. If you are using Samsung SSO, try exploring other SSO solutions like Azure AD." (source: https://docs.samsungknox.com/dev/knox-sdk/release-notes/knox-sdk-341/, via search result summary, checked 2026-11-13). Date of Knox 3.4.1: Not found precisely (release notes URL path suggests 19-12, i.e. December 2019; INFERRED).

## 3. EU regulation

### 3.1 NIS2 (Directive (EU) 2022/2555)
- Article 21(2)(i): "human resources security, access control policies and asset management;" (source: https://www.nis-2-directive.com/NIS_2_Directive_Article_21.html, mirror of the directive text, checked 2026-11-13)
- Article 21(2)(j): "the use of multi-factor authentication or continuous authentication solutions, secured voice, video and text communications and secured emergency communication systems within the entity, where appropriate." (same source, checked 2026-11-13)
- Transposition deadline 17 October 2024. On 8 July 2026 the Commission referred Ireland, Spain, France and the Netherlands to the Court of Justice for failing "to notify measures transposing the NIS2 Directive"; these four "have yet to notify full transposition". Formal notices were sent 28 November 2024 and reasoned opinions 7 May 2025. (source: https://digital-strategy.ec.europa.eu/en/news/commission-refers-ireland-spain-france-and-netherlands-court-justice-failing-transpose-rules, checked 2026-11-13)
- Count of member states with NIS2 law in force as of November 2026: Not found from a primary source (secondary trackers disagree).
- NIS2 maximum fines: Not verified (EUR-Lex fetch returned empty).

### 3.2 DORA (Regulation (EU) 2022/2554), financial services
- Application date: entered into force 16 January 2023, applies as of 17 January 2025; covers "21 different types of financial entities, of which 12 are in the remit of ESMA". (source: https://www.esma.europa.eu/digital-operational-resilience-act-dora, via search result summary, checked 2026-11-13)
- Article 9(4)(d) requires financial entities to "implement policies and protocols for strong authentication mechanisms, based on relevant standards" and "protection measures of cryptographic keys whereby data is encrypted". (source: https://www.digital-operational-resilience-act.com/Article_9.html, mirror of the regulation text, checked 2026-11-13)

## 4. Switzerland

### 4.1 FINMA Circular 2023/1 "Operational risks and resilience: banks"
- Published 7 December 2022, in force 1 January 2024 (source: https://www.finma.ch/en/news/2022/12/20221213-mm-anh-rs-op-risks/ and https://www.finma.ch/en/documentation/dossier/dossier-cyberrisiken/cyberrisiken-und-outsourcing-2024/, via search result summary, checked 2026-11-13).
- FINMA's 2024 on-site cyber reviews were primarily based on it (same source, via search result summary, checked 2026-11-13).
- Specific authentication requirements in the circular: Not found (not read directly).

### 4.2 Information Security Act: mandatory cyberattack reporting
- Operators of critical infrastructure, such as "energy and drinking water suppliers, transport companies and cantonal and local administrations", must report certain cyberattacks to the NCSC within 24 hours from 1 April 2025; fines up to CHF 100,000 apply from 1 October 2025. Financial institutions under the Banking Act, Insurance Supervision Act and Financial Infrastructure Act are also covered. (source: https://www.ncsc.admin.ch/25-mp-en, via search result summary, checked 2026-11-13)
- INFERRED: This adds pressure on Swiss cantonal administrations and police, a segment where Hypergate shows logos (see customers.md), but it is a reporting duty, not an authentication mandate.

## 5. Zero trust, MFA and passkeys

- US OMB M-22-09 required federal agencies to meet zero trust goals, including phishing-resistant MFA, by the end of FY2024 (30 September 2024) (source: https://zerotrust.cyber.gov/federal-zero-trust-strategy, via search result summary, checked 2026-11-13). Exact memo wording: Not verified.
- Microsoft Entra ID: "Microsoft Entra ID supports both synced passkeys and device-bound passkeys as Generally Available (GA) authentication methods." On Android, device-bound passkeys in Microsoft Authenticator need Authenticator Android "6.2507.4749"; sign-in to native apps with a passkey in Authenticator "requires Android 14 or later". (source: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-fido2-compatibility and https://learn.microsoft.com/en-us/intune/solutions/passwordless, via search result summary, checked 2026-11-13)
- INFERRED: Passkeys and FIDO2 serve cloud IdP sign-in (Entra, Okta). They do not by themselves give Kerberos tickets for on-prem IWA apps or SMB shares, so they are adjacent to, not a replacement for, Hypergate's on-prem use case. Needs validation.

## 6. Vendor and EMM market changes

- Omnissa: KKR closed its acquisition of Broadcom's End-User Computing division (Workspace ONE, Horizon) on 1 July 2024; reported about US$4 billion; launch figures "$1.5 billion in annual recurring revenue and 26,000 customers". (source: https://www.omnissa.com/insights/official-launch-pr/ and https://www.omm.com/news/press-releases/o-melveny-advises-broadcom-on-closing-of-us-4-billion-omnissa-acquisition-by-kkr/, via search result summary, checked 2026-11-13)
- Citrix Endpoint Management: end of sale announced July 2022 then reversed in November 2022 (no EoS, no Dec 2025 end of maintenance) (source: https://citrix.com/blogs/2022/11/15/citrix-endpoint-management-is-back-by-popular-demand, via search result summary, checked 2026-11-13).
- BlackBerry UEM: June 2026 "sovereign control" features aimed at public sector and European customers concerned about supplier-hosted cloud (source: https://itbrief.co.uk/story/blackberry-adds-sovereign-control-tools-to-uem-platform, via search result summary, checked 2026-11-13).
- MobileIron is now Ivanti: Hypergate lists "Ivanti Neurons (formerly MobileIron)" (source: https://hypergate.com/, checked 2026-11-13). Acquisition date: Not verified.
- End of life of MobileIron Core or other on-prem EMMs: Not found.

## 7. Device and workforce data

- Mobile OS share worldwide, October 2026: Android 72.36%, iOS 27.61% (source: https://gs.statcounter.com/os-market-share/mobile/worldwide, checked 2026-11-13). Note: StatCounter measures web traffic from all devices, not enterprise fleets.
- Mobile OS share Europe, October 2026: Android 63.67%, iOS 36.32% (source: https://gs.statcounter.com/os-market-share/mobile/europe, checked 2026-11-13).
- Enterprise-only Android vs iOS share: Not found.
- Frontline workers: Microsoft cites "Gartner estimates that there are 2.7 billion frontline workers" ... "more than twice the number of desk-based workers" (footnote: Gartner, Hype Cycle for Digital Workplace Applications, 2022) (source: https://blogs.microsoft.com/blog/2023/08/09/microsoft-solutions-boost-fortune-500-frontline-productivity-with-next-generation-ai/, via search result summary, checked 2026-11-13). Note: the original sentence contains an em dash, so it is quoted in parts. Microsoft's 2022 Work Trend Index used "2 billion" (same search, checked 2026-11-13).
- Growth rate of rugged or shared Android devices: Not found.

## Gaps

- EUR-Lex returned empty pages for NIS2 and DORA; article text was taken from mirror sites (nis-2-directive.com, digital-operational-resilience-act.com). Verify against EUR-Lex before external use. NIS2 fine levels not captured.
- Several items are from search result summaries, not direct page reads: Intune DA end date, FINMA circular dates, Swiss reporting obligation, OMB M-22-09, passkey GA, Omnissa figures, Citrix EoS reversal, BlackBerry sovereignty, frontline 2.7 billion figure, Samsung SSO deprecation.
- No primary source for current NIS2 transposition count (as of November 2026) or for NIS2 transposition in Switzerland (Switzerland is not EU; no equivalent found).
- No FINMA text on authentication or mobile device requirements was read.
- Next major Windows Server release date: Not found.
- Enterprise device share (Android vs iOS in managed fleets) and frontline device growth figures: Not found.
- Analyst market sizing for mobile SSO, UEM or Android Enterprise adoption (Gartner, IDC): Not found.
- EMM end-of-life events (for example MobileIron Core, on-prem Workspace ONE): Not found.
