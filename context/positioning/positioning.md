# Hypergate positioning

Status: v0.1, 2026-11-13. Built only from `context/docs/research/`. Citations use `file.md §section` in that folder. INFERRED marks our reading.

## Category

On-device Kerberos SSO and on-prem file access for managed Android and iOS. Hypergate's own line: "a fast, secure and accessible Kerberos Single Sign-On (SSO) solution for Android and iOS" (company.md §1). It sits between the EMM, which manages the device, and the identity layer: "Device management and identity are different problems, and MDM only solves the first one." (competitors.md §3.3).

## Target customer

- Organisations running on-prem or hybrid Active Directory with managed Android (or iOS) devices and Kerberos or Windows-authenticated apps, intranet or file shares (signals.md, Root condition).
- Sectors Hypergate names: "government entities, banking institutions, insurance companies, and law firms" (company.md §1), plus defence and critical infrastructure where a cloud IdP cannot sit in the auth path (customers.md §4, signals.md S4).
- Logo wall: 5 of 9 logos are public sector (customers.md §1, §2).

## The alternative they use today

| Alternative | What it means for the user | Source |
|---|---|---|
| Typing AD passwords into each app | Prompts per app, lockouts, tickets | signals.md Root condition, S12 |
| Cloud broker: Entra ID + Authenticator / Company Portal + Application Proxy (KCD) | Auth routed through Microsoft's cloud; Android browser SSO is Edge only | competitors.md §3.1 |
| Cloud IdP: Okta, Ping | Same broker model; no on-device Kerberos found | competitors.md §3.4, §3.5 |
| EMM file tools: Docs@Work + Sentry, BlackBerry Docs on BEMS, Workspace ONE Content + Content Gateway | Each needs a gateway server and is tied to that EMM | competitors.md §3.2, §3.6, §3.7; signals.md S8 |
| Acronis Cyber Files | End of life; security updates stop 31 Dec 2026 | signals.md S9 |
| On iOS: Apple Kerberos SSO extension | Free and built in | competitors.md §3.9 |

## Unique value

1. Native Kerberos on Android, which Android Enterprise does not ship (company.md §2.1, competitors.md §1).
2. Talks directly to existing domain controllers: "No need for additional servers or middleware" (company.md §3, voice.md §4).
3. No cloud broker in the path: no Entra ID, Application Proxy or Okta required (competitors.md §1).
4. EMM-agnostic: 10 EMMs listed, configured through managed config (company.md §3, §4).
5. One vendor for SSO, self-service AD password reset and SMB/NetApp file access (company.md §2.1, §2.2).

## Proof

- Three published stories: Jefferies, Maersk Drilling, York Regional Police (customers.md §3).
- Named quote: "Hypergate is easy to install and configure, and it seamlessly integrates into our existing MobileIron MDM environment" (customers.md §3.3).
- Logos: Bayerische Staatskanzlei, Linz AG, European Court of Auditors, Suva, States of Jersey Police, USPS, Noble (customers.md §1; logo only).
- Android Enterprise Recommended device guarantee; Zebra validated; Microsoft Edge for Android supports Hypergate Authenticator (company.md §3, customers.md §6, signals.md S11).
- 2024 self-reported: "over 50 paying customers", four Fortune 500, "more than 30,000 daily active users" (company.md §9). Current figures: unknown.

## Positioning statement

For IT and security teams in government, banking, insurance, legal and other regulated organisations that run Active Directory on-prem or hybrid and manage Android or iOS devices, Hypergate is the on-device Kerberos SSO and file access layer that lets phones sign in to internal apps, intranet and file shares the way domain-joined Windows PCs do (company.md §1, §3). Unlike Microsoft Entra Application Proxy or Okta, it needs no cloud identity broker, and unlike EMM file tools it needs no gateway server, because it talks directly to existing domain controllers and is configured through whichever EMM is already in place (competitors.md §1, §3; company.md §3, §4).

## Open points

- iOS claim conflict: Hypergate's FAQ says iOS has Kerberos only "through constrained delegation", while Apple documents a Kerberos SSO extension (competitors.md §3.9). Resolve before leading with iOS.
- Two homepage versions with different headlines: usability-first vs sovereignty-first (voice.md, Gaps). Which one is current is unconfirmed.
