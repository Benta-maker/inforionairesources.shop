# IMPLEMENTATION BRIEF B — infoonairesources.shop

**Version:** 1.0
**Issued:** 2 September 2026
**Deadline anchor:** 15 September 2026 (13 days) — **and this property is outside the control plane; see §1**
**Authority:** ZAWAWI Position Analysis (P-1…P-24, H-1, H-2) and Conflict Register V1 (D-1…D-19)
**Baseline facts:** Site Inventory V1.0, 28 August 2026, Property A sections (§A.1–§A.7, §C.1.1–§C.1.12, §C.1.20–§C.1.23, §C.2)
**Deployed source:** `github.com/Benta-maker/inforionairesources.shop` @ `main` — note the repository name does not match the domain (§C.1.8)
**Execution environment:** Claude Code, operating on a local clone

> **Amended 3 September 2026.** Counts in this brief have been corrected against the repository as inspected on that date, under §0 working method clause 1 — *where the brief and the file disagree, the file is the fact*. Every correction is recorded in **`docs/zawawi/BRIEF-B-CORRECTIONS.md`** (C-1…C-13), with what the brief said, what the repository contains, and how it was counted. The corrections were accepted by Benta, convener, on 3 September 2026.
>
> **These are corrections, not decisions.** No task's scope, permission or prohibition is changed. The version as issued is preserved in git at commit `3626356`.
>
> `docs/zawawi/site-inventory-v1.md` is **not** amended — it is a dated observation record, and its internal inconsistencies are recorded in the corrections file instead.

---

## 0. INSTRUCTION HEADER — READ BEFORE ANYTHING ELSE

You are implementing decisions that have already been made. You are not deciding strategy. If a task seems to call for a judgement this brief has not made, **stop and ask**.

**Working method — read, plan, confirm, execute.**

1. **Read.** Read the current file before editing it. This brief describes the repository as inspected on 28 August 2026. Where the brief and the file disagree, the file is the fact and you report the discrepancy.
2. **Plan.** State what you will change, in which files, and why. One task at a time.
3. **Confirm.** Wait for go-ahead before executing. The site is hand-authored static HTML with the full chrome duplicated into every file (§A.7.3) — a careless find-and-replace touches thirteen documents at once.
4. **Execute.** One task, one commit.

**Commit message format — mandatory:**

```
<task-id>: <one-line description>

Implements: <ruling ID(s)>
Inventory: <finding ID(s)>
Files: <list>
Human-visible change: yes | no
ARIA added: none | <attribute> because <native element that cannot express it>
```

**Absolute rules:**

- **Never modify anything in the DO-NOT-CHANGE register (§3).**
- **Never invent a fact.** No price, date, statistic, availability claim, contact detail or source enters this site or its markup unless it is already rendered on a page or supplied by the convener in writing.
- **Never state in markup something the page does not state in text.** This is P-14 and it is the single most-violated rule on this property today — see task B-9.
- **Never cite 78.33 / 41.67 / 28.33** or write any zoom or keyboard specification from them (D-4, barred pending V-4). **Never cite a spoof rate** (D-10, barred pending CL-2). **Never cite "+115.1%" or "up to 40%"** as a rationale for any editorial change — D-6 is explicit: those are one paper appearing twice, and *"any brief citing those figures as a rationale is citing one paper twice."*
- **Do not touch DNS, Cloudflare, GitHub Pages settings or any dashboard.** Where a task concerns configuration, your output is a worksheet, not a change.
- **Do not delete content.** D-16 rules that no content is withdrawn and none is gated. Where something is stale, it is marked, not removed. Where a *reference* points at nothing, the reference goes — not the content.
- If a `PRE-TASK` item a task depends on is unanswered, mark the task **BLOCKED**. Do not improvise a value.

---

## 1. MISSION AND NON-GOALS

### Mission

This property has an unusual shape, and the shape determines the work. The inventory puts it plainly at §C.1.22: dense structured data across thirteen pages — `JobPosting`, `Course`, `FAQPage`, `BlogPosting`, `ItemList`, `BreadcrumbList` — sitting on a site whose navigation is mostly broken and whose conversion mechanisms are all placeholders.

Five of the seven main-nav destinations return 404. Six of the seven footer links return 404. Eighteen of thirty-two sitemap URLs have no file behind them. The `llms.txt` describes eleven content areas of which two exist — the inventory calls it *"the most complete description of a site that does not exist."* Both subscribe forms post to `REPLACE_WITH_YOUR_ID`. The WhatsApp link is `REPLACE_WITH_WHATSAPP_NUMBER`, and it is live. The footer advertises `info@infoonairesources.shop` on a domain that publishes no MX record.

So the mission is not to add a machine layer. It is to **make the existing declarations true**, and only then to extend them.

Three things:

1. **Close the gap between what this property tells machines and what it actually serves.** Every false declaration is an active liability under D-9 and P-14, and repairing them costs nothing but attention.
2. **Repair the conversion mechanisms**, because a discovery layer feeding a broken funnel is wasted work.
3. **Serve as the programme's control case across 15 September.** This property is DNS-only (unproxied) — the records resolve directly to GitHub Pages anycast addresses, so Cloudflare's bot management, WAF, crawler controls and the 15 September default change are **outside its path entirely** (§A.1.3, §C.1.20). D-5 confirms the concession *"binds swakaadvocates.co.ke and does not bind infoonairesources.shop."* That makes this the paired comparison's control arm, which is a reason to observe it carefully and not to change its infrastructure before the date.

### One decision the convener should see clearly before work starts

The current `robots.txt` blocks nine named training crawlers — `GPTBot`, `ClaudeBot`, `Google-Extended`, `CCBot`, `Bytespider`, `meta-externalagent`, `omgili`, `omgilibot`, `FacebookBot` — with a comment reading *"Our content is original human intelligence — not available for training."*

**D-1 rules CONCEDE and it is final.** Both properties admit both audiences. The council *"stops spending on the attempt"*: no robots.txt engineering aimed at splitting training from search, and no Google-Extended posture presented as a strategic choice. The reasoning is the corpus's best-corroborated finding, at three independent instrument classes: Googlebot unification means publishers cannot refuse AI-feature use without losing search visibility; mixed-use crawlers are judged most-restrictive-wins, so blocking Training also blocks Googlebot, Applebot and Bingbot; and the EPC complaint alleges the opt-out is coercive precisely because refusing ingestion costs search visibility.

What is conceded is stated precisely by the ruling: *"the property has lost the ability to price or refuse training ingestion as a condition of human discovery, and that loss was effected by a party with no relationship to either the property or its clients."*

Task B-2 removes those blocks. **This is a real trade and the convener should agree to it knowingly.** If the convener chooses to keep the blocks, that is an override of a final ruling and it must be recorded as one — see OPEN DECISION OD-L.

### Non-goals — do not build these

| Not doing | Because |
|---|---|
| Cart, checkout, payment integration, agentic checkout | D-11: *"Build nothing on the completion side."* The honest write-task ceiling is 46.6% and its extension to checkout is an inference, not a measurement; no production agentic-checkout conversion rate exists anywhere in public. P-16 places agent transaction out of scope for 2026. |
| M-Pesa Daraja or any payment rail integration | D-15 HELD on V-18 — the mandate mechanism is unverified against primary Safaricom documentation. D-11 and P-15 have already adopted human completion, so the absence binds nothing now, *"but that is a coincidence of posture, not a discharge."* |
| Product feed, Merchant Center feed, `/.well-known/ucp`, Universal Cart attributes | D-11 authorises feed correctness only where a commerce gate demands it; this property sells no product through a feed. D-12: the sitemap/feed bifurcation that already exists is **unmeasured**, and the council *"commissions measurement of it rather than authorising a build on top of it."* |
| WebMCP, capability endpoints, any second machine-facing surface | D-12: pattern conceded as rational for an operator whose customers are the AI industry, **not adopted for either property**. One surface, two legibilities. |
| Signed crawler identity / Web Bot Auth | D-10, CONCEDE this cycle. |
| HTTP 402 / Pay Per Crawl | P-11 carried 7–4, confidence LOW. And moot: unproxied. |
| Proxying this property through Cloudflare | OPEN DECISION OD-A. **Not before 15 September under any circumstances** — it would destroy the control case D-5 authorises. |
| New content areas — `/brief/`, `/tools/`, `/policy/`, `/industry/*`, `/podcasts/`, `/research/`, `/mentors/`, `/advisory/` | Content production is not this brief. What this brief does is stop the site declaring them. |
| Off-site mention-building, seeded citations, distributed brand mentions | P-20: manufacturing is refused. Test: *would the statement be true and attributable if a human read it?* |
| Any editorial change justified by GEO lift figures | D-6, S-5: the ~40% and +115.1% figures are one unreplicated KDD 2024 paper appearing twice. Only zero-regret components are authorised, and they are authorised at P-13 level 1 regardless of the lift. |

---

## 2. PRE-TASK CHECKLIST — CONVENER-SUPPLIED FACTS AND ACCESS

### Blocking the most work

- [ ] **P-1. Which of the eighteen phantom paths are real commitments, and when?** `/brief/`, `/brief/latest`, `/tools/`, `/policy/`, `/industry/` and its five verticals, `/podcasts/`, `/research/`, `/mentors/`, `/advisory/`, `/opportunities/grants/`, `/about.html`, `/contact.html`, `/privacy.html`, `/terms.html`, `/search`. Inventory §C.2.7 asks whether the sitemap and `llms.txt` are aspirational-by-design or stale. **For each: launching within 30 days, launching later, or not launching.** Anything not launching within 30 days comes out of the sitemap, `llms.txt` and navigation now, and goes back in when it ships. *This single answer unblocks B-4, B-5, B-6 and B-7.*
- [ ] **P-2. Formspree form ID** — the real value replacing `REPLACE_WITH_YOUR_ID`, or a decision to use a different provider, or a decision to remove the forms. Both homepage forms are non-functional (§A.4.9, §A.6.1).
- [ ] **P-3. WhatsApp number** replacing `REPLACE_WITH_WHATSAPP_NUMBER` — or a decision to remove the link. It is live on the production site today (§C.1.1).
- [ ] **P-4. Mail routing for `info@infoonairesources.shop`.** The domain publishes no MX record while thirteen pages advertise the address in a `mailto:` and the `Organization.contactPoint.email` asserts it (§C.1.12). Either mail is configured, or the address comes off the site. There is no third option.

### Repository and deployment (§C.2.3)

- [ ] **P-5.** GitHub Pages settings for `inforionairesources.shop`: source branch and folder, "Enforce HTTPS" state, custom-domain verification status. Inventory grades "GitHub Pages, `main` branch" as INFERRED (§A.7.2).
- [ ] **P-6. Disposition of the second repository** `Benta-maker/infoonairesources-site` — archive, merge or retain? It holds **working versions of four pages the deployed site 404s on**: `about.html`, `contact.html`, `privacy.html`, `terms.html`, plus `404.html` and `resources.html` (§A.7.6, §C.1.9). Are these to be ported? See OPEN DECISION OD-G.
- [ ] **P-7.** Is `Super45` a second operator account or a collaborator? (§A.7.4)

### Cloudflare zone — `infoonairesources.shop` (§C.2.2)

- [ ] **P-8.** Confirm the apex and `www` records are DNS-only / unproxied (grey cloud). Inventory grades the unproxied conclusion INFERRED and confirmable only in the dashboard (§A.1.3). **This confirmation is deadline-relevant**: the entire control-case design rests on it.
- [ ] **P-9.** Is any Cloudflare feature currently active on this zone at all?
- [ ] **P-10.** Why does the zone publish no MX? (Same question as P-4, from the DNS side.)

### Commercial and legal facts (§C.2.7)

- [ ] **P-11. What does "Launching Month 4" count from?** The tier block states it as a relative date with no anchor (§A.5.4).
- [ ] **P-12. Is M-Pesa live, or still "from launch"?** The FAQ names it as available from launch — a stated future capability, not an implemented one, and no payment integration exists (§A.6.2). This determines whether task B-12 may express a payment method in markup at all. See OPEN DECISION OD-H.
- [ ] **P-13. Legal entity behind InfoOnAIResources** — registered name, jurisdiction, registration number, registered address. Currently none exists anywhere on the property (§A.6.3).
- [ ] **P-14. Sources for the two unsourced homepage statistics**: "198M internet-connected knowledge workers" and "54% … only 4% are acting" (§A.5.6). Four other statistics on the same block carry named sources.
- [ ] **P-15.** Do the three social profiles asserted in `Organization.sameAs` (Instagram, TikTok, LinkedIn) exist and are they active? None is linked from any visible page — they exist only inside JSON-LD (§A.6.3).
- [ ] **P-16.** Do `/assets/logo.png` and `/assets/og-image.jpg` exist anywhere and were simply never committed? The `assets/` directory does not exist in the repository, yet every `og:image`, every `twitter:image`, the `BlogPosting.image` and `Organization.logo` reference it (§C.1.5).

### Content currency

- [ ] **P-17.** The three job listings and the course are all past their closing dates (§C.1.11). Should they be marked closed, or have any been renewed?
- [ ] **P-18.** The homepage advertises a weekly Monday brief; one issue exists, dated 21 March 2026 (§C.1.10). Is the cadence claim still accurate, or does the copy change?

### Measurement (§C.2.5)

- [ ] **P-19. Google Search Console** — the verification file was committed 23 June 2026. Is the property verified, and what does Coverage report about the eighteen non-existent sitemap URLs? Any manual actions?
- [ ] **P-20.** Confirm what the convener already knows: GitHub Pages provides **no log access at all**. This is not a gap to close; it is a finding to record. P-22's African-test amendment governs.

---

## 3. DO-NOT-CHANGE REGISTER

| # | Protected | Authority |
|---|---|---|
| **DNC-1** | **The design tokens and the dark palette.** `--bg #080a0e`, `--surface #0d1017`, `--text #eef0f3`, `--muted #7a8394`, `--teal #2dd4bf`, `--gold #f0b429`, `--rust #e05c3a`. Every computed pairing passes WCAG AA (§A.4.7). Do not "improve" contrast that already passes. | D-14 KEEP; §A.4.7 |
| **DNC-2** | **The homepage `<h1>` and the editorial voice throughout.** D-6 rules the dual layer **rhetorical, not technical** — one document, two registers, the voice written around the factual spine. The voice is not the machine layer's to trade. | D-6; §A.4.1 |
| **DNC-3** | **The stated prices and the PPP ladder as values**: "$0 — always free"; "From $3/month — PPP pricing applies"; "from $3/month in Africa and India, $8–12/month in the Gulf, and $12–15/month for diaspora readers in the US and UK". Task B-12 wraps these in markup. It does not alter, round, normalise or restate them. | §A.3.9; DNC-8 |
| **DNC-4** | **The outbound-application posture** — "you always apply on their site, never here" — and `directApply: false` on all four `JobPosting` nodes. Prose and markup agree; keep them agreeing. | §A.6.4 |
| **DNC-5** | **The zero-image property.** There are no `<img>`, `<picture>`, `<video>`, `<iframe>` or `<canvas>` elements anywhere, so **no commercial fact is trapped in an image** (§A.4.5). Do not introduce any element that carries a fact as pixels. | D-4 (severed, ruled component) |
| **DNC-6** | **The FAQ accordion mechanics.** Built on real `<button>` elements with `aria-expanded`/`aria-controls` maintained in the handler; zero inline event handlers; zero `tabindex`; no `role="button"` on a `<div>`. This is the pattern D-17 ratifies. | **D-17 (binding)**; §A.4.4 |
| **DNC-7** | **The absence of testimonials and social proof.** Do not add, do not fabricate, do not markup. | §A.6.3; D-18 |
| **DNC-8** | **All existing content.** No article, listing, page or section is deleted. Stale items are **marked**, not withdrawn. | **D-16: no content is withdrawn, none is gated** |
| **DNC-9** | **The one-`h1`-per-page, no-skipped-levels heading structure** already present on all thirteen content pages (§A.4.1). Task B-13 adds landmarks; it does not restructure headings. | D-17; §A.4.1 |
| **DNC-10** | **The proxy state.** Do not proxy this zone before 16 September. It is the control case. | D-5; §C.1.20; OD-A |

---

## 4. TASK LIST — ORDERED

**⏰** = deadline-critical.

---

### ⏰ B-1 — External observation (shared instrument with Brief A)

**Objective.** Observe this property's crawl posture across 15 September as the unproxied control arm.

**Traces to.** P-23 clause 2; D-5, which authorises the paired observation as *"the programme's only natural experiment"*; §C.1.20.

**Change specification.** **This is task A-1 in Brief A and it is one instrument, not two.** The script covers both properties in a single log. Do not build a second one. If A-1 is already running, this task is complete — record that fact and move on.

The point of including this property is precisely that nothing should change for it. If a change appears here across the boundary, whatever caused it was not the Cloudflare default flip, because this property is not behind Cloudflare's edge.

**Acceptance criteria.** As A-1, with the additional check that the four `infoonairesources.shop` URLs appear in every daily file.

---

### ⏰ B-2 — Rewrite `robots.txt`

**Objective.** Bring the property's crawl directives into line with a final ruling.

**Traces to.** **D-1, CONCEDE, final** — see §1 above for the full reasoning and the trade it involves. **P-8** — *"In the interim the publisher reserves rights in machine-readable form without enforcing at the door."* **D-9, ADAPT** — every machine-facing signal authored, and the human-readable equivalent published on the same property.

**Depends on.** Convener's knowing agreement (see OD-L). Nothing else.

**Files affected.** `robots.txt` (2,061 B at repository root).

**Change specification.** Replace the entire file with:

```
# infoonairesources.shop — robots.txt
# Authored decision, <date>. Rulings: D-1 (both audiences admitted; the property
# does not attempt to split training from search), P-8 (rights reserved in
# machine-readable form, not enforced at the door), D-9 (every machine-facing
# signal authored by a human decision).
#
# Rights reservation: the publisher reserves its rights in the content of this
# site. This is a claim-preserving statement, not an access control, and it is
# not represented as enforceable. Human-readable equivalent: /terms.html
#
# Previous version (March 2026) blocked nine named training crawlers. Those
# blocks are removed under D-1: blocking training crawlers also blocks Googlebot,
# Applebot and Bingbot under most-restrictive-wins, so the block cost search
# visibility without achieving the refusal it intended.

User-agent: *
Allow: /

Sitemap: https://infoonairesources.shop/sitemap.xml
```

Note the `Sitemap:` host: **apex, not `www.`** — see B-3.

**Acceptance criteria.**
1. Zero occurrences of `Disallow` in the file.
2. Zero per-crawler `User-agent:` stanzas — exactly one, `*`.
3. Exactly one `Sitemap:` line; its host has no `www.` prefix; the URL returns 200.
4. The comment block names D-1, P-8 and D-9 and carries a date.
5. `docs/machine-layer-changelog.md` has an entry for this change naming the convener as the deciding party.
6. The `/terms.html` reference is live **only if** `/terms.html` returns 200 — otherwise the reference line is omitted until B-7 lands.

---

### ⏰ B-3 — Correct the canonical host across the property

**Objective.** Stop the site declaring a canonical host that the server redirects away from.

**Traces to.** Inventory §C.1.7, §A.1.5, §A.3.7: every `<link rel="canonical">`, every `og:url`, every sitemap `<loc>` and the `robots.txt` Sitemap line specify the `www.` host — *"the host the server redirects away from."* P-13 level 1 (configuration hygiene). P-15 (retrievability is part of the thin common core).

**Files affected.** All thirteen content HTML files, `sitemap.xml`, `robots.txt`, and the JSON-LD blocks within those files.

**Change specification.** Replace every occurrence of `www.infoonairesources.shop` with `infoonairesources.shop`. This affects canonicals, `og:url`, JSON-LD `url` and `@id` values, the `WebSite.potentialAction.target`, and every sitemap `<loc>`.

Do this as a single mechanical pass, then **read every changed file** to confirm nothing else moved. The site chrome is duplicated across thirteen files (§A.7.3), so a global replace is correct here — but verify it.

> **Verified fact, 3 September 2026 (BRIEF-B-CORRECTIONS C-7).** `https://www.infoonairesources.shop/` returns **HTTP 301** to the apex host. Inventory §A.1.5 graded this status code NOT DETERMINABLE. This does not change the task; it removes the doubt about why it matters — the property declares a canonical host from which the server permanently redirects away.
>
> **Method note, 3 September 2026.** This machine has `core.autocrlf=true`: the HTML files, `robots.txt` and `sitemap.xml` are **CRLF in the working tree, LF in the repository**. The mechanical pass must preserve working-tree line endings, or acceptance criterion "confirm nothing else moved" cannot be satisfied — every line of every file would show as changed. Git configuration is not to be altered.

**Acceptance criteria.**
1. `grep -rc 'www\.infoonairesources\.shop' .` returns 0 across the entire repository.
2. Every page's canonical is self-referential, absolute, and on the apex host.
3. Each `@id` value that was previously referenced by another node still resolves within its graph — no dangling `@id` references introduced.
4. Live check after deploy: fetching any page returns a canonical matching its own final URL.

---

### ⏰ B-4 — Make `sitemap.xml` true

**Objective.** A sitemap that lists only URLs that exist.

**Traces to.** Inventory §C.1.2, §A.2.4: thirty-two URLs declared, thirteen HTML pages exist, **eighteen do not**, and one entry (`/llms.txt`) is a non-HTML resource; four confirmed 404 by direct fetch. D-9: author every machine-facing signal or emit none. P-13 level 1. P-14 (admissibility: the machine layer is a projection of the human page).

**Depends on.** P-1.

**Files affected.** `sitemap.xml`.

**Change specification.**
- One `<url>` entry per file that exists in the repository and serves HTML. Currently that is fourteen — thirteen content pages plus the Search Console verification file, and **the verification file should be excluded** (54 bytes, no `<title>`, no `<h1>`, §A.5.6).
- **Remove the `llms.txt` entry** — a non-HTML resource listed as a crawlable page (§A.2.4).
- Remove all eighteen phantom entries. When a page ships, it is added back in the same commit that ships it.
- `<lastmod>`: use the real git commit date of each file. Do not carry forward `2026-03-21` values that no longer describe anything.
- Keep `<changefreq>` and `<priority>` or drop them; both are ignored by major consumers. Dropping them is cleaner and is a valid byproduct of this pass.

**Acceptance criteria.**
1. Every `<loc>` corresponds to a file present in the repository. Write this as `tools/verify-sitemap.py` and add it to the verification suite.
2. Count of `<url>` elements equals count of served content pages exactly.
3. No `<loc>` names a `.txt`, `.xml` or other non-HTML resource.
4. Every `<lastmod>` is a real commit date for that file.
5. XML validates against sitemaps.org 0.9.

---

### ⏰ B-5 — Make `llms.txt` true, or remove it

**Objective.** Resolve the property's most conspicuous false machine-facing declaration.

**Traces to.** Inventory §C.1.3, §A.2.3: the file describes eleven content areas of which only Opportunities and Deep Dives have any page behind them — *"the AI-facing summary file is the most complete description of a site that does not exist."* **D-9, ADAPT: "Author every machine-facing signal or emit none. No plugin stubs, ever."** P-13 level 3: specification without consumer, built only where marginal cost is near zero **and** the artifact is a byproduct of level 1 or 2 work — never as primary spend. D-12: the smallest bifurcation already present is unmeasured.

**Depends on.** P-1.

**Files affected.** `llms.txt` (8,965 B).

**Change specification.** The file already exists, so the question is not whether to build one but whether to keep one that is false.

**Default: rewrite to match reality exactly.** Every section and every linked path must correspond to a page that returns 200 — which is the same truth set B-4 establishes for the sitemap, making this a genuine byproduct of level-1 work and therefore permissible under P-13 level 3. Do not expand it. Do not add sections for content that does not exist. Do not describe planned areas in future tense.

**Alternative, if the convener prefers:** delete the file. P-13 level 3 does not require its existence, and D-9 permits "emit none" as an equally valid answer to "author every machine-facing signal or emit none." Record whichever is chosen and why.

**Acceptance criteria.**
1. Every path appearing in `llms.txt` also appears in `sitemap.xml` — set equality, checked by script.
2. Every such path corresponds to a file in the repository.
3. Zero future-tense descriptions of content that does not exist.
4. The file's header records the authoring decision and its date.
5. If deleted: the deletion is recorded in the changelog citing D-9 and P-13(3), and no remaining file references it.

---

### ⏰ B-6 — Repair navigation

**Objective.** Stop sending every visitor and every crawler into 404s.

**Traces to.** Inventory §A.5.3: *"The homepage's primary navigation offers seven destinations; five of the seven resolve to 404. The homepage's nine-tile 'Content categories' nav offers nine destinations; five of nine 404. The homepage footer nav offers seven; six of seven 404."* §C.1.6: six distinct nav variants across thirteen pages, *"every variant contains at least one 404 destination; `/about.html` appears in all six."* P-13 level 1. P-15 (retrievability).

> **Verified fact, 3 September 2026 (BRIEF-B-CORRECTIONS C-3).** The seven-link **footer navigation exists only on `index.html`**. The footers of the other twelve content pages carry the `mailto:info@infoonairesources.shop` address and no navigation links. So specification item 3 below is a single-file edit, while items 1–2 are a thirteen-file edit. Do not expect to find a footer nav to repair on the other twelve.

**Depends on.** P-1, and P-6 if pages are being ported.

**Files affected.** All thirteen content HTML files.

**Change specification.**
1. Define **one** canonical navigation link set, containing only destinations that return 200 after B-7 lands.
2. Apply it identically to all thirteen files. The current six-variant divergence is an artifact of hand-copying chrome (§A.7.3) and has no design intent behind it.
3. Same for the footer nav and the nine-tile category nav on the homepage: remove tiles whose destination does not exist. **Do not stub them with placeholder pages** — that trades a 404 for a thin page, which is worse.
4. Preserve the breadcrumb `<nav>` elements and their `aria-label`s (§A.4.2). They are correct.

**Acceptance criteria.**
1. The set of primary-nav `href` values is byte-identical across all thirteen files.
2. Every `href` in every nav resolves to a file in the repository, or to an in-page anchor whose `id` exists on that page.
3. Zero occurrences of `/tools/`, `/brief/`, `/industry/`, `/policy/`, `/podcasts/`, `/research/`, `/mentors/`, `/advisory/` in any nav, unless that path now has a file.
4. Every `<nav>` retains a distinct `aria-label`.

---

### B-7 — Restore or de-reference the missing standard pages

**Objective.** Resolve `/about.html`, `/contact.html`, `/privacy.html` and `/terms.html`, which the site links to from every page and which all 404.

**Traces to.** Inventory §C.1.9: the second repository `infoonairesources-site` *"holds working versions of four of the pages the deployed site 404s on"* and received maintenance commits on 16–17 June 2026, three months after it stopped being deployed. §A.6.3: the privacy policy is linked from the footer **and from the hero form microcopy** — so the site asks for an email address and points at a policy that does not exist. §C.1.5: `BlogPosting.author.url` and the `Person` node both point at `/about.html`.

**Depends on.** P-6 (disposition of the second repo) and OD-G.

**Change specification.** Two routes; the convener picks.

**Route 1 — port.** Copy `about.html`, `contact.html`, `privacy.html`, `terms.html` and `404.html` from `infoonairesources-site` into the deployed repository. Re-chrome them to match the current design (nav, footer, inline style block) so they are not visibly from an older generation. Update their canonicals to the apex host. Add them to `sitemap.xml`. **Review the privacy text against the actual data flows before publishing it** — it was written for a different form implementation and the current forms post to Formspree.

**Route 2 — de-reference.** Remove every link to all four from nav, footer, form microcopy and JSON-LD. This means the site stops offering a privacy policy while collecting email addresses, which is a worse position than Route 1 and should be chosen only as a temporary state with a date attached.

Either route: the `404.html` from the second repository should be ported regardless. A custom 404 costs nothing and the site currently has none.

**Acceptance criteria.**
1. For each of the four paths: it returns 200, **or** `grep -r` finds zero references to it anywhere in the repository including JSON-LD.
2. `BlogPosting.author.url` and the `Person` node `url` resolve to 200 or the property is removed.
3. Hero form microcopy references a privacy policy only if one exists.
4. `404.html` exists at repository root.

---

### ⏰ B-8 — Repair the conversion mechanisms

**Objective.** Make it possible for a person who wants to subscribe to actually subscribe.

**Traces to.** Inventory §A.6.1: four mechanisms offered, **one functions**. Both forms carry `REPLACE_WITH_YOUR_ID`; the WhatsApp link carries `REPLACE_WITH_WHATSAPP_NUMBER` and is confirmed live in production (§C.1.1); the `mailto:` address has no MX route (§C.1.12); "Join the Waitlist" anchors to the same broken form. D-3 (contact among the facts a description must carry). P-16 (the destination's retained functions are verification and **completion**). P-13 level 1.

**Depends on.** P-2, P-3, P-4.

**Files affected.** `index.html`; DNS for the MX half (convener action).

**Change specification.**
1. Replace both `REPLACE_WITH_YOUR_ID` values with the real Formspree endpoint (P-2). Add a `_next` redirect to a thank-you state and a honeypot field. Add an `aria-live` region for success and error messaging — the forms currently have none (§A.4.9).
2. WhatsApp (P-3): insert the real number, **or remove the link entirely**. Do not leave a placeholder in production for one more day.
3. Email (P-4): either MX records are published for the domain, or `info@infoonairesources.shop` is removed from the footer of all thirteen pages **and** from `Organization.contactPoint.email`. An advertised address that cannot receive mail is a broken promise in the one place a machine will most reliably extract and repeat it.
4. Preserve the existing correct labelling: explicit `<label for>`, `required`, `aria-required` (§A.4.9). Do not regress it.

**Acceptance criteria.**
1. `grep -rc 'REPLACE_WITH' .` returns 0 across the repository.
2. A live test submission through each form arrives at the configured destination.
3. If `info@` is retained, `dig MX infoonairesources.shop` returns at least one record; if it is removed, `grep -rc 'info@infoonairesources\.shop' .` returns 0.
4. Both forms retain `<label for>` matching the input `id`, `required` and `aria-required`.
5. No ARIA attribute added beyond the `aria-live` region, which is justified in the commit body as a case where no native element expresses the semantics (D-17).

---

### B-20 — Build the machine-layer generator

*Numbered late, executes early. Appended rather than renumbered, per the Conflict Register's principle that traceability outranks tidy sequence. **This task runs before B-9, B-11 and B-12, and all three depend on it.***

**Objective.** Make the structured data a derived artifact of the page rather than a second copy of it maintained by hand.

**Traces to.** **P-14**, verbatim: *"the machine layer is a projection of the human page rather than a parallel artifact… Test of admissibility: if a human-facing edit does not propagate automatically, the artifact is a liability and is refused."* Also D-3 (the property as the highest-quality source for its own description) and OPEN DECISION OD-J, as revised.

**Why this exists.** Inventory §C.1.4 is the proof. The homepage carries six marked-up FAQ questions and renders five, and *"three marked-up questions and their answers appear nowhere on the page; three rendered questions appear nowhere in the markup."* Nobody edited the markup incorrectly. The page changed and the markup did not, because nothing connected them. A generator connects them, and that divergence becomes impossible rather than merely detectable.

**Files affected.** New: `tools/generate-machine-layer.py`, `data/declared-values.json`, `tools/verify-jsonld-verbatim.py`. Then, on each run, the JSON-LD blocks inside the thirteen content HTML files.

**Change specification.**

**Part 1 — the extractor.** A script that parses each content page's rendered HTML and pulls the facts out of the page itself:

| Extracted from the page | Feeds |
|---|---|
| The five FAQ `<button>` texts and their `.faq-answer` bodies | `FAQPage.mainEntity` |
| The `#tiers` block — tier names, price strings, feature lists | `Service` / `Offer` price values |
| The FAQ price-ladder prose | `PriceSpecification` entries |
| Footer contact email and location text | `Organization.contactPoint` |
| Each detail page's `<h1>`, dates, organisation names, location strings | `JobPosting` / `Course` fields |
| Page `<title>`, `<h1>`, meta description | `WebPage`, `BreadcrumbList` |

**Part 2 — the declared-values file.** A small JSON file holding only what cannot be read off a page: `@type` choices, `addressCountry: "KE"`, `@id` URI patterns, `inLanguage`, `foundingDate` normalised from "Established 2025", and the mapping from a rendered region label ("Africa and India") to an `eligibleRegion` value. **Keep this file under about twenty entries.** Every entry is a fact stated in one place and nowhere else, and each one is a small standing drift risk — so each needs a one-line comment saying which rendered string it corresponds to, or a note that it corresponds to none.

**Part 3 — the writer.** Replaces the `<script type="application/ld+json">` block in each page with the generated graph. Idempotent: running it twice on an unchanged page produces a byte-identical file. It must not touch anything outside that script block.

**Part 4 — the verifier.** `tools/verify-jsonld-verbatim.py`, as previously specified: every string-valued leaf in the generated graph appears verbatim in the rendered text of the same page, except values sourced from `data/declared-values.json`, which are checked against that file instead. Every URL-valued leaf resolves to a repository file or an external 200.

**Operating discipline.** After this task, **no JSON-LD block is edited by hand on this property, ever.** To change what the markup says, change what the page says and re-run the generator. If a needed fact cannot be produced that way, that is a signal the page should state it — which is exactly the outcome P-14 is designed to force.

**Acceptance criteria.**
1. `python tools/generate-machine-layer.py` runs clean across all thirteen pages.
2. Idempotence: running it twice produces zero diff on the second run.
3. `python tools/verify-jsonld-verbatim.py` exits 0.
4. **Drift test:** change one FAQ answer's rendered text, re-run the generator, and confirm the corresponding `Answer.text` changed to match. Then revert both. Record the test output in the commit body — this is the evidence that P-14's propagation requirement is met rather than substituted for.
5. `data/declared-values.json` has at most 20 entries, each with a comment naming its rendered counterpart or stating there is none.
6. Rendered page output is byte-identical before and after, except inside the JSON-LD script blocks.
7. `docs/machine-layer-changelog.md` records the generator's adoption, citing P-14 and OD-J.

---

### B-9 — Reconcile the FAQ markup with the rendered FAQ

**Objective.** Stop asserting to machines six questions and answers, three of which appear nowhere on the page.

**Traces to.** **This is a direct P-14 violation and the clearest one on either property.** P-14: *"No fact may appear in the machine layer that is not also stated as text on the human page. Test of admissibility: if a human-facing edit does not propagate automatically, the artifact is a liability and is refused."* Inventory §C.1.4: the homepage marks up six questions and renders five; *"three marked-up questions and their answers appear nowhere on the page; three rendered questions appear nowhere in the markup."* D-3 (the property as the highest-quality source for its own description — currently it is a source for a description of itself that is partly fictional).

**Files affected.** `index.html` (the `@graph` block, 7,797 chars).

**Depends on.** B-20. **This task is now executed by running the generator, not by hand-editing the graph.**

**Change specification.** Run `tools/generate-machine-layer.py`. It extracts the five rendered questions and their answer bodies from the page and writes the `FAQPage.mainEntity` array from them. The six-versus-five divergence resolves as a consequence, and cannot recur.

Do not hand-write the corrected array. If the generator produces something wrong, fix the generator — the hand-edit is the failure mode this whole approach exists to remove.

The three orphaned marked-up answers (on AI jobs in Africa, AI tools for healthcare professionals, AI regulation in Africa) are 471–591 characters each of real content. **Do not delete them from the repository.** Move them to `docs/orphaned-faq-content.md` with a note that they may be rendered on the page in a future edit, at which point they return to the markup. D-16: no content is withdrawn.

Apply the same reconciliation to the `FAQPage` on `/deep-dives/glm-5-2-global-south/` — verify it matches its rendered six-question FAQ before assuming it does.

> **Verified fact, 3 September 2026 (BRIEF-B-CORRECTIONS C-8).** It matches. All six marked-up `Question.name` strings on `/deep-dives/glm-5-2-global-south/index.html` correspond to the six rendered `<h3>` question headings. **The six-versus-five divergence is homepage-only.**
>
> **Scope of that check: question strings only.** The `acceptedAnswer.text` bodies have not been compared verbatim against the rendered answer text, and nothing here asserts that they match. That comparison remains the job of `tools/verify-jsonld-verbatim.py`, and acceptance criteria 1 and 3 below still bind on both pages.

**Acceptance criteria.**
1. For every `mainEntity` entry, both the question string and the answer string appear verbatim in the rendered text of the same page.
2. Count of marked-up questions equals count of rendered questions, on both FAQ-bearing pages.
3. `tools/verify-jsonld-verbatim.py` passes on both pages.
4. `docs/orphaned-faq-content.md` contains the three removed answers in full.
5. `git diff` on the JSON-LD block is entirely attributable to generator output — no hand-authored lines.

---

### B-10 — Mark expired listings as expired

**Objective.** Stop presenting closed opportunities as open.

**Traces to.** Inventory §C.1.11: GRIT `validThrough` 26 Jun 2026, Anthropic 21 Aug 2026, Oxford 12 Jun 2026, AI Impact Lab `availabilityEnds` 24 Jul 2026 — all past, all still published with `index, follow`, and *"`/opportunities/` still labels the AI Impact Lab 'Open · closes 24 Jul 2026'."* Only the Oxford page marks its status. P-16: the arriving visitor is checking recency. D-3. **D-16: no content withdrawn, none gated** — this is a marking task, not a deletion task.

**Depends on.** P-17.

**Files affected.** The four detail pages, `/opportunities/index.html`, `/opportunities/jobs/index.html`, `/opportunities/courses/index.html`, `/opportunities/scholarships/index.html`.

**Change specification.** Follow the pattern the Oxford page already uses, since it is the site's own established convention (§A.5.2): `(Closed)` appended to `<title>`, a visible status statement in the page prose near the top, and the index-page label changed from "Open · closes …" to "Closed · closed 24 Jul 2026".

Do not remove `validThrough` or `availabilityEnds` from the JSON-LD — a past `validThrough` is correct, machine-readable information. Do not change `index, follow`.

Fix the two markup defects the inventory notes while you are in these files, both of which are factual corrections rather than additions: `applicantLocationRequirements` on the Oxford node uses `@type: Country` with `name: "Worldwide"`, and *"Worldwide" is not a country* — express it as `Continent` or omit it. And the Oxford page is typed `JobPosting` while presented as a fellowship; leave the type unless the convener directs otherwise, but record the discrepancy.

**Acceptance criteria.**
1. For every `JobPosting` or `Course` node whose `validThrough` or `availabilityEnds` is earlier than today, the page `<title>` contains a closure marker and the prose states the closure.
2. Zero index-page labels reading "Open" for an item whose date is past. Script this as a date comparison, not an eyeball check.
3. No listing deleted; page count unchanged.
4. `name: "Worldwide"` no longer appears under `@type: Country`.

---

### B-11 — Repair every dangling reference in the machine layer

**Objective.** Make every URL the markup asserts actually resolve.

**Traces to.** Inventory §C.1.5: `Organization.logo` → `/assets/logo.png` (absent); `BlogPosting.image` and every `og:image`/`twitter:image` → `/assets/og-image.jpg` (absent); `Person.url` → `/about.html` (404, confirmed); `WebSite.potentialAction.target` → `/search?q=…` (absent); `<link rel="icon">` → `/favicon.ico` (absent). **The `assets/` directory does not exist in the repository at all** (§A.3.2). P-14. D-3. P-13 level 1.

**Depends on.** P-16 for the image assets; B-7 for `/about.html`.

**Files affected.** All thirteen content HTML files.

**Change specification.**
1. **Images (P-16):** if the assets exist, commit them to `assets/` and leave the references. If they do not, **remove `og:image`, `twitter:image`, `BlogPosting.image` and `Organization.logo` entirely.** A reference to a missing image is worse than no reference: it produces a broken card everywhere the site is shared, and `Organization.logo` failing invalidates the node for several consumers.
2. **`twitter:` tags** are present on only 4 of 13 pages (§A.3.6). Either add them to all thirteen or remove them from the four. Consistency matters more than presence, and **no `twitter:card` may exist without a valid image** — so if P-16 comes back empty, remove all four sets.
3. **`WebSite.potentialAction`:** remove the `SearchAction` entirely. No `/search` endpoint exists and none is being built.
4. **`Person.url`:** resolves after B-7, or the property is removed. Note the node is typed `Person` but named "InfoOnAIResources Editorial Team" (§A.3.5) — a team is not a `Person`. Retype to `Organization`, or supply a named individual (P-13). Do not invent one.
5. **`favicon.ico`:** commit one or remove the `<link rel="icon">`. **Verified fact, 3 September 2026 (BRIEF-B-CORRECTIONS C-4):** `<link rel="icon" href="/favicon.ico">` is present on **all thirteen** content pages and `favicon.ico` does not exist in the repository. The reference is therefore broken thirteen times, and the removal branch of this item is a thirteen-file edit, not a one-file edit.
6. **`Organization` node:** if P-13 supplies legal entity details, add `legalName` and `address` as a `PostalAddress`. The footer states "Nairobi, Kenya" as text but no address is expressed in markup (§A.3.2). Only add what the page states — if the page does not carry a street address, do not put one in markup. P-14 binds.
7. **`WebPage.dateModified`** is `2026-03-21`, three months older than the last content commit (§A.3.2). Set it to the real last-modified date, or remove it.

**Depends on.** B-20 — the verifier and the generator are built there, not here. This task supplies the *decisions* the generator needs: which references are repaired and which are removed. Once decided, the generator writes the result.

The URL half of the verification is the part that stays a checker rather than becoming a generator: a URL can be produced correctly and still stop resolving later, because the target is outside the page. So `tools/verify-jsonld-verbatim.py` retains the standing resolve-check for every URL-valued leaf plus every `og:`, `twitter:` and `<link>` URL, and it is run on every commit.

**Acceptance criteria.**
1. Every URL in any JSON-LD node, `og:` tag, `twitter:` tag or `<link>` resolves to a repository file or returns 200 externally. Zero exceptions.
2. `tools/verify-jsonld-verbatim.py` runs clean and is documented in the repository README.
3. No `SearchAction` remains.
4. `twitter:` tag presence is all-thirteen or zero.
5. No node typed `Person` carries a collective name.

---

### B-12 — Express the property's own commercial facts as structured data

**Objective.** The one genuine addition to the machine layer on this property.

**Traces to.** D-3 ADAPT: *"a canonical, dated, extractable statement of its own facts… and for the shop, product identity and price as text."* Inventory §A.3.9: the property's own pricing *"exists as page text only, with no markup"* — no `Offer`, `PriceSpecification`, `Service` or `Product` node expresses any of it, on a property that carries `JobPosting` and `Course` markup for other people's offerings. D-11 ADAPT — discovery side only: *"product and service identity expressed as text and structured data."* P-13 level 1.

**Depends on.** B-20, P-11, P-12, P-13.

**Files affected.** `tools/generate-machine-layer.py`, `data/declared-values.json`; then `index.html` via generator output.

**Change specification.** Extend the generator so it reads the `#tiers` block and the FAQ price-ladder prose and emits, in the homepage `@graph`, a `Service` node (not `Product` — this is a subscription information service) representing the offering, with two `Offer` children:

- **Free tier:** `price: "0"`, `priceCurrency: "USD"`, `availability: InStock`, `name` from the rendered tier name.
- **Professional tier:** the PPP ladder expressed as `PriceSpecification` entries with `eligibleRegion` values matching the three bands the FAQ names — Africa/India, Gulf, US/UK diaspora — using the exact figures rendered on the page (DNC-3).

**Availability is the sharp edge here.** The Professional tier is labelled "Launching Month 4" and does not exist yet. **Do not mark it `InStock`.** Use `PreOrder` or omit availability entirely. And do not express an anchor date unless P-11 supplies one — a relative date with no anchor cannot be made absolute by inference.

**Payment methods:** `acceptedPaymentMethod` may name M-Pesa **only if P-12 confirms it is live**. The FAQ says it is available "from launch", which is a future capability, and no payment integration exists in the repository (§A.6.2). Asserting current acceptance of a payment method that is not accepted fails P-14 and is a consumer-protection exposure under P-18(i), which treats site-authored statements as the site's own publication.

**Acceptance criteria.**
1. Every price string in the emitted markup was **extracted from** the rendered text of `index.html`, not transcribed into the generator. Changing a price on the page and re-running must change the markup.
2. No `availability: InStock` on any tier not currently purchasable.
3. `acceptedPaymentMethod` present only with written confirmation from P-12, referenced in the commit body.
4. `tools/verify-jsonld-verbatim.py` passes.
5. No rendered text changed — this task adds markup only.
6. The region-band mapping is the only pricing element permitted in `data/declared-values.json`; the figures themselves are extracted.

---

### B-13 — Add landmarks; add no ARIA

**Objective.** Give the pages the structural landmarks they lack.

**Traces to.** **D-17, RATIFIED and binding:** semantic HTML first; ARIA only where a native element cannot express the semantics; every ARIA addition justified in the change log. Inventory §A.4.2: **no `<main>` element exists on any page of this property** — zero occurrences across all fourteen HTML files. `<header>` is absent on the homepage. §A.7.6 notes, pointedly, that the *undeployed* second repository has `<main>` on four pages while the deployed property has none.

**Files affected.** All thirteen content HTML files. The fourteenth `.html` file is the 54-byte Search Console verification file; it gets no `<main>` and no skip link.

**Change specification.**
1. Add exactly one `<main>` per page, wrapping the primary content between the nav and the footer.
2. Add `<header>` to the homepage — currently the top bar is a `<nav>` inside a `<div>`.
3. Add a skip link to `<main>` on every page, visually hidden until focused. `skip` currently appears zero times in any file (§A.4.8).
4. Consider removing `role="contentinfo"` where it merely duplicates a native `<footer>` semantic (§A.4.4) — this is an ARIA *reduction*, which D-17 favours.
5. **Add no ARIA.** The existing ARIA usage is already good: it decorates rather than replaces, sits on native `<button>` elements, and the inventory found no `role="button"` on a `<div>` and zero `tabindex` occurrences. Do not disturb it.
6. Add `prefers-reduced-motion` handling — currently zero occurrences while the homepage animates 20 elements (§A.4.7). This is an accessibility improvement with no machine-layer justification needed.

**Barred.** No keyboard or zoom specification derived from D-4's held magnitudes.

**Acceptance criteria.**
1. Exactly one `<main>` per content page; thirteen total.
2. Skip link present on all thirteen, focusable, targets `main`.
3. Count of ARIA attributes after ≤ count before.
4. Visual regression at 390 / 768 / 1440px: zero pixel change except the focused skip link.
5. A `prefers-reduced-motion: reduce` block exists and disables the transitions.
6. Automated accessibility scan reports no new violations.

---

### B-14 — Make the homepage legible without JavaScript

**Objective.** Ensure a rendering agent sees what a retrieval agent sees.

**Traces to.** Inventory §A.4.6: nineteen `.reveal` elements render at **opacity 0** until an `IntersectionObserver` fires — *"invisible in a screenshot — while their text is fully present in the HTML source"*; the FAQ's five answer bodies are in the DOM but visually collapsed, so *"a retrieval agent reading the DOM gets all five answers; a vision agent working from a rendered screenshot gets five question strings and no answers"*; and the copyright year is JS-generated, so the live footer serves with **no year at all** (§C.1.1). Charter II.4, the dual-eyes finding. D-4 severed and ruled component: *"anything a machine must read is real text; the early portion of a page carries the substantive claim."* P-16: *"no fact layer gated behind JavaScript."*

**Files affected.** `index.html` — the inline `<style>` and the 1,391-character inline `<script>`. The other twelve pages have no script and no `.reveal` usage (§A.4.6); do not touch them.

**Change specification.**
1. **Invert the `.reveal` default.** Declare `.reveal { opacity: 1; transform: none; }` as the base state. Have the script add a class to `<html>` on execution — e.g. `js-enabled` — and scope the hidden-then-animate rule to `.js-enabled .reveal:not(.visible)`. Net effect: with JavaScript, the animation is unchanged; without it, all nineteen blocks are visible. **The animation as a human sees it must not change.**
2. **Copyright year:** replace the JS assignment with the literal year in the HTML. Keep the `id` if the script still uses it, or remove both.
3. **The FAQ accordion stays as it is.** DNC-6 protects it; the pattern is what D-17 ratifies; and the answers are in the DOM, which is what P-16's non-obstruction requirement asks for. A collapsed-by-default accordion is a legitimate human-facing design choice.

**Acceptance criteria.**
1. With JavaScript disabled, all nineteen `.reveal` elements compute to `opacity: 1`.
2. With JavaScript enabled, the reveal animation is visually identical to before — verify by recording both.
3. The served footer contains a literal four-digit year with no script execution.
4. Visual regression with JS enabled: zero pixel change.

---

### B-15 — Source or remove the two unsourced statistics

**Objective.** Every claim on the page attributable.

**Traces to.** Inventory §A.5.6. **Corrected 3 September 2026 (BRIEF-B-CORRECTIONS C-5):** the homepage stat block carries **four** statistics. **Two** carry named sources ("Microsoft AI Diffusion Report, 2026"; "PwC, analysing 1 billion job ads, 2025"). **Two** do not — "198M internet-connected knowledge workers" and "54% … only 4% are acting" — and on those two the `stat-source` slot is occupied by descriptive copy rather than left empty: "Africa, South Asia & MENA combined" and "The gap this platform exists to close". The scope is two of four, not two of six, and the work is a replacement in an occupied slot, not the addition of a missing element. D-3 (highest-quality source for its own description). **P-20's test: would the statement be true and attributable if a human read it?** Charter Part VI: date-stamp everything; state what is being counted.

**Depends on.** P-14.

**Change specification.** Add the named source inline, matching the existing convention on the same block ("Microsoft AI Diffusion Report, 2026"; "PwC, analysing 1 billion job ads, 2025"), **or remove the statistic**. Do not search for a plausible source and attach it — the requirement is the source the copy was actually written from.

**Acceptance criteria.** Every numeric claim in the homepage stat block carries a named source with a year, or is absent.

---

### B-16 — Machine-layer change log and provenance convention

**Traces to.** D-9 (every machine-facing signal attributable to a human decision recorded in a change log). D-14 (provenance marking as a design primitive, adopted early because retrofitting is expensive and early adoption is nearly free).

**Change specification.** Create `docs/machine-layer-changelog.md` and `docs/provenance-convention.md`, as specified in Brief A tasks A-13 and A-12. Backfill entries for B-2 through B-12 as they land. Copy §3 of this brief into `docs/DO-NOT-CHANGE.md`.

**Acceptance criteria.** Every commit touching `robots.txt`, `sitemap.xml`, `llms.txt`, any JSON-LD block or any `<meta>` tag has a corresponding changelog entry in the same commit.

---

### B-17 — Deliberate non-actions, recorded

**Objective.** Record what was considered and refused, so it is not re-proposed next cycle as a new idea.

**Traces to.** D-12 (*"the council commissions measurement of it rather than authorising a build on top of it"*), D-11, P-13's binding cost rule.

**Change specification.** Write `docs/deliberate-non-actions.md` recording, each with its ruling:

- No RSS/Atom/JSON feed built. The property has none (§A.2.7), and D-12 holds that the existing sitemap bifurcation is unmeasured — measurement precedes any build on top of it.
- No product feed, no Merchant Center feed, no `/.well-known/ucp` (D-11: no commerce gate demands it here).
- No checkout, cart or payment integration (D-11, P-16, D-15).
- No `.well-known/` directory of any kind, no Web Bot Auth key material (D-10).
- No WebMCP (D-12, P-13 level 3 — spec, tooling, origin trial, and no shipped consuming agent).
- No proxying of this zone before 16 September (D-5 control case).
- No second machine-facing surface (D-12).

**Acceptance criteria.** The file exists and each entry names its ruling.

---

### B-18 — Repository hygiene (post-deadline)

**Traces to.** §C.1.8 (repository name `inforionairesources.shop` vs domain `infoonairesources.shop`), §C.1.9 / §A.7.6 (second repository), §C.2.3.

**Change specification.** After B-7 has taken whatever is needed from `infoonairesources-site`, archive it — do not delete. Rename the deployed repository to match the domain **only if** the convener confirms GitHub Pages custom-domain configuration survives the rename; if there is any doubt, leave it. A working deployment is worth more than a tidy name.

Consider adding a minimal CI check running the verification suite on push. There is currently no `.github/workflows/` and no CI of any kind (§A.7.2). This is optional and post-deadline.

**Acceptance criteria.** Second repository archived; disposition recorded; deployment unaffected — verified by fetching the live site after any change.

---

### B-19 — Citation probe (post-deadline)

Same instrument as Brief A task A-15, with a query set fitted to this property: AI opportunity queries a Global South reader would actually ask, plus the property by name. Run monthly. Same standing citation restrictions apply (CL-5, CL-4, CL-2, P-3).

Per D-16, evergreen material on this property — the GLM-5.2 deep dive in particular — is reclassified as a **citation asset**, evaluated on whether it is cited rather than whether it is visited. This is an accounting change only. No content is withdrawn and no editorial decision follows from it; D-16's evidence is *"too thin to carry one."*

---

## 5. VERIFICATION

### 5.1 Run after every task

- `tools/generate-machine-layer.py` — re-run after **any** change to page text, then commit the regenerated markup in the same commit. Never hand-edit a JSON-LD block.
- `tools/verify-jsonld-verbatim.py` — the P-14 guard. Every string in the machine layer appears verbatim on the human page or in `data/declared-values.json`; every URL resolves.
- `tools/verify-sitemap.py` — every `<loc>` has a file behind it.
- `grep -rc 'REPLACE_WITH\|TODO\|FIXME\|lorem' .` → 0.
- `grep -rc 'www\.infoonairesources\.shop' .` → 0.
- Link check: every `href`, `src`, `<loc>`, and JSON-LD URL resolves.
- Nav consistency: the primary-nav href set is identical across all thirteen files.
- Visual regression at 390 / 768 / 1440px.
- Accessibility scan: no new violations; ARIA count not increased.
- Expiry check: no index label says "Open" for a date in the past.

### 5.2 Run before 15 September

1. **B-1 is running** and has produced at least seven consecutive daily files covering both properties.
2. `robots.txt` is in its target state with zero `Disallow` lines, and the removal is recorded in the changelog with the convener named as the deciding party.
3. Sitemap, `llms.txt` and navigation all describe only what exists.
4. `grep -rc 'REPLACE_WITH'` returns 0 and a live test submission reaches its destination.
5. **Confirm with the convener that this zone is still DNS-only.** If it has been proxied, the control case is gone and §5.3 must be rewritten before the date, not after.

### 5.3 Run on 16–20 September

This property's role is to show what *doesn't* change.

1. Diff the observation logs across the boundary for the four `infoonairesources.shop` URLs. Expected result: no change in status codes, no new challenge headers, no body-hash change other than from your own deploys — because Cloudflare's edge is not in this path.
2. **Compare against Property B (swakaadvocates.co.ke).** A change appearing on both is not attributable to the Cloudflare default. A change appearing only on the proxied property is a candidate — and only a candidate.
3. Record in `docs/observation-findings-2026-09.md` with raw log references.
4. **Grade honestly.** One network path, one set of user-agent strings, one date range. P-23 clause 1 grades the flip as announced policy, not shipped; no brief in the corpus observed it in production; and V-1 and V-3 are dischargeable only on or after the date. State what was observed and what it does not establish.

### 5.4 Measurement setup (P-22)

1. **Server-side request logs** — **not available.** GitHub Pages provides no log access at all (§C.2.5). Per P-22's African-test amendment, adopted 11–0: the minimum is the external probe plus whatever the host provides, **and the absence of log access is itself recorded as a finding about the host.** Record it in `docs/measurement-baseline.md`, dated, as a finding — not as a caveat buried in a footnote. It is the reason this property cannot see its own machine traffic, and it is a property of the hosting choice.
2. **Baseline emission-and-blocking audit** — B-1.
3. **Citation probe** — B-19.

**No AEO/GEO spend is authorised until 1 and 2 are in place**, with clause 1 satisfied in its amended form.

---

## 6. TRACEABILITY INDEX

| Task | Rulings | Inventory |
|---|---|---|
| B-1 | P-23(2), P-22(2), D-5 | §A.1.3, §C.1.20 |
| B-2 | **D-1**, P-8, D-9 | §A.2.1, §A.2.2, §C.1.21 |
| B-3 | P-13(1), P-15 | §C.1.7, §A.1.5, §A.3.7 |
| B-4 | D-9, P-13(1), P-14 | §C.1.2, §A.2.4, §A.5.3 |
| B-5 | **D-9**, P-13(3), D-12 | §C.1.3, §A.2.3 |
| B-6 | P-13(1), P-15 | §A.5.3, §C.1.6 |
| B-7 | D-3, P-16 | §C.1.9, §A.6.3, §A.7.6 |
| B-8 | D-3, P-16, P-13(1) | §A.6.1, §C.1.1, §C.1.12 |
| B-9 | **P-14**, D-3, D-16 | §C.1.4, §A.3.2 |
| B-10 | P-16, D-3, D-16 | §C.1.11, §A.3.3, §A.3.4 |
| B-11 | P-14, D-3, P-13(1) | §C.1.5, §A.3.2, §A.3.5, §A.3.6 |
| B-12 | D-3, D-11, P-13(1), P-14, P-18(i) | §A.3.9, §A.5.4 |
| B-13 | **D-17 (binding)** | §A.4.2, §A.4.4, §A.4.8 |
| B-14 | D-4 (severed), P-16, Charter II.4 | §A.4.6, §C.1.1 |
| B-15 | D-3, P-20 | §A.5.6 |
| B-16 | D-9, D-14, P-4 | — |
| B-17 | D-10, D-11, D-12, D-15, P-13 | §A.2.7, §A.2.8, §A.6.2 |
| B-18 | — | §C.1.8, §C.1.9, §A.7.2 |
| B-19 | P-22(3), D-16, D-18 | §C.2.5 |
| **B-20** | **P-14**, D-3, OD-J | §C.1.4, §A.3.2, §A.7.3 |

*B-20 is numbered last and executes before B-9, B-11 and B-12. Appended rather than renumbered, per the Conflict Register's numbering principle.*

---

*End of Implementation Brief B. Every task traces to a ruling or an inventory finding. Where a decision was needed and none existed, it was routed to the OPEN DECISIONS LIST rather than taken silently.*
