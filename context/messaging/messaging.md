# Hypergate messaging

Status: v0.1, 2026-11-13, draft for review. Built only from `context/docs/research/`. Citations use `file.md §section`. Proof points are limited to what the research supports; there are no quantified results (customers.md, Gaps). This is not yet `facts.md`: claims here still need Hypergate approval before use in copy.

## Core message

Your phones can sign in to Active Directory the way your Windows PCs do: native Kerberos, straight to your own domain controllers, with no extra servers and no cloud broker.

Sources: "uses native Kerberos protocols, like your domain-joined Windows clients, and connects directly to existing Domain Controllers" (company.md §3); "No need for additional servers or middleware" (voice.md §4); no requirement for Entra ID, Application Proxy or any cloud IdP (competitors.md §1).

## Message pillars

### 1. Closes the Android Kerberos gap

- Android Enterprise ships no built-in Kerberos SSO (competitors.md §1).
- Samsung deprecated its own AD Kerberos SSO "due to low usage" (competitors.md §3.3).
- Proof: Maersk Drilling and York Regional Police both name this gap as their problem (customers.md §3.2, §3.3). Edge for Android supports Hypergate Authenticator (signals.md S11).

### 2. Uses what you already have

- Direct to existing domain controllers; multi-forest and air-gapped (company.md §3).
- Configured through your EMM; 10 EMMs listed (company.md §3, §4).
- Files: SMB2/SMB3 and NetApp "without requiring additional infrastructure, proxies, or middleware" (company.md §2.2).
- Proof: "easy to install and configure, and it seamlessly integrates into our existing MobileIron MDM environment" (customers.md §3.3).

### 3. Keeps authentication under your control

- No Entra ID, Application Proxy or Okta in the path (competitors.md §1).
- Built for sites where a cloud IdP "cannot be a single point of failure" or must stay within national boundaries (signals.md S4).
- Proof: public-sector logos (customers.md §1); Maersk rigs authenticate locally when the connection drops (customers.md §3.2).

### 4. Fewer prompts, fewer tickets

- Sign in once by certificate, Kerberos in the background (company.md §3).
- Self-service AD password reset on the device (company.md §2.1).
- Proof: all three stories report less support, with no figures (customers.md §3). Do not add numbers.

## Angle per persona

| Persona | Angle | Lead pillar | Source |
|---|---|---|---|
| Mobility / EMM admin | SSO and file shares from the EMM you run today, and they survive an EMM switch | 2, 4 | signals.md S8, customers.md §3.3 |
| Identity / security engineer | Kerberos on mobile with no cloud broker, ready for NTLM removal | 3, 1 | competitors.md §1, signals.md S5 |
| Android app developer / ISV | Swap NTLM for Kerberos in your app with one SDK | 1 | company.md §2.3, signals.md S5 |
| Business or operations lead | Shift and field staff stop typing passwords app by app | 4 | customers.md §3.2 |

Timely hooks: Acronis Cyber Files security updates end 31 Dec 2026 (signals.md S9); NTLMv1 SSO enforcement from 13 Oct 2026 (market.md §1.2); network NTLM off in the next Windows Server, date not given by Microsoft (market.md §1.1).

## Words to use

- native Kerberos, domain controllers, Active Directory (company.md §3)
- like your Windows PCs / domain-joined clients (company.md §3, voice.md §5)
- no extra servers, no middleware (voice.md §4)
- your EMM, EMM-agnostic (competitors.md §1)
- on-prem, hybrid, control, sovereignty (voice.md §5)
- named apps and devices: Chrome, Edge, SAP Fiori, ServiceNow, Zebra, Samsung (company.md §3, §5; customers.md §6)

## Words to avoid

- "seamless" as a lead word: Hypergate overuses it (voice.md §9).
- "Unmatched", "Win Across The Board" and similar generic claims (voice.md §9).
- Any number not in the research: ticket reduction %, device counts, time saved (customers.md, Gaps).
- "50+ customers" or "30,000 users" without saying they are 2024 self-reported (company.md §9).
- "Only" or "first" claims, except the sourced "only Hypori Compatible Files solution" (company.md §2.2).
- Jefferies quotes as Hypergate endorsements: they are about Android work profile (customers.md §3.1).
- Em dashes, and the site typos ("Suport", "ect.", "by themself") (voice.md §9).
