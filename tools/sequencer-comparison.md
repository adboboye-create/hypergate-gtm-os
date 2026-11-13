# Cold-email sequencer comparison: EmailBison vs Instantly vs PlusVibe

Prepared 2026-11-13 for step 8 (sequence), step 9 (replies) and step 10 (CRM) of `context/docs/gtm-system.md`.

**How to read the citations.** Every claim carries a source tag like [S4]. The full URL for each tag is in the Sources list at the end, and every source was checked 2026-11-13. Tags marked **(snippet)** are facts seen only in a search-engine snippet because the page itself could not be fetched (404 or empty). Treat those as unverified until someone opens the page in a browser. "Unknown" means no source was found. Nothing here is guessed.

**Context that shapes the choice**

- Hypergate is a Swiss vendor (Papers AG, Zug) selling to enterprise IT and public sector in DACH, the EU, the US and Canada (CLAUDE.md; `context/docs/research/company.md`).
- Volume is low and signal-based: a few contacts per account. Sending capacity is not the constraint. Data residency, deliverability on a small fleet, and clean data flow to Zoho CRM matter more.
- Step 8 already plans LinkedIn as manual via Sales Navigator at the start (`context/docs/gtm-system.md`, step 8). So a sequencer without LinkedIn steps does not block the system.

---

## 1. Comparison table

| Criterion | EmailBison | Instantly | PlusVibe |
|---|---|---|---|
| **DPA** | Yes. The privacy policy says a DPA must be signed before any personal data is processed, on request to support@emailbison.com [S4]. The trust center lists "EmailBison-DPA-2026-08-04.pdf", gated behind an NDA or access request [S3]. Text not reviewed. | Yes, public. It includes the EU SCCs (Decision 2021/914) and the UK Addendum, applies the SCCs to Swiss data under the FADP with modifications, and gives 15 days' notice of new subprocessors with a right to object [S12]. Two different "last updated" dates appear on the page (Sept 10, 2026 and May 6, 2026) [S12]. | Yes, public. It includes the EU SCCs (Modules 2 and 3) and the UK Addendum. It names no processor entity and has no date. The subprocessor list (Exhibit A) and SCC annexes (Exhibit B) are referenced but not shown [S25]. No Swiss FADP mention found [S25]. |
| **Data hosting / EU option** | Recipient and campaign data is stored on servers "located in the United States, Germany, Finland, or Sweden" [S4]. Enterprise customers can choose "any of our data centre locations" across North America and Europe [S2]. Region pinning per customer is not confirmed in writing. | Unknown. The DPA states no storage location [S12]. The subprocessor list shows mostly "USA" locations, with Hetzner listed as hosting **(snippet)** [S13]. No EU-only option found. | United States. The DPA says "we process personal data in the United States of America" [S25]. The privacy policy says data "may be viewed and hosted anywhere in the world" [S24]. |
| **Subprocessors list** | Not published. The trust center shows "0" subprocessors [S3], while the privacy policy names Stripe as a third party [S4]. | Published in the help center, with USA, USA/Canada and USA/EU locations **(snippet)** [S13]. The page returned 404 when fetched directly. | Not published. The DPA references Exhibit A, but it is not on the page [S25]. |
| **Certifications** | SOC 2 Type 2, GDPR and HIPAA marked "Compliant" on the trust center [S3]. Report access is gated [S3]. | Trust center exists, but its content could not be read [S34]. Unknown. | Unknown. |
| **Legal entity** | Unknown. Not named in the privacy policy [S4]. | Unknown from the pages reviewed. | Unclear. The privacy policy names Pipl Software Inc. at a Dover, Delaware (US) address and also says "PlusVibe.ai is incorporated in Poland" [S24]. The DPA footer says Pipl Software Inc [S25]. |
| **Warmup** | Yes: "Private Email Warm-up" [S5] and "smart warm-up and bounce protection" [S1]. Webhooks fire when warmup is disabled for bounces [S6]. | Unlimited warmup on all Outreach plans [S11]. Warmup analytics are available via the API [S14]. | Basic on Personal; advanced on Business; advanced plus a recovery scheme on Agency [S23]. Warmup stats are available via the API [S27]. |
| **Inbox rotation** | Not explicitly claimed. The site mentions routing sequences across IP pools [S5]. | SISR (server and IP sharding and rotation) on Lightspeed ($358/mo) and above [S11]. Sender rotation on lower plans: unknown. | Sender auto-rotation on all plans; "AI-algorithmic IP rotation" on Business and Agency [S23]. |
| **Dedicated vs shared infra** | Dedicated. "Isolated infrastructure with dedicated IPs" is in the base plan [S1]. The site also claims "single tenant clusters", dedicated VPCs and static egress IPs [S5]. The API base is a dedicated instance (`dedi.emailbison.com`) [S9]. | Shared by default. Dedicated or private server and IP blocks via SISR from Lightspeed. "Private Deliverability Network" on Enterprise [S11]. | Shared on Personal and Business; dedicated IPs "No" on both. Isolated sending server and dedicated connector IPs on Agency only [S23]. |
| **Placement testing** | Claimed as "Native deliverability testing with EmailGuard" [S5]. The repo's `/inbox-placement-test` uses MailReach seeds via the Bison API instead (see section 8). | Native, with a full API: create a test, read results, read blacklist and SpamAssassin reports [S14]. Sold as an add-on: Growth Inbox Placement $47/mo and Hypergrowth Inbox Placement $97/mo **(snippet)** [S19]. | Paid add-on: Starter $19/mo (300 credits), Growth $39/mo (1,000), Scale $89/mo (5,000) [S23]. API endpoints for placement tests were not found in the API index [S27]. |
| **API: load leads from Clay** | Native Clay integration with "Import Lead(s) to Campaign", "Create or Update Lead" and blocklist actions, plus an HTTP API fallback [S8][S10]. Leads attach by list ID or lead IDs; sync into an active campaign takes up to 5 minutes [S9]. Bearer token auth [S9]. Rate limit: unknown. | API v2 with scoped keys [S14]. Bulk add up to 1,000 leads per call, with email validation, blocklist and duplicate checks [S17]. Rate limit is 100 requests/s and 6,000/min per workspace [S16]. Native Clay integration: unknown. Plan needed for API access: unknown (pricing-table checkmarks were not readable) [S11]. | "Add leads to a campaign" takes a list of lead objects, with skip options for leads already in the workspace or in other campaigns [S27][S29]. Rate limit is 10 requests/s [S26]. **The API requires the Business plan** [S26]. Native Clay integration: unknown. |
| **API: weekly results export** | Fetch replies and campaign emails per lead [S10]. Campaign leads and sequence steps endpoints are used in `/campaign-qa` (repo). Campaign stats endpoint: not checked in the reference (unknown). | Campaign analytics, daily analytics, per-step analytics, and a POST-based List leads endpoint [S14]. | Campaign stats, all-campaign stats by date range, variation stats, and paginated workspace leads [S27]. Known gotcha: the bulk leads endpoint omits `custom_*` variables (repo `/campaign-qa`). |
| **Webhooks** | Rich set: Contact Replied, Contact Interested (manual or auto AI categorization), Contact Unsubscribed, Email Bounced, Untracked Reply, Tag Attached, warmup alerts and more [S6]. | email_sent, reply_received, auto_reply_received, email_bounced, lead_unsubscribed, lead_interested, lead_not_interested, lead_meeting_booked, lead_wrong_person, lead_out_of_office, and custom labels as event types [S15]. | First reply, all replies, positive replies, LEAD_MARKED_AS_{LABEL}, bounces, emails sent, unibox sends, system alerts [S28]. Business plan or higher [S23]. |
| **Native Zoho CRM** | No. Native sync is HubSpot and Salesforce, plus "CRM integrations powered by OutboundSync" [S5]. Whether OutboundSync covers Zoho: unknown. | No native Zoho connector found. The help center lists HubSpot, Salesforce and Pipedrive **(snippet)** [S22]. **Instantly is a listed app in Zoho Flow** (Zoho's own automation tool), with 7 triggers (including Email replied and Lead event occurred) and 14 actions (including Add lead to campaign and Add to blocklist) [S18]. | No native Zoho found. The pricing page names HubSpot, Salesforce and GoHighLevel [S23]. Webhooks are documented for CRMs, Zapier and Make [S28]. |
| **Zoho path** | Webhooks to a Zoho Flow or Make webhook trigger, or a small script calling the Zoho CRM API. Suppression syncs back via the blocklist API [S8][S6]. | Zoho Flow out of the box [S18], or webhooks [S15]. | Webhooks [S28] to Zoho Flow, Zapier or Make. |
| **Unified inbox** | Master Inbox: all senders in one view, filterable by campaign, reply status, sender and tag [S7]. | Unibox. Listed with "Built-in CRM integrated with Unibox" on Hypergrowth [S11]. Whether Growth includes Unibox: unknown [S11]. | Unified inbox on all plans [S23]. Full Unibox API, including drafts and scheduled replies [S27]. |
| **Reply classification** | "Auto AI categorization" toggle marks replies as Interested automatically [S6]. Other auto categories: unknown. | AI auto-tagging into lead labels, including custom labels; a test endpoint predicts the label for a reply text [S14]. | Sentiment detection on Personal; "AI reply agents" on Business and above [S23]. |
| **LinkedIn steps** | None found [S5][S10]. | None native found. The blog calls Instantly "email-first" **(snippet)** [S21]. LinkedIn is via a marketplace partner (Aimfox) **(snippet)** [S20]. | None native found in plans or API [S23][S27]. A LinkedIn scraper extension is listed, not LinkedIn sending [S23]. |
| **Published price** | Base plan $599/month with 500,000 emails/month, unlimited leads and unlimited teammates [S1]. No lower tier is shown [S1]. | Growth $47/mo (5,000 emails, 1,000 contacts). Hypergrowth $107/mo (125,000 emails, 25,000 contacts). Lightspeed $358/mo (500,000 emails, 100,000 contacts). Enterprise: custom. Yearly toggle shows about 20% less [S11]. The page contradicts itself on Hypergrowth: a bundle section shows $358/mo [S11]. | Personal $37/mo (25,000 emails, 30,000 active leads). Business $77/mo (150,000 emails, 100,000 active leads). Agency from $497/mo. Yearly is "2 months free" [S23]. |
| **Cheapest plan that meets our needs** (API, webhooks, inbox) | $599/mo [S1]. | Hypergrowth $107/mo for Unibox [S11]. API plan requirement unknown. Placement add-on extra [S19, snippet]. | Business $77/mo for the API and webhooks [S23][S26]. Placement add-on extra [S23]. |
| **Fit with repo skills** | Best. `/inbox-placement-test` is built only on EmailBison + MailReach. `/campaign-qa` Option C covers Bison. | Good. `/campaign-qa` Option A (labelled "preferred"). `/inbox-placement-test` would need porting, though Instantly's own placement API could replace it. | Good for QA. `/campaign-qa` Option B has the most detailed gotchas. `/inbox-placement-test` would need porting. |

Repo skill references: `.claude/skills/inbox-placement-test/SKILL.md` (description and lines 290 to 294: "Built on the EmailBison and MailReach APIs"); `.claude/skills/campaign-qa/SKILL.md` (lines 397 to 553: Options A Instantly, B PlusVibe, C Email Bison).

---

## 2. Recommendation: EmailBison, conditional on two written confirmations

**Pick EmailBison**, but only after it confirms two things in writing (see "Main risk").

**Why**

1. **Best GDPR position for a Swiss vendor selling to EU public sector.** EmailBison is the only one of the three that names EU data centres for recipient data (Germany, Finland, Sweden) [S4]. It also offers enterprise customers a choice of European locations [S2]. It requires a signed DPA before any processing [S4] and shows SOC 2 Type 2 on its trust center [S3]. PlusVibe processes in the US [S25] and its legal entity is unclear [S24]. Instantly's hosting location is not stated anywhere I could read [S12][S13].
2. **Dedicated infrastructure in the base plan.** Isolated infrastructure with dedicated IPs is included at the entry price [S1][S5]. For a security vendor sending a few targeted emails a day, our reputation then does not depend on other tenants' sending. With Instantly, dedicated IPs start at Lightspeed ($358/mo) [S11]. With PlusVibe, they start at Agency (from $497/mo) [S23].
3. **Cleanest Clay-to-sequencer path.** EmailBison has a native Clay integration with "Import Lead(s) to Campaign" and blocklist actions [S8][S10]. That covers step 7 to 8 hand-off and step 2 suppression without custom code.
4. **The repo already runs on it.** `/inbox-placement-test` works only with EmailBison + MailReach, and `/campaign-qa` supports it. No skill needs rewriting.
5. **Good event model for step 9 and step 10.** EmailBison has Contact Replied, Contact Interested (with auto AI categorization), Unsubscribed, Bounced and Untracked Reply webhooks [S6]. These map directly to the CRM activity and suppression rules in `gtm-system.md` steps 9 and 10.

**Main risk: GDPR terms are claimed, not yet read.** The DPA sits behind an NDA [S3]. The trust center lists zero subprocessors [S3], while the privacy policy names Stripe [S4], so the list is incomplete. The policy says recipient data may sit in the US *or* the EU [S4]. Per-customer EU pinning is only stated for "enterprise customers" [S2], and the Swiss FADP is not mentioned. If Hypergate cannot get, in writing: (a) EU-only hosting for its workspace, and (b) a DPA with SCCs, a Swiss FADP clause and a full subprocessor list, then the main reason for choosing EmailBison falls away.

**Secondary risks**

- **Cost per contact.** $599/month [S1] (12 x $599 = $7,188 a year at list price, my arithmetic) buys 500,000 emails a month, far above a signal-based volume. Instantly Hypergrowth ($107/mo) and PlusVibe Business ($77/mo) are much cheaper at list price [S11][S23].
- **No native Zoho.** Step 10 needs a webhook-to-Zoho build (Zoho Flow, Make, or a small script). Instantly is the only one with a ready-made Zoho Flow app [S18].
- **No LinkedIn steps.** None of the three has native LinkedIn steps. This matches the current plan of manual Sales Navigator (step 8).

**Actions before signing**

1. Request the DPA through trust.emailbison.com [S3] or support@emailbison.com [S4]. Have the person who owns privacy at Papers AG review it.
2. Ask EmailBison to confirm in writing: EU-only data centre for the workspace, the full subprocessor list, Swiss FADP coverage, the contracting entity and country, and whether $599 is the lowest tier.
3. Confirm whether OutboundSync [S5] supports Zoho CRM. If not, plan step 10 as a webhook to Zoho Flow.

---

## 3. What would change the recommendation

| If this turns out to be true | Then choose | Why |
|---|---|---|
| EmailBison will not commit to EU-only hosting, or its DPA lacks SCCs or a Swiss clause | **Instantly** (Hypergrowth, plus the placement add-on) | It has the most complete *public* DPA (EU SCCs, UK Addendum, Swiss FADP clause, 15-day subprocessor notice) [S12], plus the Zoho Flow app [S18] and native placement tests [S14]. Hosting still needs confirming [S13]. |
| Instantly confirms EU hosting, or its subprocessor list shows EU hosting (for example Hetzner in Germany) **(snippet)** [S13] | **Instantly** | It would then match EmailBison on GDPR at a fraction of the list price, with a better Zoho path. The cost is porting `/inbox-placement-test` to Instantly's placement API. |
| Budget is capped well under $599/month and GDPR review accepts US processing under SCCs | **Instantly** first, PlusVibe second | Instantly has the public DPA. PlusVibe is cheapest (Business $77/mo) [S23], but it processes in the US [S25], publishes no subprocessor list [S25] and has an unclear legal entity [S24]. |
| Volume grows to several shared-IP-sensitive domains, or reply rates drop for infrastructure reasons | **EmailBison** stays the right choice | Its dedicated, isolated IPs and the existing placement-test skill are the levers. |
| The team wants LinkedIn automated inside the same tool | **None of these three** | No native LinkedIn steps were found in any of them [S5][S21][S23]. Pick a separate LinkedIn tool, or a different multichannel sequencer, and re-run this comparison. |
| Zoho CRM is not actually the CRM (step 10 says it is unconfirmed) | Re-score row "Native Zoho CRM" | EmailBison has native HubSpot and Salesforce sync [S5], and Instantly lists HubSpot, Salesforce and Pipedrive **(snippet)** [S22]. |

---

## 4. Not verified (open items)

- EmailBison: DPA text, contracting entity, full subprocessor list, Swiss FADP coverage, whether EU-only pinning is available below "enterprise", API rate limits, any tier below $599, and whether EmailGuard placement testing is included or extra.
- Instantly: hosting location (DPA silent [S12]). The subprocessor list is **(snippet)** only, because the page returned 404 [S13]. Trust center content is unreadable [S34]. API and webhook plan requirements are unknown, since pricing-table checkmarks did not render [S11]. Placement add-on prices are **(snippet)** [S19]. The Hypergrowth price is contradictory on the pricing page [S11]. Native Clay integration is unknown.
- PlusVibe: subprocessor list (Exhibit A not shown [S25]), the Pipl Software Inc. (Delaware) vs Poland incorporation question [S24], certifications, native Clay integration, and placement-test API.
- All three: no native Zoho CRM integration found. No native LinkedIn steps found. A search snippet suggests PlusVibe's blog describes a LinkedIn step in a sequence, while a competitor's review says PlusVibe is email-only. Neither is a product doc, so this is treated as not supported.

---

## Sources (all checked 2026-11-13)

- [S1] EmailBison pricing: https://emailbison.com/pricing, checked 2026-11-13
- [S2] EmailBison security page: https://emailbison.com/security, checked 2026-11-13
- [S3] EmailBison trust center: https://trust.emailbison.com, checked 2026-11-13
- [S4] EmailBison privacy policy (effective Oct 18, 2025): https://emailbison.com/emailbison-privacy-policy.pdf, checked 2026-11-13
- [S5] EmailBison homepage: https://emailbison.com, checked 2026-11-13
- [S6] EmailBison docs, when webhooks are triggered: https://docs.emailbison.com/webhooks/when-are-webhooks-triggered.md, checked 2026-11-13
- [S7] EmailBison docs, Master Inbox overview: https://docs.emailbison.com/master-inbox/overview.md, checked 2026-11-13
- [S8] EmailBison docs, Clay overview: https://docs.emailbison.com/low-code-tools/clay/overview.md, checked 2026-11-13
- [S9] EmailBison docs, adding leads to a campaign: https://docs.emailbison.com/campaigns/adding-leads-to-a-campaign.md, checked 2026-11-13
- [S10] EmailBison docs index: https://docs.emailbison.com/llms.txt, checked 2026-11-13
- [S11] Instantly pricing: https://instantly.ai/pricing, checked 2026-11-13
- [S12] Instantly Data Processing Addendum: https://instantly.ai/dpa, checked 2026-11-13
- [S13] Instantly sub-processors (snippet only; direct fetch returned 404): https://help.instantly.ai/en/articles/8177025-instantly-sub-processors, checked 2026-11-13
- [S14] Instantly API v2 docs index (endpoints, scopes, inbox placement, lead labels, AI auto-tagging): https://developer.instantly.ai/llms.txt, checked 2026-11-13
- [S15] Instantly webhook events: https://developer.instantly.ai/guides/webhook-events.md, checked 2026-11-13
- [S16] Instantly API rate limit: https://developer.instantly.ai/getting-started/rate-limit.md, checked 2026-11-13
- [S17] Instantly, add leads in bulk (described in the S14 index): https://developer.instantly.ai/api-reference/lead/add-leads-in-bulk-to-a-campaign-or-list.md, checked 2026-11-13
- [S18] Zoho Flow, Instantly + Zoho CRM: https://www.zohoflow.com/apps/instantly/integrations/zoho-crm/, checked 2026-11-13
- [S19] Instantly plans overview, inbox placement add-on prices (snippet only): https://help.instantly.ai/en/articles/10273259-instantly-plans-overview, checked 2026-11-13
- [S20] Instantly marketplace, Aimfox (snippet only): https://instantly.ai/marketplace/aimfox, checked 2026-11-13
- [S21] Instantly blog, multi-channel outreach (snippet only): https://instantly.ai/blog/multi-channel-outreach/, checked 2026-11-13
- [S22] Instantly help center, integrations collection (snippet only): https://help.instantly.ai/en/collections/3491403-integrations, checked 2026-11-13
- [S23] PlusVibe pricing: https://www.plusvibe.ai/pricing, checked 2026-11-13
- [S24] PlusVibe privacy policy: https://plusvibe.ai/privacy-policy, checked 2026-11-13
- [S25] PlusVibe data processing agreement: https://plusvibe.ai/data-processing-agreement, checked 2026-11-13
- [S26] PlusVibe API getting started (auth, rate limit, Business plan): https://developer.plusvibe.ai/, checked 2026-11-13
- [S27] PlusVibe API docs index: https://developer.plusvibe.ai/llms.txt, checked 2026-11-13
- [S28] PlusVibe webhooks overview: https://developer.plusvibe.ai/webhooks-overview-2268181m0.md, checked 2026-11-13
- [S29] PlusVibe, add leads to a campaign: https://developer.plusvibe.ai/add-leads-to-a-campaign-38494490e0.md, checked 2026-11-13
- [S34] Instantly trust center (page content did not render): https://trust.instantly.ai/, checked 2026-11-13
