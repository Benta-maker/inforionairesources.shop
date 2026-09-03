# SITE INVENTORY — infoonairesources.shop & swakaadvocates.co.ke

**Inventory version:** 1.0
**Inspection window:** 28 August 2026, 12:30–13:10 UTC (15:30–16:10 EAT)
**Character:** Findings only. Descriptive baseline. No recommendations, no remediation, no prioritisation.
**Repository handling:** Read-only throughout. No commits, branches, issues, pull requests, forks or writes of any kind were made. Repository contents were obtained by anonymous public HTTPS download of the `main` branch archive.

---

## 0. ACCESS CONDITIONS AND OBSERVATIONAL LIMITS

These conditions determine what could and could not be graded OBSERVED. They are stated first because several gradings below turn on them.

| # | Condition | Effect on inventory |
|---|---|---|
| 0.1 | **No GitHub connector is present in this session.** The mission specifies "the connected GitHub repositories"; no GitHub MCP server or first-party GitHub tool is available. Repository access was obtained anonymously over public HTTPS (`codeload.github.com` archive download, `github.com` profile page, `commits/main.atom` feed). | Only **public** repositories are visible. Any private repository is invisible from here. This is material to the swakaadvocates.co.ke finding at §B.7. |
| 0.2 | **Sandbox egress is allow-listed.** Direct HTTP requests to `swakaadvocates.co.ke` and `infoonairesources.shop` are refused by the egress proxy (`HTTP/2 403`, `x-deny-reason: host_not_allowed`, observed 28 Aug 2026 12:49 UTC). | **No response headers were obtainable for either live site.** No `server`, `cf-ray`, `x-robots-tag`, `cache-control`, `strict-transport-security`, `content-security-policy`, cookie, or redirect-chain header could be read. All header-dependent items are graded NOT DETERMINABLE FROM HERE. |
| 0.3 | **The live-fetch tool returns extracted text plus `<meta>`/`<link rel=canonical>` frontmatter, not raw HTML.** It does not surface `<script type="application/ld+json">` blocks, heading tag levels, landmark elements, ARIA attributes, `alt` attributes, or `<form>` markup. | For infoonairesources.shop this is mitigated: the deployed repository is identified and its raw source was read directly. For swakaadvocates.co.ke it is not mitigated — **no repository was found**, so the machine-legible and semantic layers of that site are largely NOT DETERMINABLE FROM HERE. |
| 0.4 | **The live-fetch tool does not execute JavaScript.** | Content dependent on client-side execution is absent from fetched output. This was used affirmatively as a detection method (see §A.4.6). |
| 0.5 | **The live-fetch tool refuses constructed URLs.** It will only fetch a URL that appeared verbatim in a prior search result, a prior fetch, or the operator's message. `https://swakaadvocates.co.ke/robots.txt` and `https://infoonairesources.shop/robots.txt` were both refused on this basis (`PERMISSIONS_ERROR`, 28 Aug 2026). | **No `robots.txt`, `sitemap.xml`, `llms.txt` or `/.well-known/` path on either live host could be fetched directly.** Where the deployed source is known, the served content is graded INFERRED with the inference stated. |
| 0.6 | DNS was resolved directly (system resolver + `dnspython` against the sandbox resolver), 28 Aug 2026 12:47–12:52 UTC. | DNS findings are OBSERVED and are the strongest infrastructure evidence in this inventory. |

**Repository-to-property mapping**

| Property | Repository | Mapping basis | Status |
|---|---|---|---|
| infoonairesources.shop | `github.com/Benta-maker/inforionairesources.shop` (branch `main`) | `CNAME` file contains `infoonairesources.shop`; page-for-page match against live fetches | **Deployed source.** OBSERVED |
| infoonairesources.shop | `github.com/Benta-maker/infoonairesources-site` (branch `main`) | Contains an earlier version of the same property; `CNAME` was deleted 22 Mar 2026 | **Not deployed.** OBSERVED |
| swakaadvocates.co.ke | *(none found)* | Account `Benta-maker` holds three public repos: `inforionairesources.shop`, `infoonairesources-site`, `telegram-transcriber`. GitHub repository search for `swakaadvocates` returns `total_count: 0`. | **No public repository corresponds to this deployed site.** OBSERVED (as absence-of-public-record; see §B.7) |

Note the repository name is **`inforionairesources.shop`** — it does not match the domain `infoonairesources.shop`. The repo name contains "inforion…", the domain "infoonai…". OBSERVED (GitHub profile listing and archive path, 28 Aug 2026).

---

# PROPERTY A — infoonairesources.shop

## A.1 STACK & DELIVERY

**A.1.1 Framework / CMS**
No framework, no CMS, no build step. Hand-authored static HTML files with a single inline `<style>` block per page and (on the homepage only) a single inline `<script>` block. No external CSS file, no JS bundle, no `package.json`, no lockfile, no `_config.yml`, no Jekyll front-matter.
— OBSERVED: repo file listing and per-file parse, `inforionairesources.shop-main/`, 28 Aug 2026.

**A.1.2 Rendering model**
Fully static, server-delivered HTML. All text content is present in the initial HTML response. Nothing in the content is fetched or generated client-side.
— OBSERVED: repo source; corroborated by live fetch of `https://www.infoonairesources.shop/` (28 Aug 2026), which returned the complete page body without JavaScript execution.

Two exceptions where the **rendered** state depends on JavaScript, though the text exists in the DOM either way — see §A.4.6.

**A.1.3 Hosting signals**

| Record | Value | Grade |
|---|---|---|
| Nameservers (`infoonairesources.shop`) | `nick.ns.cloudflare.com.`, `sharon.ns.cloudflare.com.` | OBSERVED |
| A (apex) | `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153` | OBSERVED |
| AAAA (apex) | NoAnswer | OBSERVED |
| CNAME (`www`) | `benta-maker.github.io.` | OBSERVED |
| A (`www`) | same four `185.199.*` addresses | OBSERVED |
| AAAA (`www`) | `2606:50c0:8000::153` … `:8003::153` | OBSERVED |
| PTR for `185.199.108.153` | `cdn-185-199-108-153.github.com` | OBSERVED |
| CAA (`www`) | `issue`/`issuewild` for `letsencrypt.org`, `digicert.com`, `sectigo.com` | OBSERVED |
| MX | **NoAnswer — no MX record published** | OBSERVED |
| TXT (apex) | **NoAnswer — no TXT record published** | OBSERVED |
| `_dmarc` | NXDOMAIN | OBSERVED |

**This is the single most consequential infrastructure finding on this property.** DNS is *managed by* Cloudflare, but the records resolve directly to GitHub Pages anycast addresses. The records are therefore **DNS-only (unproxied)** — traffic does not pass through Cloudflare's edge. Cloudflare's bot management, WAF, crawler controls, Pay-Per-Crawl, and the 15 September 2026 default change apply to *proxied* hostnames; an unproxied record is outside that control plane entirely.
— Grade: **OBSERVED** for the DNS records and the GitHub PTR. **INFERRED** for the conclusion "traffic does not traverse Cloudflare's proxy" — the inference is that Cloudflare's proxy always answers on its own anycast ranges (`104.16.0.0/12`, `172.64.0.0/13` and adjacent), and these addresses are GitHub's, so the orange-cloud toggle is off for these records. Confirmable only in the Cloudflare dashboard.

**A.1.4 TLS state**
Certificates could not be inspected (§0.2). Both live fetches succeeded over `https://` without a TLS error being surfaced by the fetch tool, and CAA records authorise Let's Encrypt, DigiCert and Sectigo.
— INFERRED: GitHub Pages provisions and renews a certificate automatically for custom domains, and the CAA set includes Let's Encrypt, GitHub Pages' issuer. Cipher suites, protocol versions, HSTS, and certificate expiry are NOT DETERMINABLE FROM HERE (requires a TLS handshake or the GitHub Pages settings screen).

**A.1.5 www / apex and redirect behaviour**
The `CNAME` file in the deployed repository contains the **apex**: `infoonairesources.shop`.
A fetch of `https://www.infoonairesources.shop/` resolved to a final URL of `https://infoonairesources.shop` — i.e. **www redirects to apex**.
— OBSERVED: fetch metadata `destination_url: https://infoonairesources.shop/`, `final_url: https://infoonairesources.shop`, 28 Aug 2026.
The HTTP status code of that redirect (301 vs 302) is NOT DETERMINABLE FROM HERE (§0.2).

**This conflicts with the site's own canonical declarations.** Every `<link rel="canonical">`, every `og:url`, every `<loc>` in `sitemap.xml`, and the `Sitemap:` line in `robots.txt` specify the **`www.` host** — the host the server redirects away from. Recorded as a divergence at §C.1.7.

---

## A.2 CRAWL & AGENT POSTURE

**A.2.1 robots.txt — verbatim**
Served content could not be fetched directly (§0.5). The file below is the deployed repository's `robots.txt`, read at `inforionairesources.shop-main/robots.txt` on 28 Aug 2026. GitHub Pages serves repository root files byte-for-byte, so served content is **INFERRED** to be identical; the inference is unverified.

```
# InfoOnAIResources — robots.txt
# Strategic crawler configuration for AI-era discoverability
# Block training crawlers. Allow search and retrieval crawlers.
# Last updated: March 2026

# ── AI TRAINING BOTS — BLOCK ─────────────────────────────────────
# These bots scrape content for model training. We do not permit this.
# Our content is original human intelligence — not available for training.

User-agent: GPTBot
Disallow: /

User-agent: ClaudeBot
Disallow: /

User-agent: Google-Extended
Disallow: /

User-agent: CCBot
Disallow: /

User-agent: Bytespider
Disallow: /

User-agent: meta-externalagent
Disallow: /

User-agent: omgili
Disallow: /

User-agent: omgilibot
Disallow: /

User-agent: FacebookBot
Disallow: /

# ── AI SEARCH AND RETRIEVAL BOTS — ALLOW ─────────────────────────
# These bots index content so AI agents can find and cite it.
# This is exactly what we want — maximum discoverability.

User-agent: OAI-SearchBot
Allow: /

User-agent: Claude-SearchBot
Allow: /

User-agent: ChatGPT-User
Allow: /

User-agent: Claude-User
Allow: /

User-agent: Perplexity-User
Allow: /

User-agent: PerplexityBot
Allow: /

User-agent: Amazonbot
Allow: /

User-agent: Gemini-Deep-Research
Allow: /

User-agent: cohere-ai
Allow: /

# ── TRADITIONAL SEARCH — ALLOW ───────────────────────────────────

User-agent: Googlebot
Allow: /

User-agent: Bingbot
Allow: /

User-agent: Slurp
Allow: /

User-agent: DuckDuckBot
Allow: /

# ── ALL OTHER BOTS — ALLOW ───────────────────────────────────────

User-agent: *
Allow: /

# ── SITEMAPS ─────────────────────────────────────────────────────

Sitemap: https://www.infoonairesources.shop/sitemap.xml
```

**A.2.2 Named agents, as written**

*Disallowed (9):* `GPTBot`, `ClaudeBot`, `Google-Extended`, `CCBot`, `Bytespider`, `meta-externalagent`, `omgili`, `omgilibot`, `FacebookBot`.
*Explicitly allowed (13):* `OAI-SearchBot`, `Claude-SearchBot`, `ChatGPT-User`, `Claude-User`, `Perplexity-User`, `PerplexityBot`, `Amazonbot`, `Gemini-Deep-Research`, `cohere-ai`, `Googlebot`, `Bingbot`, `Slurp`, `DuckDuckBot`.
*Catch-all:* `User-agent: *` → `Allow: /`.
*Absent by name:* `Applebot`, `Applebot-Extended`, `Google-CloudVertexBot`, `Meta-ExternalFetcher`, `Diffbot`, `Timpibot`, `ImagesiftBot`, `AI2Bot`, `anthropic-ai`, `Claude-Web`, `OpenAI's `SearchGPT` variants beyond `OAI-SearchBot`, `MistralAI-User`, `NovaAct`, `Operator`/`ChatGPT-Operator`, `Bingbot`'s `BingPreview`, `YandexBot`, `Baiduspider`, `Bytespider`'s `TikTokSpider` sibling. These fall to `User-agent: *` → allowed.
— OBSERVED (repo file). Whether any of these strings correspond to a currently-operating crawler as of 28 Aug 2026 was not verified in this inventory; the finding is what the file says, not whether it is current.

**A.2.3 llms.txt**
**Present**, 8,965 bytes, at repository root. Format follows the llms.txt convention: H1 site name, blockquote summary, prose paragraph, then H2 sections with linked bullet entries. Sections: Weekly Intelligence Brief; Opportunity Database; Intelligence by Industry; Tools & Tutorials; Laws & Policy Library; Deep Dives & Analysis; Podcasts; Research & Papers; Mentor & Mentee Space; About & Advisory; Optional.
— OBSERVED (repo, `llms.txt`). Served status INFERRED as in §A.2.1.

**Content-to-reality state:** the file describes 11 content areas and links roughly 22 paths. Of the linked paths, **six resolve to real pages** (`/opportunities/jobs/`, `/opportunities/scholarships/`, `/opportunities/courses/`, `/opportunities/resources/far-ai/`, `/deep-dives/`, plus the four individual opportunity detail pages and the one deep-dive detail page). The remainder — `/brief/latest`, `/brief/`, `/opportunities/grants/`, `/industry/health/`, `/industry/legal/`, `/industry/finance/`, `/industry/education/`, `/industry/agriculture/`, `/tools/`, `/policy/`, `/podcasts/`, `/research/`, `/mentors/`, `/advisory/`, `/about.html`, `/contact.html`, `/privacy.html`, `/terms.html` — have no corresponding file in the deployed repository. See §A.5.3.
— OBSERVED (cross-reference of `llms.txt` against repo file listing).

**A.2.4 sitemap.xml**
**Present** at repository root, 6,644 bytes, well-formed XML against the sitemaps.org 0.9 schema, referenced from `robots.txt`.
Contains **31 `<url>` entries**. Every `<loc>` uses the `www.` host. `<lastmod>` values are `2026-03-21` (18 entries) or `2026-06-22` (13 entries). `<changefreq>` and `<priority>` are populated throughout.
— OBSERVED (repo, `sitemap.xml`).

**Currency:** the most recent commit to the repository is 23 June 2026 (§A.7.4); the newest `lastmod` is 22 June 2026. The sitemap has not been updated since the last content commit.

**Validity against deployed reality:** of the 31 URLs, **13 correspond to files that exist** in the deployed repository and **18 do not**. Four of the 18 were confirmed by live fetch to return HTTP 404 (`/tools/`, `/about.html`, `/privacy.html`, `/opportunities/grants/`, all 28 Aug 2026); the remaining 14 are INFERRED to 404 on the same basis (absent from the repository; GitHub Pages serves only repository contents). Full enumeration at §A.5.3.
The sitemap also lists `https://www.infoonairesources.shop/llms.txt` as a `<url>` entry — a non-HTML resource listed as a crawlable page.
— OBSERVED.

**A.2.5 Meta robots directives**

| Page | `<meta name="robots">` |
|---|---|
| `/` | `index, follow` |
| `/opportunities/` | `index, follow` |
| `/opportunities/jobs/` | `index, follow` |
| `/opportunities/jobs/ai-technical-lead-grit/` | `index, follow` |
| `/opportunities/jobs/research-engineer-domain-scaling-anthropic/` | `index, follow` |
| `/opportunities/jobs/knowledge-lawyer-ai-innovation-weightmans/` | `index, follow` |
| `/opportunities/scholarships/` | `index, follow` |
| `/opportunities/scholarships/oxford-ethics-ai-accelerator-fellowship/` | `index, follow, max-snippet:-1` |
| `/opportunities/courses/` | `index, follow` |
| `/opportunities/courses/ai-impact-lab-humanitarian-supply-chain/` | `index, follow, max-snippet:-1` |
| `/opportunities/resources/far-ai/` | `index, follow` |
| `/deep-dives/` | `index, follow` |
| `/deep-dives/glm-5-2-global-south/` | `index, follow, max-image-preview:large, max-snippet:-1` |

— OBSERVED (repo parse; the `/` and `/opportunities/` values corroborated in live fetch frontmatter, 28 Aug 2026).
`X-Robots-Tag` response headers: NOT DETERMINABLE FROM HERE (§0.2). GitHub Pages does not offer per-response header configuration, so the practical likelihood of one existing is low, but this was not verified.

**A.2.6 Bot-management / challenge behaviour on fetch**
Both live fetches returned page content directly with no interstitial, no JS challenge, no CAPTCHA, no rate-limit response. Consistent with A.1.3 (records unproxied; no Cloudflare edge in path).
— OBSERVED (fetches of `/` and `/opportunities/`, 28 Aug 2026).

**A.2.7 Feeds**
No RSS, Atom, or JSON Feed file exists in the repository. No `<link rel="alternate" type="application/rss+xml">` on any page.
— OBSERVED (repo file listing; per-page `<link>` enumeration).

**A.2.8 `.well-known` endpoints**
No `.well-known/` directory exists in the repository. No `security.txt`, no `ai.txt`, no Web Bot Auth material, no `x402`/payment discovery document.
— OBSERVED (repo file listing). Served status INFERRED (GitHub Pages serves only repository contents).

**A.2.9 Verification artifacts**
`google9d706cf5c30241d2.html` at repository root, 54 bytes, content: `google-site-verification: google9d706cf5c30241d2.html`. Committed 23 June 2026. No corresponding DNS TXT verification record exists on this domain (§A.1.3).
— OBSERVED.

---

## A.3 MACHINE-LEGIBLE LAYER

### A.3.1 Structured data inventory (all thirteen content pages)

| Page | JSON-LD types present |
|---|---|
| `/` | `Organization`, `WebSite`, `WebPage`, `FAQPage` (single `@graph` block, 7,797 chars) |
| `/opportunities/` | `CollectionPage`, `BreadcrumbList` |
| `/opportunities/jobs/` | `BreadcrumbList`, `ItemList` |
| `/opportunities/jobs/ai-technical-lead-grit/` | `JobPosting`, `BreadcrumbList` |
| `/opportunities/jobs/research-engineer-domain-scaling-anthropic/` | `JobPosting`, `BreadcrumbList` |
| `/opportunities/jobs/knowledge-lawyer-ai-innovation-weightmans/` | `JobPosting`, `BreadcrumbList` |
| `/opportunities/scholarships/` | `BreadcrumbList`, `ItemList` |
| `/opportunities/scholarships/oxford-ethics-ai-accelerator-fellowship/` | `JobPosting`, `BreadcrumbList` |
| `/opportunities/courses/` | `BreadcrumbList`, `ItemList` |
| `/opportunities/courses/ai-impact-lab-humanitarian-supply-chain/` | `Course` (with nested `Offer`, `CourseInstance`), `BreadcrumbList` |
| `/opportunities/resources/far-ai/` | `Organization`, `BreadcrumbList` |
| `/deep-dives/` | `BreadcrumbList`, `ItemList` |
| `/deep-dives/glm-5-2-global-south/` | `BlogPosting`, `Person`, `Organization`, `BreadcrumbList`, `FAQPage` |

All blocks parsed as valid JSON. No parse errors. No microdata (`itemscope`/`itemprop`) or RDFa anywhere in the property.
— OBSERVED (repo parse, 28 Aug 2026).

### A.3.2 Homepage `@graph` — properties populated vs empty

**`Organization`** (`@id` `…/#organization`): `name`, `alternateName`, `url`, `logo` (`…/assets/logo.png`), `description`, `foundingDate` (`"2025"`), `areaServed` (5 `Place`/`Country` nodes), `knowsAbout` (13 strings), `sameAs` (Instagram, TikTok, LinkedIn), `contactPoint` (`ContactPoint` with `email: info@infoonairesources.shop`, `contactType: "General Enquiries"`) — all populated.
**Absent:** `address` / `PostalAddress`, `telephone`, `legalName`, `vatID`, `founder`, `numberOfEmployees`, `identifier`. The page footer states "Nairobi, Kenya" as text; no address is expressed in markup.
**Referenced-but-nonexistent asset:** `logo` points to `/assets/logo.png`; the repository contains **no `assets/` directory**.
— OBSERVED (repo parse + repo file listing).

**`WebSite`** (`@id` `…/#website`): `url`, `name`, `description`, `publisher` (`@id` reference, resolves), `potentialAction` → `SearchAction` with `target: https://www.infoonairesources.shop/search?q={search_term_string}`.
**No `/search` endpoint exists** in the repository. The declared search action targets a path that does not resolve.
— OBSERVED.

**`WebPage`** (`@id` `…/#webpage`): `url`, `name`, `isPartOf`, `about`, `description`, `dateModified: "2026-03-21"`.
`dateModified` is 3 months older than the last content commit (23 June 2026).
— OBSERVED.

**`FAQPage`**: 6 `Question`/`Answer` pairs, all `text` fields populated (471–591 chars each).
**The six marked-up questions do not match the five questions rendered on the page.** See §C.1.4.
— OBSERVED.

### A.3.3 `JobPosting` markup — required-property audit

Four `JobPosting` nodes exist (three job pages plus the Oxford fellowship page, which is typed `JobPosting` although presented as a fellowship).

| Property | GRIT | Anthropic | Weightmans | Oxford |
|---|---|---|---|---|
| `title` | ✓ | ✓ | ✓ | ✓ |
| `description` (HTML) | ✓ | ✓ | ✓ (short; defers to source) | ✓ |
| `datePosted` | `2026-06-22` | `2026-06-22` | `2026-06-22` | **absent** |
| `validThrough` | `2026-06-26` | `2026-08-21` | **absent** (rolling) | `2026-06-12` |
| `hiringOrganization` | ✓ | ✓ | ✓ | ✓ |
| `jobLocation` | ✓ (Fish Hoek, ZA) | ✓ (SF + NYC) | ✓ (4 UK cities) | ✓ (Oxford, GB) |
| `jobLocationType` | `TELECOMMUTE` | absent | absent | `TELECOMMUTE` |
| `applicantLocationRequirements` | `Continent: Africa` | `Country: USA` | `Country: United Kingdom` | `Country: Worldwide` |
| `employmentType` | `FULL_TIME` | `FULL_TIME` | **absent** | `OTHER` |
| `baseSalary` | **absent** | **absent** | **absent** | **absent** (£2,000/mo stipend stated in `description` prose only) |
| `identifier` | absent | ✓ (`PropertyValue`, Anthropic `5271380008`) | absent | absent |
| `directApply` | `false` | `false` | `false` | `false` |
| `url` | self | self | self | **external** (`afp.oxford-aiethics.ox.ac.uk/join`) |

Two date-state facts as of 28 Aug 2026: the GRIT posting's `validThrough` (26 Jun 2026) and the Oxford `validThrough` (12 Jun 2026) are **past**; the Anthropic posting's `validThrough` (21 Aug 2026) is **past by seven days**. All three remain published with `index, follow`. The Oxford page's `<title>` carries "(Closed)" and its prose states the closure; the Anthropic and GRIT pages carry no expiry marker in prose or title.
— OBSERVED (repo parse; date comparison against inspection date 28 Aug 2026).

`applicantLocationRequirements` on the Oxford node uses `@type: Country` with `name: "Worldwide"` — "Worldwide" is not a country.
Three of four nodes set `url` to their own page while `directApply: false`; the Oxford node sets `url` to the third-party application page.
— OBSERVED.

### A.3.4 `Course` markup (AI Impact Lab page)
`name`, `description`, `url`, `provider` (`Tech To The Rescue`), `contributor` (`HELP Logistics (Kühne Foundation)`), `courseMode: "online"`, `isAccessibleForFree: true`, `inLanguage: "en"`, `offers` (`Offer`: `price "0"`, `priceCurrency "USD"`, `availability InStock`, `availabilityStarts 2026-06-15`, `availabilityEnds 2026-07-24`), `hasCourseInstance` (`CourseInstance`: `courseWorkload "PT13H"`, `startDate 2026-08-10`, `endDate 2026-11-09`, `VirtualLocation`, nested `Offer`).
All declared properties populated. `availabilityEnds` (24 Jul 2026) is **past** as of 28 Aug 2026; the course instance `startDate` (10 Aug 2026) is also past, `endDate` (9 Nov 2026) is future. The `/opportunities/` index page still labels this listing "Open · closes 24 Jul 2026".
— OBSERVED (repo parse; live fetch of `/opportunities/`, 28 Aug 2026).

### A.3.5 `BlogPosting` markup (deep dive)
`headline`, `description`, `datePublished` / `dateModified` (`2026-06-22`), `url`, `image` (`…/assets/og-image.jpg`), `articleSection`, `about` (5 strings), `keywords`, `author` (`@id` → `Person` node `#editorial-team`, name "InfoOnAIResources Editorial Team"), `publisher` (`@id` → `Organization` node), `isPartOf`, `mainEntityOfPage`.
`author` is typed `Person` but named as a team; its `url` points to `/about.html`, which does not exist. `image` points to `/assets/og-image.jpg`, which does not exist in the repository.
— OBSERVED.

### A.3.6 Open Graph and Twitter cards

`og:title`, `og:description`, `og:type`, `og:url`, `og:image` present on all twelve content pages.
`og:image` is `https://www.infoonairesources.shop/assets/og-image.jpg` on every page — **one shared image reference, and the `assets/` directory does not exist in the repository**. `og:image:width`, `og:image:height`, `og:image:alt`, `og:site_name`, `og:locale` are absent everywhere.
Twitter card tags (`twitter:card: summary_large_image`, `twitter:title`, `twitter:description`, `twitter:image`) present on **4 of 12** pages: `/`, `/deep-dives/glm-5-2-global-south/`, `/opportunities/jobs/ai-technical-lead-grit/`, `/opportunities/jobs/research-engineer-domain-scaling-anthropic/`. Absent on the other eight.
— OBSERVED (repo parse; `/` and `/opportunities/` corroborated by live fetch frontmatter, 28 Aug 2026).

### A.3.7 Canonical tags
Every one of the twelve content pages carries `<link rel="canonical">` with a self-referential absolute URL on the **`www.`** host. Live-fetch frontmatter for `/` and `/opportunities/` confirms the `www.` canonical is served — while the server itself redirects `www.` → apex (§A.1.5).
— OBSERVED.

### A.3.8 hreflang
No `hreflang` attributes anywhere. No `<link rel="alternate" hreflang>`. Single-language property.
— OBSERVED.

### A.3.9 Commercial facts as machine-readable text (shop context)
This property does not sell a product. It has no cart, no checkout, no product catalogue, and no `Product`, `Offer` (except within the `Course` node), `AggregateOffer` or `ItemAvailability` markup for its own offering.

Its own pricing exists **as page text only, with no markup**: the tiers block (`#tiers`) renders "Free forever / Essential / **$0 — always free**" and "Launching Month 4 / For serious professionals / Professional / **From $3/month — PPP pricing applies**". The homepage FAQ prose adds a fuller price ladder: "from $3/month in Africa and India, $8–12/month in the Gulf, and $12–15/month for diaspora readers in the US and UK", plus "M-Pesa and local mobile payment options are available from launch."
No `Offer`, `PriceSpecification`, `Service`, or `Product` node expresses any of this.
— OBSERVED (repo parse of `#tiers` and the FAQ block; corroborated in live fetch, 28 Aug 2026).

No product feed of any kind (no Merchant Center feed, no `product.xml`, no CSV/TSV feed file) exists in the repository.
— OBSERVED.

---

## A.4 SEMANTIC & ACCESSIBILITY STRUCTURE

**A.4.1 Heading hierarchy**
All twelve content pages carry **exactly one `<h1>`**. Level ordering is sane on every page: `h1` → `h2` → `h3`, no skipped levels observed.
Homepage outline: `h1` "What AI means for your career, your future." → `h2` "The Weekly Intelligence Brief" → `h2` "Every AI opportunity. One place." → nine `h3` category names → `h2` "Start free. Upgrade when you're ready." → `h2` "What people ask us" → `h2` "The window is open. Get in before it narrows."
— OBSERVED (repo parse of all files).

**A.4.2 Landmarks**
**No `<main>` element exists on any page of this property.** Zero occurrences across all thirteen HTML files.
`<footer>`: present on all twelve content pages.
`<header>`: present on eleven of twelve (absent on `/` — the homepage top bar is a `<nav>` inside a `<div>`).
`<nav>`: 2 per subpage (main + breadcrumb); 3 on the homepage (main, "Content categories", "Footer navigation"), each with a distinct `aria-label`.
`<article>`: present on the six detail pages (three jobs, one fellowship, one course, one deep dive) and the FAR.AI page. Absent on index pages and the homepage.
`<section>`: 6 on `/`, 1 on most index pages, 0 on detail pages.
`<address>`, `<aside>`, `<time>`: absent everywhere.
— OBSERVED.

**A.4.3 Semantic HTML vs div-soup**
Homepage element census: `div` 81, `span` 29, `section` 6, `nav` 3, `footer` 1, `a` 30, `button` 7, `ul` 3, `form` 2, `input` 2, `label` 2, `svg` 6, `header` 0, `main` 0, `article` 0, `img` 0, `table` 0.
Subpage detail pages run 8–14 `div`s each — materially leaner. The homepage is the div-heavy page; the content pages are close to semantic.
— OBSERVED.

**A.4.4 ARIA usage**
Homepage: `role` values `list` (2), `listitem` (5), `article` (1), `complementary` (1), `region` (5), `contentinfo` (1). ARIA attributes: `aria-label` (27), `aria-labelledby` (11), `aria-hidden` (15), `aria-expanded` (5), `aria-controls` (5), `aria-required` (2).
Pattern assessment: ARIA is **decorating** rather than replacing. The FAQ accordion is built on real `<button>` elements with `aria-expanded` / `aria-controls` maintained in the click handler. `aria-hidden` is applied to decorative emoji and SVG. `role="region"` with `aria-labelledby` is applied to `<section>` elements that already have accessible names. `role="contentinfo"` duplicates the native `<footer>` semantic. No `role="button"` on a `<div>`, no `role="link"` on a non-anchor, no custom widget replacing a native control was found.
`tabindex` attributes: **zero occurrences** across the entire property — no positive `tabindex`, no `tabindex="-1"` misuse.
Inline event handlers (`onclick=` and siblings): **zero occurrences**. All interactivity is bound via `addEventListener`.
— OBSERVED.

**A.4.5 Images and information-in-images**
**Zero `<img>` elements exist anywhere in this property.** Zero `<picture>`, `<video>`, `<iframe>`, `<canvas>`. Six inline `<svg>` on the homepage, all `aria-hidden`.
Consequence: **no commercial fact is trapped in an image.** Prices, service names, deadlines, salary notes, contact email, tier contents, statistics — all exist as selectable, extractable text. Alt-text coverage is trivially complete because there is nothing to cover.
Two referenced-but-absent image assets exist only as *URLs inside metadata*: `/assets/logo.png` (Organization logo) and `/assets/og-image.jpg` (all `og:image`/`twitter:image`, and the `BlogPosting` `image`). Neither file exists in the repository. These affect social/preview rendering and `Organization.logo` validity, not page content.
— OBSERVED.

**A.4.6 JavaScript-dependent rendering (the dual-eyes layer)**
The homepage carries a single 1,391-character inline script doing four things. Two of them change what a *rendering* agent sees while leaving the DOM text intact for a *retrieval* agent:

1. **`.reveal` animation gate.** CSS declares `.reveal { opacity: 0; transform: translateY(24px); }` and `.reveal.visible { opacity: 1; transform: none; }`. An `IntersectionObserver` adds `.visible` on scroll-into-view. There are **20 `.reveal` elements on the homepage**. Until the observer fires, those blocks render at **opacity 0** — invisible in a screenshot — while their text is fully present in the HTML source.
2. **FAQ accordion.** CSS declares `.faq-answer { display: none; }`, `.faq-answer.open { display: block; }`. All **five answer bodies are present in the DOM at load** and are visually collapsed until clicked. A retrieval agent reading the DOM gets all five answers; a vision agent working from a rendered screenshot gets five question strings and no answers.
3. **Copyright year.** `document.getElementById('year').textContent = new Date().getFullYear();` — the year is empty without JS. The live fetch confirms this: the served footer reads `© InfoOnAIResources.shop · Nairobi, Kenya` with **no year**.
4. **Staggered card transition delays** — cosmetic only.

These four are the property's entire JavaScript surface. The other eleven content pages have **no script at all** and no `.reveal` usage — they render identically with and without JS.
— OBSERVED (repo CSS/JS parse; the missing-year effect corroborated in live fetch output, 28 Aug 2026).

**A.4.7 Colour contrast (computed from declared CSS custom properties)**
Design tokens: `--bg #080a0e`, `--surface #0d1017`, `--text #eef0f3`, `--muted #7a8394`, `--teal #2dd4bf`, `--gold #f0b429`, `--rust #e05c3a`.

| Pair | Ratio | WCAG 2.x AA normal text (4.5:1) |
|---|---|---|
| `--text` on `--bg` | 17.35 : 1 | pass |
| `--muted` on `--bg` | 5.19 : 1 | pass |
| `--muted` on `--surface` | 4.99 : 1 | pass |
| `--teal` on `--bg` | 10.64 : 1 | pass |
| `--gold` on `--bg` | 10.63 : 1 | pass |
| `--rust` on `--bg` | 5.43 : 1 | pass |
| `--bg` on `--teal` (inverted button) | 10.64 : 1 | pass |

— Grade: **INFERRED**. Ratios are computed from the declared token values, not measured on rendered output. The inference assumes each token is used against the background paired with it here; actual rendered pairings (e.g. muted text over a gradient or an image) were not verified. No pairing computed here falls below AA.
Also: `prefers-reduced-motion` — **zero occurrences** in CSS, while the homepage runs opacity/transform transitions on 20 elements. `prefers-color-scheme` — zero occurrences; the palette is fixed dark.
— OBSERVED.

**A.4.8 Keyboard operability signals**
No skip link on any page (`skip` appears zero times in any HTML file).
`:focus` rules: **two on the homepage, zero on every other page**. Both are `border-color` changes on form inputs (`.subscribe-form input[type="email"]:focus`, `.cta-form input:focus`) — not `outline` declarations.
`outline: none` / `outline: 0`: not found. Browser default focus indicators are therefore **not suppressed**, and remain the only focus affordance for links, buttons and the FAQ accordion.
Click-only handlers: none — see §A.4.4; interactivity sits on native `<button>` elements which are keyboard-operable by default.
— OBSERVED.

**A.4.9 Forms**
Two forms, both on the homepage, both `method="POST"`.

```
<form action="https://formspree.io/f/REPLACE_WITH_YOUR_ID" method="POST">
  <label for="hero-email">Email address</label>
  <input type="email" name="email" id="hero-email" required aria-required="true"
         placeholder="your@email.com">
  <button type="submit">…</button>
</form>
```
The second form is identical with `id="cta-email"`.

Labelling: both inputs have an explicit `<label for="…">` matching the input `id`; both carry `required` and `aria-required="true"`. Labelling is correct.
**Both `action` attributes contain the literal placeholder `REPLACE_WITH_YOUR_ID`.** Neither form has a working endpoint.
Error handling: no client-side validation script, no `aria-live` region, no error container, no `novalidate`. Error surfacing is browser-native constraint validation only.
No honeypot, no `_next` redirect, no `_subject`, no CAPTCHA.
— OBSERVED (repo parse; the placeholder confirmed still live at §C.1.1).

---

## A.5 CONTENT INVENTORY

**A.5.1 Language**
`<html lang="en">` on all twelve content pages. Single language. Copy uses British spelling (`programme`, `organisation`, `localisation`) mixed with US-dollar pricing.
— OBSERVED.

**A.5.2 Page map — pages that exist**

| # | Path | `<title>` | `<h1>` | Purpose (one line) |
|---|---|---|---|---|
| 1 | `/` | InfoOnAIResources – AI Opportunity Intelligence for the Global South | What AI means for your career, your future. | Homepage: proposition, sample brief, nine category tiles, two-tier pricing, FAQ, two email captures |
| 2 | `/opportunities/` | Opportunity Database — AI Jobs, Scholarships, Programmes & Grants | Opportunity Database | Hub listing four categories and five current items |
| 3 | `/opportunities/jobs/` | AI Jobs — Verified Listings | AI Jobs | Index of three job listings |
| 4 | `/opportunities/jobs/ai-technical-lead-grit/` | AI Technical Lead — GRIT (Gender Rights in Tech) | AI Technical Lead | Detail page; external application by email |
| 5 | `/opportunities/jobs/research-engineer-domain-scaling-anthropic/` | Research Engineer, Domain Scaling — Anthropic | Research Engineer, Domain Scaling | Detail page; external application on Greenhouse |
| 6 | `/opportunities/jobs/knowledge-lawyer-ai-innovation-weightmans/` | Knowledge Lawyer, AI and Innovation — Weightmans LLP | Knowledge Lawyer, AI and Innovation | Detail page; external application on Weightmans site |
| 7 | `/opportunities/scholarships/` | Scholarships & Fellowships — Funded AI Opportunities | Scholarships & Fellowships | Index; **one** item |
| 8 | `/opportunities/scholarships/oxford-ethics-ai-accelerator-fellowship/` | Accelerator Fellowship — Oxford Institute for Ethics in AI (Closed) | Accelerator Fellowship — Institute for Ethics in AI | Detail page; marked closed |
| 9 | `/opportunities/courses/` | Courses & Programmes — AI Bootcamps, Accelerators & Certifications | Courses & Programmes | Index; **one** item |
| 10 | `/opportunities/courses/ai-impact-lab-humanitarian-supply-chain/` | AI Impact Lab: Humanitarian Supply Chain — Free 10-Week AI Programme | AI Impact Lab: Humanitarian Supply Chain | Detail page; external application |
| 11 | `/opportunities/resources/far-ai/` | FAR.AI — AI-Safety Research Nonprofit (Org Context) | FAR.AI | Employer-context page, explicitly not a job listing |
| 12 | `/deep-dives/` | Deep Dives — Long-form AI Analysis for the Global South | Deep Dives | Index; **one** item |
| 13 | `/deep-dives/glm-5-2-global-south/` | GLM-5.2: The First Open AI Model Good Enough for Daily Work — What It Means for the Global South | (same) | The property's single long-form article; 8 `h2` sections + 6-question FAQ |

Plus `/google9d706cf5c30241d2.html` (54-byte Search Console verification file, no `<title>`, no `<h1>`).
— OBSERVED (repo parse; entries 1 and 2 corroborated by live fetch, 28 Aug 2026).

**A.5.3 Page map — paths referenced but not present**

Referenced from `sitemap.xml`, `llms.txt`, navigation, or footer; no corresponding file in the deployed repository.

| Path | Referenced from | Live status |
|---|---|---|
| `/about.html` | sitemap, llms.txt, main nav (all 12 pages), footer, `BlogPosting.author.url` | **404 — OBSERVED** (fetched 28 Aug 2026) |
| `/tools/` | sitemap, llms.txt, main nav (11 pages), homepage category tile, footer | **404 — OBSERVED** (fetched 28 Aug 2026) |
| `/privacy.html` | sitemap, llms.txt, footer, hero form microcopy | **404 — OBSERVED** (fetched 28 Aug 2026) |
| `/opportunities/grants/` | sitemap, llms.txt, `/opportunities/` category card | **404 — OBSERVED** (fetched 28 Aug 2026) |
| `/contact.html` | sitemap, llms.txt, footer | 404 — INFERRED |
| `/terms.html` | sitemap, llms.txt, footer | 404 — INFERRED |
| `/brief/` | sitemap, llms.txt, homepage main nav, job-page nav | 404 — INFERRED |
| `/brief/latest` | llms.txt | 404 — INFERRED |
| `/policy/` | sitemap, llms.txt, main nav, category tile, footer | 404 — INFERRED |
| `/industry/` | sitemap, homepage main nav | 404 — INFERRED |
| `/industry/health/`, `/industry/legal/`, `/industry/finance/`, `/industry/education/`, `/industry/agriculture/` | sitemap, llms.txt | 404 — INFERRED |
| `/podcasts/` | sitemap, llms.txt, homepage category tile | 404 — INFERRED |
| `/research/` | sitemap, llms.txt, homepage category tile | 404 — INFERRED |
| `/mentors/` | sitemap, llms.txt, homepage category tile | 404 — INFERRED |
| `/advisory/` | sitemap, llms.txt | 404 — INFERRED |
| `/search?q=…` | `WebSite.potentialAction.target` (JSON-LD) | 404 — INFERRED |
| `/assets/logo.png` | `Organization.logo` | 404 — INFERRED |
| `/assets/og-image.jpg` | every `og:image`, `twitter:image`, `BlogPosting.image` | 404 — INFERRED |
| `/favicon.ico` | `<link rel="icon">` on homepage | 404 — INFERRED |

Inference basis for every INFERRED row: the file is absent from the deployed repository, GitHub Pages serves only repository contents, and four comparable paths were confirmed 404 by direct fetch.

**Counting.** The homepage's primary navigation offers seven destinations; **five of the seven resolve to 404** (`/tools/`, `/brief/`, `/industry/`, `/policy/`, `/about.html`). The homepage's nine-tile "Content categories" nav offers nine destinations; **five of nine 404** (`/tools/`, `/policy/`, `/podcasts/`, `/mentors/`, `/research/`). The homepage footer nav offers seven; **six of seven 404** (all but `/opportunities/`).
— OBSERVED (link enumeration per page) + INFERRED (404 status where not directly fetched).

**A.5.4 Where the commercial facts live, and in what form**

| Fact | Location | Machine-readable text? | In markup? |
|---|---|---|---|
| Free tier price ($0) | `/` `#tiers` | Yes | No |
| Professional tier price (from $3/mo, PPP ladder $3 / $8–12 / $12–15) | `/` `#tiers` + `/` FAQ prose | Yes | No |
| Payment methods (M-Pesa, "local mobile payment") | `/` FAQ prose only | Yes | No |
| Professional-tier launch timing ("Launching Month 4") | `/` `#tiers` | Yes — but **relative, with no anchor date** | No |
| Free-tier feature list (10 items) | `/` `#tiers` | Yes | No |
| Contact email | footer of all 12 pages; `mailto:` link; `Organization.contactPoint.email` | Yes | Yes |
| Location ("Nairobi, Kenya") | footer text; `Organization.areaServed` | Yes | Partially — as `areaServed`, not `address` |
| Phone / WhatsApp | Homepage WhatsApp link only, and it is a placeholder (§A.6) | No working value | No |
| Publication cadence ("every Monday") | `/` hero microcopy, `llms.txt` | Yes | No |
| Individual opportunity facts (deadlines, stipends, eligibility, salaries) | detail pages | Yes | Yes (`JobPosting`, `Course`) |

— OBSERVED.

**A.5.5 Last-modified signals**

| Signal | Value |
|---|---|
| Newest repository commit | 23 June 2026, 10:47 UTC |
| `sitemap.xml` `<lastmod>` range | 2026-03-21 to 2026-06-22 |
| `WebPage.dateModified` (homepage JSON-LD) | 2026-03-21 |
| `BlogPosting.datePublished` / `dateModified` | 2026-06-22 |
| `JobPosting.datePosted` (all three) | 2026-06-22 |
| `robots.txt` comment | "Last updated: March 2026" |
| Visible date text on `/` | "Weekly Intelligence Brief — Issue #1 · Week of 21 March 2026" |
| `Last-Modified` response header | NOT DETERMINABLE FROM HERE (§0.2) |

**Elapsed since last content change: 66 days** as of 28 August 2026. The homepage advertises a weekly Monday cadence and displays Issue #1 dated 21 March 2026; no Issue #2 exists on the property.
— OBSERVED.

**A.5.6 Thin and placeholder pages**
- `/opportunities/scholarships/` — index page carrying exactly one item, that item marked closed.
- `/opportunities/courses/` — index page carrying exactly one item, whose application window closed 24 July 2026.
- `/deep-dives/` — index page carrying exactly one item.
- `/opportunities/jobs/` — index page carrying three items, all three past `validThrough` or rolling.
- `/opportunities/resources/far-ai/` — single-entry section with no index page above it (no `/opportunities/resources/`).
- `/google9d706cf5c30241d2.html` — 54 bytes; no `<title>`, no `<html lang>`, no `<h1>`. Verification artifact, but crawlable.
- Homepage stat block cites four statistics with named sources ("Microsoft AI Diffusion Report, 2026"; "PwC, analysing 1 billion job ads, 2025") and two without a source ("198M internet-connected knowledge workers"; "54% … only 4% are acting").
— OBSERVED.

---

## A.6 HUMAN CONVERSION LAYER

**A.6.1 How a visitor converts**
Four mechanisms are offered on the homepage; the number that currently function is **one**.

| Mechanism | Implementation | State |
|---|---|---|
| Hero email capture | `<form action="https://formspree.io/f/REPLACE_WITH_YOUR_ID">` | **Non-functional** — placeholder endpoint. OBSERVED |
| Footer CTA email capture | identical placeholder endpoint | **Non-functional.** OBSERVED |
| WhatsApp channel | `<a href="https://wa.me/REPLACE_WITH_WHATSAPP_NUMBER?text=Subscribe">` | **Non-functional** — placeholder number. OBSERVED in repo **and confirmed present in the live fetch of 28 Aug 2026** |
| Email | `mailto:info@infoonairesources.shop` in the footer of all twelve pages | Link is well-formed. **But the domain publishes no MX record** (§A.1.3), so this address has no declared mail route on this domain. OBSERVED (DNS) |
| "Join the Waitlist" (Professional tier) | `<a href="#subscribe">` — in-page anchor to the same broken form | **Non-functional.** OBSERVED |

**A.6.2 Checkout / payment mechanics**
None implemented. No cart, no checkout, no payment provider script, no Stripe/Paystack/Flutterwave/DPO/M-Pesa Daraja integration, no `<script src>` to any payment domain. The only external hosts referenced anywhere in the property are `fonts.googleapis.com`, `fonts.gstatic.com`, `formspree.io`, `wa.me`, `schema.org`, and outbound links to `instagram.com`, `tiktok.com`, `linkedin.com`, `grit-gbv.org`, `anthropic.com`, `job-boards.greenhouse.io`, `weightmans.com`, `apply.weightmans.com`, `oxford-aiethics.ox.ac.uk`, `afp.oxford-aiethics.ox.ac.uk`, `techtotherescue.org`, `app.techtotherescue.org`, `far.ai`.
M-Pesa is named in the FAQ as available "from launch" — a stated future capability, not an implemented one.
— OBSERVED (full external-host enumeration across all repository HTML, 28 Aug 2026).

**A.6.3 Trust artifacts**

| Artifact | State |
|---|---|
| Privacy policy | Linked from footer and from hero form microcopy; **`/privacy.html` returns 404** (OBSERVED) |
| Terms of service | Linked from footer; `/terms.html` absent from repo (404 — INFERRED) |
| Returns / refunds policy | Not present, not linked. OBSERVED |
| Cookie notice / consent | None. No cookie-setting script found. OBSERVED |
| Named team / editorial identity | `Person` node "InfoOnAIResources Editorial Team" in JSON-LD; no named individual anywhere on the property. `/about.html` 404. OBSERVED |
| Registration / legal entity details | None. No company number, no registered address, no `PostalAddress`. OBSERVED |
| Testimonials / social proof | None. OBSERVED |
| Social profiles | Three URLs in `Organization.sameAs` (Instagram, TikTok, LinkedIn `/company/infoonairesources`). **None of the three is linked from any visible page** — they exist only inside JSON-LD. Whether the profiles exist was not verified. OBSERVED (absence of visible links) |
| Third-party verification | Google Search Console HTML file present (§A.2.9) |
| Editorial sourcing | Deep-dive and FAQ content names sources for most statistics; two homepage statistics carry no source (§A.5.6) |

**A.6.4 Outbound-link posture**
Every opportunity page routes application to the source organisation and says so explicitly ("you always apply on their site, never here"). `directApply: false` is set on all four `JobPosting` nodes, consistent with the prose.
— OBSERVED.

---

## A.7 REPO HEALTH

**A.7.1 Structure — `Benta-maker/inforionairesources.shop` @ `main`**
19 files, 81,016 bytes compressed.

```
CNAME                                             23 B    → infoonairesources.shop
robots.txt                                     2,061 B
sitemap.xml                                    6,644 B
llms.txt                                       8,965 B
google9d706cf5c30241d2.html                       54 B
index.html                                    60,316 B
deep-dives/index.html                          9,508 B
deep-dives/glm-5-2-global-south/index.html    30,253 B
opportunities/index.html                      12,397 B
opportunities/jobs/index.html                 11,397 B
opportunities/jobs/ai-technical-lead-grit/index.html                      18,055 B
opportunities/jobs/research-engineer-domain-scaling-anthropic/index.html  18,085 B
opportunities/jobs/knowledge-lawyer-ai-innovation-weightmans/index.html   15,556 B
opportunities/scholarships/index.html          8,830 B
opportunities/scholarships/oxford-ethics-ai-accelerator-fellowship/index.html  15,626 B
opportunities/courses/index.html               8,804 B
opportunities/courses/ai-impact-lab-humanitarian-supply-chain/index.html  15,570 B
opportunities/resources/far-ai/index.html     12,202 B
.claude/settings.local.json                      129 B
```
— OBSERVED (archive extraction, 28 Aug 2026).

**A.7.2 Build / deploy setup**
No `.github/workflows/`. No CI configuration of any kind. No build tooling, no `package.json`, no `Gemfile`, no `_config.yml`, no `.nojekyll`.
Deployment is **GitHub Pages serving the `main` branch directly**, with a custom apex domain set by the `CNAME` file.
— OBSERVED for the absence of CI and for the `CNAME` contents; **INFERRED** for "GitHub Pages, `main` branch" — the inference rests on the GitHub Pages IP addresses and the `benta-maker.github.io` CNAME target (§A.1.3) plus the presence of a root `CNAME` file. The Pages source branch/folder setting itself is NOT DETERMINABLE FROM HERE (repository Settings → Pages).

**A.7.3 How content is edited**
By hand, as raw HTML, in the repository. No CMS, no page builder, no headless content source, no data files (`.json`/`.yml`/`.md`) driving templates. Each opportunity listing is a self-contained hand-written HTML document that duplicates the site chrome — nav, footer, and the full inline `<style>` block are copied into every file, and the nav link set **differs between pages** (§C.1.6).
The presence of `.claude/settings.local.json` (permitting `gh auth`, `git --version`, `git config`) indicates the working environment is Claude Code operating on a local clone.
— OBSERVED.

**A.7.4 Commit activity**
17 entries in the commits feed for `main`. Three distinct authors: `Benta-maker`, `claude`, `Super45`.

| Date (UTC) | Author | Subject |
|---|---|---|
| 2026-06-23 10:47 | Benta-maker | Add Google Search Console verification file (#6) |
| 2026-06-23 10:47 | claude | Add Google Search Console HTML verification file |
| 2026-06-23 10:39 | Benta-maker | Add Weightmans Knowledge Lawyer (AI & Innovation) — rolling UK listing |
| 2026-06-22 13:39 | claude | Add Weightmans Knowledge Lawyer (AI & Innovation) — rolling UK listing |
| 2026-06-22 13:25 | Benta-maker | Add GRIT AI Technical Lead (urgent) + FAR.AI org-context resource (#4) |
| 2026-06-22 11:03 | claude | Add GRIT AI Technical Lead job (urgent) + FAR.AI org-context resource |
| 2026-06-22 08:47 | Benta-maker | Add opportunity listings: AI Impact Lab (open) + Oxford AI Ethics Fel… |
| 2026-06-22 07:42 | claude | (same) |
| 2026-06-22 07:21 | Benta-maker | Publish deep dive: GLM-5.2 and the Global South (#2) |
| 2026-06-22 07:18 | claude | Publish deep dive: GLM-5.2 and the Global South |
| 2026-06-22 06:46 | Benta-maker | Add external job listing: Research Engineer, Domain Scaling (Anthropi… |
| 2026-06-22 06:24 | claude | Add external job listing: Research Engineer, Domain Scaling (Anthropic) |
| 2026-03-22 16:55 | Super45 | Fix CNAME for custom domain infoonairesources.shop |
| 2026-03-22 16:54 | Super45 | Add CNAME for custom domain infoonairesources.shop |
| 2026-03-22 16:53 | Benta-maker | Update CNAME |
| 2026-03-22 16:46 | Benta-maker | Create CNAME |
| 2026-03-22 16:40 | Super45 | Initial commit - website files |

Pattern: paired `claude` authored commit → `Benta-maker` merge commit with a PR number (`#2`, `#4`, `#6`). Six PRs implied; PR numbers 1, 3 and 5 are not represented among merges in this feed.
**Two activity clusters: 22 March 2026 (scaffolding) and 22–23 June 2026 (all content). Nothing since 23 June 2026 — 66 days before this inspection.**
— OBSERVED (`commits/main.atom`, retrieved 28 Aug 2026). Note the feed returns recent entries; that this is the complete history is INFERRED from the presence of "Initial commit" as the oldest entry.

**A.7.5 In the repo but not deployed / deployed but not in the repo**
Nothing deployed that is not in the repository — the four live fetches matched repository source. Nothing in the repository that is not deployed, except `.claude/settings.local.json` (dot-directory; GitHub Pages does not serve it) and `CNAME` (consumed as configuration).
The larger gap runs the other way: **18 sitemap URLs and roughly a dozen navigation destinations have no file to serve** (§A.5.3).
— OBSERVED / INFERRED as noted.

**A.7.6 Second repository — `Benta-maker/infoonairesources-site` @ `main`**
Public, 13,811 bytes, 7 files: `index.html`, `about.html`, `contact.html`, `resources.html`, `privacy.html`, `terms.html`, `404.html`. No `CNAME` — it was deleted on 22 March 2026, the same day the current repository's `CNAME` was created.
Content generation: earlier, plainer. `<h1>` "Info on AI Resources"; a single `Organization` JSON-LD node per page; `<main>` landmark **present** on four pages (the current deployed property has none); forms posting to `mailto:info@infoonairesources.shop?subject=…`.
Commits: 19 entries, 1 October 2025 → 17 June 2026, sole author `Benta-maker`. Recent commit subjects: "Fix home page form and metadata placeholders" (16 Jun), "Fix contact form and metadata placeholders" (16 Jun), "Remove placeholder social metadata from about page" (16 Jun), "Remove placeholder social metadata from resources page" (17 Jun), "Restore external link attributes on resources page" (17 Jun).

**This repository holds working versions of four of the pages the deployed site 404s on** — `about.html`, `contact.html`, `privacy.html`, `terms.html` — plus a `404.html` and a `resources.html`. It also carries a canonical set pointing at `www.infoonairesources.shop`, matching the deployed site's canonicals.
Its last five commits (16–17 June 2026) predate the deployed repository's content burst (22–23 June 2026) by five days, and are edits to a repository that had already been undeployed for three months.
— OBSERVED (archive extraction and commits feed, 28 Aug 2026).

---

# PROPERTY B — swakaadvocates.co.ke

**Standing caveat for this entire section.** No repository was found for this property (§0.1, §B.7). The live-fetch tool returns extracted text and `<meta>`/`<link rel=canonical>` frontmatter only — not raw HTML (§0.3). Direct HTTP is blocked (§0.2). Consequently **§B.3 (structured data), §B.4 (semantic and accessibility structure) and §B.7 (repo health) are substantially NOT DETERMINABLE FROM HERE**, and are recorded as such rather than inferred. What follows is what the available instruments could actually establish.

## B.1 STACK & DELIVERY

**B.1.1 Framework / CMS**
NOT DETERMINABLE FROM HERE. No repository; no response headers (a `server` or `x-powered-by` header, or a `X-Generator` meta, would ordinarily settle this). No generator meta tag appeared in the fetched frontmatter. The URL pattern (`/publications`, extensionless, no trailing slash) and the absence of query strings or `?p=` style parameters are consistent with a static site or a framework with clean routing, but neither is diagnostic.
— Determined by: repository access (if one exists, privately), or the hosting control panel / Cloudflare dashboard.

**B.1.2 Rendering model**
Both fetched pages returned **complete content without JavaScript execution** — full hero copy, all seven practice-area descriptions, the four-item timeline, the four client segments, and the entire contact block were present. On `/publications`, all six article entries with abstracts and status labels were present.
— OBSERVED: server-rendered or static HTML for all substantive content.
Whether any content is *added* by JavaScript beyond what was returned is not determinable, but nothing evidently missing was detected — unlike Property A, where a missing copyright year exposed the JS dependency.

**B.1.3 Hosting signals**

| Record | Value | Grade |
|---|---|---|
| Nameservers | `terin.ns.cloudflare.com.`, `lorna.ns.cloudflare.com.` | OBSERVED |
| A (apex) | `104.21.48.16`, `172.67.176.1` | OBSERVED |
| AAAA (apex) | `2606:4700:3035::6815:3010`, `2606:4700:3031::ac43:b001` | OBSERVED |
| `www` — all record types | **NXDOMAIN** | OBSERVED |
| MX | `10 mx.zoho.com.`, `20 mx2.zoho.com.`, `50 mx3.zoho.com.` | OBSERVED |
| TXT | `zoho-verification=zb69655812.zmverify.zoho.com`; `google-site-verification=WzTrnx_mNJwZ8WeBrs0l3pNV7T5IqG33drRaFn_31s0` | OBSERVED |
| SPF (`v=spf1…`) | **not published** | OBSERVED |
| `_dmarc` | **NXDOMAIN** | OBSERVED |
| CAA | NoAnswer | OBSERVED |
| SOA | `lorna.ns.cloudflare.com. dns.cloudflare.com.` | OBSERVED |

`104.21.0.0/16` and `172.67.0.0/16` are Cloudflare anycast ranges; the AAAA records are in `2606:4700::/32`, Cloudflare's IPv6 range. Reverse DNS returns no PTR for either address, consistent with Cloudflare edge behaviour.
**This property is behind the Cloudflare proxy (orange-clouded).** — Grade: **INFERRED** from the anycast address ranges and absence of PTR; the inference is that only Cloudflare's edge answers on those ranges. Confirmable in the Cloudflare dashboard.

**The origin behind the proxy is completely masked.** Whether the origin is Cloudflare Pages, a Kenyan cPanel host, a VPS, or another CDN cannot be determined from outside — that is what the proxy is for.

**This is the operative structural difference between the two properties.** Property B sits inside Cloudflare's control plane — its bot rules, WAF, crawler directives, Pay-Per-Crawl posture, and the 15 September 2026 default change all apply to it. Property A does not (§A.1.3). Which Cloudflare plan, and what any of those settings currently are, is NOT DETERMINABLE FROM HERE.

**B.1.4 TLS state**
Both fetches succeeded over `https://` with no error surfaced. No CAA record is published, so certificate issuance is unconstrained at the DNS layer. Certificate issuer, chain, expiry, protocol versions, cipher suites, HSTS and OCSP stapling: NOT DETERMINABLE FROM HERE (§0.2).
— Determined by: a TLS handshake, or the Cloudflare dashboard SSL/TLS tab (which would also show the SSL mode — Flexible / Full / Full-Strict — a material setting not visible from outside).

**B.1.5 www / apex and redirect behaviour**
**`www.swakaadvocates.co.ke` does not exist in DNS. All record types return NXDOMAIN.**
There is no www hostname to redirect from. Any inbound link, citation, directory listing, business-profile entry, or printed reference using `www.swakaadvocates.co.ke` fails at resolution — before any HTTP request, before any redirect, before Cloudflare.
All canonicals, `og:url` values, and internal links observed use the bare apex `https://swakaadvocates.co.ke/`, which is internally consistent.
— OBSERVED (DNS resolution, 28 Aug 2026; canonical values from fetch frontmatter).
Apex redirect behaviour (whether `http://` → `https://`, whether trailing-slash normalisation occurs): NOT DETERMINABLE FROM HERE (§0.2). One observation: the homepage fetch reported `destination_url: https://swakaadvocates.co.ke/` and `final_url: https://swakaadvocates.co.ke` — a trailing-slash normalisation, direction unconfirmed.

---

## B.2 CRAWL & AGENT POSTURE

**B.2.1 robots.txt** — **NOT DETERMINABLE FROM HERE.** The URL could not be fetched (§0.5) and there is no repository to read it from. Presence, absence, and contents are all unknown. No inference is offered.

**B.2.2 llms.txt** — **NOT DETERMINABLE FROM HERE.** Same basis.

**B.2.3 sitemap.xml** — **NOT DETERMINABLE FROM HERE.** Same basis. No `<link rel="sitemap">` appeared in either page's frontmatter, but that element is uncommon and its absence is not evidence.

**B.2.4 `.well-known` endpoints** — **NOT DETERMINABLE FROM HERE.** Same basis. This includes any Web Bot Auth / RFC 9421 key material, `security.txt`, and payment-discovery documents.

**B.2.5 Meta robots**
**No `<meta name="robots">` tag was present in the extracted frontmatter of either fetched page.** The extractor did surface `description`, `keywords`, `viewport`, and the full `og:` set for both pages, so it is reporting meta tags it finds.
— Grade: **INFERRED** (absence of a robots meta tag). The inference is that the extractor would have surfaced a `robots` meta as it surfaced the others; it is not a raw-source observation. Default crawler behaviour in the absence of the tag is index/follow.

**B.2.6 X-Robots-Tag** — **NOT DETERMINABLE FROM HERE** (§0.2). Note this is a live question for a Cloudflare-proxied site: a header could be injected at the edge by a Transform Rule or Worker without touching the origin.

**B.2.7 Bot-management / challenge behaviour on fetch**
Both fetches (28 Aug 2026, from an Anthropic-operated fetcher) returned full page content. **No challenge, no interstitial, no Managed Challenge, no JS challenge, no block.** The site was also indexed and returned in web search results with body content, indicating at least one search crawler is being served.
— OBSERVED, with the qualification that this is a single observation from one user-agent and one network path on one date. It establishes that *this* fetcher was not challenged; it establishes nothing about other agent classes, and Cloudflare rules are frequently user-agent- and ASN-conditional.

**B.2.8 Feeds**
No `<link rel="alternate">` feed reference appeared in the frontmatter of either page. The publications page distributes via **Substack** (`https://swakaadvocates.substack.com`), which maintains its own feed on its own domain.
— INFERRED (no first-party feed on this domain); OBSERVED (Substack as the distribution channel).

---

## B.3 MACHINE-LEGIBLE LAYER

**B.3.1 Structured data (JSON-LD / microdata)** — **NOT DETERMINABLE FROM HERE.**
The fetch tool does not surface `<script type="application/ld+json">` content (§0.3) and there is no repository. Whether this site carries `LegalService`, `Attorney`, `LocalBusiness`, `ProfessionalService`, `Organization`, `Person`, `FAQPage`, `BreadcrumbList` or `Article` markup — **or no markup at all** — is unknown. This is the single largest evidentiary gap in this inventory and it is recorded as absence-of-observation, not absence-of-markup.
— Determined by: repository access, or a raw-HTML view of the served page (browser view-source, `curl`, or a structured-data testing tool run against the live URL).

**B.3.2 Meta tags — as served (OBSERVED, from fetch frontmatter, 28 Aug 2026)**

**`/` (homepage)**
| Tag | Value |
|---|---|
| `title` | Swaka Advocates \| AI-Era Legal Counsel · Nairobi, Kenya |
| `canonical` | `https://swakaadvocates.co.ke/` |
| `description` | "Swaka Advocates provides AI liability architecture, data sovereignty counsel, cybersecurity law, cross-border transaction advisory, and AI-era criminal and family law from Nairobi, Kenya. Legal architecture for enterprises, institutions, and high-net-worth individuals at the frontier of the AI transition. Established 2016." (~330 chars) |
| `keywords` | AI liability Kenya, data sovereignty lawyer Nairobi, Kenya AI Bill 2026, enterprise AI legal counsel East Africa, cross-border data partnership law, AI criminal law Kenya, cybersecurity law Kenya, Swaka Advocates, John Swaka advocate, Hurlingham Nairobi lawyer |
| `og:title` | Swaka Advocates \| AI-Era Legal Counsel · Nairobi |
| `og:description` | Legal architecture for the AI transition. AI liability, data sovereignty, cybersecurity law, and cross-border transactions from Nairobi, Kenya. |
| `og:type` | website |
| `og:url` | `https://swakaadvocates.co.ke/` |
| `viewport` | width=device-width, initial-scale=1.0 |

**`/publications`**
| Tag | Value |
|---|---|
| `title` | Publications — Swaka Advocates |
| `canonical` | `https://swakaadvocates.co.ke/publications` |
| `description` | Original analysis on AI law, data sovereignty, and the East African legal frontier from Swaka Advocates. |
| `og:title` | Publications — Swaka Advocates |
| `og:description` | Original analysis on AI law, data sovereignty, and the East African legal frontier. |
| `og:type` | website |
| `og:url` | `https://swakaadvocates.co.ke/publications` |
| `og:site_name` | Swaka Advocates |
| `viewport` | width=device-width, initial-scale=1.0 |

Observations on the meta layer:
- `<title>` and `og:title` **differ on the homepage** (the `og:title` omits ", Kenya"). They match on `/publications`.
- `og:site_name` is present on `/publications` and **absent on the homepage**.
- **No `og:image` on either page.** No `twitter:card` or any `twitter:` tag on either page. Link previews in messaging apps, Slack, LinkedIn and X will render without an image.
- No `keywords` on `/publications`; a long `keywords` list on the homepage.
- No `og:locale`, no `article:published_time` on the publications entries.
- Both canonicals are self-referential, absolute, and on the correct (apex) host.
— OBSERVED.

**B.3.3 hreflang** — none appeared in frontmatter. Single-language property. INFERRED (absence).

**B.3.4 LegalService / LocalBusiness / Attorney-class markup** — **NOT DETERMINABLE FROM HERE** (§B.3.1).

**B.3.5 Practice areas as marked up** — **NOT DETERMINABLE FROM HERE.** As *rendered text*, seven practice areas are fully articulated (§B.5.3). Whether any of them is expressed as a `Service`, `serviceType`, `hasOfferCatalog`, or `knowsAbout` value is unknown.

**B.3.6 NAP consistency (name–address–phone)**

The contact block renders these values as text:

| Field | Value as rendered |
|---|---|
| Name | Swaka Advocates |
| Primary contact | `johnswaka@swakaadvocates.co.ke` |
| Telephone 1 | `+254 703 308 873` — linked `tel:+254703308873` |
| Telephone 2 | `+254 721 476 685` — linked `tel:+254721476685` |
| Street address | Hurlingham Court, Woodlands Lane, off Argwings Kodhek Road, 1st Floor, Room 1, Nairobi, Kenya |
| Postal | P.O. Box 12803-00400, Nairobi |
| Jurisdiction | Republic of Kenya · East Africa · International |
| Established | 2016 · Admitted to the Bar 2006 |
| Regulatory | Regulated by the Law Society of Kenya; East Africa Law Society Member |

Internal consistency: the address, phones and email are stated **once**, in one block on the homepage. `/publications` carries only the email in its header. There is no second rendering of the address to conflict with — so no internal NAP inconsistency was found, because there is only one instance.
Second telephone number: `tel:+254721476685` is a link; the *displayed* text is `+254 721 476 685`. Consistent.
**Consistency between rendered text and structured markup: NOT DETERMINABLE FROM HERE** (§B.3.1) — this is precisely the check that requires seeing the JSON-LD.
Consistency against external sources (Google Business Profile, LSK directory, legal directories) was not in scope for this inventory. One stale third-party listing was encountered in search: `biz-ads.co.ke/listing/swaka-advocates/`, dated March 2023, containing Lorem-ipsum body text and a different (directory operator's) address. Its existence is OBSERVED; its content is not this property's.
— OBSERVED (fetched pages, 28 Aug 2026).

---

## B.4 SEMANTIC & ACCESSIBILITY STRUCTURE

**B.4.1 Heading hierarchy** — **PARTIALLY DETERMINABLE.**
The extractor renders heading levels it detects. On that basis:

`/` (homepage): **one `h1`** — "Law for the AI transition." Then `h2` "The legal frontier is not a technology question. It is a power question." → `h2` "Legal services for consequential matters." → seven `h3` (the numbered practice areas 01–07) → `h2` "Decision-makers operating at consequential scale." → four `h3` (client segments) → `h2` "The right matter. The right counsel."
Ordering is sane; no level skipped; one `h1`.

`/publications`: **one `h1`** — "Published thinking on AI law, data sovereignty, and the East African legal frontier." Then six `h2`, one per article, then `h2` "Subscribe to receive analysis as it is published." and `h2` "Follow on LinkedIn".
Ordering is sane.

**Content that carries no heading level:** the seven Roman-numeral service teasers in the hero band (I–VII: "AI Liability Architecture", "Data Sovereignty Counsel", "Cybersecurity Law", "AI-Era Criminal Law", "Geopolitical Transaction Counsel", "AI-Era Family Law", "High-Net-Worth Personal Architecture") render as plain text with no heading markup. Likewise the eyebrow labels ("Our Position", "Practice Areas", "The Current Moment", "Who We Serve", "Engagement", "Phase 3."), the four timeline date entries ("18 March 2026", "February 2026", "May 2026", "2026 — Active globally"), and the four client-segment tags ("Enterprise", "Cross-Border", "Institutional", "Individual").
So the **first** statement of the seven practice areas — the one at the top of the page — is unheaded; the **second** statement, further down, is the one carrying `h3`s.
— Grade: **INFERRED.** The extractor's markdown output preserves heading levels for elements it identifies as headings, and these strings appeared without heading syntax. That is strong evidence they are not `h1`–`h6`, but it is not a raw-source observation.

**B.4.2 Landmarks (`main`, `header`, `nav`, `footer`, `article`, `aside`)** — **NOT DETERMINABLE FROM HERE** (§0.3).
**B.4.3 Semantic HTML vs div-soup** — **NOT DETERMINABLE FROM HERE.**
**B.4.4 ARIA usage, roles, `tabindex`, inline handlers** — **NOT DETERMINABLE FROM HERE.**
**B.4.5 Text contrast** — **NOT DETERMINABLE FROM HERE.** No stylesheet was readable. The rendered design is evidently dark-themed, but no colour value could be extracted.
**B.4.6 Keyboard operability (focus styles, skip links)** — **NOT DETERMINABLE FROM HERE.**
— All of the above determined by: repository access or a raw-HTML/CSS view of the served pages, or an automated accessibility scan run against the live URLs (axe, Lighthouse, WAVE, or an AXTree dump from a headless browser).

**B.4.7 Images and information-in-images** — **PARTIALLY DETERMINABLE, and the finding is favourable.**
Exactly **one image** appeared in the extraction of each page: the site logo, in the header, wrapped in a link to `/`.
- On `/publications`: `![Swaka Advocates](https://swakaadvocates.co.ke/logo-dark.png)` — alt text **"Swaka Advocates"** present; source `logo-dark.png`.
- On `/`: `[![Swaka Advocates]()](https://swakaadvocates.co.ke/)` — alt text **"Swaka Advocates"** present; **source resolved to empty** in the extraction, on both `markdown` and `traf` extraction passes. This may indicate a different image mechanism on the homepage (inline SVG, `srcset`-only, CSS background with an empty `src`, or a lazy-loading placeholder). Flagged as ambiguous, not resolved.

**No other image of any kind was detected on either page.** Consequently:
**Every commercial fact on this property exists as machine-readable text.** The seven practice areas and their full descriptions; both telephone numbers; the email address; the street address and P.O. box; "Established 2016 · Admitted to the Bar 2006"; "Regulated by the Law Society of Kenya"; "East Africa Law Society Member"; the four timeline entries; the four client-segment descriptions; all six publication titles, abstracts, dates and status labels — all are text. **Nothing was found rendered only as a graphic.** No price is stated anywhere on the property, in text or otherwise (§B.5.4).
— OBSERVED (both extraction passes of both pages, 28 Aug 2026), subject to the standing caveat that the extractor reports images it identifies; a CSS `background-image` carrying text would not be visible to it.

**B.4.8 Forms** — none. Neither page contains a form. Conversion is by `mailto:` and `tel:` links only (§B.6). Nothing to label, no error handling to inspect.
— OBSERVED.

---

## B.5 CONTENT INVENTORY

**B.5.1 Language**
Content is English throughout, British/Kenyan spelling conventions (`authorisation`, `organisation`, `programme`, `defence`, `localisation`). `<html lang>` attribute: NOT DETERMINABLE FROM HERE (§0.3).
— OBSERVED (content); NOT DETERMINABLE (markup).

**B.5.2 Page map**

| # | Path | `<title>` | `<h1>` | Purpose |
|---|---|---|---|---|
| 1 | `/` | Swaka Advocates \| AI-Era Legal Counsel · Nairobi, Kenya | Law for the AI transition. | Single-page firm site: hero, seven service teasers, positioning essay, seven full practice-area descriptions, four-item market timeline, four client segments, engagement statement, contact block |
| 2 | `/publications` | Publications — Swaka Advocates | Published thinking on AI law, data sovereignty, and the East African legal frontier. | Six-item publication index; one published, five forthcoming; distribution via Substack |

**The property has two pages.** The homepage navigation offers five destinations, of which **four are in-page anchors** (`#thesis`, `#services`, `#clients`, `#contact`) and one is the only other page (`/publications`). No practice-area detail pages, no team/people page, no insights archive on-domain, no case studies, no careers page, no privacy or terms page.
Whether additional pages exist that are unlinked from these two: NOT DETERMINABLE FROM HERE (no sitemap or robots.txt readable, no repository).
— OBSERVED for what exists and is linked; NOT DETERMINABLE for what may exist unlinked.

Navigation order differs between the two pages: homepage is Practice / Services / Clients / Contact / Publications; `/publications` is Practice / Services / Clients / Publications / Contact. On `/publications` the first four nav items are absolute links back to homepage anchors (`https://swakaadvocates.co.ke/#thesis` etc.), which is correct cross-page anchor behaviour.
— OBSERVED.

**B.5.3 The seven practice areas (each stated twice)**

| # | Name | Teaser (hero band) | Full description (services section) |
|---|---|---|---|
| I / 01 | AI Liability Architecture | "Enterprise legal frameworks for the Kenya AI Bill, 2026." | Kenya AI Bill 2026 compliance; vendor contract architecture; board-level governance obligations; human rights impact assessment counsel |
| II / 02 | Data Sovereignty (Counsel / & Cross-Border Transactions) | "Cross-border AI partnerships that keep African institutions in control." | Data partnerships with Chinese firms, Gulf sovereign funds, American hyperscalers, European DFIs; data ownership, audit rights, exit terms; Kenya DPA 2019 and data localisation |
| III / 03 | Cybersecurity Law | "Incident response, regulatory compliance, and cyber insurance disputes." | 72-hour breach notification under Kenya DPA; audit preparation; cyber insurance coverage disputes; cybercrime prosecution/defence; vendor liability allocation; standing incident-response retainers |
| IV / 04 | AI-Era Criminal Law | "Serious crime where AI is the instrument, the evidence, or the question." | AI-enabled fraud, voice spoofing, synthetic identity crime; deepfake evidence under the Kenya Evidence Act and Computer Misuse and Cybercrimes Act 2018; criminal practice active since 2016 across robbery, murder, sexual offences, financial crime |
| V / 05 | Geopolitical Transaction Counsel | "Cross-border deals where capital, data, and sovereign interest converge." | Cross-border deals at the intersection of capital flows, AI infrastructure and geopolitical alignment; African institutions as strategic actors |
| VI / 06 | AI-Era Family Law | "Divorce, custody, and succession in the age of deepfakes and digital assets." | Synthetic-media authentication in matrimonial proceedings; digital asset division; custody where automated decision systems are material; succession of AI-generated IP |
| VII / 07 | High-Net-Worth Personal Architecture | "Estate, succession, and digital asset structures for significant wealth." | Post-liquidity estate and succession structure; cross-border wealth; crypto, AI-generated IP and data-asset succession; "engaged in strict confidence" |

Note the naming divergence at II: teaser reads "Data Sovereignty **Counsel**", full section reads "Data Sovereignty **& Cross-Border Transactions**".
A separately-framed eighth offering appears under "Established Practice": financial institution disputes, commercial matters, constitutional petitions, and **immigration** — the last of which appears nowhere in the seven numbered areas.
— OBSERVED.

**B.5.4 Commercial facts and their form**

| Fact | Present? | Form |
|---|---|---|
| Services offered | Yes, in depth (7 areas + established-practice list) | Machine-readable text |
| Prices / fee structure / fee basis | **Absent** — no price, no range, no hourly/retainer indication, no "fees on application" | n/a |
| Credentials | Yes: "Established 2016 · Admitted to the Bar 2006"; "Regulated by the Law Society of Kenya"; "East Africa Law Society Member"; criminal practice "active since 2016" | Machine-readable text |
| Named practitioners | **One name only**, and only via the email local-part and the LinkedIn caption: "John Swaka". No biography, no photograph, no admission number, no education, no reported matters. Homepage `keywords` includes "John Swaka advocate" | Text (incidental) |
| Team size | Absent | n/a |
| Location | Yes: full street address + P.O. box | Machine-readable text |
| Opening hours | **Absent** | n/a |
| Phone | Yes, two numbers, both `tel:`-linked | Machine-readable text |
| Consultation booking | **Absent** — no scheduler, no form, no calendar link. Engagement described as "a structured assessment" reached by contacting the firm | n/a |
| Languages of service | Absent | n/a |
| Client references / matters | Absent (consistent with the stated confidentiality posture) | n/a |

— OBSERVED.

**B.5.5 Last-modified signals**
No `Last-Modified` or `ETag` header readable (§0.2). No repository (§B.7). No `dateModified` observable (§B.3.1).
Content-internal dating:
- Footer: "© 2026 Swaka Advocates" — a **static** year, not JS-generated (it rendered in a non-JS fetch).
- The publications page dates its one published item **21 March 2026** and labels five items "Coming April 2026", "Coming April 2026", "Coming May 2026", "Coming May 2026", "Coming June 2026".
- The homepage timeline's most recent entry is May 2026 (GITEX Kenya).
- The homepage states Kenya "entered the legislative inflection point... on 18 March 2026" and that "The compliance window is open."

**As of 28 August 2026, all five "forthcoming" publication dates are past** — by roughly two to five months. The page still labels them "Forthcoming" with future-tense "Coming" dates.
— OBSERVED (fetched content, 28 Aug 2026; comparison against inspection date).

**B.5.6 Thin or placeholder content**
- `/publications` lists six items; **one is a published piece, five are unwritten**. The one published item's full text is not on this domain — the link goes to Substack.
- "Follow on LinkedIn" section: the link `href` is **`#`** — an empty anchor. The section renders with copy ("John Swaka publishes shorter observations on AI law developments...") and a call to action that goes nowhere.
- No 404 page behaviour could be tested (no known invalid path was fetchable without constructing a URL, which the tool refuses — §0.5).
— OBSERVED.

---

## B.6 HUMAN CONVERSION LAYER

**B.6.1 How a visitor contacts the firm**

| Mechanism | Implementation | State |
|---|---|---|
| Email | `johnswaka@swakaadvocates.co.ke`, rendered in the header of both pages and in the contact block | Functional. Domain publishes Zoho MX records (§B.1.3), so mail has a delivery path — **OBSERVED**, in contrast to Property A |
| Telephone (2) | `tel:+254703308873`, `tel:+254721476685` | Functional tel: links |
| Contact form | **None** | — |
| WhatsApp | **None** — no `wa.me` link, no click-to-chat | — |
| Booking / scheduler | **None** | — |
| Substack subscribe | `https://swakaadvocates.substack.com` — linked twice from `/publications` | External, off-domain |
| LinkedIn | `href="#"` | **Dead link** — OBSERVED |
| Anchor CTAs | "Explore our practice →" (`#services`), "Get in touch" (`#contact`) | In-page anchors |

**B.6.2 Checkout / payment**
Not applicable and not present. No e-commerce, no payment method, no M-Pesa, no card, no invoicing surface.
— OBSERVED.

**B.6.3 Trust artifacts**

| Artifact | State |
|---|---|
| Regulatory statement | "Regulated by the Law Society of Kenya" — present in footer of both pages. OBSERVED |
| Professional membership | "East Africa Law Society Member" — footer of both pages. OBSERVED |
| Firm age / admission | "Established 2016 · Admitted to the Bar 2006" — contact block. OBSERVED |
| Jurisdictional scope | "Republic of Kenya · East Africa · International" — contact block. OBSERVED |
| Physical address | Full street address + P.O. box. OBSERVED |
| Named advocate | "John Swaka" — only via email local-part, LinkedIn caption and meta `keywords`. No bio, no photograph, no LSK practising-certificate number. OBSERVED |
| Privacy policy | **Not present, not linked** on either page. OBSERVED |
| Terms of engagement / legal notice / disclaimer | **Not present, not linked.** OBSERVED |
| Cookie notice | None rendered. OBSERVED (subject to §0.4 — a JS-injected banner would not appear in a non-JS fetch) |
| Data-protection notice (Kenya DPA 2019) | **None**, on a site whose own practice offering includes Kenya DPA compliance counsel. OBSERVED |
| Testimonials / client names / rankings | None (consistent with stated confidentiality posture). OBSERVED |
| Published thought leadership | One article, hosted off-domain on Substack. OBSERVED |
| Copyright | "© 2026 Swaka Advocates. All rights reserved." OBSERVED |

**B.6.4 Selectivity framing**
The engagement section states the firm engages selectively, that a first conversation is "a structured assessment of whether the matter and the firm are the right fit", and that where the fit is wrong the firm will say so and where possible refer. Recorded as a stated conversion posture, not evaluated.
— OBSERVED.

---

## B.7 REPO HEALTH

**No public GitHub repository corresponds to this property.**

Evidence:
- `github.com/Benta-maker?tab=repositories` (retrieved 28 Aug 2026) lists three public repositories: `inforionairesources.shop` (HTML, updated 2026-06-23), `infoonairesources-site` (HTML, updated 2026-06-22), `telegram-transcriber` (Python, updated 2026-03-26). None relates to this property.
- GitHub repository search API for `swakaadvocates` returns `{"total_count": 0}` (28 Aug 2026).
- The live site resolves to Cloudflare anycast, not GitHub Pages addresses (§B.1.3), so it is not served from GitHub Pages in any case.

**Grade: OBSERVED as absence-of-public-record.** This is *not* a finding that no repository exists. A private repository, a repository under a different account or organisation, a non-GitHub host (GitLab, Bitbucket, self-hosted Git), or no version control at all are all consistent with this evidence. Section 0.1 records that no GitHub connector is available in this session, so private repositories are invisible from here regardless of account.

Everything else in §7 for this property — repository structure, build/deploy setup, CI, how content is edited, last commit activity, and repo-vs-deployed drift — is **NOT DETERMINABLE FROM HERE.**

---

# C. COMBINED SECTIONS

## C.1 DIVERGENCES

### Property A — repo vs live

**C.1.1 No content divergence between repository and deployed site.**
Four live fetches (`/`, `/opportunities/`, and 404 confirmations on `/tools/`, `/about.html`, `/privacy.html`, `/opportunities/grants/`) matched `Benta-maker/inforionairesources.shop` @ `main` in title, meta, canonical, navigation, headings, body copy and link targets. The repository is the deployed source and is current with it.
— OBSERVED, 28 Aug 2026.

Specifically confirmed present **on the live site**, not just in the repository:
- `https://wa.me/REPLACE_WITH_WHATSAPP_NUMBER?text=Subscribe` — the placeholder WhatsApp link is live.
- The empty copyright year (`© InfoOnAIResources.shop`) — the JS-dependent year, absent to any non-executing client.
- `www.` canonicals served on a host that redirects `www.` → apex.

The Formspree placeholder `REPLACE_WITH_YOUR_ID` sits in a `<form action>`, which the text extractor does not surface; it is OBSERVED in the repository and **INFERRED** to be live on the same basis as everything else that matched.

### Property A — internal divergences

**C.1.2 Sitemap vs deployed reality.** `sitemap.xml` declares 31 URLs; 13 exist, **18 do not**. Four confirmed 404 by fetch; 14 inferred. (§A.2.4, §A.5.3)

**C.1.3 `llms.txt` vs deployed reality.** The file describes eleven content areas — Weekly Brief, Grants, five Industry verticals, Tools, Policy, Podcasts, Research, Mentorship, Advisory, About, Contact, Privacy, Terms — of which **only the Opportunities and Deep Dives areas have any page behind them.** The AI-facing summary file is the most complete description of a site that does not exist. (§A.2.3)

**C.1.4 JSON-LD `FAQPage` vs rendered FAQ.** The homepage marks up **six** questions and renders **five**, and only one of the five matches a marked-up question even loosely.

| Rendered (visible `<button>` text) | Marked up (`FAQPage.mainEntity`) |
|---|---|
| What is InfoOnAIResources and who is it for? | What is InfoOnAIResources? |
| Are there AI scholarships currently open for African students? | Are there AI scholarships and fellowships available for African students? |
| Do I need a technical background to benefit from this platform? | What AI jobs are available for professionals in Africa? |
| How is this different from other AI newsletters? | What AI tools are available for healthcare professionals in Africa? |
| How much does the platform cost? | How does AI affect jobs in Kenya and East Africa? |
| — | What is the AI regulation situation in Africa? |

Three marked-up questions and their answers appear **nowhere on the page**. Three rendered questions appear **nowhere in the markup**.
— OBSERVED (§A.3.2).

**C.1.5 JSON-LD references to non-existent resources.** `Organization.logo` → `/assets/logo.png` (absent). `BlogPosting.image` and every `og:image`/`twitter:image` → `/assets/og-image.jpg` (absent). `Person.url` (`#editorial-team`) → `/about.html` (404, confirmed). `WebSite.potentialAction.target` → `/search?q=…` (absent). `<link rel="icon">` → `/favicon.ico` (absent).
— OBSERVED.

**C.1.6 Navigation inconsistency across pages.** The primary nav link set differs on six of the twelve content pages:

| Nav variant | Pages |
|---|---|
| `/` `/opportunities/` `/tools/` `/brief/` `/industry/` `/policy/` `/about.html` `#subscribe` | homepage |
| `/` `/opportunities/` `/tools/` `/deep-dives/` `/policy/` `/about.html` | both deep-dive pages |
| `/` `/opportunities/` `/deep-dives/` `/tools/` `/about.html` | `/opportunities/` |
| `/` `/opportunities/` `/opportunities/jobs/` `/tools/` `/brief/` `/about.html` | three job pages + FAR.AI |
| `/` `/opportunities/` `/opportunities/scholarships/` `/deep-dives/` `/about.html` | two scholarship pages |
| `/` `/opportunities/` `/opportunities/courses/` `/deep-dives/` `/about.html` | two course pages |

Every variant contains at least one 404 destination; `/about.html` appears in all six.
— OBSERVED (§A.7.3).

**C.1.7 Canonical host vs redirect target.** All twelve pages declare a `www.` canonical; the server redirects `www.` → apex. Sitemap and `robots.txt` also use `www.`. Internal `<a href>` values are root-relative and therefore resolve to whichever host was requested.
— OBSERVED (§A.1.5, §A.3.7).

**C.1.8 Repository name vs domain.** `inforionairesources.shop` vs `infoonairesources.shop`.
— OBSERVED.

**C.1.9 Two repositories, one property.** `infoonairesources-site` contains working `about.html`, `contact.html`, `privacy.html`, `terms.html`, `resources.html` and `404.html` — four of which the deployed site 404s on — and received maintenance commits on 16–17 June 2026, three months after its `CNAME` was deleted and it stopped being deployed.
— OBSERVED (§A.7.6).

**C.1.10 Advertised cadence vs published output.** The homepage advertises a weekly Monday brief; one issue exists, dated 21 March 2026; no `/brief/` path exists; last repository commit 23 June 2026.
— OBSERVED.

**C.1.11 Expired items still published as current.** GRIT (`validThrough` 26 Jun 2026), Anthropic (`validThrough` 21 Aug 2026), Oxford (`validThrough` 12 Jun 2026), AI Impact Lab (`availabilityEnds` 24 Jul 2026) are all past as of 28 Aug 2026. Only the Oxford page marks its status in title and prose; `/opportunities/` still labels the AI Impact Lab "Open · closes 24 Jul 2026".
— OBSERVED.

**C.1.12 Mail address advertised on a domain with no MX.** `info@infoonairesources.shop` appears in the footer `mailto:` of all twelve pages and in `Organization.contactPoint.email`. The domain publishes no MX record.
— OBSERVED (§A.1.3, §A.6.1).

### Property B — divergences

**C.1.13 No repo-vs-live comparison is possible** (no repository found, §B.7).

**C.1.14 `www` hostname does not exist.** NXDOMAIN on all record types. Any reference to `www.swakaadvocates.co.ke` fails at DNS.
— OBSERVED (§B.1.5).

**C.1.15 Forthcoming publications past their stated dates.** Five items labelled "Forthcoming / Coming April–June 2026" as of 28 Aug 2026.
— OBSERVED (§B.5.5).

**C.1.16 Dead LinkedIn link.** `href="#"` under a section captioned "Follow John Swaka on LinkedIn →".
— OBSERVED (§B.5.6).

**C.1.17 Homepage `<title>` ≠ `og:title`; `og:site_name` present on one page only; no `og:image` or `twitter:` tags on either page.**
— OBSERVED (§B.3.2).

**C.1.18 Practice-area naming divergence within the homepage.** "Data Sovereignty Counsel" (teaser II) vs "Data Sovereignty & Cross-Border Transactions" (section 02). "Immigration" appears in the established-practice sentence but in none of the seven numbered areas.
— OBSERVED (§B.5.3).

**C.1.19 Logo image source resolved on `/publications` (`logo-dark.png`) but empty on `/`** across both extraction methods. Cause unresolved.
— OBSERVED, unexplained (§B.4.7).

### Cross-property divergence

**C.1.20 Opposite infrastructure postures under the same DNS provider.** Both domains use Cloudflare nameservers. `swakaadvocates.co.ke` is proxied (Cloudflare anycast at the edge). `infoonairesources.shop` is unproxied (GitHub Pages addresses served directly). Cloudflare's crawler-control surface — including the 15 September 2026 default change — reaches one property and not the other.
— OBSERVED (DNS), INFERRED (proxy state) — §A.1.3, §B.1.3.

**C.1.21 Opposite crawl-directive postures.** Property A publishes an elaborate, explicitly reasoned `robots.txt` and an `llms.txt`, and blocks nine named training crawlers by name. Property B's crawl directives could not be read at all and may not exist.
— OBSERVED (A), NOT DETERMINABLE (B).

**C.1.22 Inverse content/infrastructure fit.** Property A carries dense structured data (13 pages, `JobPosting`/`Course`/`FAQPage`/`BlogPosting`/`ItemList`/`BreadcrumbList`) across a site whose navigation is mostly broken and whose conversion mechanisms are all placeholders. Property B carries complete, coherent, entirely-text commercial facts and working contact paths across a two-page site whose machine-legible layer is unknown and may be absent.
— OBSERVED / NOT DETERMINABLE as noted.

**C.1.23 Neither domain publishes SPF or DMARC.** `_dmarc` is NXDOMAIN on both; neither apex TXT set contains `v=spf1`. Property B has Zoho MX and therefore live mail flow without published sender authentication; Property A has no MX at all while advertising an address on the domain.
— OBSERVED.

---

## C.2 NOT DETERMINABLE FROM HERE — checklist of owner-supplied facts required

Grouped by the access that would resolve each item.

### C.2.1 Cloudflare dashboard — `swakaadvocates.co.ke` zone
- [ ] Confirm the apex A/AAAA records are **proxied** (orange cloud), and whether any subdomain records exist beyond apex
- [ ] Plan tier (Free / Pro / Business / Enterprise) — determines which bot and header controls are available
- [ ] **AI Crawl Control / "Block AI bots" / AI Scrapers & Crawlers** setting: on, off, or per-crawler
- [ ] **Pay Per Crawl** enrolment status and any configured price
- [ ] Bot Fight Mode / Super Bot Fight Mode state; verified-bot allowances
- [ ] WAF custom rules, rate-limiting rules, and any user-agent- or ASN-conditional logic
- [ ] Transform Rules or Workers injecting response headers (in particular any `X-Robots-Tag`)
- [ ] SSL/TLS encryption mode (Flexible / Full / Full-Strict); Always Use HTTPS; HSTS settings
- [ ] Whether Cloudflare is serving `robots.txt`, or the origin is
- [ ] Cache rules and whether HTML is cached at the edge
- [ ] **Confirm posture ahead of the 15 September 2026 default change**, and whether this zone is in scope for it
- [ ] Whether `www` should exist (currently NXDOMAIN) and whether it ever did

### C.2.2 Cloudflare dashboard — `infoonairesources.shop` zone
- [ ] Confirm the apex and `www` records are **DNS-only / unproxied** (grey cloud) — the inference at §A.1.3
- [ ] Whether making them proxied is intended, and whether GitHub Pages custom-domain HTTPS would survive it
- [ ] Whether any Cloudflare feature is currently active on this zone at all
- [ ] Why the zone publishes no MX record while the site advertises `info@infoonairesources.shop`

### C.2.3 GitHub — repository access
- [ ] **Does a repository exist for `swakaadvocates.co.ke`?** If so: where (account/org, host), and can it be connected read-only? This is the single item that would close the largest gap in this inventory
- [ ] GitHub Pages settings for `inforionairesources.shop`: source branch and folder, "Enforce HTTPS" state, custom-domain verification status
- [ ] Intended disposition of `infoonairesources-site` — archive, merge, or retain
- [ ] Full commit history beyond the ~20 entries the public Atom feed returns; whether PRs #1, #3, #5 were closed unmerged
- [ ] Whether `Super45` is a second operator account or a collaborator

### C.2.4 Hosting / origin — `swakaadvocates.co.ke`
- [ ] **What is the origin behind the Cloudflare proxy?** Cloudflare Pages, a Kenyan cPanel host (Truehost / Safaricom / HostPinnacle), a VPS, another platform
- [ ] Framework, CMS, or generator; whether there is a build step; how content is authored and published
- [ ] Origin response headers as sent (`server`, `x-powered-by`, `cache-control`, `last-modified`, `etag`, cookies)
- [ ] Whether `robots.txt`, `sitemap.xml`, `llms.txt` and `/.well-known/*` exist — and their contents
- [ ] **Raw HTML of `/` and `/publications`** — sufficient to resolve every NOT DETERMINABLE item in §B.3 and §B.4 in one step: JSON-LD presence and contents, `<html lang>`, landmark elements, ARIA, `tabindex`, focus styles, form markup, the homepage logo `src` anomaly, and the stylesheet needed for contrast computation
- [ ] Whether pages exist that are not linked from `/` or `/publications`

### C.2.5 Analytics and search consoles — both properties
- [ ] **Google Search Console** for `infoonairesources.shop` — a verification file was committed 23 Jun 2026: is the property verified, and what does Coverage report about the 18 non-existent sitemap URLs? Any manual actions?
- [ ] Google Search Console for `swakaadvocates.co.ke` — a `google-site-verification` TXT record is published: whose property, and what does it show?
- [ ] Bing Webmaster Tools status for both
- [ ] Any analytics platform on either property — none was detected in Property A's source, and none could be detected on Property B. If analytics exist on B, they are either server-side, edge-side, or JS-injected in a way the non-executing fetch did not reveal
- [ ] **Server or edge logs** — the only source that would show actual AI-agent request volume by user-agent. Neither property exposes this from outside. For Property A, GitHub Pages provides no log access at all; for Property B, Cloudflare Analytics would

### C.2.6 Third-party services and accounts
- [ ] Formspree: is there an account, and what is the real form ID that should replace `REPLACE_WITH_YOUR_ID`?
- [ ] WhatsApp: the number that should replace `REPLACE_WITH_WHATSAPP_NUMBER`, and whether a Channel or Business account exists
- [ ] Mail routing for `info@infoonairesources.shop` — currently no MX; where is this mailbox, if anywhere?
- [ ] Zoho Mail account for `swakaadvocates.co.ke` — confirm SPF/DKIM/DMARC absence is intended
- [ ] Substack (`swakaadvocates.substack.com`) — subscriber count and whether content should be syndicated back on-domain
- [ ] Social profiles asserted in Property A's `Organization.sameAs` (Instagram, TikTok, LinkedIn) — do they exist, are they active, should they be linked from visible pages?
- [ ] John Swaka's LinkedIn URL, to replace the `href="#"` on `/publications`
- [ ] Whether `/assets/logo.png` and `/assets/og-image.jpg` exist anywhere and were simply never committed

### C.2.7 Facts only the owner holds
- [ ] Property A: intended launch dates for `/brief/`, `/tools/`, `/policy/`, `/industry/*`, `/podcasts/`, `/research/`, `/mentors/`, `/advisory/`, `/opportunities/grants/` — i.e. whether the sitemap and `llms.txt` are aspirational-by-design or stale
- [ ] Property A: what "Launching Month 4" counts from
- [ ] Property A: legal entity behind `InfoOnAIResources` — registered name, jurisdiction, registration number, registered address; and whether a privacy policy and terms exist in draft
- [ ] Property A: sources for the two unsourced homepage statistics ("198M internet-connected knowledge workers"; "54% … only 4% are acting")
- [ ] Property B: LSK practising-certificate number; whether a firm profile/bio is intended
- [ ] Property B: whether a privacy policy / data-protection notice is required or intended under the Kenya DPA 2019 given the site collects no data through a form but does receive email
- [ ] Property B: revised publication dates for the five overdue "forthcoming" pieces
- [ ] Both: registrar and domain-expiry dates; who controls the Cloudflare account(s)

---

## C.3 INSPECTION DATE-STAMP

| Item | Value |
|---|---|
| **Inventory compiled** | **Friday, 28 August 2026** |
| Repository archive downloads (`inforionairesources.shop`, `infoonairesources-site`) | 28 August 2026, ~12:40 UTC |
| GitHub profile and commit-feed retrieval | 28 August 2026, ~12:44–12:46 UTC |
| DNS resolution, both domains (A, AAAA, NS, CNAME, TXT, MX, CAA, SOA, `_dmarc`, PTR) | 28 August 2026, 12:47–12:52 UTC |
| Egress-block confirmation (`x-deny-reason: host_not_allowed`) | 28 August 2026, 12:49:37–12:49:38 UTC |
| Live fetch — `https://swakaadvocates.co.ke/` (markdown and traf passes) | 28 August 2026 |
| Live fetch — `https://swakaadvocates.co.ke/publications` | 28 August 2026 |
| Live fetch — `https://www.infoonairesources.shop/` (resolved to apex) | 28 August 2026 |
| Live fetch — `https://infoonairesources.shop/opportunities/` | 28 August 2026 |
| Live 404 confirmations — `/tools/`, `/about.html`, `/privacy.html`, `/opportunities/grants/` | 28 August 2026 |
| Contrast ratios computed from declared CSS tokens (Property A) | 28 August 2026 |
| Expiry comparisons (`validThrough`, `availabilityEnds`, "Coming …" labels) evaluated against | 28 August 2026 |
| Repository state captured | `inforionairesources.shop` @ `main`, last commit 23 June 2026 10:47 UTC; `infoonairesources-site` @ `main`, last commit 17 June 2026 06:28 UTC |
| Write operations performed | **None.** No commit, branch, tag, issue, pull request, fork, star, or settings change on any repository |

---

*End of inventory. Findings only. This document records the observed state of two web properties on 28 August 2026 and makes no recommendation, ranking, or remediation proposal. Every item is graded OBSERVED, INFERRED (with the inference stated), or NOT DETERMINABLE FROM HERE (with the determining access named).*
