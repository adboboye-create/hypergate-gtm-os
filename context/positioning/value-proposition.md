# Hypergate value proposition by persona

Status: v0.1, 2026-11-13. Built only from `context/docs/research/`. Citations use the short form `file.md §section`, all in that folder. INFERRED marks our reading, not a source fact.

Personas are taken from the roles that appear in the research (customer quote givers, blog audience, SDK readers). The economic buyer (who signs) is not named in any source: unknown, flagged.

## 1. Mobility / EMM administrator (champion)

Evidence for the role: Pierre Hanlon, "Security Administrator", York Regional Police, praises install and MDM fit (customers.md §3.3). INFERRED: 2026 blog is written for IT admins (voice.md §9).

| | |
|---|---|
| Job to be done | Give managed Android and iOS users access to AD-protected apps, intranet and file shares, configured from the EMM they already run (company.md §3, voice.md §4 "Vendor freedom"). |
| Pain | "Android Enterprise ships no built-in Kerberos SSO, so users on fully managed Samsung fleets still type Active Directory passwords into their phones, app by app." (signals.md, Root condition). "Mobile password prompts drive lockouts, and every lockout is a ticket." (signals.md S12). Moving EMM leaves vendor file tools behind; "Intune lacks a built-in solution for accessing SMB/CIFS network file shares" (signals.md S8). |
| Gain | One sign-in by certificate, then Kerberos in the background (company.md §3). Configured through managed config in the EMM (company.md §3). Works with 10 listed EMMs, so an EMM switch does not break SSO (company.md §4, voice.md §4 "Vendor freedom"). Users reset AD passwords on the device (company.md §2.1). |
| Proof | "Hypergate is easy to install and configure, and it seamlessly integrates into our existing MobileIron MDM environment" (Pierre Hanlon, customers.md §3.3). York lists "Greatly reduced support due to Single Sign-On" (customers.md §3.3, no figure). Android Enterprise Recommended device guarantee and Zebra validation (company.md §3, customers.md §6). |

## 2. Identity, AD and security engineer (influencer)

Evidence for the role: Mittul Mehta, "vice president, platform security engineering", Jefferies (customers.md §3.1). Hypergate's 2026 posts on NTLM, RC4 and cloud Kerberos trust target this reader (voice.md §8, signals.md S5, S6, S10).

| | |
|---|---|
| Job to be done | Keep mobile authentication on the organisation's own AD, with no cloud broker in the path, while Microsoft retires NTLM and RC4 (competitors.md §1, market.md §1). |
| Pain | Microsoft's route to on-prem Kerberos apps runs through Entra ID preauthentication and Application Proxy; on Android its browser SSO is Edge only (competitors.md §3.1). "Microsoft's plan ships no mobile equivalent, so those flows break when NTLM is blocked." (signals.md S5). Sovereignty rules "often prevent the use of a cloud identity provider" (signals.md S4). |
| Gain | Native Kerberos straight to existing domain controllers, multi-forest and air-gapped (company.md §3). "There is no requirement for Microsoft Entra ID, Microsoft Application Proxy, or any other cloud identity provider." (competitors.md §1). Password changes land in the AD log (company.md §3). Negotiates AES by default after RC4 removal (market.md §1.3). |
| Proof | York lists "Increased operational security through Kerberos authentication" (customers.md §3.3). Hypergate states deployments in "defence, government, and other regulated environments where cloud identity providers cannot be placed in the authentication path" (customers.md §4, Hypergate's claim, no named customer). |

## 3. Android app developer or ISV (SDK user)

Evidence for the role: SDK post with code for "any HTTP client" (competitors.md §3.12, company.md §2.3).

| | |
|---|---|
| Job to be done | Make an in-house or commercial Android app authenticate to on-prem Windows servers after NTLM goes away (signals.md S5). |
| Pain | "Android apps that still authenticate with NTLM need a replacement, and that replacement is Kerberos." (signals.md S5). "Users will not accept the alternative, which is typing domain passwords into phones." (voice.md §8). |
| Gain | `com.hypergate:sdk` on Maven Central "adds SPNEGO negotiate tokens to any Android app, so your app answers with Kerberos instead of NTLM." Cordova plugin and sample app exist (company.md §2.3). |
| Proof | None published: no SDK customer or download figure in the research (flagged). Competing SDKs: not found (competitors.md §3.12). |

## 4. Business or operations lead (user-side sponsor)

Evidence for the role: Lukas Landsberg, "Project Manager Business Performance", Maersk Drilling (customers.md §3.2). INFERRED: owns productivity of frontline or travelling staff.

| | |
|---|---|
| Job to be done | Let shift workers, officers or travelling staff do their work on the phone without IT friction (signals.md, purchase triggers table). |
| Pain | Shared devices log out after every shift and "each user was prompted for their credentials for each application" (customers.md §3.2). Bankers travel but still need in-house systems (customers.md §3.1). |
| Gain | "Improved efficiency & productivity on the rigs", "Less support due to one-time logging" (customers.md §3.2). Jefferies saw onboarding "requiring only minutes to set up the device" and fewer tickets (customers.md §3.1). |
| Proof | "I can recommend the Hypergate Solution and the Team" (Lukas Landsberg, customers.md §3.2). No case study has a number (customers.md, Gaps). |

## Gaps

- Economic buyer title, budget owner and price: unknown (company.md §8, Gaps).
- No quantified outcome in any story (customers.md, Gaps). Do not add figures.
- No Hypergate Files customer story, so Files proof is product claims only (customers.md, Gaps).
