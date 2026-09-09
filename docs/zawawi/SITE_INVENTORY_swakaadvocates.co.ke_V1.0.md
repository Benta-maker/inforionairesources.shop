# SITE INVENTORY — swakaadvocates.co.ke
**Version:** 1.0 · **Inspection date-stamp:** Friday 4 September 2026, approx. 08:40–08:50 UTC
**Status:** Findings only. Descriptive baseline. No recommendations.

---

## 0. PRELIMINARY: ACCESS CONDITIONS AND THEIR EFFECT ON THIS INVENTORY

Two access constraints shaped what could be observed. Both are stated here once, and every item below is graded against them.

**0.1 Repository mapping — repository NOT ACCESSIBLE**
- URL supplied: `https://github.com/Benta-maker/swaka-advocates-website/tree/main`
- Observed 4 Sep 2026 via unauthenticated HTTPS from the inspection environment:
  - `https://github.com/Benta-maker/swaka-advocates-website` → HTTP **404**
  - `https://codeload.github.com/Benta-maker/swaka-advocates-website/zip/refs/heads/main` → HTTP **404**
  - `https://raw.githubusercontent.com/Benta-maker/swaka-advocates-website/main/README.md` → HTTP **404**
  - `git clone` (anonymous) → authentication prompt, i.e. GitHub treats the repository as non-public or non-existent.
  - Alternative casings tried (`Swaka-Advocates-Website`, `swakaadvocates`) → 404.
- Observed: the public profile `https://github.com/Benta-maker` returns 200 and lists **3 repositories**: `infoonairesources-site`, `inforionairesources.shop` (spelled with "inforion", as displayed), `telegram-transcriber`. No repository name containing "swaka" is publicly listed.
- GitHub API (`api.github.com`) was rate-limited for unauthenticated calls from this environment's shared IP, so API-side confirmation was not available.
- **Grade: NOT DETERMINABLE FROM HERE.** Inference stated: the repository most likely exists and is **private** (GitHub returns 404 rather than 403 for private repositories to unauthenticated clients). What would determine it: an authenticated GitHub session (Benta's own login, or Claude Code with the GitHub connection), or the repository being made public.
- **Consequence:** Section 7 (Repo Health) and every "repo file (path)" observation method in Sections 1–6 are absent. This inventory proceeds on **live fetches alone**, as the mission instructs when no repository matches.

**0.2 Live-fetch instrument limits**
- Live pages were retrieved with a content-fetch tool that returns the **served HTML converted to text plus a subset of `<head>` metadata** (title, canonical, meta name/property tags). It does **not** expose raw HTML source, HTTP response headers, TLS certificate details, or status codes for arbitrary paths.
- The fetch tool only accepts URLs that have already appeared in a prior fetch or search result. `robots.txt`, `sitemap.xml`, `llms.txt`, `/.well-known/*`, feed URLs and deliberate-404 test paths are not linked from any page and did not surface in web search, so they **could not be requested**.
- Direct HTTP from the shell sandbox to `swakaadvocates.co.ke` is blocked by the environment's egress policy (`x-deny-reason: host_not_allowed`). **DNS resolution from the sandbox does work** and was used for Section 1.
- Consequence: anything requiring raw source (JSON-LD blocks, heading tags as tags, `alt` attributes as attributes, ARIA, landmarks, CSS, form markup, `<html lang>`), response headers, or unlinked root files is graded **NOT DETERMINABLE FROM HERE — instrument limit**, and the checklist in Section 9(a) names the exact fetch that resolves each one. These are *not* owner-supplied facts; a single unrestricted `curl` session (e.g. from Claude Code, or any machine with a browser) resolves all of them.

**Pages actually fetched (HTTPS, 4 Sep 2026):**
1. `https://swakaadvocates.co.ke/` (final URL `https://swakaadvocates.co.ke`) — 200-equivalent, full content returned
2. `https://swakaadvocates.co.ke/publications` — 200-equivalent, full content returned
3. `https://swakaadvocates.substack.com` — external, fetched only to check the outbound link target

---

## 1. STACK & DELIVERY

| # | Item | Finding | Method | Grade |
|---|------|---------|--------|-------|
| 1.1 | Framework / CMS / version | Not identifiable from rendered text. No generator meta tag appeared in the extracted `<head>` metadata of either page (the extractor did surface other meta tags, so a `<meta name="generator">` would likely have appeared if present). No CMS-style URL patterns (`/wp-content/`, `?p=`, `/node/`) observed in any link on either page. | Live fetch `/`, `/publications` | **INFERRED (absent generator tag)** for "no generator meta"; **NOT DETERMINABLE FROM HERE** for framework/version — needs raw source (script/asset paths, comments) or repository. |
| 1.2 | Static vs server-rendered vs client-rendered | All substantive content of both pages (hero, seven practice areas, thesis, timeline, client segments, contact block, six publication entries, footer) was present in the HTML **as served to a non-JavaScript fetcher**. Nothing in the inventory below exists only after JavaScript. Whether the HTML is a static file or server-rendered on request is not distinguishable from the served output. | Live fetch `/`, `/publications` | **OBSERVED** (content present without JS); static-vs-SSR distinction **NOT DETERMINABLE FROM HERE** (needs headers/repo). |
| 1.3 | DNS — apex A records | `104.21.48.16`, `172.67.176.1` | DNS resolution from sandbox, 4 Sep 2026 ~08:42 UTC | **OBSERVED** |
| 1.4 | DNS — apex AAAA records | `2606:4700:3031::ac43:b001`, `2606:4700:3035::6815:3010` | DNS | **OBSERVED** |
| 1.5 | DNS — name servers | `lorna.ns.cloudflare.com`, `terin.ns.cloudflare.com` | DNS (NS) | **OBSERVED** |
| 1.6 | DNS — MX | `10 mx.zoho.com`, `20 mx2.zoho.com`, `50 mx3.zoho.com` | DNS (MX) | **OBSERVED** — mail is hosted at Zoho. |
| 1.7 | DNS — TXT | `google-site-verification=WzTrnx_mNJwZ8WeBrs0l3pNV7T5IqG33drRaFn_31s0`; `zoho-verification=zb69655812.zmverify.zoho.com` | DNS (TXT) | **OBSERVED** — a Google Search Console (or other Google property) verification exists at domain level; no SPF/DMARC TXT record was returned at the apex (DMARC lives at `_dmarc.` and was not queried). |
| 1.8 | DNS — CNAME at apex | None (NoAnswer) | DNS | **OBSERVED** |
| 1.9 | Is the site behind Cloudflare? | Name servers are Cloudflare's, and the A/AAAA records are in Cloudflare-announced address space (`104.21.0.0/16`, `172.67.0.0/16`, `2606:4700::/32`), which is the signature of **Cloudflare proxy ("orange cloud") mode** rather than DNS-only. A DNS-only record would expose the origin host's own IP. | DNS + IP-range knowledge | **INFERRED** (strong). The dashboard toggle itself, plan tier, and origin host are **NOT DETERMINABLE FROM HERE** — Cloudflare dashboard. Response headers (`server: cloudflare`, `cf-ray`) would corroborate but could not be read (instrument limit). |
| 1.10 | Origin host / server software | Not observable — proxy masks origin IP; headers not readable. | — | **NOT DETERMINABLE FROM HERE** — Cloudflare dashboard (DNS origin record) or hosting control panel. |
| 1.11 | Response headers (server, x-powered-by, cache, security headers, X-Robots-Tag) | Not readable by the fetch tool. | — | **NOT DETERMINABLE FROM HERE** — instrument limit; one `curl -I` resolves. |
| 1.12 | TLS state | HTTPS fetches of both pages succeeded without certificate error, so a valid, trusted certificate is being served for the apex. Issuer, expiry, and TLS version not observable. | Live fetch (HTTPS success) | **OBSERVED** (valid cert present); details **NOT DETERMINABLE FROM HERE** — `openssl s_client` or browser padlock. |
| 1.13 | www vs apex | `www.swakaadvocates.co.ke` returns **NXDOMAIN** for both A and CNAME. The `www` hostname does not exist in DNS; any user typing `www.` gets a resolution failure, not a redirect. Canonical tags on both pages point to the **apex** (`https://swakaadvocates.co.ke/`). | DNS + live fetch (canonical) | **OBSERVED** |
| 1.14 | http→https redirect | Could not test (fetch tool used HTTPS; sandbox HTTP blocked). | — | **NOT DETERMINABLE FROM HERE** — `curl -I http://swakaadvocates.co.ke/`. |
| 1.15 | Trailing-slash / URL normalisation | `https://swakaadvocates.co.ke/` resolved to final URL `https://swakaadvocates.co.ke` (slash dropped by the tool or the server — not distinguishable). `/publications` is served without trailing slash and without `.html` extension. | Live fetch | **OBSERVED** (extensionless URL); redirect behaviour **NOT DETERMINABLE FROM HERE**. |

---

## 2. CRAWL & AGENT POSTURE

| # | Item | Finding | Method | Grade |
|---|------|---------|--------|-------|
| 2.1 | `robots.txt` full contents | **Could not be fetched** (see 0.2). Presence, absence, and contents are all unknown. Consequently, the allow/block status of GPTBot, OAI-SearchBot, ChatGPT-User, ClaudeBot, Claude-SearchBot, Claude-User, Google-Extended, PerplexityBot, Bytespider, CCBot, and any other named crawler is **unknown**. Note: Cloudflare's managed robots.txt feature, if enabled in the dashboard, injects directives at the edge that would not exist in any repository file; the served file is the only authority. | — | **NOT DETERMINABLE FROM HERE** — `curl https://swakaadvocates.co.ke/robots.txt`. Highest-priority gap in this inventory. |
| 2.2 | `llms.txt` | Not fetchable; not linked from any page. | — | **NOT DETERMINABLE FROM HERE** — `curl https://swakaadvocates.co.ke/llms.txt`. |
| 2.3 | `sitemap.xml` (presence, validity, currency, referenced from robots.txt) | Not fetchable; not linked from any page; not surfaced in web search. | — | **NOT DETERMINABLE FROM HERE** — `curl https://swakaadvocates.co.ke/sitemap.xml` and read robots.txt `Sitemap:` line. |
| 2.4 | Meta robots per page | No `<meta name="robots">` appeared in the extracted head metadata of `/` or `/publications`. The same extractor **did** surface `meta-robots: noindex` on the Substack page, so the extractor reports this tag when present. | Live fetch, head metadata | **INFERRED — absent** on both pages (extractor evidence; raw source would make it OBSERVED). |
| 2.5 | `X-Robots-Tag` header | Not readable. | — | **NOT DETERMINABLE FROM HERE** — `curl -I`. |
| 2.6 | Bot-management / challenge behaviour | Two fetches with the fetch tool's own user-agent returned full page content with **no Cloudflare challenge page, no interstitial, no 403**. Behaviour toward specific AI crawler user-agents, and toward the sandbox's blocked direct requests, was not testable. | Live fetch ×2 | **OBSERVED** (no challenge for this one UA); per-UA behaviour **NOT DETERMINABLE FROM HERE** — Cloudflare dashboard (Bot Fight Mode / AI crawler settings / WAF rules) plus `curl -A "<bot UA>"` tests. |
| 2.7 | RSS / Atom feeds | No `<link rel="alternate" type="application/rss+xml">` surfaced in head metadata; no feed link in page body. The Publications page directs readers to Substack for distribution. Substack publications expose a feed at `<publication>/feed` by default — that would be an external feed, not one served by the site. | Live fetch | **INFERRED — absent** on-site; Substack feed **NOT DETERMINABLE FROM HERE** (not fetched). |
| 2.8 | `/.well-known/*` endpoints | Not fetchable. | — | **NOT DETERMINABLE FROM HERE** — `curl https://swakaadvocates.co.ke/.well-known/security.txt` etc. |
| 2.9 | Does the site serve ads? | No advertising units, sponsor blocks, affiliate links, or third-party ad-network text observed in the rendered content of either page. Script-loaded ad slots would not be visible to this instrument. | Live fetch `/`, `/publications` | **OBSERVED — none in rendered content**; script-injected ads **NOT DETERMINABLE FROM HERE** — raw source / browser network panel. |
| 2.10 | Outbound-link crawl posture | Substack destination page carries `meta-robots: noindex` on its landing page (Substack default for the subscribe landing). | Live fetch (external) | **OBSERVED** (external property). |

---

## 3. MACHINE-LEGIBLE LAYER

| # | Item | Finding | Method | Grade |
|---|------|---------|--------|-------|
| 3.1 | JSON-LD / microdata blocks (every block, quoted) | **Cannot be quoted** — `<script type="application/ld+json">` content is not returned by the text-extracting fetch tool, and microdata attributes (`itemscope`, `itemprop`) are stripped. Presence or absence of `LegalService`, `LocalBusiness`, `Attorney`, `Person`, `Organization`, `Article`, `BreadcrumbList` is therefore **unknown**. | — | **NOT DETERMINABLE FROM HERE** — `curl -s https://swakaadvocates.co.ke/ \| grep -A200 'ld+json'` (one command). Second-highest-priority gap. |
| 3.2 | Practice areas: marked up vs prose | Seven practice areas exist as visible prose (numbered I–VII in the hero strip and 01–07 in the Services section, each with a heading and paragraph). Whether any structured-data equivalent exists depends on 3.1. | Live fetch `/` | **OBSERVED** as prose; markup status **NOT DETERMINABLE FROM HERE**. |
| 3.3 | `<title>` | `/`: "Swaka Advocates \| AI-Era Legal Counsel · Nairobi, Kenya". `/publications`: "Publications — Swaka Advocates". | Live fetch | **OBSERVED** |
| 3.4 | `meta description` | `/`: 300-character description naming AI liability architecture, data sovereignty, cybersecurity law, cross-border transactions, AI-era criminal and family law, Nairobi, "Established 2016". `/publications`: "Original analysis on AI law, data sovereignty, and the East African legal frontier from Swaka Advocates." | Live fetch | **OBSERVED** |
| 3.5 | `meta keywords` | `/` only: "AI liability Kenya, data sovereignty lawyer Nairobi, Kenya AI Bill 2026, enterprise AI legal counsel East Africa, cross-border data partnership law, AI criminal law Kenya, cybersecurity law Kenya, Swaka Advocates, John Swaka advocate, Hurlingham Nairobi lawyer". Absent on `/publications`. | Live fetch | **OBSERVED** |
| 3.6 | Open Graph — `/` | `og:title` = "Swaka Advocates \| AI-Era Legal Counsel · Nairobi" (differs from `<title>`, which adds ", Kenya"); `og:description` populated (shorter than meta description); `og:type` = website; `og:url` = `https://swakaadvocates.co.ke/`. **No `og:image`. No `og:site_name`. No `og:locale`.** | Live fetch | **OBSERVED** |
| 3.7 | Open Graph — `/publications` | `og:title`, `og:description`, `og:type` = website, `og:url`, **`og:site_name` = "Swaka Advocates"** (present here, absent on homepage). **No `og:image`.** | Live fetch | **OBSERVED** — og:site_name inconsistency between pages. |
| 3.8 | Twitter/X card tags | None surfaced on either page (the extractor did surface `twitter:*` tags on Substack, so it reports them when present). | Live fetch | **INFERRED — absent.** |
| 3.9 | Canonical | `/` → `https://swakaadvocates.co.ke/`; `/publications` → `https://swakaadvocates.co.ke/publications`. Both self-referential, both apex, both HTTPS. | Live fetch | **OBSERVED** |
| 3.10 | hreflang | None surfaced. Single-language site. | Live fetch | **INFERRED — absent.** |
| 3.11 | `<html lang>` | Not returned by extractor. | — | **NOT DETERMINABLE FROM HERE** — raw source. |
| 3.12 | Viewport | `width=device-width, initial-scale=1.0` on both pages. | Live fetch | **OBSERVED** |
| 3.13 | Favicon / icon links | Not surfaced. | — | **NOT DETERMINABLE FROM HERE** — raw source or `/favicon.ico` fetch. |
| 3.14 | NAP — as it appears on the site | **Name:** "Swaka Advocates" (header, footer, title). **Address:** "Hurlingham Court, Woodlands Lane, off Argwings Kodhek Road, 1st Floor, Room 1 · Nairobi, Kenya" (homepage Contact section only). **Postal:** "P.O. Box 12803-00400, Nairobi" (homepage Contact section only). **Phone:** +254 703 308 873 and +254 721 476 685 (homepage Contact section, both as `tel:` links). **Email:** johnswaka@swakaadvocates.co.ke (header on both pages; Contact section). | Live fetch | **OBSERVED** |
| 3.15 | NAP consistency: markup vs footer vs contact page | There is **no separate contact page** (contact is a `#contact` section on the homepage). The **footer carries no address or phone** — only the firm name, copyright line, "Regulated by the Law Society of Kenya", and "East Africa Law Society Member". The Publications page carries only the email. Markup-side NAP depends on 3.1. So: one NAP instance in visible text, in one location, on one page; no second instance to be inconsistent with. | Live fetch `/`, `/publications` | **OBSERVED** (single visible instance); markup comparison **NOT DETERMINABLE FROM HERE**. |
| 3.16 | Named individuals in machine-readable text | "John Swaka" appears in: meta keywords ("John Swaka advocate"), the email local part, and the Publications page sentence "John Swaka publishes shorter observations…". Nowhere on either page is a full-name-plus-role statement such as "John Swaka, Advocate of the High Court of Kenya / Managing Partner" rendered as a heading or profile. No other individual is named. | Live fetch | **OBSERVED** |

---

## 4. SEMANTIC & ACCESSIBILITY STRUCTURE (dual-eyes layer)

| # | Item | Finding | Method | Grade |
|---|------|---------|--------|-------|
| 4.1 | Heading hierarchy — `/` | **One h1:** "Law for the *AI* transition." (the word "AI" is emphasised — rendered as `<em>` or `<i>`). **h2 ×4:** "The legal frontier is not a technology question. It is a *power* question."; "Legal services for *consequential* matters."; "Decision-makers operating at *consequential scale.*"; "The right matter. The right *counsel.*" **h3 ×11:** seven practice-area titles (AI Liability Architecture; Data Sovereignty & Cross-Border Transactions; Cybersecurity Law; AI-Era Criminal Law; Geopolitical Transaction Counsel; AI-Era Family Law; High-Net-Worth Personal Architecture) and four client-segment titles. Levels are ordered (h1→h2→h3) with no skipped level observed. **Section labels rendered as plain text, not headings:** "Our Position", "Practice Areas", "The Current Moment", "Who We Serve", "Engagement", "Established Practice", "Phase 3." The four timeline entries (18 March 2026, February 2026, May 2026, "2026 — Active globally") are plain text, not headings. The seven hero-strip items (I–VII) are plain text, not headings. | Live fetch (heading markers in extracted text) | **OBSERVED** via extraction; exact tag names (`h2` vs styled `p`) would need raw source — graded OBSERVED because the extractor emits heading levels only from heading elements. |
| 4.2 | Heading hierarchy — `/publications` | **One h1:** "Published thinking on AI law, data sovereignty, and the East African legal frontier." **h2 ×8:** six publication titles + "Subscribe to receive analysis as it is published." + "Follow on LinkedIn". No h3. Labels "Analysis & Commentary", dates, and "Forthcoming" are plain text. | Live fetch | **OBSERVED** |
| 4.3 | Semantic HTML vs div-soup; landmarks (`header`, `nav`, `main`, `footer`, `section`) | Not observable — extractor strips container elements. Navigation renders as a list of links (consistent with `<ul>` inside `<nav>`, but not confirmable). | — | **NOT DETERMINABLE FROM HERE** — raw source. |
| 4.4 | ARIA usage | Not observable. | — | **NOT DETERMINABLE FROM HERE** — raw source. |
| 4.5 | Images — inventory | **Homepage:** one image, the header logo, alt text "Swaka Advocates", **with an empty `src`** in the extracted output (`![Swaka Advocates]()`). **Publications page:** one image, header logo, alt "Swaka Advocates", `src` = `https://swakaadvocates.co.ke/logo-dark.png`. No other `<img>` elements observed on either page. | Live fetch | **OBSERVED**. The empty homepage logo `src` is either (a) an inline SVG the extractor could not represent, (b) a lazy-load pattern (`data-src`), or (c) a genuinely missing source — **not distinguishable here**; raw source resolves. |
| 4.6 | Alt-text coverage | 2 of 2 observed images carry alt text (denominator: 2 images across 2 pages). | Live fetch | **OBSERVED** |
| 4.7 | Information existing ONLY inside images | **None observed.** Practice areas, advocate name, admission year, establishment year, address, phones, email, LSK/EALS statements, timeline facts, and publication titles all exist as text. Roman numerals I–VII and "01"–"07" are text. No credential badges, award graphics, map images, or scanned certificates observed. CSS `background-image` content is not observable and could carry text. | Live fetch | **OBSERVED** for `<img>`; CSS-background text **NOT DETERMINABLE FROM HERE**. |
| 4.8 | Text-contrast flags from CSS | CSS not retrievable. | — | **NOT DETERMINABLE FROM HERE** — stylesheet fetch or browser audit (Lighthouse/axe). |
| 4.9 | Keyboard operability (focus styles, tabindex, click-only handlers) | Not observable. All observed navigation is via `<a href>` links (fragment anchors and page links), which are natively keyboard-operable; no button-styled non-link controls surfaced in text. | Live fetch | **INFERRED** (anchor-based nav) ; full assessment **NOT DETERMINABLE FROM HERE**. |
| 4.10 | Contact / intake forms | **No form on either page.** Contact is via `mailto:` and `tel:` links only. There is nothing to label, no required fields, no submission endpoint. | Live fetch | **OBSERVED** |
| 4.11 | Dead / placeholder link | Publications page: "Follow John Swaka on LinkedIn →" links to **`#`** (no destination). | Live fetch | **OBSERVED** |
| 4.12 | In-page navigation | Homepage nav: Practice (`#thesis`), Services (`#services`), Clients (`#clients`), Contact (`#contact`), Publications (`/publications`). Publications-page nav: Practice, Services, Clients, **Publications, Contact** (order differs from homepage — Publications before Contact) and links back to homepage fragments. Two CTA links in hero: "Explore our practice →" (`#services`), "Get in touch" (`#contact`). | Live fetch | **OBSERVED** |
| 4.13 | Skip-to-content link | Not observed in extracted text. | Live fetch | **INFERRED — absent** (a visually-hidden skip link would normally appear in extraction). |

---

## 5. CONTENT INVENTORY

### 5.1 Page map (from nav crawl; sitemap unavailable)

| URL | `<title>` | h1 | One-line purpose |
|-----|-----------|----|------------------|
| `/` | Swaka Advocates \| AI-Era Legal Counsel · Nairobi, Kenya | Law for the AI transition. | Single-page firm site: positioning statement, seven practice areas, "current moment" timeline, four client segments, engagement statement, contact block. |
| `/publications` | Publications — Swaka Advocates | Published thinking on AI law, data sovereignty, and the East African legal frontier. | Index of one published and five forthcoming analyses; Substack and LinkedIn pointers. |

Only these two internal URLs are linked from the site. No About, Team, Contact, Privacy, Terms, individual practice-area, or individual article pages are linked. Whether additional unlinked pages exist (orphan pages, old pages returning 200 or 404) is **NOT DETERMINABLE FROM HERE** — `sitemap.xml` fetch, Search Console coverage report, or repository listing.

### 5.2 Core professional facts — where each exists and in what form

| Fact | Present? | Location | Machine-readable text? |
|------|----------|----------|------------------------|
| Practice areas | Yes — 7 | `/` hero strip and Services section | Yes (prose; h3 headings) |
| Advocate name | Partial | "John Swaka" in meta keywords, email address, one sentence on `/publications` | Yes, but never as a profile, heading, or name-plus-title statement |
| Advocate credentials (qualification, university, admission body) | Partial | "Admitted to the Bar 2006" in Contact block (which bar is not stated; no individual is attached to the statement) | Yes (text) |
| Admission / registration / practising-certificate details | No | — | — |
| LSK membership | Statement only | Footer: "Regulated by the Law Society of Kenya" | Yes (text); no member number |
| Other memberships | Statement only | Footer: "East Africa Law Society Member" | Yes (text) |
| Firm establishment year | Yes | Header strip "Est. 2016"; Contact block "Established 2016"; meta description | Yes |
| Physical location | Yes | Contact block (homepage) | Yes (text, unlinked — no map) |
| Postal address | Yes | Contact block | Yes |
| Office hours | **No** | — | — |
| Phone | Yes ×2 | Contact block | Yes, `tel:` links |
| Email | Yes | Header both pages; Contact block | Yes, `mailto:` link |
| Jurisdiction statement | Yes | Contact block: "Republic of Kenya · East Africa · International" | Yes |
| Other staff / associates | No | — | — |
| Fees / engagement terms | No (only "We engage selectively…") | Engagement section | Yes (prose) |

### 5.3 Languages
English only. No language switcher, no hreflang, no non-English content observed. `<html lang>` attribute not determinable (3.11).

### 5.4 Last-modified signals
- HTTP `Last-Modified` / `ETag`: **NOT DETERMINABLE FROM HERE** (headers).
- Visible date signals: Publications page entries dated "21 March 2026" (published) and "Coming April 2026" (×2), "Coming May 2026" (×2), "Coming June 2026" (×1), each labelled "Forthcoming". **All five "Coming" dates are in the past as of the inspection date (4 September 2026) while still labelled Forthcoming.** Homepage timeline references events dated 18 March 2026, February 2026, May 2026. Copyright line "© 2026". Substack landing page states "Launched 5 months ago" (≈ April 2026), which post-dates the 21 March 2026 item that the site says is on Substack. Whether that article exists on Substack could not be confirmed — the Substack landing page requires JavaScript to list posts.
- Grade for stale-label observation: **OBSERVED**. No inference is drawn about why.

### 5.5 Thin or placeholder pages
- `/publications`: 5 of 6 entries (denominator 6) are placeholders with no link; the one published entry links to the Substack **root**, not to the article. The LinkedIn link is `#`.
- No other thin pages observed (only two pages exist).

### 5.6 Blog / articles section state
No on-site article pages. Publications are hosted off-site (Substack). The on-site Publications page functions as an index/teaser page. Grade: **OBSERVED**.

---

## 6. HUMAN CONVERSION LAYER (reported, not judged)

| # | Item | Finding | Grade |
|---|------|---------|-------|
| 6.1 | Contact mechanisms | `mailto:johnswaka@swakaadvocates.co.ke` (header, both pages; Contact block). `tel:+254703308873`, `tel:+254721476685` (Contact block). No form. No WhatsApp link. No map embed. No booking/calendar mechanism. No live chat observed in rendered text (script-injected chat widgets not observable). | **OBSERVED** (rendered); script widgets **NOT DETERMINABLE FROM HERE**. |
| 6.2 | Advocate profiles | None. No team page, no headshots, no biography. | **OBSERVED — absent** |
| 6.3 | Credentials stated | "Admitted to the Bar 2006"; "Established 2016"; "Regulated by the Law Society of Kenya"; "East Africa Law Society Member". | **OBSERVED** |
| 6.4 | Testimonials / case results / client names | None. Client *categories* are described (banks, insurers, "Chinese technology firms, Gulf sovereign funds, American hyperscalers, European DFIs", development bodies, universities, founders). Matter types are described ("robbery, murder, sexual offences, and financial crime"; "financial institution disputes, constitutional petitions, commercial matters, immigration"). No named clients, no outcomes, no reviews. | **OBSERVED** |
| 6.5 | Privacy policy | None linked. | **OBSERVED — absent** |
| 6.6 | Terms of use | None linked. | **OBSERVED — absent** |
| 6.7 | Cookie notice / consent | None in rendered text. | **OBSERVED — absent** in rendered content; script-injected banner **NOT DETERMINABLE FROM HERE**. |
| 6.8 | External trust/authority pointers | Substack publication (linked, root only); LinkedIn (link target `#`). | **OBSERVED** |
| 6.9 | Advertising-style content present on the site (factual presence, for LSK-rule review by the advocate — no legal judgment here) | The following categories of statement are present as visible text: (a) comparative/superlative self-description — e.g. "produces something rare", "the practitioner who builds the framework before the urgency is obvious is the only one positioned to serve when it arrives", "for those who cannot afford to get it wrong"; (b) specialism/expertise claims — seven named practice areas each described as a discrete competence; "AI-Era" branding across service names; (c) market/urgency statements with figures — "$10 billion AI Initiative", "15,000 attendees and 100+ investors from 75 countries", "Over 70 AI copyright infringement suits", "The compliance window is open. It will close."; (d) client-targeting language naming categories of prospective client and their nationalities/sectors; (e) calls to action — "Explore our practice →", "Get in touch", "Subscribe on Substack"; (f) meta-keyword targeting phrases ("data sovereignty lawyer Nairobi", "Hurlingham Nairobi lawyer"). The site contains no fee information, no "no win no fee" or guarantee language, no client testimonials, and no comparison with named competitors. | **OBSERVED** (presence only) |

---

## 7. REPO HEALTH (from GitHub)

**Entire section NOT DETERMINABLE FROM HERE.** See 0.1. Items that an authenticated repository view would settle:

- Repository structure (single `index.html` + `publications.html`? framework project? build output committed?)
- Build/deploy mechanism (GitHub Pages, Cloudflare Pages, Netlify/Vercel, FTP to shared host, or manual upload) — this also settles Section 1.1/1.2.
- Content-editing model (hand-authored HTML, static-site generator, CMS export).
- Last commit date; commit count; contributors; branches; open PRs/issues.
- Whether `robots.txt`, `sitemap.xml`, `llms.txt`, `logo-dark.png`, and a homepage logo asset exist in the repository (cross-check for 2.1–2.3 and 4.5).
- Whether the repository contains pages not deployed, or whether the live site serves anything not in the repository (e.g. Cloudflare-injected robots.txt, Cloudflare Pages redirects/headers files).

What was observed on the public profile (4 Sep 2026): three public repositories — `infoonairesources-site`, `inforionairesources.shop` (spelling as displayed on the profile page; reported verbatim), `telegram-transcriber`. **Grade: OBSERVED.** No inference is drawn about whether the "inforion…" spelling is a distinct repository or the shop repository under a different name; that is for the shop's own inventory.

---

## 8. (i) REPO-VS-LIVE DIVERGENCES

**None determinable** — the repository could not be read. Recorded instead are the **live-vs-live internal inconsistencies** observed, so that a future repo comparison has a checklist:

| # | Inconsistency | Location |
|---|---------------|----------|
| D-a | Homepage logo `<img>` has empty `src`; Publications logo `src` is `/logo-dark.png`. | 4.5 |
| D-b | `og:site_name` present on `/publications`, absent on `/`. | 3.6–3.7 |
| D-c | `meta keywords` present on `/`, absent on `/publications`. | 3.5 |
| D-d | Homepage `<title>` ends "· Nairobi, Kenya"; homepage `og:title` ends "· Nairobi". | 3.6 |
| D-e | Nav item order differs between the two pages (Contact/Publications swapped). | 4.12 |
| D-f | Five "Forthcoming" items carry dates that have passed. | 5.4 |
| D-g | Publications page says the 21 March 2026 piece is on Substack; Substack landing says the publication launched ≈ April 2026. | 5.4 |
| D-h | LinkedIn CTA links to `#`. | 4.11 |
| D-i | `www` hostname absent from DNS while the domain is otherwise fully configured (Cloudflare NS, Zoho MX, Google verification). | 1.13 |

---

## 9. (ii) NOT DETERMINABLE FROM HERE — COMPLETE CHECKLIST

Split into two classes, because they are resolved by different people.

### 9(a) Instrument-limit items — resolvable by anyone with an unrestricted HTTP client (e.g. Claude Code session, browser DevTools), no dashboard access required

| Item | Exact action that resolves it |
|------|-------------------------------|
| `robots.txt` contents and named-crawler allow/block list (2.1) | `curl -s https://swakaadvocates.co.ke/robots.txt` |
| `llms.txt` (2.2) | `curl -si https://swakaadvocates.co.ke/llms.txt` |
| `sitemap.xml` presence/validity/currency (2.3) | `curl -s https://swakaadvocates.co.ke/sitemap.xml`; also `/sitemap_index.xml` |
| Response headers incl. `server`, `cf-ray`, `cf-cache-status`, `x-robots-tag`, security headers, `last-modified`, `etag` (1.9–1.11, 2.5, 5.4) | `curl -sI https://swakaadvocates.co.ke/` and same for `/publications` |
| http→https and slash redirects (1.14–1.15) | `curl -sI http://swakaadvocates.co.ke/`; `curl -sI https://swakaadvocates.co.ke/publications/` |
| TLS issuer/expiry/version (1.12) | `openssl s_client -connect swakaadvocates.co.ke:443 -servername swakaadvocates.co.ke </dev/null 2>/dev/null \| openssl x509 -noout -issuer -dates` |
| Per-UA bot behaviour (2.6) | `curl -sI -A "GPTBot/1.0" https://swakaadvocates.co.ke/` repeated for ClaudeBot, PerplexityBot, Bytespider, CCBot, Google-Extended |
| `/.well-known/security.txt` and any other well-known (2.8) | `curl -si https://swakaadvocates.co.ke/.well-known/security.txt` |
| 404 behaviour and custom 404 page | `curl -si https://swakaadvocates.co.ke/does-not-exist-zawawi-test` |
| JSON-LD / microdata, every block quoted (3.1) | `curl -s https://swakaadvocates.co.ke/ \| grep -A400 'application/ld+json'`; same for `/publications` |
| `<html lang>`, generator meta, favicon links, twitter tags confirmation (1.1, 3.8, 3.11, 3.13) | `curl -s https://swakaadvocates.co.ke/ \| sed -n '1,120p'` |
| Landmarks, ARIA, semantic vs div, skip link, tabindex, focus CSS, contrast, CSS background-image text, script-injected widgets/ads/cookie banners (4.3, 4.4, 4.7–4.9, 4.13, 2.9, 6.1, 6.7) | Save full source + linked stylesheets; or run Lighthouse/axe in a browser |
| Homepage logo `src` resolution (4.5) | Inspect `<img>` in raw source |
| Substack feed and whether the 21 March 2026 article exists (2.7, 5.4) | `curl -s https://swakaadvocates.substack.com/feed` |
| Orphan/unlinked pages | Sitemap fetch plus Search Console "Pages" report |
| SPF/DMARC (1.7 footnote) | `dig TXT _dmarc.swakaadvocates.co.ke` |

### 9(b) Owner-supplied facts — require dashboard, account, or the advocate

| Item | Who / where |
|------|-------------|
| Cloudflare proxy status per DNS record (confirming 1.9), plan tier, origin host IP/hostname | Cloudflare dashboard → DNS |
| Cloudflare Bot Fight Mode / AI-crawler blocking / managed robots.txt / "block AI scrapers" / WAF custom rules — and the state of every setting the 15 September 2026 default change touches | Cloudflare dashboard → Security → Bots; Settings |
| Cloudflare cache rules, page rules, redirect rules, SSL mode (Flexible/Full/Strict), HSTS | Cloudflare dashboard |
| Hosting provider, plan, and deploy method | Hosting control panel / repository CI config |
| Repository access (all of Section 7) | Benta's GitHub login or Claude Code GitHub connection; or make the repo public |
| Google Search Console verified property, indexed-page count, robots.txt report, coverage errors | Search Console (verification token observed in DNS, so a property likely exists) |
| Analytics presence and provider | Raw source (script tags) *or* owner statement |
| Which bar/jurisdiction "Admitted to the Bar 2006" refers to; practising-certificate status; LSK member number; whether any other advocates practise at the firm | The advocate |
| Whether Substack and LinkedIn links are intended destinations | The advocate / Benta |
| Whether the `www` hostname is intentionally unconfigured | Benta / Cloudflare DNS |

---

## 10. (iii) INSPECTION DATE-STAMP

All observations in this inventory were made on **Friday 4 September 2026, between approximately 08:40 and 08:50 UTC** (11:40–11:50 EAT), from an Anthropic sandbox environment (shared egress IP) using: DNS resolution (dnspython), unauthenticated HTTPS to GitHub, and a text-extracting HTTPS content fetch of `https://swakaadvocates.co.ke/`, `https://swakaadvocates.co.ke/publications`, and `https://swakaadvocates.substack.com`.

No commits, branches, issues, or pull requests were created. No write action of any kind was taken.

**Coverage summary (denominator = 7 inventory sections):** Sections 5 and 6 substantially observed; Sections 1, 3 and 4 partially observed with the machine-facing half (headers, JSON-LD, source-level accessibility) outstanding; Section 2 largely outstanding (robots.txt not retrievable); Section 7 wholly outstanding (repository inaccessible). Every outstanding item is listed in Section 9 with the specific action that closes it.

*End of inventory.*
