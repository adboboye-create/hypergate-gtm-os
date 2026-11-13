# Hypergate buyer personas

Built only from `context/docs/research/` (checked 2026-11-13). The source keys are the same as in [icp.md](icp.md):

- **CO** company.md
- **CU** customers.md
- **CP** competitors.md
- **MK** market.md
- **SG** signals.md
- **VO** voice.md

**INF** means the source marks the point as INFERRED.

**Read first:**

- There are very few buyer quotes in the research. Each quote below is tagged:
  - **[customer]**: said by a named customer.
  - **[story]**: a Hypergate-written customer story.
  - **[Hypergate]**: Hypergate's own framing of the pain.
- No sales-call notes exist, so every objection is inferred from the competitor and market research. Validate them on calls.
- "Measured on" is inferred from the outcomes customers reported. No source lists anyone's KPIs.

---

## 1. Champion: Mobility / EMM administrator

| | |
|---|---|
| **Job titles** | Security Administrator (Pierre Hanlon, York Regional Police, CU §3.3). Mobility engineer, EUC team (SG S3, S8 detection ideas, INF). The 2026 blog is "written for IT admins and mobile engineers" (VO §9, INF) |
| **Measured on** | Support tickets and lockouts (all three stories list reduced support, CU §3). Device onboarding time ("only minutes to set up the device", CU §3.1). User adoption (CU §3.1). Operational security (CU §3.3) |
| **What they valued** | [customer] "Hypergate is easy to install and configure, and it seamlessly integrates into our existing MobileIron MDM environment" (Hanlon, CU §3.3) |

**Top three pains**

1. [story] "each user was prompted for their credentials for each application they launched on their Android phones." (Maersk, CU §3.2)
2. [story] "Android Enterprise doesn't support Kerberos Authentication natively, so therefore enablement of Single Sign-On with a local active directory previously was not possible." (York Regional Police, CU §3.3)
3. [story] "The devices log out automatically and close all open sessions in the background after each shift, interrupting the workflow." (Maersk, CU §3.2)

**What makes them start looking**

- Rolling out Android Enterprise or BYOD work profile (SG S1, S2; Jefferies, CU §3.1)
- A shared or rugged device rollout on shift work (SG S3)
- An EMM migration that leaves behind Docs@Work, BlackBerry Work, Workspace ONE Content or SOTI Hub. "Intune lacks a built-in solution for accessing SMB/CIFS network file shares" (SG S8)
- Acronis Cyber Files EOL, with security updates ending 2026-12-31 (SG S9)

**Objections** (inferred)

| Objection | Where the research points |
|---|---|
| "Our EMM already does file access and SSO" | Docs@Work needs Sentry, BlackBerry Docs needs a BEMS server, Workspace ONE Content needs Content Gateway (CP §3.2, §3.6, §3.7). Hypergate claims "No need for additional servers or middleware" (VO §4) |
| "Samsung Knox covers it" | Samsung deprecated its own AD Kerberos SSO and pointed users to Azure AD (CP §3.3). Hypergate: "Device management and identity are different problems, and MDM only solves the first one." (CP §3.3) |
| "Will it work with our apps and devices?" | Chrome Custom Tabs / webview rule, the tested app list, and AER plus Samsung guarantee (CO §3, §5). FAQ: "just contact us and we will test it together with you." (VO §6) |

---

## 2. Economic buyer: unconfirmed

| | |
|---|---|
| **Job titles** | **Unknown.** No source says who approved a purchase. Hypotheses only: CIO, CISO or head of EUC/mobility (SG "no evidence found", INF). The most senior named customer contact is a VP of platform security engineering (Mittul Mehta, Jefferies, CU §3.1), but his role in the purchase is not stated |
| **Measured on** | Not in the research. Hypergate pitches support cost ("Reduce your support costs", VO §4), no added infrastructure cost (VO §4), control and sovereignty (VO §4) and regulatory strong authentication (DORA Art. 9, NIS2 Art. 21, MK §3). Treat these as hypotheses |

**Top three pains** (no buyer quotes exist; these are Hypergate's words)

1. [Hypergate] "Sovereignty and classification requirements often prevent the use of a cloud identity provider." (SG S4)
2. [Hypergate] "Mobile password prompts drive lockouts, and every lockout is a ticket." (SG S12)
3. [Hypergate] "Companies want to regain control of their infrastructure but still want secure and seamless access to their corporate resources." (VO §4)

**What makes them start looking**

- Vendor end-of-life: "For many IT leaders, end-of-life announcements act as a forced checkpoint" [Hypergate] (SG S9)
- An EMM ownership or pricing change. Gartner advised Workspace ONE customers to expect pricing changes after Omnissa (SG S8)
- A cloud-exit or sovereignty policy, or a cloud IdP outage (Entra ID outages in Feb and Oct 2025) (SG S4)
- Cyber insurers asking about Kerberos encryption in 2026 renewals. This is Hypergate's claim and is unverified (SG S6)

**Objections** (inferred)

| Objection | Where the research points |
|---|---|
| "Is the vendor big enough?" | Team size unknown: 5 in a 2024 profile with unclear scope, 10 to 50 per a third-party source. Contracting entity unclear (Papers AG vs Papers Group AG) (CO §11, §14) |
| "Where is the ROI?" | No case study has numbers (CU "Gaps"). Pricing is not public (CO §8) |
| "We are moving to Entra ID / Okta / passkeys anyway" | Cloud brokers need Entra ID or Application Proxy in the path (CP §3.1). Passkeys do not issue Kerberos tickets for on-prem apps (MK §5, INF) |

---

## 3. Influencer: Identity and security engineering, app developers, business lead

| | |
|---|---|
| **Job titles** | VP platform security engineering (Mehta, Jefferies, CU §3.1). AD / PKI / NDES / SCEP admins (SG S6, S7 detection ideas, INF). Android app developers on in-house apps (SG S5; CO §2.3). Business side: Project Manager Business Performance (Lukas Landsberg, Maersk, CU §3.2) |
| **Measured on** | Engineering: moving the AD estate off NTLM and RC4 without breaking access (MK §1; SG S5, S6, INF). Business lead: "Improved efficiency & productivity on the rigs" (CU §3.2) |
| **What they valued** | [customer] "they were available even on short notice and always found solutions to upcoming challenges" (Landsberg, on the rollout, CU §3.2) |

**Top three pains**

1. [Hypergate] "On Android and iOS, NTLM was often the actual path to on-prem SharePoint, file shares, and internal web apps." (SG S5)
2. [Hypergate] "Users will not accept the alternative, which is typing domain passwords into phones." (VO §8)
3. [Hypergate] Cloud Kerberos trust "exists only on Windows and macOS. On Android there is no Kerberos client at all" (SG S10)

**What makes them start looking**

- Microsoft's NTLM phase-out, including the NTLMv1 SSO block from 13 Oct 2026 (MK §1.2; SG S5)
- Mobile 401 loops after Windows or DC updates: RC4 removal in July 2026 (SG S6) or strong certificate mapping (SG S7)
- A passwordless rollout on Windows that leaves mobile behind (SG S10)
- In-house Android apps that still authenticate with NTLM (SG S5)

**Objections** (inferred)

| Objection | Where the research points |
|---|---|
| "Will it break under AES-only / RC4 removal?" | Hypergate says Authenticator "negotiates AES by default" (SG S6) |
| "It still needs certificates, which means PKI work" | The first sign-in is by certificate, then Kerberos runs in the background (CO §3). Strong mapping rejects certificates without the AD SID (SG S7) |
| "How does it reach the KDC with no middleware?" | It needs a VPN or tunnel that can reach the KDC (CO §3) |

---

## Open questions

1. Who signs, and from which budget? Interview the York Regional Police, Maersk/Noble and Jefferies contacts, or check with Hypergate sales.
2. The real objections, in the buyer's words. There are no call notes or reviews in the research (Capterra and G2 were blocked, CU §5).
3. What KPIs each persona is actually measured on.
4. Is there a separate persona for Hypergate Files buyers? No Files case study exists (CU "Gaps").
5. Partner role: does the reseller act as an influencer or a gatekeeper in the deal (CO §7)?
