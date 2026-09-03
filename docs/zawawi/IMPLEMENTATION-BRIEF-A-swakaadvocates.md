# IMPLEMENTATION BRIEF A — swakaadvocates.co.ke

**Version:** 1.0
**Issued:** 2 September 2026
**Deadline anchor:** 15 September 2026 (13 days)
**Authority:** ZAWAWI Position Analysis (P-1…P-24, H-1, H-2) and Conflict Register V1 (D-1…D-19), both dated 28 August / 2 September 2026
**Baseline facts:** Site Inventory V1.0, 28 August 2026, Property B sections (§B.1–§B.7, §C.1.13–§C.1.23, §C.2)
**Execution environment:** Claude Code

---

## 0. INSTRUCTION HEADER — READ BEFORE ANYTHING ELSE

You are implementing decisions that have already been made. You are not deciding strategy. If a task seems to call for a judgement this brief has not made, **stop and ask** — do not resolve it yourself and do not infer it from the rest of the document.

**Working method — read, plan, confirm, execute.**

1. **Read.** Before touching any file, read the current state of it. Do not act on this brief's description of a file; this brief describes the site as inspected on 28 August 2026 and the site may have changed. Where the brief and the file disagree, the file is the fact and you report the discrepancy.
2. **Plan.** For each task, write out what you intend to change, in which files, and why, and show it before you edit. One task at a time.
3. **Confirm.** Wait for the convener's go-ahead on the plan. This applies to every task without exception on this property, because the human-visible surface of a regulated legal practice carries advertising exposure under Law Society of Kenya rules and neither you nor this brief is competent to judge that exposure.
4. **Execute.** One task, one commit. Small, reversible, individually revertable units.

**Commit message format — mandatory:**

```
<task-id>: <one-line description>

Implements: <ruling ID(s)> — e.g. D-3, P-13(1)
Inventory: <finding ID(s)> — e.g. B.3.1, C.1.16
Files: <list>
Human-visible change: yes | no
ARIA added: none | <attribute> because <native element that cannot express it>
```

**Absolute rules:**

- **Never modify anything in the DO-NOT-CHANGE register (§3).** If a task appears to require it, the task is wrong. Stop and report.
- **Never invent a fact.** No date, price, credential, name, address, phone number, statistic or qualification enters this site or its markup unless it is already rendered on the page or has been supplied by the convener in writing. If a value is missing, the task is blocked, not improvised.
- **Never add a marketing claim.** Not in prose, not in a meta description, not in structured data. Everything on this property is subject to legal-professional advertising rules.
- **Never cite the figures 78.33 / 41.67 / 28.33** or write any zoom-tolerance or keyboard-operability specification derived from them. Barred by D-4 pending verification V-4.
- **Never cite a crawler spoof rate.** Barred by D-10 pending CL-2.
- **Never rely on D-7** (whose permission an agent carries) for any decision here. Marked provisional, blocking on V-10.
- **Do not touch any Cloudflare, DNS, GitHub or hosting dashboard.** You have no such access and must not seek it. Where a task concerns configuration, your output is a worksheet or a script, not a settings change.
- If a `PRE-TASK` item a task depends on is unanswered, mark the task **BLOCKED** and move to the next one. Do not proceed on an assumption.

---

## 1. MISSION AND NON-GOALS

### Mission

This property is a two-page site for a Nairobi legal practice whose conversion is an offline hire. A person who is told about this firm by an AI assistant and never clicks through has still, potentially, converted — which makes the accuracy of what the assistant says about the firm more consequential than the traffic the site receives.

The council's finding is that no accountable party holds the account of an entity that reaches the human (Position Analysis Part J, fifth holding). The firm cannot fix that. What it can do is become the highest-quality available source for its own description — a canonical, dated, extractable statement of its own facts, positioned where retrieval agents reach it without rendering (D-3, ADAPT).

That is the whole of the mission. Concretely, three things:

1. **Make the firm's existing facts machine-legible** — services, jurisdiction, admission status, credentials, contact, recency — without adding a single new claim.
2. **Repair what is broken or stale**, because on a verification surface, staleness is the failure mode that matters (P-16).
3. **Establish observation before 15 September**, so that whatever the fronting intermediary's default change does to this property is observed rather than inferred (P-23 clause 2).

The inventory records something favourable that must be preserved: every commercial fact on this property already exists as machine-readable text, and nothing was found rendered only as a graphic (§B.4.7). The site is starting from a better place than most. The work is additive.

### Non-goals — do not build these

| Not doing | Because |
|---|---|
| Any agent-transaction or checkout capability | P-16: out of scope for 2026 as investment, in scope only as non-obstruction. D-11: build nothing on the completion side. |
| Signed crawler identity / Web Bot Auth / RFC 9421 key material | D-10, CONCEDE this cycle. Two named production participants implement incompatible draft generations. The council does not build against it and does not recommend any client do so. |
| HTTP 402, Pay Per Crawl enrolment, any paid-passage posture | P-11 carried 7–4, the session's most divided position, confidence LOW. D-8: below the paid tier the instrument is non-configurable anyway. Not authorised for implementation. |
| A separate machine-facing surface, WebMCP, `/.well-known/*` capability endpoints | D-12: the pattern is conceded as real and rational for an operator whose customers are the AI industry, and **not adopted for either property**. One surface, two legibilities. |
| `llms.txt` | P-13 level 3 — specification without a consumer, built only as a near-zero-cost byproduct of level 1 work, never as primary spend. D-9 bars any unauthored machine-facing file. There is no level-1 byproduct here to justify one. |
| robots.txt engineering that splits training crawlers from search crawlers | D-1, CONCEDE. The council stops spending on the attempt. Blocking training also blocks Googlebot, Applebot and Bingbot under most-restrictive-wins. |
| Any fee, price or fee-basis statement | The firm states none (§B.5.4). Adding one is a business decision with LSK advertising exposure. Position Analysis S-2 bars the council from ruling on the decision layer for this property. See OPEN DECISION OD-D. |
| Testimonials, client names, matter descriptions, ratings, review markup | Absent by the firm's stated confidentiality posture (§B.6.4), and D-18 holds the third-party-signal question open on Tier 5 evidence throughout. Do not manufacture what the corpus cannot support. |
| Off-site mention-building, distributed brand mentions, seeded citations | P-20: if it requires volume or anonymity to work, it is manufacturing, and manufacturing is refused as already unlawful in substance. |
| Practice-area content expansion, new pages, blog migration from Substack | Content strategy is not this brief. Any new page is a convener decision and an LSK question. |

---

## 2. PRE-TASK CHECKLIST — CONVENER-SUPPLIED FACTS AND ACCESS

Every item below was graded NOT DETERMINABLE FROM HERE in the inventory. Tasks that depend on them are marked BLOCKED until they are answered. Answer in writing, in this order — item 1 unblocks more work than the rest combined.

### Blocking the largest number of tasks

- [ ] **P-1. Raw HTML of `/` and `/publications`.** Browser view-source, saved to file, or `curl` output. Inventory §C.2.4 records this as sufficient to resolve every NOT DETERMINABLE item in §B.3 and §B.4 in one step: whether JSON-LD exists at all and what it contains, `<html lang>`, landmark elements, ARIA usage, `tabindex`, focus styles, the homepage logo `src` anomaly, and the stylesheet needed for contrast computation. *Without this, tasks A-4, A-8 and A-9 cannot be specified, only guessed at.*
- [ ] **P-2. Does a repository exist for this property?** Inventory §B.7 records absence-of-public-record, explicitly **not** a finding that none exists — a private repo, a different account, GitLab, or no version control at all are all consistent. If one exists: where, and can Claude Code be given read-write access? If none exists, task A-2 creates one from the live HTML.
- [ ] **P-3. How is this site published?** What is the origin behind the Cloudflare proxy — Cloudflare Pages, a Kenyan cPanel host, a VPS? Is there a build step? How does a change reach production today? *Every task in §4 assumes an answer to this.*

### Cloudflare zone — `swakaadvocates.co.ke` (inventory §C.2.1)

Screenshots are acceptable and preferred over transcription.

- [ ] **P-4.** Confirm apex A/AAAA records are proxied (orange cloud). The inventory grades this INFERRED from anycast ranges; it is confirmable only in the dashboard.
- [ ] **P-5.** **Plan tier** — Free / Pro / Business / Enterprise. This is the single most consequential answer in the checklist. D-8: below the paid tier the crawler instrument is non-configurable, and *"the tier decision has stopped being a billing decision and has become a strategy decision, and it should be taken as one, on the record."* See OPEN DECISION OD-B.
- [ ] **P-6.** AI Crawl Control / "Block AI bots" / AI Scrapers & Crawlers — on, off, or per-crawler?
- [ ] **P-7.** Bot Fight Mode / Super Bot Fight Mode state; verified-bot allowances.
- [ ] **P-8.** Pay Per Crawl enrolment status. *(Expected answer: not enrolled. If enrolled, report immediately — it conflicts with the non-goals above.)*
- [ ] **P-9.** WAF custom rules, rate-limiting rules, any user-agent- or ASN-conditional logic.
- [ ] **P-10.** Transform Rules or Workers injecting response headers — in particular any `X-Robots-Tag`. A header injected at the edge would be invisible to the origin and to the repository.
- [ ] **P-11.** SSL/TLS encryption mode (Flexible / Full / Full-Strict), Always Use HTTPS, HSTS.
- [ ] **P-12.** Is Cloudflare serving `robots.txt`, or the origin?
- [ ] **P-13.** Whether this zone is in scope for the 15 September default change, per whatever the dashboard now says.

### Files and endpoints (inventory §B.2.1–§B.2.4, all NOT DETERMINABLE)

- [ ] **P-14.** Does `/robots.txt` exist? Contents verbatim if so.
- [ ] **P-15.** Does `/sitemap.xml` exist? Contents if so.
- [ ] **P-16.** Does `/llms.txt` or any `/.well-known/` path exist? *(If a platform default created one, D-9 requires it be authored or removed — no plugin stubs, ever.)*
- [ ] **P-17.** Do pages exist that are not linked from `/` or `/publications`?

### Measurement (P-22, mandated before any AEO/GEO spend)

- [ ] **P-18.** **Are server-side or edge request logs available with user-agent retention?** Cloudflare Analytics would provide this for a proxied zone. P-22 clause 1 is not negotiable: analytics JavaScript cannot see a client that does not execute JavaScript, and that is a category of traffic the standard instrument cannot see at all. If logs are unavailable, the African-test amendment applies — external probe only, **and the absence of log access is recorded as a finding about the host.**
- [ ] **P-19.** Google Search Console — a `google-site-verification` TXT record is published for this domain (§B.1.3). Whose property is it, and what does it report?
- [ ] **P-20.** Any analytics platform in use? None was detectable from outside.

### Owner-held facts (inventory §C.2.6, §C.2.7)

- [ ] **P-21.** John Swaka's LinkedIn URL, to replace `href="#"` on `/publications` (§C.1.16). *If there is no profile, say so — task A-5 removes the section rather than ship a dead link.*
- [ ] **P-22.** Revised dates, or a decision to drop dates, for the five publications still labelled "Coming April–June 2026" (§C.1.15).
- [ ] **P-23.** LSK practising certificate number — and **whether it may be published**. See OPEN DECISION OD-E.
- [ ] **P-24.** Is a logo image file available? The homepage logo `src` resolved empty across both extraction passes (§C.1.19), and there is no `og:image` on either page (§B.3.2).
- [ ] **P-25.** Should `www.swakaadvocates.co.ke` exist? It is currently NXDOMAIN on all record types, so any citation, directory listing or printed reference using `www.` fails at DNS before any request is made (§B.1.5). See OPEN DECISION OD-F.
- [ ] **P-26.** Practice area II is named "Data Sovereignty Counsel" in the hero and "Data Sovereignty & Cross-Border Transactions" in the services section (§C.1.18). Which is the name? *Do not resolve this yourself — it is the firm's own service naming.*
- [ ] **P-27.** "Immigration" appears in the established-practice sentence but in none of the seven numbered areas (§C.1.18). Intentional?
- [ ] **P-28.** **Who signs off human-visible text changes?** Every such change on this property is an advertising decision under LSK rules. Name the person and the process. See OPEN DECISION OD-I.

---

## 3. DO-NOT-CHANGE REGISTER

These are protected by council ruling. **Claude Code must not modify, restructure, reword, restyle or "improve" any of them.** If a task appears to require it, stop and report to the convener.

D-14 rules **KEEP** on this property's human-facing surface: the regulatory marking obligations it discusses are additive and *"do not require conceding anything to the machine layer."* D-6 rules DUAL-LAYER as **rhetorical, not technical** — one document, two registers, with the human voice written around the factual spine rather than the spine bolted onto the voice. Both mean the same thing here: the machine layer is added underneath, and the surface a client sees is not traded away for it.

| # | Protected | Authority |
|---|---|---|
| **DNC-1** | **All seven practice-area names and their full prose descriptions, as displayed.** Including the hero teasers and the numbered service sections. The naming divergence at II is an OPEN DECISION, not a task. | D-14 KEEP; §B.5.3; P-28 pending |
| **DNC-2** | **The engagement / selectivity statement** — "a structured assessment of whether the matter and the firm are the right fit", and the referral undertaking. | D-14 KEEP; §B.6.4 |
| **DNC-3** | **The confidentiality posture.** No testimonials, no client names, no matter descriptions, no rankings are to be added. Their absence is deliberate. | §B.6.3; D-18 (Tier 5 throughout) |
| **DNC-4** | **The absence of any fee or price statement.** Do not add one, do not add `priceRange`, do not add "fees on application". | §B.5.4; S-2; OD-D |
| **DNC-5** | **The visual design system** — dark theme, typography, spacing, the whole rendered appearance. Task A-8 changes markup semantics and must produce **no visible change**. | D-14 KEEP; Charter II.3 |
| **DNC-6** | **The regulatory footer statements, verbatim**: "Regulated by the Law Society of Kenya"; "East Africa Law Society Member"; "© 2026 Swaka Advocates. All rights reserved." | §B.6.3; D-14 |
| **DNC-7** | **All contact facts as rendered** — both telephone numbers, the email address, the street address, the P.O. box, "Established 2016 · Admitted to the Bar 2006", "Republic of Kenya · East Africa · International". These may be **copied into** markup. They may not be edited, reformatted, normalised or corrected. | §B.3.6; D-3 |
| **DNC-8** | **Both `<h1>` strings.** | §B.4.1 |
| **DNC-9** | **The zero-image-carrying-facts property.** Every commercial fact currently exists as text and nothing is trapped in a graphic. Do not introduce any element that carries a fact as pixels. | §B.4.7; D-4 (severed, ruled component) |
| **DNC-10** | **The Substack distribution arrangement.** Do not migrate, mirror or duplicate published articles on-domain without a convener decision. | §B.2.8, §B.5.6 |

---

## 4. TASK LIST — ORDERED

Order is execution order. Deadline-critical tasks are marked **⏰**. Everything else sequences on P-13's Consumption Rule (documented consumer first, measured effect second, specification-without-consumer last) and on P-23 clause 3: *commit no resource that is wasted if the date slips.*

---

### ⏰ A-1 — Stand up external observation, both properties, before 15 September

**Objective.** Produce a recorded, repeatable observation of what this property serves to declared AI user agents from outside its own network, running on a fixed cadence starting immediately and continuing across 15 September, so that the post-date state is **observed rather than inferred**.

**Traces to.** P-23 clause 2, verbatim: *"Establish external observation capability before 15 September — fetch the property's own URLs from outside the network under declared AI user agents, on a recorded cadence, starting now, so that the post-date state is observed rather than inferred."* Also P-22 clause 2 (baseline emission-and-blocking audit) and D-5, which authorises *"the paired observation across 15 September, which converts the concession into the programme's only natural experiment."*

**Files affected.** New repository or new directory `observation/`. No site files touched.

**Change specification.**

Write a single script that runs against **both** properties (this is the paired instrument; Brief B does not duplicate it). For each target URL, issue one request per user-agent string, sequentially, with a courteous delay, and append one JSON line per request to a dated log.

Target URLs:
```
https://swakaadvocates.co.ke/
https://swakaadvocates.co.ke/publications
https://swakaadvocates.co.ke/robots.txt
https://swakaadvocates.co.ke/sitemap.xml
https://infoonairesources.shop/
https://infoonairesources.shop/opportunities/
https://infoonairesources.shop/robots.txt
https://infoonairesources.shop/sitemap.xml
```

User-agent strings — one control plus the declared agents named in the corpus:
```
control-browser   (a current Chrome UA string)
GPTBot
OAI-SearchBot
ChatGPT-User
ClaudeBot
Claude-SearchBot
Claude-User
PerplexityBot
Perplexity-User
Googlebot
Google-Extended
Bingbot
Amazonbot
CCBot
```

Record per request: UTC timestamp, target URL, user-agent string, HTTP status, final URL after redirects, full response headers (in particular `cf-ray`, `cf-mitigated`, `server`, `x-robots-tag`, `cache-control`), byte length, SHA-256 of the body, and the first 500 bytes of the body. Never overwrite; always append. One file per day, `observation/YYYY-MM-DD.jsonl`.

**Where it runs.** From a machine or scheduler **outside** both properties' networks and outside the Anthropic sandbox — the convener's own machine, a small VPS, or a scheduled CI job. Claude Code writes the script and the runbook; the convener runs it. Daily at minimum; twice daily between 13 and 18 September.

**Acceptance criteria (machine-checkable).**
1. `observation/` contains at least one `.jsonl` file per calendar day from first run onward, with no gaps.
2. Every line parses as JSON and carries all of: `ts_utc`, `url`, `user_agent`, `status`, `final_url`, `headers`, `body_sha256`.
3. Each daily file contains at least one record for every (URL × user-agent) pair — 8 × 14 = 112 records minimum per run.
4. A file dated on or before 2026-09-14 exists, and a file dated on or after 2026-09-16 exists. *This is the acceptance criterion that matters; the rest is hygiene.*
5. A `observation/README.md` states the run cadence, the machine it runs from, and the date it started.

**Note.** This task is not blocked by anything in the PRE-TASK checklist. Start it today.

---

### ⏰ A-2 — Establish version control and commit an untouched baseline

**Objective.** Before any change, capture the current live state so that every subsequent change is diffable and revertable.

**Traces to.** P-4 (change log requirement); D-9, which requires *"every machine-readable file on the properties must be attributable to a human decision recorded in the change log"*; inventory §B.7 (no repository located).

**Depends on.** PRE-TASK P-1, P-2, P-3.

**Change specification.**
- If a repository exists (P-2), clone it and confirm it matches the live site byte-for-byte. Report any drift; do not silently reconcile.
- If none exists, create one, commit the raw HTML of both pages exactly as served (P-1), plus any CSS and JS they reference, plus `robots.txt` and `sitemap.xml` if they exist (P-14, P-15), as a single commit titled `A-2: baseline capture, untouched, <date>`.
- Create `docs/machine-layer-changelog.md` with a header explaining what it is, and no entries yet.
- Create `docs/DO-NOT-CHANGE.md` containing §3 of this brief verbatim.

**Acceptance criteria.**
1. `git log` contains exactly one commit before any task after A-2.
2. `docs/machine-layer-changelog.md` and `docs/DO-NOT-CHANGE.md` exist.
3. A diff of the baseline commit against a fresh fetch of the live site returns empty.

---

### ⏰ A-3 — Record the Cloudflare posture and force the tier decision

**Objective.** Convert the dashboard state from unknown into a recorded, dated artifact, and put the plan-tier question in front of the convener as the strategy decision the council says it is.

**Traces to.** D-5, CONCEDE, which *"binds swakaadvocates.co.ke and does not bind infoonairesources.shop"*. D-8: *"the tier decision has stopped being a billing decision and has become a strategy decision, and it should be taken as one, on the record, with the loss of granularity stated."* P-23 clause 1: the flip is announced policy, not shipped. Inventory §C.2.1.

**Files affected.** New: `docs/cloudflare-posture-2026-09.md`. **No dashboard changes. No site files.**

**Change specification.** Produce a worksheet with one row per PRE-TASK item P-4 through P-13, each answered from the convener's screenshots or marked `NOT AVAILABLE AT THIS TIER`. Append a section headed *Tier decision* stating: the current tier; what crawler granularity that tier does and does not expose; and the fact that below the paid tier the instrument is non-configurable, so the property cannot distinguish a wanted retrieval agent from an unwanted training crawler at all. Do not recommend a tier. Record the decision when the convener makes it, with the date.

Append the mandatory African-test caveat from D-8, which the ruling requires be carried *"on its face"*: **most Kenyan operators are not behind a configurable edge at all, so this ruling addresses a minority of Kenyan sites.**

**Acceptance criteria.**
1. Every field P-4…P-13 is either answered or explicitly marked unavailable — no blanks.
2. The document carries an inspection date and the name of the person who read the dashboard.
3. The D-8 African caveat appears verbatim.
4. No commit in this task touches any file outside `docs/`.

**Barred within this task.** Do not enable Pay Per Crawl (non-goal). Do not enable any signed-identity gating (D-10). Do not cite any Cloudflare-derived figure as the sole basis for a decision (P-3, standing restriction).

---

### A-4 — Publish or reconcile `robots.txt` and `sitemap.xml`

**Objective.** Ensure the property emits exactly two machine-facing files, both authored by a human decision, both true.

**Traces to.** D-1 CONCEDE — *"Both properties admit both audiences… no robots.txt engineering aimed at splitting training from search, no Google-Extended posture presented as a strategic choice."* D-9 ADAPT — *"Author every machine-facing signal or emit none. No plugin stubs, ever."* P-8 — reserve rights in machine-readable form without enforcing at the door. P-13 level 1 (configuration hygiene).

**Depends on.** P-14, P-15, P-16.

**Files affected.** `/robots.txt`, `/sitemap.xml`.

**Change specification.**

`robots.txt` — target state:

```
# swakaadvocates.co.ke — robots.txt
# Authored decision, <date>. Ruling: D-1 (both audiences admitted), P-8 (rights
# reserved, not enforced at the door), D-9 (every machine-facing signal authored).
# The firm reserves its rights in the content of this site. This reservation is a
# claim-preserving statement and is not an access control. The human-readable
# equivalent is at /legal-notice.

User-agent: *
Allow: /

Sitemap: https://swakaadvocates.co.ke/sitemap.xml
```

No `Disallow` lines. No per-crawler blocks. No `Google-Extended` stanza. If the file already exists and contains training-crawler blocks, remove them and record the removal in the changelog citing D-1.

`sitemap.xml` — one `<url>` entry per page that returns 200, and no others. Currently that is exactly two: the apex and `/publications`. Use the apex host, matching the canonicals already served. `<lastmod>` from real modification dates only — if the date is not known, omit the element rather than invent one.

**Acceptance criteria.**
1. `GET /robots.txt` → 200, `content-type` text/plain.
2. The file contains zero occurrences of the string `Disallow`.
3. The file contains exactly one `Sitemap:` line and the URL it names returns 200.
4. Every `<loc>` in the sitemap returns 200 when fetched.
5. The count of `<url>` elements equals the count of pages returning 200 — no more, no fewer.
6. No `<loc>` names a non-HTML resource.
7. The host in every `<loc>` is `swakaadvocates.co.ke` with no `www.` prefix.
8. `/llms.txt` does not exist. If one is found, it is deleted and the deletion recorded (non-goal; D-9; P-13 level 3).

**Note on the human-readable reservation.** D-9 requires that *"where a reservation is made to machines, the equivalent statement is made in human-readable form on the same property, because a notice only machines can read is not notice to the people the property serves."* That page is task A-11, which is blocked on convener-supplied legal text. Until A-11 lands, the `robots.txt` comment references `/legal-notice`; **do not ship the reference before the page exists.** Either ship both together or omit the reference line until then.

---

### A-5 — Author the firm's own description as structured data

**Objective.** Make the facts the site already states as text also available as markup, so that a retrieval agent reaching this property without rendering it gets the firm's own account rather than assembling one from directories.

**Traces to.** D-3 ADAPT, verbatim: *"The property adapts by becoming the highest-quality available source for its own description: a canonical, dated, extractable statement of its own facts — services, jurisdiction, admission status, fee basis, contact… positioned where retrieval agents reach it without rendering."* And: *"The adaptation is cheap and its value is monotone under every hypothesis in the corpus."* Also D-13 ADAPT — abstention is not a strategy, and the cost of abstention **inverts with corpus presence**: a small or new property with thin presence pays everything, because the account is assembled from directories, aggregators and competitors instead. P-13 level 1. P-15 (thin common core: unambiguous entity identity, facts as retrievable text).

**Depends on.** P-1 (raw HTML — you must know what markup already exists before adding any), P-3 (how the site is published, which determines whether a generator can run at all), OD-J. Possibly P-23, P-26.

**Approach — read this before writing any markup.** OD-J, as revised, establishes that the machine layer should be **generated from the page** rather than maintained beside it, so that a text edit propagates automatically as P-14 requires. On Property B that is task B-20 and it is buildable today. Here it is not, until P-3 tells us how this site is published and whether a generation step can sit in that pipeline.

So this task proceeds in two stages:

- **Stage 1, now:** hand-author the graph to the specification below, and build `tools/verify-jsonld-verbatim.py` (task A-16) as the drift guard. This is detection, not propagation, and it is recorded as a substitution under OD-J rather than presented as compliance with P-14.
- **Stage 2, once P-3 lands:** port Property B's generator to this property if the publishing pipeline permits it, and thereafter never hand-edit the graph again. If the pipeline does not permit it, record that as the reason and keep the checker.

**Do not skip stage 1 waiting for stage 2.** The description work is what D-3 calls *"cheap and its value is monotone under every hypothesis in the corpus"*, and it should not wait on tooling.

**Files affected.** `/` and `/publications`.

**Change specification.**

First, determine from the raw HTML whether JSON-LD already exists. Inventory §B.3.1 records this as *"the single largest evidentiary gap"* and explicitly as absence-of-observation, **not** absence-of-markup. If markup exists, extend it; do not replace it.

Add one `<script type="application/ld+json">` block per page, immediately before `</head>`.

**Homepage graph** — `LegalService` (or `Attorney` if the raw HTML suggests a single-practitioner framing; default to `LegalService`), populated **only** from strings already rendered on the page:

- `name`, `url`, `description` — from the existing `<title>`/`description` meta, unchanged
- `address` → `PostalAddress`: street address, P.O. box, `addressLocality: "Nairobi"`, `addressCountry: "KE"` — copied verbatim from the contact block
- `telephone` — both numbers, in the `tel:` link format already present
- `email` — as rendered
- `areaServed` — from "Republic of Kenya · East Africa · International"
- `foundingDate: "2016"` — from "Established 2016"
- `memberOf` — two `Organization` nodes: Law Society of Kenya, East Africa Law Society, named exactly as the footer names them
- `knowsAbout` — the seven practice-area names, verbatim per DNC-1
- `hasOfferCatalog` → `OfferCatalog` → seven `Service` nodes, each `name` and `description` copied verbatim from the services section

**Publications page** — `CollectionPage` with an `ItemList` of the six entries, each `name` and `datePublished`/status copied verbatim from the rendered list.

**Hard constraints on this task.**

- **P-14 admissibility test:** *"No fact may appear in the machine layer that is not also stated as text on the human page."* Every string in the graph must be findable, verbatim, in the rendered text of the same page. There are no exceptions and no "obviously implied" values.
- **Barred properties:** no `priceRange`, no `aggregateRating`, no `review`, no `openingHours` (absent from the site, §B.5.4), no `numberOfEmployees`, no invented `identifier`.
- **`Person` node for John Swaka:** include **only** if PRE-TASK P-23 authorises it and only with values the page states. The name currently appears only in the email local-part, a LinkedIn caption and the meta `keywords` (§B.5.4) — that is thin, and inventing a bio to justify a richer node is barred by DNC-4 and the no-invention rule.
- **No `dateModified` unless a real modification date is known.**

**Acceptance criteria.**
1. Both pages contain valid, parseable JSON-LD; zero parse errors.
2. **Verbatim test, automated:** for every string-valued leaf in the graph, that exact string appears in the rendered text content of the same page, or in `data/declared-values.json` with a comment naming why it has no rendered counterpart. Built at task A-16. Any failure is a task failure, not a warning.
3. The graph contains none of: `priceRange`, `aggregateRating`, `review`, `ratingValue`, `openingHours`.
4. Google Rich Results Test and Schema.org validator both return no errors.
5. Rendered page output is byte-identical to before, except for the added `<script>` block.

---

### A-6 — Fix the dead LinkedIn link

**Objective.** Remove a call-to-action that goes nowhere.

**Traces to.** Inventory §C.1.16 — `href="#"` under a section captioned "Follow John Swaka on LinkedIn →". D-3 (contactability among the facts a verification surface must confirm). P-16 (the destination's retained function is verification).

**Depends on.** P-21.

**Files affected.** `/publications`.

**Change specification.** If a URL is supplied, replace `href="#"` with it, adding `rel="noopener"` and `target="_blank"`. **If no profile exists, delete the entire section** — heading, copy and link. Do not leave a call-to-action pointing at an anchor.

**Acceptance criteria.**
1. `grep -c 'href="#"' ` across the property returns 0, excluding legitimate in-page anchors that resolve to an existing `id`.
2. If retained, the LinkedIn URL returns 200.
3. No section remains whose only action target is `#`.

---

### A-7 — Correct the stale forthcoming-publication labels

**Objective.** Stop the site asserting a future that is four months past.

**Traces to.** Inventory §C.1.15, §B.5.5 — five items labelled "Coming April 2026" through "Coming June 2026", all past as of the inspection date. P-16: the arriving visitor's question is *"is what I was told true?"*, and the page must confirm identity, credentials, scope, price, **recency**. D-3 (the property becomes the highest-quality source for its own description; a description contradicted by a calendar is not that).

**Depends on.** P-22.

**Files affected.** `/publications`.

**Change specification.** Apply whichever the convener supplies:
- revised dates → update in place;
- or drop dates → label reads "In preparation" with no month;
- or drop items → remove the entries entirely.

**Do not invent a date under any circumstances.** If P-22 is unanswered, this task is BLOCKED and remains so.

**Acceptance criteria.**
1. Zero occurrences of any string matching `Coming (January|February|...|December) 2026` where that month is in the past.
2. No future-tense publication label carries a date earlier than the current date.
3. Item count unchanged unless the convener authorised removal.

---

### A-8 — Meta-layer hygiene

**Objective.** Make the social and title layer internally consistent.

**Traces to.** Inventory §C.1.17 — homepage `<title>` and `og:title` differ; `og:site_name` present on `/publications` and absent on `/`; no `og:image` and no `twitter:` tag on either page. P-13 level 1 (configuration hygiene, documented consumers).

**Depends on.** P-24 for the image half only. The rest is unblocked.

**Files affected.** `/`, `/publications`.

**Change specification.**
- Add `og:site_name` to the homepage: `Swaka Advocates`.
- Make `og:title` on the homepage identical to `<title>`. **DNC-6 applies to the footer strings, not to `og:title`** — but the `<title>` itself is not to be edited; change the `og:title` to match it, not the reverse.
- Add `og:locale: en_KE`. Add `og:type: website` where missing.
- If P-24 supplies an image: add `og:image` (absolute URL), `og:image:width`, `og:image:height`, `og:image:alt`, and `twitter:card: summary_large_image` with `twitter:title` and `twitter:description` mirroring the `og:` values. **If no image is supplied, add no image tags at all** — a broken `og:image` is worse than none (see Property A's `/assets/og-image.jpg`, referenced everywhere and existing nowhere, §C.1.5).

**Acceptance criteria.**
1. Both pages carry `og:site_name`, `og:title`, `og:description`, `og:type`, `og:url`, `og:locale`.
2. `og:title` string-equals `<title>` on both pages.
3. Every URL in any `og:` or `twitter:` tag returns 200. Zero tolerance.
4. No `twitter:` tag exists without a corresponding valid `og:image`.

---

### A-9 — Semantic markup pass, with zero visual change

**Objective.** Give the page's existing structure real semantics, so that a machine reading the DOM or the accessibility tree gets the same outline a human eye gets.

**Traces to.** **D-17, RATIFIED and expressly binding on implementation briefs:** *"semantic HTML first; ARIA only where a native element cannot express the semantics; every ARIA addition justified in the change log."* Inventory §B.4.1: the seven Roman-numeral practice-area teasers in the hero band render as plain text with no heading markup, as do the eyebrow labels, the four timeline dates and the four client-segment tags — so the **first** statement of the practice areas is unheaded and only the second carries `h3`s. D-6 (the extractable factual spine on the same page as the human voice). Charter II.5 convergence: agent-readability and accessibility are one discipline.

**Depends on.** P-1. This task cannot be specified without the raw HTML — §B.4.2 through §B.4.6 are all NOT DETERMINABLE, so whether `<main>`, `<header>`, `<nav>` and `<footer>` exist at all is unknown.

**Files affected.** `/`, `/publications`, and the stylesheet.

**Change specification.**
1. Confirm one `<h1>` per page (inventory indicates yes) and no skipped levels.
2. Give the seven hero teasers real heading elements at the level their position warrants — almost certainly `h3` under the hero's `h2`. **Match the existing visual treatment exactly by adding CSS that neutralises the browser's default heading styling**, so the rendered result is pixel-identical.
3. Ensure `<main>`, `<header>`, `<nav>` and `<footer>` landmarks exist, wrapping the regions they describe. Add only what is missing.
4. Add a skip link to `<main>`, visually hidden until focused.
5. Confirm `<html lang="en">` exists (§B.5.1 records this as NOT DETERMINABLE).
6. **ARIA: add none.** WebAIM 2026 measurement in D-17's material facts records ARIA-bearing pages averaging 59.1 errors against 42 for pages without. If you believe an ARIA attribute is genuinely necessary, stop and report the specific native element that cannot express the semantics, and wait.

**Barred.** No keyboard-operability or zoom-tolerance specification may be written in this task, and the figures 78.33 / 41.67 / 28.33 may not be cited as a rationale. D-4 severs: the ruled components are *"no fact of consequence is carried in a pixel-only element; anything a machine must read is real text; the early portion of a page carries the substantive claim"* — the degradation curve is held on V-4 and is not available to you.

**Acceptance criteria.**
1. Exactly one `<h1>` per page; heading levels descend without skipping.
2. Exactly one `<main>` per page.
3. **Visual regression: screenshots at 390px, 768px and 1440px viewport widths, before and after, differ by zero pixels** outside the newly-added skip link in its focused state. This is a hard gate — if it fails, revert.
4. Count of ARIA attributes after ≤ count before. Any increase requires a justification line in the commit body naming the native element that failed.
5. An automated accessibility scan (axe or Lighthouse) reports no new violations and no new "serious" or "critical" items.
6. `<html lang>` is present and correct on both pages.

---

### A-10 — Resolve the homepage logo anomaly

**Objective.** Make the logo resolvable and described on both pages.

**Traces to.** Inventory §C.1.19, §B.4.7 — the logo `src` resolved empty on `/` across both extraction passes while `/publications` served `logo-dark.png`. Cause unresolved. D-4 severed component: anything a machine must read is real text — and an unresolvable brand image weakens the entity-identity signal P-15 names as part of the thin common core.

**Depends on.** P-1, P-24.

**Change specification.** Diagnose from the raw HTML: inline SVG, `srcset` without `src`, CSS background, or a lazy-load placeholder. Then ensure the homepage logo element has a resolvable `src` and `alt="Swaka Advocates"`, matching `/publications`. Do not change how the logo looks.

**Acceptance criteria.**
1. On both pages, the logo element has a non-empty `src` (or a `<use>` reference that resolves) and non-empty `alt`.
2. The referenced asset returns 200.
3. Visual regression: zero pixel change.

---

### A-11 — Human-readable rights reservation and data-protection notice

**Objective.** Give the machine-facing reservation its human-readable equivalent, and close a notable gap: a site whose own practice offering includes Kenya DPA compliance counsel currently publishes no data-protection notice.

**Traces to.** D-9 ADAPT, the human-side half of the ruling: *"where a reservation is made to machines, the equivalent statement is made in human-readable form on the same property, because a notice only machines can read is not notice to the people the property serves."* Inventory §B.6.3: no privacy policy, no terms of engagement, no data-protection notice. P-24(a) (Kenya's regulatory frame at Tier 1).

**Depends on.** Convener-supplied legal text. **Claude Code drafts no legal content for this property under any circumstances.**

**Change specification.** Create `/legal-notice` as a page carrying: (a) the rights reservation in plain language, matching the `robots.txt` comment in substance; (b) the data-protection notice supplied by the advocate; (c) any terms of engagement or disclaimer the advocate supplies. Link it from the footer of both pages. Add it to `sitemap.xml`. Markup: `WebPage`, nothing more.

Claude Code's contribution is the page scaffold, the footer link, the sitemap entry and the routing. **The words are the advocate's.** If no text is supplied, this task is BLOCKED — and while it is blocked, task A-4's `robots.txt` must not reference `/legal-notice`.

**Acceptance criteria.**
1. `/legal-notice` returns 200 and appears in `sitemap.xml`.
2. It is linked from the footer of both existing pages.
3. `git log` shows the page content arriving in a commit whose message names the convener as the source of the text.
4. The `robots.txt` reference and the page ship in the same commit or in a strict order that never leaves the reference dangling.

---

### A-12 — Provenance-marking convention (repository policy, not a site change)

**Objective.** Adopt provenance marking as a design primitive now, while it is nearly free.

**Traces to.** D-14, ADAPT prospectively, verbatim: *"any synthetic or assisted content on either property carries its marking from creation, before any duty attaches, because retrofitting marking across a site is expensive and adopting it early is nearly free."* Material facts include Kenya's Bill expressing a human-dignity interest through a machine-legible marking duty.

**Files affected.** `docs/` only. **No site change.**

**Change specification.** Write `docs/provenance-convention.md`: any AI-assisted or AI-generated text, image or asset entering this property carries a marking from creation — at minimum a commit-message declaration, and where the content is published as an article or image, an on-page statement in the form the advocate approves. Record that this is adopted ahead of any legal duty, per D-14.

**Acceptance criteria.** The file exists, cites D-14, and is referenced from `docs/machine-layer-changelog.md`.

---

### A-13 — Machine-layer change log (running, opened now, never closed)

**Objective.** Make every machine-facing change on this property attributable to a human decision.

**Traces to.** D-9: *"Every machine-readable file on the properties must be attributable to a human decision recorded in the change log required by P-4."*

**Change specification.** One entry per machine-facing change, appended at execution time, not retrofitted. Columns: date, task ID, file, what changed, ruling ID, who decided. Backfill entries for A-4, A-5, A-8 as they land.

**Acceptance criteria.** Every commit whose message says `Human-visible change: no` and which touches `robots.txt`, `sitemap.xml`, any JSON-LD block or any `<meta>` tag has a corresponding changelog entry in the same commit.

---

### A-14 — `www` hostname decision (implementation only after OD-F)

**Objective.** Either make `www.swakaadvocates.co.ke` resolve, or record that it deliberately does not.

**Traces to.** Inventory §B.1.5, §C.1.14: NXDOMAIN on all record types, so *"any inbound link, citation, directory listing, business-profile entry, or printed reference using `www.swakaadvocates.co.ke` fails at resolution — before any HTTP request, before any redirect, before Cloudflare."* P-15 (retrievability itself is part of the thin common core).

**Depends on.** P-25 / OD-F.

**Change specification.** This is a DNS action the convener takes, not Claude Code. If the answer is yes: add a proxied CNAME `www` → apex and a redirect rule returning 301 to the apex, preserving path. If no: record the decision and its date in `docs/cloudflare-posture-2026-09.md`.

**Acceptance criteria.** Either `https://www.swakaadvocates.co.ke/publications` returns 301 to `https://swakaadvocates.co.ke/publications`, or the posture document carries a dated decision line stating that `www` will not exist and why.

---

### A-16 — Drift guard, and generator port if the pipeline allows

*Numbered late, executes with A-5. Appended rather than renumbered, per the Conflict Register's numbering principle.*

**Objective.** Prevent the machine layer and the page from drifting apart, by the strongest means this property's publishing pipeline permits.

**Traces to.** P-14; OPEN DECISION OD-J as revised. The failure this guards against is documented on the sibling property at inventory §C.1.4, where marked-up FAQ content and rendered FAQ content diverged so far that three questions exist only in the markup and three only on the page.

**Depends on.** P-3.

**Change specification.**

**Part 1 — the checker, unconditional.** Build `tools/verify-jsonld-verbatim.py`: for every page, extract all JSON-LD, and assert every string-valued leaf appears verbatim in that page's rendered text or in `data/declared-values.json`; assert every URL-valued leaf plus every `og:`, `twitter:` and `<link>` URL resolves. Run it on every commit. Exit non-zero on any failure.

**Part 2 — `data/declared-values.json`.** The small set of values with no rendered counterpart: `@type` choices, `addressCountry: "KE"`, `@id` patterns, `inLanguage`, `foundingDate` normalised from "Established 2016". Keep it under about fifteen entries. Each entry carries a comment naming its rendered counterpart, or stating that it has none and why.

**Part 3 — the generator, conditional on P-3.** If the publishing pipeline permits a generation step, port `tools/generate-machine-layer.py` from Property B, adapted to extract this property's facts: the seven practice-area names and descriptions from the services section, the contact block's address, phones and email, the credential strings, and the publications list. Thereafter the graph is never hand-edited.

If the pipeline does not permit it — for instance if the site is published through a hosted builder with no build step — **record that as a finding about the platform**, in the same spirit as P-22's African-test amendment, which converts an absence of log access into a finding about the host rather than a bar on the publisher.

**Acceptance criteria.**
1. `tools/verify-jsonld-verbatim.py` exists, runs on every commit, exits non-zero on drift.
2. `data/declared-values.json` has at most 15 entries, each commented.
3. A deliberate drift test is run and recorded: alter one rendered string, confirm the checker fails, revert.
4. Either the generator is ported and its idempotence and drift tests pass, or `docs/machine-layer-changelog.md` records why the pipeline does not permit one.

---

### A-15 — Citation probe (post-deadline; start once A-1 is stable)

**Objective.** Measure change in the property's own description over time.

**Traces to.** P-22 clause 3: *"a repeatable citation probe — a fixed set of intent-queries run against each major assistant on a fixed cadence, recorded verbatim with dates. Not to measure market share, which is unmeasurable under P-7, but to measure change in the property's own description, which is measurable and is the only remedy the corpus supports."* D-18 notes the settling instrument for the off-page question *"is the same instrument as P-4 item 3 and P-22(a), so the cost of settling this entry is zero marginal spend."* D-19 extends it: record whether the assistant surfaces the destination's own words or its own summary.

**Change specification.** Fix a query set of 10–15 intent queries — the kind a prospective client would actually ask, in Kenyan phrasing, covering the seven practice areas, the firm by name, and two or three category queries where the firm is not named. Run monthly against each major assistant. Record the full response verbatim, with date, assistant, and whether the firm was mentioned, correctly described, cited with a link, and whether the cited support was on-page or third-party.

**Standing citation restrictions that bind the reporting of this probe:** the CL-5 currency qualifier on any misattribution figure (*"as measured March 2025; not re-tested"*); no conversion-premium magnitude may be cited, averaged or merged (CL-4); no spoof rate (CL-2); no Cloudflare-derived number as the sole basis of a decision (P-3).

**Acceptance criteria.**
1. `probe/queries.md` fixed and dated; changes to it are versioned, never edited in place.
2. `probe/YYYY-MM/<assistant>.md` per run, response verbatim.
3. A per-run summary recording, per query: mentioned y/n, described accurately y/n, linked y/n, support on-page or third-party.

---

## 5. VERIFICATION

### 5.1 Run after every task

- `tools/verify-jsonld-verbatim.py` — the P-14 admissibility check, built at A-16. If the generator was ported, re-run it after any page-text change and commit the regenerated markup in the same commit. **This is the most important check in the suite** and it must pass on every commit that touches page text or markup, because the propagation problem it guards against is the reason P-14 exists.
- Visual regression at 390 / 768 / 1440px. Zero pixel change except where a task explicitly authorises one.
- Link check: every `href`, `src`, `<loc>` and JSON-LD URL returns 200.
- Accessibility scan: no new violations.
- `grep -r 'REPLACE_WITH\|TODO\|FIXME\|lorem'` returns nothing.

### 5.2 Run before 15 September

1. **A-1 is running and has produced at least seven consecutive daily files.** If this is not true, nothing else in the programme matters — the natural experiment D-5 authorises will be unobservable.
2. `docs/cloudflare-posture-2026-09.md` is complete, dated, and the tier decision has been taken and recorded.
3. `robots.txt` and `sitemap.xml` are in their target state and every URL in them resolves.
4. Every crawler user-agent in the A-1 list receives a 2xx for `/` and `/publications`. **Any non-2xx to a retrieval agent before the deadline is a live incident**, not a finding to note.

### 5.3 Run on 16–20 September

This is the paired comparison D-5 authorises, and its value depends entirely on the before-state having been captured.

1. Diff the observation logs across the boundary. For each (URL × user-agent) pair, did the status code change? Did `cf-mitigated` or a challenge header appear? Did the body hash change?
2. **Compare against Property B**, which is unproxied and therefore outside the control plane (§C.1.20). Property B is the control case. A change appearing on both properties is not attributable to the Cloudflare default; a change appearing only on this one is.
3. Record findings in `docs/observation-findings-2026-09.md` with dates and raw log references. **Grade honestly**: a single observation from one network path establishes what that path saw, and nothing about other agent classes — inventory §B.2.7 makes this point about its own single fetch and the same discipline applies here.
4. Do **not** conclude that the flip did or did not ship on the basis of this property alone. P-23 clause 1 grades it as announced policy, not shipped, and no brief in the corpus observed it in production.

### 5.4 Measurement setup (P-22, standing)

The three instruments, in the order the position mandates:

1. **Server-side request logs with user-agent retention** — from Cloudflare Analytics if the tier provides it (P-18). Not analytics JavaScript. If unavailable, apply the African-test amendment: external probe plus whatever the host provides, **and record the absence of log access as a finding about the host**, in `docs/cloudflare-posture-2026-09.md`.
2. **Baseline emission-and-blocking audit** — A-1 is this instrument. What the property emits, and what is blocked at every layer above it that the owner does not control.
3. **Repeatable citation probe** — A-15.

**No AEO/GEO spend is authorised until 1 and 2 are in place.** P-22 is explicit that the mandate precedes the spend.

### 5.5 Accounting frame

Per D-16 ADAPT, which changes the accounting and not the content: the firm's published analysis is reclassified as a **citation asset**, evaluated on whether it is being cited, not on whether it is being visited. No article is withdrawn, none is gated, and no editorial decision is taken on this — D-16's evidence is Tier 3–4 single-portfolio and *"too thin to carry one."*

---

## 6. TRACEABILITY INDEX

| Task | Rulings | Inventory |
|---|---|---|
| A-1 | P-23(2), P-22(2), D-5 | §B.2.7, §C.1.20 |
| A-2 | P-4, D-9 | §B.7, §C.2.3 |
| A-3 | D-5, D-8, P-23(1), P-3 | §C.2.1, §B.1.3 |
| A-4 | D-1, D-9, P-8, P-13(1) | §B.2.1–§B.2.4 |
| A-5 | D-3, D-13, P-13(1), P-14, P-15 | §B.3.1, §B.3.6, §B.5.3, §B.5.4 |
| A-6 | D-3, P-16 | §C.1.16, §B.6.1 |
| A-7 | P-16, D-3 | §C.1.15, §B.5.5 |
| A-8 | P-13(1) | §C.1.17, §B.3.2 |
| A-9 | **D-17 (binding)**, D-6, D-4 (severed) | §B.4.1–§B.4.6 |
| A-10 | D-4 (severed), P-15 | §C.1.19, §B.4.7 |
| A-11 | D-9, P-24(a) | §B.6.3 |
| A-12 | D-14 | — |
| A-13 | D-9, P-4 | — |
| A-14 | P-15 | §B.1.5, §C.1.14 |
| A-15 | P-22(3), D-18, D-19, P-19 | §C.2.5 |
| **A-16** | **P-14**, OD-J, P-22 (amendment logic) | §C.1.4 (sibling-property evidence), §C.2.4 |

---

*End of Implementation Brief A. Every task above traces to a ruling or an inventory finding. Where a decision was needed and none existed, it was routed to the OPEN DECISIONS LIST rather than taken silently.*
