**Research for legal review, not legal advice.** Prepared 2026-11-13 for sign-off on B2B cold outreach (email and LinkedIn) by Hypergate (Papers AG, Zug, Switzerland). Nothing here has been reviewed by a lawyer.

# Cold outreach compliance brief: email and LinkedIn

**Scope.** Unsolicited B2B email and LinkedIn messages to named IT staff (mobility/EMM admins, identity engineers, CISOs) at companies and public bodies in DE, AT, CH, FR, IT, the rest of the EU, the UK, the US and Canada. It feeds step 7 (finding and verifying emails) and step 8 (the sequence) in [`context/docs/gtm-system.md`](gtm-system.md), where the compliance gate is still open (gtm-system.md, step 7, "Compliance gate [open]").

**How sources are marked.** Every claim carries a URL and "checked 2026-11-13". Source types:

- **[law]**: official law text (gesetze-im-internet.de, ris.bka.gv.at, fedlex.admin.ch, legifrance.gouv.fr, legislation.gov.uk, laws-lois.justice.gc.ca).
- **[regulator]**: a regulator's own page or decision (CNIL, ICO, Garante, FTC).
- **[secondary]**: a law-firm blog, commentary or non-official mirror. Not verified against the primary text.
- **[snippet]**: taken only from a search-result summary. Weakest; must be checked.

**Access limits.** EUR-Lex did not load in this session, so EU texts (ePrivacy Directive, GDPR) were read from the legislation.gov.uk copies. For the GDPR that is the "as adopted by EU" version; for the ePrivacy Directive it is the UK archive copy of the consolidated text. Both should match EUR-Lex but were not compared against it. The DSK guidance PDF, the CRTC FAQ (HTTP 403) and the full CJEU judgments could not be read.

---

## 1. One-screen summary

| Jurisdiction | Regime for B2B email to a named work address | Main law | Can we cold email? | Conditions |
|---|---|---|---|---|
| Germany | Opt-in, no B2B exception | UWG §7(2) Nr. 2 | **No** | Prior express consent of the "Adressat". The soft opt-in (§7(3)) needs a prior sale. Courts treat LinkedIn messages as e-mail too [secondary] |
| Austria | Opt-in; law covers legal persons | TKG 2021 §174(3) to (5) | **No** | Prior consent of the "Empfänger". Soft opt-in needs a prior sale. Cold calls also need consent (§174(1)) |
| Switzerland | Opt-in for "Massenwerbung"; one-to-one email unclear | UWG Art. 3(1) lit. o; revFADP Art. 19, 30, 31 | **Yes with conditions** (legal to confirm) | Only genuinely individual, low-volume emails. Correct sender, free opt-out, revFADP info within one month |
| France | Opt-out for professionals (CNIL) | CPCE L34-5; GDPR Art. 6(1)(f), 14, 21 | **Yes with conditions** | Message must relate to the person's job. Identify sender, simple free opt-out, Art. 14 notice, Art. 21 objection |
| Italy | Opt-in, applied to professionals and LinkedIn-sourced leads | Codice privacy art. 130(1)-(2); GDPR Art. 6(1)(a) | **No** | Garante 2026 decision: consent only, not legitimate interest, even for a software pitch to a professional sourced via LinkedIn Sales Navigator |
| Rest of EU | Depends on each national transposition of ePrivacy Art. 13(5) | ePrivacy Dir. 2002/58/EC Art. 13; GDPR | **Unknown per country: treat as No** | Belgium (EU institutions in Brussels): only impersonal addresses of legal persons are exempt [secondary]. All others not researched |
| UK | Opt-out for corporate subscribers | PECR reg. 22 (individual subscribers only), reg. 23; UK GDPR | **Yes with conditions** | Not sole traders or partnerships. Identify sender, valid opt-out address, UK GDPR legitimate-interest test, Art. 14 notice, absolute right to object |
| US | Opt-out | CAN-SPAM, 15 U.S.C. 7701 ff. | **Yes with conditions** | True headers, honest subject, ad disclosure, physical postal address, opt-out honoured within 10 business days |
| Canada | Opt-in (express or implied) | CASL s.6, s.10(9), s.12 | **Yes with conditions** | Implied consent only if the address was conspicuously published, carries no "no unsolicited messages" statement, and the message fits the person's role. Guessed emails do not qualify |

**Biggest constraint.** Germany, Austria and Italy, three of the core DACH/EU markets (icp.md §1), require prior consent for B2B email, and German and Italian sources extend that to LinkedIn messages. In those countries there is no compliant cold email or cold promotional DM route: only opt-in routes (content, events, partners, referrals, inbound) and, in Germany only, B2B phone calls with presumed consent.

**Applies everywhere in the EU and to Swiss recipients:** the data protection layer (GDPR / revFADP) sits on top of the e-marketing rules. Even where cold email is allowed, Hypergate must have a lawful basis to collect and enrich the address, give the Art. 14 (or revFADP Art. 19) notice, and honour objections across all channels.

---

## 2. EU baseline (applies to DE, AT, FR, IT and the rest of the EU)

### 2.1 ePrivacy Directive 2002/58/EC, Article 13

Source: legislation.gov.uk copy of the consolidated Directive, https://www.legislation.gov.uk/eudr/2002/58/article/13/data.html [law, UK archive copy; not compared with EUR-Lex], checked 2026-11-13.

- **Art. 13(1):** email for direct marketing is allowed "only in respect of subscribers or users who have given their prior consent".
- **Art. 13(2):** existing-customer exception (own similar products, contact details obtained in a sale, opt-out offered "free of charge and in an easy manner"). Hypergate's targets are not customers, so this does not help prospecting.
- **Art. 13(4):** banned in all cases: disguising or concealing the sender's identity, or no "valid address to which the recipient may send a request that such communications cease".
- **Art. 13(5):** paragraphs 1 and 3 apply to subscribers who are natural persons. For other subscribers (companies, public bodies), Member States must ensure their "legitimate interests" are "sufficiently protected". This is why the B2B rule differs country by country: some states extended opt-in to legal persons (DE, AT, IT), others did not (FR for professionals, UK, BE for impersonal addresses).

**Is LinkedIn "electronic mail"?** The CJEU held in C-102/20 *StWL Städtische Werke Lauf* (25 November 2021) that ads shown in an email inbox in the form of a real email are use of electronic mail for direct marketing under Art. 13 [secondary: summaries at https://curia.europa.eu/jcms/jcms/p1_3583635/en and https://www.thomashelbing.com/en/wissen/dsgvo-hub/rechtsprechung/1.4.35-eugh-stwl-pegnitz; full judgment not read], checked 2026-11-13. German courts rely on this to treat social-network messages as e-mail (section 3). A CJEU judgment of 13 November 2025, *Inteligo Media* (C-654/23), on the scope of "direct marketing" under Art. 13 was found [snippet only, https://www.pearlcohen.com/cjeu-clarifies-why-not-all-unsolicited-newsletter-emails-require-prior-consent/], checked 2026-11-13. Its holding was not read and is **unknown**.

### 2.2 GDPR (Regulation (EU) 2016/679)

Source: "as adopted by EU" text on legislation.gov.uk [law], checked 2026-11-13.

- **Territorial scope, Art. 3(2)(a):** applies to a non-EU controller processing data of people in the Union in connection with "the offering of goods or services, irrespective of whether a payment of the data subject is required". https://www.legislation.gov.uk/eur/2016/679/article/3/adopted. Whether B2B prospecting by a Swiss company falls under Art. 3(2)(a) is a question for legal (Q3).
- **EU representative, Art. 27:** a controller caught by Art. 3(2) must "designate in writing a representative in the Union", unless processing is occasional, not large-scale special-category data and unlikely to result in a risk. A recurring outbound programme is unlikely to be "occasional" (my reading, not a legal conclusion). https://www.legislation.gov.uk/eur/2016/679/article/27/adopted. **Gap:** Hypergate's privacy policy names no EU representative, no controller address, no DPO and no legal basis, and refers once to "Papers GmbH" (https://hypergate.com/privacy-policy/, checked 2026-11-13).
- **Lawful basis, Art. 6(1)(f) and Recital 47:** legitimate interests is the basis normally relied on for B2B prospecting where national e-marketing law allows opt-out (CNIL and ICO both say so, sections 6 and 9). The text of Art. 6(1)(f) and Recital 47 was **not read** in this session (the contents page did not include them); confirm wording on EUR-Lex.
- **Information duty, Art. 14** (data not obtained from the person): https://www.legislation.gov.uk/eur/2016/679/article/14/adopted
  - Art. 14(1): controller identity and contact details (and representative), DPO if any, purposes and legal basis, categories of data, recipients, third-country transfers.
  - Art. 14(2): retention, **the legitimate interests pursued**, rights (including to object), right to complain to a supervisory authority, **the source of the data and whether it came from publicly accessible sources**, automated decision-making.
  - Art. 14(3)(b): where data is used to communicate with the person, the notice is due "at the latest at the time of the first communication to that data subject". The ICO summarises the general limit as "no later than one month from the date of collection" (https://ico.org.uk/for-organisations/direct-marketing-and-privacy-and-electronic-communications/business-to-business-marketing/, checked 2026-11-13).
  - Art. 14(5) exceptions (person already has the information, impossible or "disproportionate effort", required by law, professional secrecy) do not fit cold prospecting (my reading).
- **Right to object, Art. 21:** https://www.legislation.gov.uk/eur/2016/679/article/21/adopted
  - 21(2): right to object to direct marketing "at any time".
  - 21(3): after an objection "the personal data shall no longer be processed for such purposes".
  - 21(4): must be brought to the person's attention at the latest at the first communication, "clearly and separately from any other information".
- **Fines, Art. 83(5):** up to "20 000 000 EUR, or in the case of an undertaking, up to 4 % of the total worldwide annual turnover ... whichever is higher", covering Arts. 5, 6, 7, 9 and the rights in Arts. 12 to 22 (which includes Art. 14 and Art. 21). https://www.legislation.gov.uk/eur/2016/679/article/83/adopted

---

## 3. Germany

**1. Allowed without consent?** No. Opt-in, with no B2B carve-out for email.

**2. Law.** UWG §7(2) Nr. 2: an unreasonable nuisance is "stets anzunehmen" for "Werbung unter Verwendung ... elektronischer Post, ohne dass eine vorherige ausdrückliche Einwilligung des Adressaten vorliegt". The text says "Adressat", not "Verbraucher", so it covers business recipients. https://www.gesetze-im-internet.de/uwg_2004/__7.html [law], checked 2026-11-13.
- Contrast with phone (§7(2) Nr. 1): calls to a "sonstigen Marktteilnehmer" need only "zumindest mutmaßliche Einwilligung" (presumed consent). Same source. This is the only verified non-consent electronic-ish channel in DE (phone is outside this brief's scope beyond that note).
- Soft opt-in (§7(3)) requires the address to have been obtained "im Zusammenhang mit dem Verkauf einer Ware oder Dienstleistung". Not usable for prospects. Same source.
- GDPR applies on top (section 2.2).

**3. Mandatory content.** §7(2) Nr. 3: any advertising message is a nuisance if the sender identity is "verschleiert oder verheimlicht", if it breaches §6(1) Digitale-Dienste-Gesetz, or if there is no "gültige Adresse" for an opt-out request at basic transmission cost. Same source. Plus GDPR Art. 14 and Art. 21(4) notice.

**4. Public bodies.** No rule specific to contacting public bodies or civil servants was found. Whether a public authority is an "Adressat" under §7 is presumably yes (the text draws no distinction), but this is **unknown** and flagged (Q8).

**5. LinkedIn.** Courts treat it as e-mail [secondary only]:
- OLG Hamm, 3 May 2023, 18 U 154/22: "elektronische Post" includes messages via Xing, Facebook, LinkedIn, WhatsApp, relying on CJEU C-102/20 (https://www.it-recht-kanzlei.de/olg-hamm-werbenachrichten-internetportale-social-media-einwilligung-erforderlich.html [secondary], checked 2026-11-13).
- AG Düsseldorf, 20 November 2025, 23 C 120/25: a LinkedIn connection is not consent to e-mail advertising; reports differ on how firmly the court said this (https://www.datenschutz-notizen.de/unzulaessige-e-mail-werbung-trotz-indirektem-linkedin-kontakt-0158435/ and https://www.ferner-alsdorf.de/linkedin-kontakte-kein-einfallstor-fuer-unerwuenschte-werbung/ [secondary], checked 2026-11-13).
- Not checked: whether a bare connection request with no advertising content is "Werbung". **Unknown**.

**6. Enforcement.** UWG §20 fines cover phone calls and automatic calling machines to consumers only (up to "dreihunderttausend Euro"); **email is not listed**. https://www.gesetze-im-internet.de/uwg_2004/__20.html [law], checked 2026-11-13. Email breaches are enforced civilly (competitors, associations, recipients); civil damages or warning-letter costs: **unknown** (no primary source read). GDPR fines per Art. 83(5) (section 2.2). DSK guidance (Orientierungshilfe Direktwerbung, Feb 2022) was downloaded but could not be read: **not checked**.

---

## 4. Austria

**1. Allowed without consent?** No. Opt-in, and the law covers legal persons.

**2. Law.** TKG 2021 §174(3): sending electronic mail, including SMS, "ist ohne vorherige Einwilligung des Empfängers unzulässig, wenn die Zusendung zu Zwecken der Direktwerbung erfolgt". https://www.ris.bka.gv.at/NormDokument.wxe?Abfrage=Bundesnormen&Gesetzesnummer=20011678&Paragraf=174 [law], checked 2026-11-13.
- §174(4) exception: only for contact details obtained in a sale or service to customers, own similar products, opt-out offered, and the recipient not on the ECG list (§7(2) E-Commerce-Gesetz). Not usable for prospects. Same source.
- §174(1): advertising calls also need prior consent. Same source. The TKG defines "Nutzer" as "eine natürliche oder juristische Person" (§4 Z 13, https://www.ris.bka.gv.at/NormDokument.wxe?Abfrage=Bundesnormen&Gesetzesnummer=20011678&Paragraf=4 [law], checked 2026-11-13). So unlike Germany, B2B cold calling in Austria is also consent-only.
- §174(6): offences committed abroad count as committed where the message reaches the user's connection. Same source. Being based in Zug does not take Hypergate outside §174.
- GDPR applies on top (section 2.2).

**3. Mandatory content.** §174(5): always unlawful if the sender identity is concealed or disguised, §6(1) E-Commerce-Gesetz is breached, recipients are sent to sites breaching it, or there is no authentic address for an opt-out request. Same source. Plus GDPR Art. 14 and 21(4).

**4. Public bodies.** No specific rule found. **Unknown** (Q8).

**5. LinkedIn.** Not researched for Austria; the TKG page did not define "elektronische Post". **Unknown.** Given CJEU C-102/20 (section 2.1), treat like Germany until legal says otherwise.

**6. Enforcement.** TKG 2021 §188(4) Z 28: sending electronic mail contrary to §174(3) or (5) is an administrative offence with a fine of up to **€50,000**; §188(6) Z 9: advertising calls contrary to §174(1), up to **€100,000**. https://www.ris.bka.gv.at/NormDokument.wxe?Abfrage=Bundesnormen&Gesetzesnummer=20011678&Paragraf=188 [law], checked 2026-11-13. Plus GDPR Art. 83.

---

## 5. Switzerland

**1. Allowed without consent?** Yes with conditions, but only if the outreach is not "Massenwerbung". Legal must confirm (Q4).

**2. Law.**
- UWG Art. 3(1) lit. o: unfair if a person "Massenwerbung ohne direkten Zusammenhang mit einem angeforderten Inhalt fernmeldetechnisch sendet ... und es dabei unterlässt, vorher die Einwilligung der Kunden einzuholen, den korrekten Absender anzugeben oder auf eine problemlose und kostenlose Ablehnungsmöglichkeit hinzuweisen". Customer exception for own similar products. SR 241, version of 1 January 2025: https://fedlex.data.admin.ch/filestore/fedlex.data.admin.ch/eli/cc/1988/223_223_223/20250101/de/html/fedlex-data-admin-ch-eli-cc-1988-223_223_223-20250101-de-html-5.html [law], checked 2026-11-13. (Landing page: https://www.fedlex.admin.ch/eli/cc/1988/223_223_223/de.)
- The law does not define "Massenwerbung". Whether individually researched one-to-one emails fall outside it is **unknown**; no SECO guidance on this was found [snippet search only]. A law-firm summary restates the rule without resolving the point (https://www.weka.ch/themen/datenschutz-und-it-recht/datenschutz-umsetzen/article/datenschutz-newsletter-rechtssicheres-e-mail-marketing-in-der-schweiz/ [secondary], checked 2026-11-13). A Clay-to-sequencer pipeline that sends templated emails to many contacts could well be read as mass advertising (my reading).
- revFADP (DSG, SR 235.1, version of 7 July 2025): https://fedlex.data.admin.ch/filestore/fedlex.data.admin.ch/eli/cc/2022/491/20250707/de/html/fedlex-data-admin-ch-eli-cc-2022-491-20250707-de-html-1.html [law], checked 2026-11-13.
  - Art. 3: applies to situations "die sich in der Schweiz auswirken, auch wenn sie im Ausland veranlasst werden".
  - Art. 30(3): as a rule no infringement of personality if the person made the data "allgemein zugänglich" and did not expressly prohibit processing. Art. 30(2)(b): infringement if processed "entgegen der ausdrücklichen Willenserklärung" (i.e. after an objection).
  - Art. 31: an infringement is unlawful unless justified by consent, overriding private or public interest, or law.
  - There is no "lawful basis" requirement like GDPR Art. 6; Swiss law works on principles plus justification.

**3. Mandatory content.**
- UWG lit. o: prior consent (for mass advertising), "korrekten Absender", free and easy opt-out notice.
- revFADP Art. 19: inform the person of controller identity and contact details, purpose, recipients, and (if not collected from them) the categories of data; foreign disclosures and safeguards. If data is not collected from the person, at the latest **one month** after receiving it. Art. 20(2): exception where informing is impossible or requires disproportionate effort. Same source.

**4. Public bodies.** No specific rule found for contacting cantonal or federal staff. **Unknown** (Q8). (Hypergate's named Swiss public customers, CU §2, are suppressed anyway in step 2.)

**5. LinkedIn.** Whether a LinkedIn message is sent "fernmeldetechnisch" under lit. o: **unknown**, not researched.

**6. Enforcement.**
- UWG Art. 23: intentional unfair competition under Art. 3 is punished, on complaint, with "Freiheitsstrafe bis zu drei Jahren oder Geldstrafe". The Confederation may act as private plaintiff. Same UWG source.
- revFADP Art. 60(1): private persons who intentionally fail to inform under Art. 19(1) or give the Art. 19(2) information are fined, on complaint, up to **CHF 250,000**. Same DSG source. Note: Swiss fines target the responsible individual, not the company (general Swiss criminal-law point, not verified here).
- EDÖB/FDPIC guidance on B2B email: **not checked**.

---

## 6. France

**1. Allowed without consent?** Yes with conditions. Opt-out for professionals.

**2. Law.**
- CPCE Art. L34-5 (in force since 26 July 2020): bans direct marketing by email "utilisant ... les coordonnées d'une personne physique" who has not given prior consent; consent must be free, specific and informed. https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000042155961 [law], checked 2026-11-13.
- CNIL reads this as an opt-in for consumers and an opt-out for professionals: B2B prospecting can rely on legitimate interest "lorsque l'objet de la sollicitation est en rapport avec la profession de la personne démarchée"; the CNIL's own example is a software pitch to an IT director. The regime is "le droit d'opposition (pour le B to B)". https://cnil.fr/fr/node/892 and https://www.cnil.fr/fr/la-prospection-commerciale-par-courrier-electronique [regulator], checked 2026-11-13.
- Generic addresses of legal persons (info@, contact@) are outside these principles (same CNIL pages).

**3. Mandatory content.**
- L34-5: valid contact details to object free of charge, and "il est interdit de dissimuler l'identité de la personne" for whom the message is sent. Same Légifrance source.
- CNIL: every message must let the recipient learn "l'identité de l'organisation qui l'émet" and refuse further messages "par un moyen simple" and free. Where data was obtained from third parties, "il faut s'assurer que la personne concernée a été informée de la possible utilisation de son adresse électronique" and of the right to object. Same CNIL sources.
- GDPR Art. 14 and Art. 21(4) (section 2.2).

**4. Public bodies.** No specific rule found. **Unknown** (Q8).

**5. LinkedIn.** Not mentioned in the CNIL pages read. **Unknown.**

**6. Enforcement.** L34-5 sets an administrative fine of up to **€75,000** for a natural person and **€375,000** for a legal person, imposed by the authority in charge of competition and consumer affairs (DGCCRF); CNIL oversees compliance and takes complaints. Same Légifrance source. **Caveat:** Légifrance reports that Conseil constitutionnel decision n° 2026-1210 QPC of 25 June 2026 declared the paragraphs on CNIL oversight, the administrative fine and the cross-authority cap unconstitutional, with repeal postponed to **31 October 2027**. The fine is therefore in force until then, and what replaces it is unknown. Plus GDPR Art. 83 fines via CNIL.

---

## 7. Italy

**1. Allowed without consent?** No. The Garante applies opt-in to named professionals, including leads found on LinkedIn.

**2. Law.** Codice privacy (D.Lgs. 196/2003) art. 130(1)-(2) plus GDPR Art. 6(1)(a).
- Garante decision of 17 April 2026, n. 285 (doc. web 10252188), against Aesir S.r.l., an ERP/IT consultancy: it emailed a lawyer at addresses inferred from LinkedIn Sales Navigator and enriched via Snov.io. The Garante held that such emails "non può essere fondato sul contratto o su legittimo interesse del titolare, ma unicamente sul consenso dell'interessato", rejected the "collaborazione professionale" framing, and said presumed consent from LinkedIn's privacy policy is "ontologicamente incompatibile" with consent. https://www.garanteprivacy.it/web/guest/home/docweb/-/docweb-display/docweb/10252188 [regulator], checked 2026-11-13. This is close to Hypergate's planned workflow (Clay Find People plus email waterfall).
- Garante 2013 guidelines on promotional activity and spam (doc. web 2542348): automated marketing is "consentito solo con il consenso preventivo del contraente o utente"; addresses from public registers or the web are not usable without consent; named business addresses such as "nome.cognome@società.com" are treated as personal data. https://www.garanteprivacy.it/home/docweb/-/docweb-display/docweb/2542348 [regulator], checked 2026-11-13.

**3. Mandatory content.** Moot for cold email (consent needed first). Any message also needs GDPR Art. 13/14 information and an effective opt-out (the Garante sanctioned an ineffective opt-out in doc. web 10143278, below).

**4. Public bodies.** No specific rule found. **Unknown** (Q8).

**5. LinkedIn.** The 2013 guidelines cover "social spam": private messages to users whose data comes from their social profile are unlawful "a meno che il mittente non dimostri di aver acquisito" prior, specific, free and documented consent; for contacts or "amici", "un consenso specifico per l'attività promozionale" is needed for each. Same doc. web 2542348. The 2026 Aesir decision also notes LinkedIn's terms do not provide for users messaging others "con lo scopo di vendere". Treat LinkedIn DMs with a pitch as consent-only in Italy.

**6. Enforcement.**
- Aesir (2026): reprimand for the emails; €1,000 fine for failing to answer an access request (GDPR Arts. 12, 15). Same source.
- Noi Compriamo Auto S.r.l., decision of 4 June 2025 (doc. web 10143278): €45,000 for marketing emails without valid consent (GDPR Art. 6(1)(a), art. 130(2) Codice) and related failures; the Garante stated this was 0.23% of the €20 million maximum. B2C case. https://www.garanteprivacy.it/home/docweb/-/docweb-display/print/10143278 [regulator], checked 2026-11-13.
- Maximum: GDPR Art. 83(5) (section 2.2).

---

## 8. Rest of the EU (incl. EU institutions)

**1 to 3.** Each Member State chose how to protect legal persons under ePrivacy Art. 13(5) (section 2.1), so the answer varies by country. **Not researched for any state other than DE, AT, FR, IT and (partly) BE: unknown, treat as No until checked.**

- **Belgium (relevant to EU institutions in Brussels):** Royal Decree of 4 April 2003, art. 1, reportedly exempts from consent advertising email to legal persons only "si les coordonnées électroniques qu'il utilise à cette fin sont impersonnelles" [secondary/snippet: https://www.actualitesdroitbelge.be/droit-des-affaires/droit-commercial/le-cadre-juridique-des-services-de-l-information-en-ligne/l-interdiction-de-principe-du-spamming], checked 2026-11-13. If correct, named addresses (firstname.lastname@) need consent. Official text not read.
- **Luxembourg** (other EU institution seat): **unknown**.
- GDPR (section 2.2) applies in every EU state.

**4. Public bodies / EU institutions.** No email rule specific to EU institution staff was found. Whether the EU Transparency Register or staff contact rules apply to sales outreach: **unknown, not researched** (Q9).

**5. LinkedIn.** Per country, **unknown**.

**6. Enforcement.** Per country, **unknown**; GDPR Art. 83 applies everywhere.

---

## 9. United Kingdom

**1. Allowed without consent?** Yes with conditions, for corporate subscribers.

**2. Law.**
- PECR reg. 22(1): applies to unsolicited marketing email "to individual subscribers". Reg. 22(2) requires prior consent; 22(3) soft opt-in. Version shown includes amendments in force from 5 February 2026 (Data (Use and Access) Act 2025, S.I. 2026/82). https://www.legislation.gov.uk/uksi/2003/2426/regulation/22 [law], checked 2026-11-13.
- ICO: "The PECR rule on direct marketing by electronic mail does not apply to corporate subscribers"; "some government bodies" are corporate subscribers; sole traders and some partnerships are "individual subscribers" and need consent. https://ico.org.uk/for-organisations/direct-marketing-and-privacy-and-electronic-communications/business-to-business-marketing/ [regulator], checked 2026-11-13.
- UK GDPR still applies to named employees' addresses; legitimate interests may be appropriate but "there is no absolute rule"; a three-part test is needed. Same ICO page.

**3. Mandatory content.**
- PECR reg. 23: no direct marketing email where the sender's identity is "disguised or concealed" or no "valid address to which the recipient of the communication may send a request" to stop is provided (plus e-commerce reg. 7 information). https://www.legislation.gov.uk/uksi/2003/2426/regulation/23 [law], checked 2026-11-13.
- ICO: offer an opt-out in every message; keep a "do not email" list for businesses that object (https://ico.org.uk/for-organisations/direct-marketing-and-privacy-and-electronic-communications/guide-to-pecr/electronic-and-telephone-marketing/electronic-mail-marketing/ [regulator], checked 2026-11-13).
- UK GDPR Art. 14 notice "no later than one month from the date of collection"; the right to object to direct marketing is "absolute". ICO B2B page.

**4. Public bodies.** Government bodies can be corporate subscribers (ICO B2B page). Police forces, councils, NHS bodies: whether each is a "corporate subscriber" is not stated beyond "some government bodies". **Unknown** for specific bodies (Q8).

**5. LinkedIn.** ICO: direct messages on social media count as electronic mail under PECR; on professional networks people "are unlikely to be on the sites exclusively in their business capacity", so UK GDPR and possibly PECR apply depending on context. ICO B2B page.

**6. Enforcement.**
- The ICO "What are PECR?" page still says "a fine of up to £500,000" and that guidance is under review for the DUAA (https://ico.org.uk/for-organisations/direct-marketing-and-privacy-and-electronic-communications/guide-to-pecr/what-are-pecr/ [regulator], checked 2026-11-13).
- The statute now points higher: DUAA 2025 Sch. 13 para. 18 applies DPA 2018 s.157(2) to the PEC Regulations, listing regs. 22 and 23 among the provisions that attract "the higher maximum amount" (https://www.legislation.gov.uk/ukpga/2025/18/schedule/13 [law], checked 2026-11-13). DPA 2018 s.157(5) defines that as **£17,500,000 or 4%** of an undertaking's worldwide annual turnover, whichever is higher (https://www.legislation.gov.uk/ukpga/2018/12/section/157 [law], checked 2026-11-13). The commencement date of Sch. 13 was not read on legislation.gov.uk; law firms report 5 February 2026 [secondary, e.g. https://www.kennedyslaw.com/en/thought-leadership/article/2026/the-data-use-and-access-act-2025-commencement-dates-and-planned-guidance-for-2026], checked 2026-11-13. Legal to confirm (Q12).

---

## 10. United States

**1. Allowed without consent?** Yes, opt-out.

**2. Law.** CAN-SPAM Act, 15 U.S.C. 7701 ff. FTC: "The law makes no exception for business-to-business email." https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business [regulator], checked 2026-11-13. "Commercial electronic mail message": primary purpose is "the commercial advertisement or promotion of a commercial product or service" (15 U.S.C. 7702(2)(A), https://www.law.cornell.edu/uscode/text/15/7702 [secondary: Cornell mirror of the statute; uscode.house.gov returned 404], checked 2026-11-13). State laws: **not researched**.

**3. Mandatory content** (FTC guide, same URL):
- Truthful header information identifying the initiator.
- Subject line that accurately reflects the content.
- Clear and conspicuous disclosure that the message is an advertisement (FTC guide; the affirmative-consent exception does not help cold outreach).
- "Your valid physical postal address."
- A clear opt-out; honour it "within 10 business days".

**4. Public bodies.** No email rule specific to federal, state or police staff was found. Government ethics, gift and procurement rules: **not researched** (Q9).

**5. LinkedIn.** CAN-SPAM's "electronic mail message" is a message sent to a unique electronic mail address (7702(6), Cornell mirror). Whether a LinkedIn DM qualifies: **unknown**, not researched.

**6. Enforcement.** "Each separate email in violation of the CAN-SPAM Act is subject to penalties of up to **$53,088**" (FTC guide, updated January 2024 per the page; the 2025 or 2026 inflation adjustment, if any, was not checked).

---

## 11. Canada

**1. Allowed without consent?** No, but implied consent can cover B2B in narrow cases. Opt-in (express or implied).

**2. Law.** CASL (S.C. 2010, c. 23).
- s.6(1): no commercial electronic message to an electronic address unless the recipient consented, "express or implied". https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-1.html [law], checked 2026-11-13. No general B2B exception in s.6(5) (same page).
- s.10(9)(b): consent is implied where the person has conspicuously published the address, has not published a statement that they do not wish to receive unsolicited commercial messages, and "the message is relevant to the person's business, role, functions or duties in a business or official capacity". s.10(9)(c): same for an address disclosed to the sender. https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-2.html [law], checked 2026-11-13.
- s.10(10): existing business relationship (purchase within two years, inquiry within six months). Same page.
- s.12(1): CASL applies if "a computer system located in Canada is used to send or access the electronic message". Same page. Sending from Switzerland does not take a Canadian recipient out of scope.

**3. Mandatory content.** s.6(2): identify the sender (and anyone on whose behalf it is sent), contact information enabling the recipient to "readily contact" the sender, and an unsubscribe mechanism per s.11(1); s.6(3): contact information valid for at least 60 days after sending. page-1 URL. The exact prescribed information is in the CRTC regulations: **not read**. The CRTC FAQ (https://crtc.gc.ca/eng/com500/faq500.htm) returned HTTP 403: **not checked**.

**4. Public bodies.** CASL's implied consent explicitly covers duties "in a business or official capacity" (s.10(9)(b)), so public servants are not excluded. **Lobbying:** the federal Lobbying Act s.5(1) requires consultant lobbyists to register when, for payment, they communicate with a public office holder about "the awarding of any contract by or on behalf of Her Majesty in right of Canada"; "public office holder" includes RCMP members and federal Crown employees, and s.4(1) excludes municipal officials acting in official capacity. https://laws-lois.justice.gc.ca/eng/acts/L-12.4/page-1.html [law], checked 2026-11-13. The in-house corporation rule (s.7) was not on the page read: **unknown** whether Hypergate staff selling to federal bodies must register (Q10). Provincial and municipal lobbyist registries (e.g. Ontario, relevant to police services like York Regional Police): **not researched**. York Regional Police is a customer and is suppressed in step 2.

**5. LinkedIn.** "Electronic address" includes "an instant messaging account" and "any similar account" (s.1(1), page-1 URL). LinkedIn messaging likely falls within "similar account" (my reading); legal to confirm (Q11).

**6. Enforcement.** s.20(4): administrative monetary penalty up to **$1,000,000** for an individual and **$10,000,000** for any other person, per violation. https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-3.html [law], checked 2026-11-13.

---

## 12. What this means for the Hypergate GTM system

These gates replace the "Compliance gate [open]" line in step 7 of [`gtm-system.md`](gtm-system.md) **once legal signs off**. Until then the existing rule stands: no sends. Proposed as a Clay column `outreach_regime`, set from the account country (one regime for all of Switzerland, whatever the language region).

### 12.1 Country routing (set before step 7 runs)

| `outreach_regime` | Countries | Step 7 (find + verify emails) | Step 8 email | Step 8 LinkedIn |
|---|---|---|---|---|
| `OPT_IN_ONLY` | DE, AT, IT, and every EU state not yet researched (incl. BE for named addresses) | **Do not run the email waterfall.** Finding an email you may not use is processing without a purpose (GDPR Art. 5 data minimisation, my reading). Keep name, title, LinkedIn URL only | **None** until the person opts in (form, event, webinar, reply to a non-promotional touch, partner introduction) | Connection request with **no note or a non-promotional note** (legal to confirm a bare request is not "Werbung", Q6). **No promotional DMs** unless the person started a conversation or asked. No InMail pitches |
| `OPT_OUT_GDPR` | FR | Run waterfall. Store `email_source` (provider name) and `collected_at` for the Art. 14 notice. Skip generic addresses (they are outside CNIL's rule but also unlikely to reach the persona) | Allowed if the route's angle relates to the person's job (all W1 to W7 routes target IT roles, so yes) | Connection request plus DM (no French rule found; apply the same content rules) |
| `OPT_OUT_UKGDPR` | UK | Run waterfall. **Exclude sole traders and partnerships** (company type from enrichment; if unknown, Hold). Store source and date | Allowed, with LIA on file | Allowed; ICO treats DMs as electronic mail, so same content rules (opt-out, identity) |
| `CH_INDIVIDUAL` | CH | Run waterfall. Store source and date; revFADP Art. 19 notice due within one month | Pending Q4. If legal says one-to-one emails are not "Massenwerbung": low daily volume, written per contact (not a pure template), correct sender, opt-out. If legal says they are: treat as `OPT_IN_ONLY` | Allowed pending Q4 |
| `OPT_OUT_CANSPAM` | US | Run waterfall | Allowed with CAN-SPAM footer | Allowed (CAN-SPAM scope for DMs unknown; apply the same opt-out handling) |
| `CASL_IMPLIED` | CA | **Only addresses that pass the conspicuous-publication test.** Pattern-guessed or provider-inferred emails do **not** qualify. Required fields: `published_url` (where the address appears), `published_checked_at`, `no_unsolicited_statement = true`. If missing, LinkedIn-only | Allowed only for rows with publication evidence | Connection request; DMs treated as CASL messages (Q11), so same identity and unsubscribe content |

### 12.2 Step 7 gates (add after "Email found?")

1. **G7-C1 Regime gate.** Read `outreach_regime`. `OPT_IN_ONLY` → skip the waterfall and route to the LinkedIn opt-in track. No exceptions without written legal approval.
2. **G7-C2 Provenance.** Every email row stores `email_source` and `collected_at`. No source → no send (GDPR Art. 14(2)(f) requires telling the person the source).
3. **G7-C3 Notice clock.** If `today - collected_at > 30 days` and no notice has been sent, either send the notice now or delete the email (Art. 14(3) one month; revFADP Art. 19(5) one month). Simplest: do not enrich more than 30 days before the first send.
4. **G7-C4 Subscriber type (UK).** Sole trader or partnership, or unknown → Hold.
5. **G7-C5 Canada evidence.** No `published_url` → LinkedIn-only.
6. **G7-C6 Public sector.** Public-sector domain flag (already in step 7) now leads to: suppress if the account has an open tender Hypergate might bid on (Q9); Canada federal bodies → lobbying check (Q10); EU institutions → `OPT_IN_ONLY` (Belgian rule, pending Q7).
7. **G7-C7 Global objection list.** Before any send, check one suppression list that holds every objection from any channel (email reply, unsubscribe link, LinkedIn message, phone). GDPR Art. 21(3) and revFADP Art. 30(2)(b) make an objection binding for all direct marketing, not one sequence.
8. **G7-C8 Sender entity set.** The sending entity name and postal address are a fixed config value approved by legal (Papers AG vs Papers Group AG is open, CLAUDE.md), and the same entity is named in the privacy notice.

### 12.3 Step 8 gates (add to the sequence rules)

1. **Footer on every email (all regimes):** legal entity name, postal address (required in the US; also covers CASL contact information), a working reply address, a one-click unsubscribe link, and a link to the prospecting privacy notice.
2. **First email, EU/UK/CH:** a short notice in the body, kept separate from the pitch (Art. 21(4) "clearly and separately"), e.g. "We found your work address via [source]. Privacy notice: [link]. To object to further emails, reply 'no' or click [link]." Exact wording: Q13.
3. **Prospecting privacy notice page** (new; the current one does not cover this): Art. 14(1)-(2) items (identity, representative if any, purposes, legitimate interest, categories, recipients incl. Clay and the sequencer, transfers, retention, rights, right to complain, data source), plus revFADP Art. 19 items. Does not exist today.
4. **US:** the first email must disclose that it is an advertisement (FTC guide). Subject lines must match the body. Honour opt-outs within 10 business days (do it immediately in practice).
5. **No identity masking:** sending domains and display names must name Hypergate or Papers AG. Lookalike or unbranded "cold domains" that hide the sender would breach UWG §7(2) Nr. 3, TKG §174(5), L34-5, PECR reg. 23, ePrivacy Art. 13(4) and CAN-SPAM header rules. Legal to confirm whether a secondary domain that clearly names Hypergate is acceptable (Q14).
6. **LinkedIn:** manual only. LinkedIn's User Agreement s.8.2 bans "bots or other unauthorized automated methods" to add contacts or send messages and tools that "scrape or copy" profiles (https://www.linkedin.com/legal/user-agreement, checked 2026-11-13). This affects the [open] LinkedIn tool choice in gtm-system.md step 8. Note also that the Italian Garante cited these terms against a LinkedIn-sourced campaign.
7. **Day 2 connection request** stays "no pitch" in every country (already in the skeleton). **Day 7 DM** is removed for `OPT_IN_ONLY` unless the contact has replied or engaged.
8. **Reply handling (step 9):** "Unsubscribe / angry" and any objection on any channel go to the global list within one business day.

### 12.4 Net effect on the plan

- **Email is available in FR, UK, US, CA (narrowly) and possibly CH.** The core DACH market (DE, AT) and IT are not cold-email markets.
- For DE/AT/IT, the W1 (Acronis EOL) and W2 (NTLM) urgency angles need an opt-in vehicle: e.g. a short migration guide or webinar promoted through LinkedIn posts, partners (CO §7) and the newsletter, with a form that captures consent. In Germany, B2B phone calls with presumed consent (UWG §7(2) Nr. 1) are a legal option worth asking about (Q5); in Austria they are not.
- Partner routing (step 5 Part C) matters more: a partner with an existing customer relationship may have its own lawful basis that Hypergate does not.

---

## 13. Questions for legal

1. **Sender entity.** Which entity sends and is the controller: Papers AG or Papers Group AG? The current privacy policy also names "Papers GmbH" once (https://hypergate.com/privacy-policy/).
2. **Privacy notice.** Will legal approve a separate prospecting privacy notice covering GDPR Art. 14 and revFADP Art. 19, and what must it say about Clay, enrichment providers and the sequencer as recipients and about transfers?
3. **GDPR Art. 3(2) and Art. 27.** Does B2B prospecting of EU-based employees bring Papers AG under GDPR Art. 3(2)(a), and if so must it appoint an EU representative (the "occasional" exemption looks unlikely to fit)?
4. **Switzerland, "Massenwerbung".** Does UWG Art. 3(1) lit. o cover individually researched but templated sequences sent from a sequencer? Is there SECO or court guidance on volume or personalisation thresholds? Does lit. o cover LinkedIn messages?
5. **Germany, phone.** Can the champion persona be called under UWG §7(2) Nr. 1 ("zumindest mutmaßliche Einwilligung") when a public signal (e.g. an Acronis Files job post) shows a concrete need? What documentation is needed?
6. **LinkedIn connection requests.** In DE, AT and IT, is a connection request with no note (or a neutral note) "Werbung" / direct marketing? Is a DM sent after acceptance, with no prior conversation, still unsolicited advertising (AG Düsseldorf 23 C 120/25 suggests yes)?
7. **Rest of the EU.** Which other Member States allow B2B email to named work addresses without consent? At minimum: Belgium (confirm the 2003 Royal Decree, art. 1, "impersonnelles"), Luxembourg, Netherlands, Nordics, Spain. Which do we prioritise given the ICP?
8. **Public bodies as recipients.** In DE, AT, CH, FR and the UK, are ministries, police forces, state chancelleries and municipal utilities treated as businesses/"Adressaten"/corporate subscribers for these rules? Any rule restricting unsolicited commercial contact with civil servants?
9. **Procurement and ethics.** Must outreach stop when the target body has an open tender in our category (quiet periods under EU, Swiss, UK, US or Canadian procurement rules)? Any gift or hospitality limits that affect offers such as free trials or event invitations? Does contacting EU institution staff require EU Transparency Register registration?
10. **Canada lobbying.** Do Hypergate employees contacting federal bodies (e.g. RCMP) about a sale need to register as in-house lobbyists under Lobbying Act s.7? Do Ontario provincial or municipal lobbyist registries apply to police services boards?
11. **CASL and LinkedIn.** Is a LinkedIn message a commercial electronic message to an "electronic address" ("any similar account")? Does a LinkedIn profile that shows an email count as conspicuous publication under s.10(9)(b)?
12. **UK penalties.** Confirm the commencement date of DUAA 2025 Sch. 13 and that PECR regs. 22 and 23 now carry the DPA 2018 s.157 "higher maximum amount" (£17.5m or 4%).
13. **Wording.** Approve the opt-out sentence, the Art. 21(4) objection notice and the US advertisement disclosure, in EN, DE, FR and IT.
14. **Sending domains.** Is a secondary sending domain acceptable if the display name, signature and footer clearly identify Hypergate / Papers AG?
15. **Legitimate-interest assessment.** Will legal write or approve the LIA for FR and UK (and any other opt-out country), including the data sources used (Clay Find People, email waterfall, LeadMagic, BounceBan)?
16. **Italy.** Given Garante decision 10252188 (2026), confirm there is no route for cold email or cold LinkedIn DMs to Italian professionals, including at legal-person or PEC addresses.
17. **France.** After Conseil constitutionnel decision 2026-1210 QPC, which authority and fine apply to L34-5 breaches after 31 October 2027?
18. **Retention.** How long may we keep prospect data for contacts who never replied, and for objectors (we must keep a minimal record to honour the objection)?

---

## 14. Could not verify (flagged)

- EUR-Lex texts (ePrivacy Directive, GDPR) read only via legislation.gov.uk copies; GDPR Art. 6(1)(f) and Recital 47 wording not read.
- DSK Orientierungshilfe Direktwerbung (Germany): PDF downloaded but not readable in this session.
- CRTC FAQ and CASL regulations (prescribed sender information): HTTP 403 / not read.
- CJEU C-102/20 and C-654/23: summaries only; C-654/23 holding unknown.
- German and Austrian rules on LinkedIn: German case law from law-firm blogs only; Austria unknown.
- Belgian Royal Decree of 4 April 2003: secondary only. All other EU Member States: unknown.
- Swiss meaning of "Massenwerbung" and any EDÖB/SECO guidance: unknown.
- Public-body-specific rules, procurement quiet periods, gift rules, EU Transparency Register, provincial and municipal lobbying registries: unknown.
- US state anti-spam laws and the current CAN-SPAM inflation-adjusted penalty after January 2024: not checked.
- DUAA 2025 Sch. 13 commencement date: secondary only.
- German civil damages for spam: no figure from a primary source.
