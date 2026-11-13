# Hypergate: Company Research

Checked: 2026-11-13

Raw research only. Every fact has a source and date checked. Inferences are marked "INFERRED:".

## Sources used

- https://hypergate.com/ (homepage)
- https://hypergate.com/homepage/ (a second homepage version with newer copy, live at this URL)
- https://hypergate.com/authenticator-sso/
- https://hypergate.com/files/
- https://hypergate.com/why-hypergate/
- https://hypergate.com/supported-emms/
- https://hypergate.com/supported-apps/
- https://hypergate.com/plattforms/ (supported platforms; the URL is spelled this way)
- https://hypergate.com/partners/
- https://hypergate.com/about-us/
- https://hypergate.com/faq/
- https://hypergate.com/get-in-touch/
- https://hypergate.com/webinars/
- https://hypergate.com/blog/ and https://hypergate.com/blog/android-kerberos-sso-ntlm-sdk/
- https://hypergate.com/blog/success-story-jefferies/ , https://hypergate.com/blog/success-story-with-maersk-drilling/ , https://hypergate.com/blog/success-story-with-york-regional-police/
- https://hypergate.com/privacy-policy/
- https://papers.ch/ , /portfolio/ , /studio/ , /careers/ , /contact/ , /imprint/
- Zefix (Swiss central business name index) REST API: https://www.zefix.ch/ZefixREST/api/v1/firm/1544713.json (Papers AG) and https://www.zefix.ch/ZefixREST/api/v1/firm/355933.json (Papers Group AG)
- Google Play: https://play.google.com/store/apps/details?id=com.hypergate.authenticator and https://play.google.com/store/apps/details?id=com.hypergate.files.intune
- Google blog case study: https://blog.google/products/android-enterprise/jefferies-case-study/
- Venturelab profile: https://www.venturelab.swiss/Hypergate-Zero-The-Venture-Leader-Mobile-prioritizing-privacy-and-security
- Swiss Made Software listing: https://www.swissmadesoftware.org/en/companies/papers-ag/home.html
- Web search snippets (third party, lower confidence): onlineinfo.ch, Capterra, G2, SignalHire, Village.ai, prospeo.io

## 1. What Hypergate sells (one line)

- "Hypergate is a fast, secure and accessible Kerberos Single Sign-On (SSO) solution for Android and iOS." (source: https://hypergate.com/, checked 2026-11-13)
- Two named products on the site: "Hypergate Authenticator and Hypergate Files" (source: https://hypergate.com/, checked 2026-11-13). A developer SDK also exists (see 2.3).
- Target environments: "Specially designed for on-premise and hybrid environments, our products cater to organizations that prioritize privacy and security." (source: https://hypergate.com/, checked 2026-11-13)
- Stated client base: "Our client base includes government entities, banking institutions, insurance companies, and law firms" (source: https://hypergate.com/, checked 2026-11-13)

## 2. Products

### 2.1 Hypergate Authenticator (SSO)

- "Hypergate Authenticator is a managed application on the mobile device that delivers a seamless and secure Single Sign-On solution, integrating directly with your Active Directory." (source: https://hypergate.com/authenticator-sso/, checked 2026-11-13)
- Core gap it fills: "Enable SSO specifically with Android Enterprise, which is otherwise not available." (source: https://hypergate.com/authenticator-sso/, checked 2026-11-13)
- Features listed on the homepage: "SSO (Single Sign On) with Certificates", "Password Reset", "Active Directory Multiforest Environment" (source: https://hypergate.com/, checked 2026-11-13)
- Feature list on why-hypergate: "Seamless SSO Solution", "Self Service Password Management (SSPM)", "MFA and Conditional Access Components", "No Infrastructure Changes Needed", "Configurable through your EMM" (source: https://hypergate.com/why-hypergate/, checked 2026-11-13)
- iOS additions vs Apple's built-in Kerberos (FAQ): "Reset Expired AD Password", "Expiry Notification", "Change AD Password", "Smart Access", "Local Authentication" (source: https://hypergate.com/faq/, checked 2026-11-13)
- Kiosk and shared devices: "Yes it will work with the Android Enterprise Kiosk Mode. Multiple users are supported on Android 9 or newer devices as well." (source: https://hypergate.com/faq/, checked 2026-11-13)
- Google Play listing name: "Hypergate Authenticator SSO", package com.hypergate.authenticator, short description "Kerberos / ADFS SSO authentication on your Android Enterprise Managed device.", downloads shown as "1K+", last updated "Nov 4, 2026" (source: https://play.google.com/store/apps/details?id=com.hypergate.authenticator&hl=en&gl=US, checked 2026-11-13)

### 2.2 Hypergate Files

- "Seamless access to on-premise network CIFS, SMB (Samba) and Windows shares. Let your users collaborate freely with their teams and edit all files directly on their mobile devices." (source: https://hypergate.com/, checked 2026-11-13)
- Protocols and backends: "Hypergate Files supports modern SMB2/SMB3 protocols" and "integrates seamlessly with a NetApp on-premises backend, without requiring additional infrastructure, proxies, or middleware." (source: https://hypergate.com/files/, checked 2026-11-13)
- Opens files in native apps: "Users can open files in their respective native apps (Word, Excel, PDF ect.) without requiring additional viewers" (source: https://hypergate.com/files/, checked 2026-11-13)
- "Access files from applications like Gmail, Outlook etc." (source: https://hypergate.com/why-hypergate/, checked 2026-11-13)
- Google Play listing name: "Hypergate Files for Intune", package com.hypergate.files.intune, downloads shown as "10+", last updated "Nov 4, 2026". Listing text: "Available as standalone or fully Hypergate Authenticator enabled solution." (source: https://play.google.com/store/apps/details?id=com.hypergate.files.intune&hl=en&gl=US, checked 2026-11-13)
- Positioned as an Intune gap filler (German webinar copy): "Hypergate-Files App füllt die Intune-Lücke" (source: https://hypergate.com/webinars/, checked 2026-11-13)
- Hypori: "Hypergate Files is the only Hypori Compatible Files solution." (source: https://hypergate.com/plattforms/, checked 2026-11-13)
- Recent blog topics target Acronis Cyber Files end of life: "Acronis Cyber Files Is End-of-Life: A Migration Guide for Mobile Access to On-Prem File Servers" (source: https://hypergate.com/blog/, checked 2026-11-13)

### 2.3 Hypergate SDK (developer product)

- "The Hypergate SDK (com.hypergate:sdk on Maven Central) adds SPNEGO negotiate tokens to any Android app, so your app answers with Kerberos instead of NTLM." Example version in the post: "com.hypergate:sdk:1.6.0". Blog post by Lukas Schönbächler, dated "July 2026" on the post and "13 May" on the blog index (dates conflict). (source: https://hypergate.com/blog/android-kerberos-sso-ntlm-sdk/ and https://hypergate.com/blog/, checked 2026-11-13)
- Account type used on Android: "For Hypergate this is ch.papers.hypergate." (source: https://hypergate.com/blog/android-kerberos-sso-ntlm-sdk/, checked 2026-11-13)
- Cordova plugin and sample app are mentioned in the post (source: same, checked 2026-11-13)

### 2.4 Hypergate Zero (separate venture or product, status unclear)

- Venturelab profile dated 29.01.2024: "Hypergate Zero employs a Zero Trust security model, designed to enhance network security in remote work environments. Using mobile devices, it performs continuous network scans in home settings." Listed under "Papers AG (Hypergate Zero)", positioned at the "Secure Access Service Edge (SASE) market". (source: https://www.venturelab.swiss/Hypergate-Zero-The-Venture-Leader-Mobile-prioritizing-privacy-and-security, checked 2026-11-13)
- Not mentioned anywhere on hypergate.com pages fetched. INFERRED: Hypergate Zero may have been an exploratory product in 2024 that is not currently marketed. Flag for confirmation.

## 3. How it works technically

- Native Kerberos, no middleware: "Direct interaction with your Kerberos Key Distribution Center (KDC) removes the need for middleware" (source: https://hypergate.com/authenticator-sso/, checked 2026-11-13)
- Talks directly to Domain Controllers, like a domain-joined Windows client: "It uses native Kerberos protocols, like your domain-joined Windows clients, and connects directly to existing Domain Controllers." Supports "multiple forest configurations and air-gapped setups." (source: https://hypergate.com/authenticator-sso/, checked 2026-11-13)
- Android integration: "Hypergate leverages the open Android account's APIs and enables SPNEGO Kerberos SSO authentication while using system apps like Google Chrome to browse the intranet." (source: https://hypergate.com/authenticator-sso/, checked 2026-11-13)
- Initial authentication by certificate, then Kerberos in the background: "authenticates against your Active Directory via Certificate and all further app and website authentications is happening in the background for you (via Kerberos / Windows Integrated Authentication)." (source: https://hypergate.com/, checked 2026-11-13)
- Configuration via EMM/MDM managed configuration: "Configuration is minimal and managed through an MDM" (source: https://hypergate.com/authenticator-sso/, checked 2026-11-13)
- Network path: "it will work with any VPN/Tunnel which enables you to contact your KDC." (source: https://hypergate.com/faq/, checked 2026-11-13)
- App compatibility rule of thumb: "Generally speaking, all applications that support Chrome Custom Tabs are compatible out of the box." (source: https://hypergate.com/supported-apps/, checked 2026-11-13). Also: "If the App uses a Webview during the authentication process, it usually works out of the box." (source: https://hypergate.com/faq/, checked 2026-11-13)
- Password change audit: "As we use the native Kerberos protocol, this log can be found in the active directory password change log." (source: https://hypergate.com/faq/, checked 2026-11-13)
- Files authentication: "Authentication is done via Kerberos which has the benefit that access rights are handled on the protocol level." (source: https://hypergate.com/, checked 2026-11-13)
- Play listing also mentions ADFS: "Kerberos / ADFS SSO authentication" (source: https://play.google.com/store/apps/details?id=com.hypergate.authenticator&hl=en&gl=US, checked 2026-11-13). SAML is not mentioned on the authenticator page (checked 2026-11-13).

### Supported OS and devices

- "Android 7.0 or higher." and "All iOS 13 or higher devices are supported." (source: https://hypergate.com/faq/, checked 2026-11-13)
- Device guarantee: "we guarantee Hypergate to run on all devices which are branded by Google as "Android Enterprise Recommended" as well as on all Samsung Galaxy devices." (source: https://hypergate.com/faq/, checked 2026-11-13)
- iOS App Store: Not found. Searched the iTunes Search API for "hypergate" and "hypergate authenticator" in US, CH and DE stores (checked 2026-11-13). INFERRED: the iOS app may be distributed via Apple Business Manager / custom apps rather than the public store. Needs confirmation.

## 4. Supported EMMs (list)

From the supported EMMs page (source: https://hypergate.com/supported-emms/, checked 2026-11-13):

1. Microsoft Intune
2. Ivanti MobileIron (Ivanti Neurons for MDM)
3. SOTI MobiControl
4. 42Gears
5. Samsung Knox
6. VMware Workspace ONE
7. BlackBerry UEM
8. Techstep
9. Kace
10. PushManager

FAQ says it was "specifically tested" with: MobileIron, Blackberry, Microsoft InTune, VMWare Workspace One, SOTI (source: https://hypergate.com/faq/, checked 2026-11-13).

Marketplace listings: the supported EMMs page links an "Ivanti Store" and "VMWare Solution Exchange" listing (source: https://hypergate.com/supported-emms/, checked 2026-11-13). A SOTI marketplace listing exists: https://pulse.soti.net/marketplace/security/1819/Hypergate-Authenticator--Android--iOS (seen in search results only, not fetched, 2026-11-13).

## 5. Supported apps (list)

From the supported apps page, "tested and confirmed" (source: https://hypergate.com/supported-apps/, checked 2026-11-13):

Microsoft Edge, Chrome, Evernote, Slack, myCWT, SAP Fiori, Box, Brave, zoom, Salesforce, ServiceNow, Jira, Confluence, WorkDay, iSEC7 MED, "and many more.."

FAQ adds "Office 365" as tested (source: https://hypergate.com/faq/, checked 2026-11-13).

## 6. Supported platforms (list)

From https://hypergate.com/plattforms/ (checked 2026-11-13): Android, iOS, Hypori, Chrome Custom Tabs, Samsung DeX, Apache Cordova, Xamarin.

## 7. Partners (list, with region as shown on the site)

Intro: "Hypergate is distributed through our partner network, where available" (source: https://hypergate.com/partners/, checked 2026-11-13). Partner names below are taken from the partner logo links and image file names on that page; the region text sits next to each logo.

| Partner (from link / logo) | Website | Region shown |
|---|---|---|
| Nomasis | https://nomasis.ch/en/ | Switzerland |
| Mobco | https://mob.co | Belgium |
| XSAT India | http://www.xsatindia.in | India |
| Enox | https://enox.com.tr | Turkey |
| QBS Software | https://www.qbssoftware.com | UK, Germany |
| Anyplace IT | https://anyplace-it.de/ | Germany |
| Blaud | https://blaud.com | The Netherlands |
| Headtechnology | https://headtechnology.com | Eastern Europe |
| 3Eye Technologies | https://www.3eyetech.com | USA |
| Leaders Fort Tech | https://leadersfort-tech.com | UAE |
| Conscia | https://conscia.com | Nordics |
| Appurity | https://appurity.co.uk | United Kingdom |
| EBF | https://ebf.com | UK, USA, Germany |
| CANCOM (Austria) | https://www.cancom.at | Austria |
| SDS | https://sds4e.com | Saudi Arabia |
| Qolcom | https://qolcom.co.uk | United Kingdom |
| iSEC7 | https://www.isec7-gs.com | Germany, USA, Australia, New Zealand |
| IT Point | https://www.itpoint.ch/en/ | Switzerland |
| Milan Consult | https://www.milanconsult.de | Germany |
| HiTech Defense | https://hitechdefense.com | Brazil |
| Troy Mobility | https://www.troymobility.com | USA |
| Kontron Hungary (logo file "ST") | https://kontron.hu/english/ | Hungary |
| SoftwareONE | https://www.softwareone.com/en-ch | Switzerland |
| Techstep | https://www.techstep.io | Nordics |
| System4u | https://www.system4u.com | Czechia |
| Symphony Solutions | https://symphony-solutions.com | Israel |
| Proget | https://proget.pl/en/ | Eastern Europe |
| IMTAC | https://www.imtac.com | Sultanate of Oman |

Count: 28 partner links (counted from page, 2026-11-13). A gated "Partner Portal" login exists at https://hypergate.com/partnerportal/ (checked 2026-11-13).

Past co-marketing webinars named partners AnyplaceIT, Nomasis, Delv (Australia), Mobco and Headtechnology (source: https://hypergate.com/webinars/, checked 2026-11-13). Delv is not on the current partner page.

## 8. Pricing model

- No pricing on hypergate.com. /pricing/ returns "Page not found" (source: https://hypergate.com/pricing/, checked 2026-11-13).
- Capterra (search snippet only, direct fetch returned 403): "Contact vendor for pricing", free trial available; Capterra NZ snippet says flat rate, free version and free trial, pricing depends on number of licenses (source: https://www.capterra.com/p/202867/Hypergate-Authenticator/ and https://www.capterra.co.nz/software/202867/hypergate-authenticator, via search 2026-11-13). Low confidence.
- G2 snippet: vendor has not provided pricing (source: https://www.g2.com/products/hypergate-authenticator/pricing, via search 2026-11-13).
- Price per user or per device: unknown (flagged).
- INFERRED: sold as licenses through the partner channel (partners page says it is "distributed through our partner network, where available").

## 9. Markets and geographies

- Site languages: English plus /de/, /fr/, /it/ versions linked from the homepage (source: https://hypergate.com/, checked 2026-11-13).
- Partner regions listed: Switzerland, Belgium, India, Turkey, UK, Germany, The Netherlands, Eastern Europe, USA, UAE, Nordics, Austria, Saudi Arabia, Australia, New Zealand, Brazil, Hungary, Czechia, Israel, Sultanate of Oman (source: https://hypergate.com/partners/, checked 2026-11-13).
- Named customer logos on the homepage (image file names): Noble, York Police, Bayrische Staatskanzlei, Linz AG, European Court of Auditors, Suva Insurance, Jersey Police, Jefferies Bank (source: https://hypergate.com/ "Selected clients", checked 2026-11-13). Customer detail is out of scope for this file.
- Published success stories: Jefferies (US), Maersk Drilling, York Regional Police (Canada) (source: https://hypergate.com/blog/category/success-story/, checked 2026-11-13).
- Self-reported traction (2024): "secured contracts with four Fortune 500 companies and over 50 paying customers, resulting in more than 30,000 daily active users." (source: Venturelab profile, dated 29.01.2024, https://www.venturelab.swiss/Hypergate-Zero-The-Venture-Leader-Mobile-prioritizing-privacy-and-security, checked 2026-11-13). These are 2024 self-reported numbers; current figures unknown.
- Papers portfolio page: "Hypergate customers include Fortune 500 companies, governmental agencies, and financial institutions." (source: https://papers.ch/portfolio/, checked 2026-11-13)

## 10. Funding

- Venturelab (2024, self-reported): "achieving organic growth without external investment." (source: https://www.venturelab.swiss/Hypergate-Zero-The-Venture-Leader-Mobile-prioritizing-privacy-and-security, checked 2026-11-13)
- Crunchbase: Not found (searched "Hypergate crunchbase Papers Zug funding", 2026-11-13).
- startup.ch profile "Papers AG (Hypergate Zero)" exists but funding is gated, and the page did not load via direct fetch (source: https://www.startup.ch/papers-ag-hypergate-zero, checked 2026-11-13).
- Funding total: unknown (flagged). INFERRED: bootstrapped inside Papers, based on the 2024 statement above.

## 11. Team size

- Venturelab 2024 profile: "Number of employees: 5" (for Hypergate Zero / Papers AG entry, dated 29.01.2024) (source: https://www.venturelab.swiss/Hypergate-Zero-The-Venture-Leader-Mobile-prioritizing-privacy-and-security, checked 2026-11-13). Unclear if this counts the Hypergate team or only Hypergate Zero.
- SignalHire snippet: 10 to 50 employees (source: https://www.signalhire.com/companies/hypergate, via search 2026-11-13). Low confidence.
- LinkedIn headcount: Not found (LinkedIn returned 403 for https://www.linkedin.com/company/hypergate-ch/, 2026-11-13).
- Current Hypergate team size: unknown (flagged).

## 12. Leadership and people

- Lukas Schönbächler: Venturelab lists "Job title: Software Engineer - Founder" and calls him "CEO of Hypergate Zero" (source: https://www.venturelab.swiss/Hypergate-Zero-The-Venture-Leader-Mobile-prioritizing-privacy-and-security, checked 2026-11-13). He authors Hypergate blog posts including the Jefferies story and SDK post (source: https://hypergate.com/blog/success-story-jefferies/ , checked 2026-11-13). Current title at Hypergate: unknown, not stated on hypergate.com.
- Alessandro De Carli: listed as "The legal representative(s) of Papers AG" on the Papers imprint (source: https://papers.ch/imprint/, checked 2026-11-13). Search snippets from June 2026 press releases call him "CEO Papers AG" (source: https://www.einpresswire.com/article/917558983/swiss-papers-ag-launches-obsidio-for-realistic-ddos-resilience-testing, via search 2026-11-13, not fetched).
- Mike Godenzi: "CTO" on the Papers careers page (source: https://papers.ch/careers/, checked 2026-11-13).
- Register snippets (onlineinfo.ch, third party, direct fetch blocked): Papers Group AG board includes Alessandro Decarli (president), Bea Knecht, Jürg Bühler, Luca Decarli, Pascal Brun; Lukas Schönbächler shown with resigned signing roles. Papers AG people include Decarli, Schönbächler and Brun (source: https://onlineinfo.ch/company/papers-group-ag---che-103-383-956/pdf and https://onlineinfo.ch/azienda/papers-ag---che-497-975-775/pdf, via search 2026-11-13). Low confidence until checked against the cantonal extract.
- Papers says it was "Founded by childhood friends" (source: https://papers.ch/, checked 2026-11-13).

## 13. Office locations and contact

- Hypergate about page: "Hypergate is developed and maintained by Papers AG, a software security company located in Zug, Switzerland." (source: https://hypergate.com/about-us/, checked 2026-11-13)
- Papers AG address: Baarerstrasse 43, 6300 Zug, Switzerland; phone +41 44 512 90 04; VAT ID CHE-497.975.775 (source: https://papers.ch/imprint/, checked 2026-11-13)
- Hypergate phone on every page: "+41 44 500 88 95" (source: https://hypergate.com/, checked 2026-11-13)
- Google Play developer contact: developer name "Hypergate", email sales@hypergate.com, legal entity "Papers Group AG", Baarerstrasse 43 (source: https://play.google.com/store/apps/details?id=com.hypergate.authenticator&hl=en&gl=US, page data, checked 2026-11-13)
- Other offices: Not found (checked hypergate.com about, contact and footer, papers.ch contact and imprint, 2026-11-13).

## 14. Relationship to Papers AG

- Trademark line on every hypergate.com page: "Copyright © 2026, Hypergate is a registered trademark of Papers AG" (source: https://hypergate.com/, checked 2026-11-13)
- "Founded a decade ago, Hypergate is developed and maintained by Papers AG" and "Papers AG has dedicated its 10+ years of existence to developing secure, mobile-first software" (source: https://hypergate.com/about-us/, checked 2026-11-13). Founding year not given as a number on the site.
- Papers describes itself as "a Swiss software house" and lists Hypergate in its portfolio next to Acurast, Obsidio, Archonum, AirGap, anoma, Beacon, Ecoo, objkt.com and youves (source: https://papers.ch/portfolio/, checked 2026-11-13). Papers says "We develop ventures in Edge Computing, Cybersecurity, Mobile Development" (source: https://papers.ch/, checked 2026-11-13).
- Entity names used inconsistently across Hypergate pages: "Hypergate (Papers GmbH)" on supported EMMs and platforms pages, "Hypergate (Papers AG)" on supported apps page (sources: https://hypergate.com/supported-emms/ , https://hypergate.com/supported-apps/ , checked 2026-11-13). Privacy policy says the app "was created by Papers AG" and also references "Papers GmbH" (source: https://hypergate.com/privacy-policy/, checked 2026-11-13).
- Swiss register (Zefix, checked 2026-11-13):
  - Papers AG, UID CHE-497.975.775, seat Zug, status active ("EXISTIEREND"), address Baarerstrasse 43, 6300 Zug. Purpose: "Die Gesellschaft bezweckt das Erbringen von IT-Dienstleistungen im In- und Ausland." (IT services) (source: https://www.zefix.ch/ZefixREST/api/v1/firm/1544713.json)
  - Papers Group AG, UID CHE-103.383.956, seat Zug, status active, same address. Purpose: holding participations in other companies ("das Eingehen und Halten von Beteiligungen an anderen Gesellschaften"). Former names listed by Zefix: "Ecosave GmbH", "Papers AG", "Papers GmbH" (source: https://www.zefix.ch/ZefixREST/api/v1/firm/355933.json)
  - INFERRED: Papers Group AG is the older company (formerly Papers GmbH, then Papers AG) and now acts as a holding company; the current Papers AG (CHE-497.975.775) is a newer operating entity. This would explain why Hypergate pages mention both "Papers GmbH" and "Papers AG", and why the Google Play developer entity is Papers Group AG. Confirm with the cantonal extracts: https://zg.chregister.ch/cr-portal/auszug/auszug.xhtml?uid=CHE-497.975.775 and https://zg.chregister.ch/cr-portal/auszug/auszug.xhtml?uid=CHE-103.383.956
  - Founding/registration date of each entity: unknown (Zefix API response did not include it; Companexia snippet says Papers AG founded 2022, and Capterra/Village.ai snippets say 2009, all third party and unverified).
- Hypergate carries the "Swiss made software" label (logo link to swissmadesoftware.org on the site) (source: https://hypergate.com/, checked 2026-11-13).

## 15. Other channels

- LinkedIn: https://www.linkedin.com/company/hypergate-ch/ (linked from site footer; content not readable, 403) (source: https://hypergate.com/, checked 2026-11-13)
- YouTube: https://www.youtube.com/channel/UCLwydNq12rSpIv9tzSxOH2g (source: https://hypergate.com/, checked 2026-11-13)
- Medium: https://medium.com/@hypergate_ch (search result only, 2026-11-13)
- Blog categories with post counts shown: Announcement 14, Mobile Security Talk 5, Success Story 3, Technical 27 (source: https://hypergate.com/blog/, checked 2026-11-13)
- Webinars: "Currently no Webinars are scheduled" (source: https://hypergate.com/webinars/, checked 2026-11-13)

## Gaps

- Pricing: no public price, unit (per user or per device) unknown. Only third-party snippets.
- Funding: no Crunchbase profile found; total funding unknown; only a 2024 self-reported "without external investment" statement.
- Team size: only a 2024 figure of 5 (scope unclear) and a third-party 10 to 50 range. LinkedIn blocked (403).
- Leadership: no team page on hypergate.com. Lukas Schönbächler's current title and Hypergate's sales or marketing leads unknown.
- Founding year: site says "a decade ago" and "10+ years"; no exact year from a primary source.
- Legal entity: which Papers entity contracts with customers is unclear (Papers AG vs Papers Group AG vs "Papers GmbH" wording). Cantonal register extracts not fetched (onlineinfo.ch and moneyhouse returned 403 or were not reachable).
- iOS App Store listing: not found in public store search.
- Hypergate Zero: status unknown (2024 Venturelab only).
- Capterra, G2, startup.ch and LinkedIn pages could not be fetched directly (403 or empty); facts from them are search snippets only.
- Revenue, ARR and customer count today: unknown.
