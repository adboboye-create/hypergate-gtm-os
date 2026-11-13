# Hypergate: Authorized Copy Facts

**Status:** DRAFT v0.1. Every claim below is taken word for word, or close to it, from Hypergate's own public pages and cited. **None is approved by Hypergate yet.** Copy written from this file stays draft until the "Approved by" column is filled in.

This file is the ONLY source of names, numbers and claims for prospect-facing copy (`/campaign-copy` FACTS GATE). Anything not listed here renders as `{{placeholder}}` in copy, never from memory and never invented.

**Last updated:** 2026-11-13 by Claude (draft from `context/docs/research/`), for review by the Hypergate GTM owner.

---

## Sender identity

| Field | Value |
|---|---|
| Sender name(s) | `{{sender_name}}`: unknown, to confirm with Hypergate |
| Title | `{{sender_title}}`: unknown |
| Signature format | `{{sender_signature}}`, resolved by the sequencer: "First / Title / Hypergate" (proposed) |
| Sender persona notes | First person singular. Technical peer writing to an IT admin, not a marketer (brand.md "How we write") |

## What we do (locked value prop)

The lead-in is verbatim; the tail may adapt per route.

- **Variant A (Files):** "Hypergate Files gives phones access to your on-prem SMB and Windows file shares, on any EMM, with no extra servers or middleware."
  Sources: "Seamless access to on-premise network CIFS, SMB (Samba) and Windows shares" (https://hypergate.com/); "Hypergate Files is completely EMM-agnostic" (https://hypergate.com/blog/mobile-file-access-acronis-cyber-files/); "without requiring additional infrastructure, proxies, or middleware" (https://hypergate.com/files/). All via [company.md §2.2](../docs/research/company.md) and [signals.md S8](../docs/research/signals.md).
- **Variant B (Authenticator):** "Hypergate gives Android phones native Kerberos sign-in to your own Active Directory, like your Windows PCs, with no extra servers and no cloud broker."
  Sources: [messaging.md "Core message"](messaging.md), [company.md §3](../docs/research/company.md).

Product one-liner (context, not copy): Kerberos SSO and on-prem file access for managed Android and iOS devices, configured through the customer's EMM, connecting directly to their own domain controllers and file servers ([CLAUDE.md](../../CLAUDE.md)).

## Approved claims and numbers (use these exact phrasings)

| # | Claim | Phrasing for copy | Source | Approved by / date |
|---|---|---|---|---|
| F1 | Intune has no built-in SMB access | "Intune has no built-in way to reach SMB file shares" | "Intune lacks a built-in solution for accessing SMB/CIFS network file shares" (https://hypergate.com/blog/simplify-intune-migration-with-hypergate-files-for-on-prem-access/, [signals.md S8](../docs/research/signals.md)) | pending |
| F2 | Old EMM file tools stay behind | "{{old_file_tool}} stays with {{old_emm}}" (tool names: Docs@Work, Workspace ONE Content, BlackBerry Work, SOTI Hub) | Same Hypergate blog post lists "Ivanti (MobileIron) Docs@Work", "BlackBerry Work", "VMware Workspace ONE Content", "SOTI Hub" as vendor-tied tools ([signals.md S8](../docs/research/signals.md)) | pending |
| F3 | Works on any EMM | "works on any EMM" | "Hypergate Files is completely EMM-agnostic" ([signals.md S8](../docs/research/signals.md)) | pending |
| F4 | No extra infrastructure | "no extra servers, proxies or middleware" | "without requiring additional infrastructure, proxies, or middleware" (https://hypergate.com/files/, [company.md §2.2](../docs/research/company.md)) | pending |
| F5 | Files open in native apps | "files open in Word, Excel or the PDF app, no extra viewer" | "Users can open files in their respective native apps (Word, Excel, PDF ect.) without requiring additional viewers" (https://hypergate.com/files/, [company.md §2.2](../docs/research/company.md)) | pending |
| F6 | SMB2/SMB3 and NetApp | "SMB2/SMB3 shares and NetApp" | https://hypergate.com/files/ ([company.md §2.2](../docs/research/company.md)) | pending |
| F7 | Intune app exists | "there's a version built for Intune (Hypergate Files for Intune)" | Google Play listing "Hypergate Files for Intune", package com.hypergate.files.intune ([company.md §2.2](../docs/research/company.md)) | pending |
| F8 | Swiss company | "Hypergate is built by Papers AG in Zug, Switzerland" | https://hypergate.com/about-us/ ([CLAUDE.md](../../CLAUDE.md)) | pending |
| F9 | Compatibility tested with the customer | "Hypergate tests it with you on your own devices and shares" | FAQ: "just contact us and we will test it together with you." (https://hypergate.com/faq/, via [personas.md §1 Objections](../icp/personas.md) and [voice.md §6](../docs/research/voice.md)) | pending |

**Formatting rules for proof**
- Write "Hypergate" and "Hypergate Files", never "hypergate.com" (domains turn into links).
- Product names exactly as their vendors write them: "Intune", "Workspace ONE", "Docs@Work", "BlackBerry Work", "SOTI Hub".

## Numbers to keep fuzzy (never quote as hard numbers)

- Customer count, users, Fortune 500 count: last public figures are self-reported from January 2024 ([company.md §9](../docs/research/company.md)). Do not use in cold copy.
- Download counts on Google Play.
- Any ticket reduction, time saved or device count: none exists in the research ([case-studies.md](../docs/case-studies.md)).

## Authorized social-proof names

**None yet.** Every customer name stays out of copy until Hypergate approves it here.

Candidates waiting for approval (do not use):

| Name | What it would prove | Caveat |
|---|---|---|
| York Regional Police | Kerberos SSO on Android inside MobileIron, police | An integration, not an Intune migration. Not proof for the Intune Files campaign |
| Maersk Drilling | Shared shift devices, offline local AD | Now part of Noble. Authenticator, not Files |
| Jefferies | Bank on Android work profile | 2019. Quotes are about work profile, not Hypergate |

No Hypergate Files customer story exists ([case-studies.md](../docs/case-studies.md)).

## Proof caveats

- No Files case study exists, so Files copy leads with the mechanism (F1 to F6), not a story.
- F2 says the tool is tied to the old EMM. It does not say the prospect uses that tool. Copy must hedge: "if file access runs through {{old_file_tool}} today".

## Banned

### Banned angles
- Attacking an EMM vendor. Ivanti, Omnissa, BlackBerry, SOTI, Samsung and Microsoft are partners or integrations ([competitors.md](../positioning/competitors.md)).
- Using the Ivanti EPMM CVEs as a scare line ([signal-matrix.md, Killed signals](../icp/signal-matrix.md)).
- Telling the prospect their migration plan has a gap or a mistake (iron law 14, insult test).
- Regulation (DORA, NIS2) as the reason to buy.
- Price, discounts, trials.

### Banned words and phrasing (company-specific)
- "seamless", "unmatched", "win across the board" ([messaging.md "Words to avoid"](messaging.md)).
- "only" or "first" claims (except the sourced Hypori line, which is not for cold copy).
- "50+ customers", "30,000 users".

### Never in copy, under any circumstance
- Customer names not listed under Authorized social-proof names.
- Hypergate partner names in prospect copy unless the partner has agreed.

## Voice notes

- Register: technical, plain, peer to peer. The voice of the 2026 Hypergate blog, not the old product pages ([brand.md](../brand-kit/brand.md)).
- Hedges about the prospect: "my guess is", "could be off", "if that's how it works today".
- Spelling: British or American still to confirm with Hypergate ([brand.md](../brand-kit/brand.md)). Draft copy uses American spelling for UK/US/CA sends.
- Subjects: lowercase, 3 to 5 words, no variables, same subject across the thread.

## CTA ladder

- **Primary:** a question about their plan: "Is phone access to file shares part of the Intune plan?"
- **Secondary:** offer the short how-to: "Want the one-page setup for Intune?" (only if Hypergate confirms the asset exists: `{{intune_setup_asset}}`).
- **Never:** calendar links, "book a call", "free", demo requests in email 1.

## Internal only (never in prospect copy)

- Pricing (unknown), customer roster, partner terms, signal sources (TheirStack, Clay), reply rates.
