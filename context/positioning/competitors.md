# Hypergate competitors and alternatives

Status: v0.1, 2026-11-13. Built only from `context/docs/research/`, mainly competitors.md. Citations use `file.md §section`. INFERRED marks our reading. Several competitor facts come from search summaries (marked in the source file); verify before quoting externally (competitors.md, Gaps).

Hypergate publicly names only Entra ID, Application Proxy and Okta, as brokers it avoids (competitors.md, Gaps).

## Main competitors

| Vendor / route | Relationship | What they offer for this job | Where it falls short for on-prem AD | Source |
|---|---|---|---|---|
| Microsoft Entra ID + Authenticator / Company Portal + Application Proxy | Direct alternative (Intune is also a partner) | Broker-based SSO on Android; KCD to on-prem apps via Application Proxy | Needs Entra preauthentication in the cloud; Android browser SSO is Edge only; shared device mode needs MSAL-built apps | competitors.md §3.1 |
| Okta Verify / FastPass | Alternative (cloud IdP) | Device trust, passwordless | No on-prem Kerberos to AD without a broker found (INFERRED) | competitors.md §3.4 |
| Ping Identity | Alternative (IdP) | SSO "That Works Everywhere" | No Android on-device Kerberos found | competitors.md §3.5 |
| Apple Kerberos SSO extension | Direct alternative on iOS | Built-in Kerberos TGT and AD password change | iOS/macOS only; nothing for Android | competitors.md §3.9 |
| Omnissa Workspace ONE (Content, Access) | Partner, partial overlap | SMB access via Content app | Needs Content Gateway server; Android Mobile SSO is certificate based, not Kerberos | competitors.md §3.2 |
| Ivanti Docs@Work + Sentry | Partner, partial overlap | File and KCD SSO via AppTunnel | Needs Standalone Sentry | competitors.md §3.6 |
| BlackBerry Work / BEMS Docs | Partner, partial overlap | KCD file access; 2026 "sovereign control" message | Needs BEMS server; competes for the same sovereignty buyer (INFERRED) | competitors.md §3.7 |
| Samsung Knox | Complementary | Device security and config; Knox Authentication Manager uses Entra ID | Samsung deprecated its own AD Kerberos SSO "due to low usage" | competitors.md §3.3 |
| Acronis Cyber Files | Replacement target (Files) | On-prem mobile file access | End of life; security updates stop 31 Dec 2026, no on-prem successor | signals.md S9 |
| Imprivata, BlueFletch, Specops, ManageEngine | Adjacent | Shared-device badge SSO; AD password reset | No Kerberos to on-prem AD found; not researched further | competitors.md §3.11, §3.12 |

## Where Hypergate wins

- On-prem or hybrid AD that cannot or will not put a cloud IdP in the mobile auth path: sovereignty, defence, air-gapped, offline sites (signals.md S4, customers.md §4).
- Android fleets: the platform has no built-in Kerberos and Samsung withdrew its own (competitors.md §1, §3.3).
- Browser choice: SPNEGO in Chrome via the account API, and Edge for Android supports Hypergate Authenticator (company.md §3, signals.md S11). Microsoft's Android browser SSO is Edge only (competitors.md §3.1).
- No extra servers: EMM file and SSO tools need Sentry, BEMS or Content Gateway (competitors.md §3.2, §3.6, §3.7).
- EMM changes: Intune has no built-in SMB access, and Hypergate works across 10 EMMs (signals.md S8, company.md §4).
- Shared and kiosk devices, multi-user on Android 9+ (company.md §2.1), with a Maersk Drilling shift-work story (customers.md §3.2).
- Acronis Cyber Files customers before 31 Dec 2026 (signals.md S9).

## Where Hypergate loses or is exposed

- Cloud-first estates already on Entra ID: Microsoft's broker covers SSO and comes with the stack (competitors.md §3.1). INFERRED.
- iOS-only fleets: Apple ships Kerberos SSO for free, and Hypergate's iOS FAQ line conflicts with Apple docs (competitors.md §3.9).
- Customers happy with their EMM's file tool and already running the gateway (competitors.md §3.6, INFERRED).
- Thin public proof: 3 stories, no numbers, newest from 2024, no Files story (customers.md, Gaps).
- Size and trust: 2024 team of 5 (scope unclear), no public pricing, contracting entity unclear (company.md §8, §11, §14).
- BlackBerry now sells sovereignty too (competitors.md §3.7).

## How to respond

| Objection or situation | Response grounded in research | Source |
|---|---|---|
| "We have Entra ID / Intune, Microsoft does SSO" | Microsoft's route to on-prem Kerberos apps needs Entra preauthentication and Application Proxy; Android browser SSO is Edge only. Hypergate talks to your DCs directly, and Intune is a supported EMM. | competitors.md §3.1, company.md §4 |
| "Our EMM already does file access" | Docs@Work needs Sentry, BEMS Docs needs a BEMS server, Workspace ONE Content needs Content Gateway. Hypergate Files needs no proxy or middleware and survives an EMM switch. | competitors.md §3.2, §3.6, §3.7; company.md §2.2 |
| "Samsung Knox covers this" | Knox secures the device; Samsung deprecated its AD Kerberos SSO and points to Azure AD. Hypergate deploys through Knox Manage. | competitors.md §3.3 |
| "We are moving to passkeys" | INFERRED: passkeys serve cloud IdP sign-in and do not issue Kerberos tickets for on-prem apps or SMB shares. Needs validation. | market.md §5 |
| "iOS already has Kerberos" | Concede on SSO. Point to the iOS extras Hypergate lists: expiry notification, AD password reset when expired, Files. | company.md §2.1, competitors.md §3.9 |
| "Who else uses you?" | Jefferies, Maersk Drilling, York Regional Police stories; public-sector logos. Do not quote counts newer than 2024. | customers.md §3, company.md §9 |
