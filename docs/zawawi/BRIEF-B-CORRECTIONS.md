# BRIEF B — CORRECTIONS AGAINST THE REPOSITORY

**Property:** infoonairesources.shop
**Repository inspected:** `C:/Users/User/inforionairesources.shop`, working tree at commit `08a8adb`
**Date of inspection:** 3 September 2026
**Corrections recorded by:** Claude (implementing agent)
**Corrections accepted by:** Benta (convener), 3 September 2026

---

## What this file is

Implementation Brief B and the site inventory describe the property as it stood on **28 August 2026**. This file records every place where the repository as inspected on **3 September 2026** does not match that description.

Brief B §0, working method clause 1, is the governing rule:

> Where the brief and the file disagree, **the file is the fact**.

These are **corrections to the convener's documents, not decisions**. Nothing here changes what is to be built, what is permitted, or what is forbidden. Each entry records what the document said, what the repository contains, how it was counted, and whether the brief was amended in consequence.

**`docs/zawawi/site-inventory-v1.md` is NOT amended.** It is a dated observation record. Amending it would destroy the only thing it is good for — a statement of what was true on a stated date, made by a stated observer. Where the inventory is internally inconsistent, that inconsistency is recorded here and the inventory is left as issued.

**`docs/zawawi/IMPLEMENTATION-BRIEF-B-infoonairesources.md` IS amended**, because its acceptance criteria are written as counts and an acceptance criterion that names the wrong number cannot be checked.

Both documents were committed to version control unmodified in commit `3626356` (DOC-0) before any amendment, so that the record shows what was issued and what was subsequently corrected.

---

## C-1 — The property has thirteen content pages, not twelve

**What the brief says.** The brief is written in twelves throughout: "twelve documents" (§0), "all twelve content HTML files" (B-3, B-6, B-11, B-13), "all twelve pages" (B-8, B-20), "4 of 12 pages" (B-11), "twelve total" (B-13), "all twelve files" (§5.1).

**What the inventory says.** The inventory is internally inconsistent on this point. §A.3.1 says **thirteen**. §A.3.6, §A.3.7 and §A.4.1 say **twelve**.

**What the repository contains.** **Thirteen** content HTML files, plus one Search Console verification file, for **fourteen** `.html` files in total.

The thirteen content pages:

1. `index.html`
2. `deep-dives/index.html`
3. `deep-dives/glm-5-2-global-south/index.html`
4. `opportunities/index.html`
5. `opportunities/courses/index.html`
6. `opportunities/courses/ai-impact-lab-humanitarian-supply-chain/index.html`
7. `opportunities/jobs/index.html`
8. `opportunities/jobs/ai-technical-lead-grit/index.html`
9. `opportunities/jobs/knowledge-lawyer-ai-innovation-weightmans/index.html`
10. `opportunities/jobs/research-engineer-domain-scaling-anthropic/index.html`
11. `opportunities/resources/far-ai/index.html`
12. `opportunities/scholarships/index.html`
13. `opportunities/scholarships/oxford-ethics-ai-accelerator-fellowship/index.html`

The fourteenth: `google9d706cf5c30241d2.html` (54 bytes, Search Console verification, no `<title>`, no `<h1>`).

**How counted.** Directory listing of every `.html` file in the working tree, cross-checked against `grep -rl "mailto:info@infoonairesources.shop" --include=*.html .`, which returns exactly the thirteen content pages and not the verification file.

**Brief amended.** Yes — every "twelve" that counts content pages becomes "thirteen"; the one place that counts `.html` files becomes "fourteen" (see C-11).

---

## C-2 — `sitemap.xml` declares thirty-two URLs, not thirty-one

**What the brief says.** §1 Mission: "Eighteen of thirty-one sitemap URLs have no file behind them." B-4 traces line: "thirty-one URLs declared, thirteen exist, **eighteen do not**."

**What the repository contains.** **Thirty-two** `<url>` elements. Thirteen correspond to content pages that exist. Eighteen are phantom — no file behind them. One is `/llms.txt`, which exists but is not an HTML page.

13 + 18 + 1 = 32. The brief's arithmetic (13 + 18 = 31) omits the `llms.txt` entry, which B-4's own change specification separately instructs be removed.

**How counted.** `grep -c "<url>" sitemap.xml` → 32; `<loc>` values enumerated and each checked against the working tree.

**Brief amended.** Yes — §1 and the B-4 traces line now read thirty-two, and the traces line states the composition explicitly so the three categories add up.

---

## C-3 — The seven-link footer navigation exists only on `index.html`

**What the brief says.** B-6 traces line quotes inventory §A.5.3: "The homepage footer nav offers seven; six of seven 404." The change specification then says "Same for the footer nav … on the homepage", which is correct, but §C.1.6's "six distinct nav variants across twelve pages" invites the reading that a footer nav is present site-wide.

**What the repository contains.** Only `index.html` carries the seven-link footer navigation. The footers of the other **twelve** content pages contain the `mailto:info@infoonairesources.shop` address and no navigation links.

**How counted.** Read of the footer block in all thirteen content pages.

**Brief amended.** Yes — a dated verified-fact note added under B-6 recording that the footer-nav repair is a single-file change while the primary-nav repair is a thirteen-file change.

---

## C-4 — `<link rel="icon">` is present on all thirteen pages, not the homepage alone

**What the brief says.** B-11 traces line lists `<link rel="icon">` → `/favicon.ico` among the dangling references, without stating its extent. Acceptance criterion 5 says "commit one or remove the `<link rel="icon">`", singular.

**What the repository contains.** `<link rel="icon" href="/favicon.ico">` appears on **all thirteen** content pages. `favicon.ico` does not exist in the repository. So the reference is broken thirteen times, and the removal branch of B-11(5) is a thirteen-file edit, not a one-file edit.

**How counted.** `grep -rl 'rel="icon"' --include=*.html .` → thirteen files.

**Brief amended.** Yes — a dated verified-fact note added under B-11(5).

---

## C-5 — The homepage carries four statistics, of which two are unsourced — not six of which two are unsourced

**What the brief says.** B-15 traces line: "four homepage statistics carry named sources; two do not". That reads as six statistics in total.

**What the repository contains.** **Four** statistics in the homepage stat block. **Two** carry named sources in the `stat-source` slot:

- "Microsoft AI Diffusion Report, 2026"
- "PwC, analysing 1 billion job ads, 2025"

**Two** carry non-source text in the same slot — descriptive copy occupying the position where a source belongs:

- "Africa, South Asia & MENA combined" (against "198M internet-connected knowledge workers")
- "The gap this platform exists to close" (against "54% … only 4% are acting")

The two statistics B-15 names are correctly identified. Only the total is wrong. B-15's scope is therefore **two of four**, not two of six.

**How counted.** Read of the homepage stat block; each `stat-source` element enumerated and classified.

**Brief amended.** Yes — the B-15 traces line is rewritten to state four total, two sourced, two not, and to name what currently occupies the source slot on the two unsourced ones, so that the task is not mistaken for one of adding a missing element.

---

## C-6 — Nineteen `.reveal` elements, not twenty

**What the brief says.** B-14 traces line and acceptance criteria: "twenty `.reveal` elements".

**What the repository contains.** **Nineteen** elements whose `class` attribute contains `reveal`, all on `index.html`.

**How counted.** `grep -c 'class="[^"]*reveal' index.html` and a read of each match.

**Brief amended.** Yes — four occurrences of "twenty" in B-14 become "nineteen".

---

## C-7 — The `www` → apex redirect is HTTP 301, not undetermined

**What the inventory says.** §A.1.5 grades the status code of the `www` → apex redirect **NOT DETERMINABLE**.

**What was observed.** `https://www.infoonairesources.shop/` returns **HTTP 301** with `Location:` on the apex host. Observed 3 September 2026 by direct fetch from this machine's network path.

This does not change what B-3 does. It removes the uncertainty about *why* it matters: the property currently declares a canonical host from which the server permanently redirects away, which is a definite defect rather than a suspected one.

**How observed.** Single HTTPS fetch, headers only. This establishes what one fetcher saw on one date from one network path and nothing more.

**Brief amended.** Yes — a dated verified-fact note added under B-3.

---

## C-8 — The deep-dive `FAQPage` is clean; the divergence is homepage-only

**What the brief says.** B-9, final paragraph: "Apply the same reconciliation to the `FAQPage` on `/deep-dives/glm-5-2-global-south/` — verify it matches its rendered six-question FAQ before assuming it does."

**What the repository contains.** It matches. All **six** marked-up `Question` name strings on `/deep-dives/glm-5-2-global-south/index.html` correspond to the six rendered `<h3>` question headings. There is no six-versus-five divergence on that page.

**Scope of this check.** Question strings only. The `acceptedAnswer.text` bodies have **not** been compared verbatim against the rendered answer text. That comparison is the job of `tools/verify-jsonld-verbatim.py` and is not asserted here.

**How counted.** Marked-up `Question.name` values and rendered `<h3>` strings enumerated and compared.

**Brief amended.** Yes — a dated verified-fact note added under B-9 recording the question-string check as done and the answer-body check as outstanding.

---

## C-9 — The programme documents were duplicated at the repository root

**What was found.** Four programme documents existed both at the repository root and in `docs/zawawi/`, all untracked. A fifth, Implementation Brief A, existed **only** at the repository root.

**Resolved.** The convener ruled `docs/zawawi/` canonical on 3 September 2026. Commit `3626356` (DOC-0) committed the `docs/zawawi/` copies unmodified, moved Brief A into `docs/zawawi/`, and deleted the four root duplicates.

**Brief amended.** No — this is a repository-hygiene fact, not a statement in the brief.

---

## C-10 — DNC-9 attributes landmarks to the wrong task

**What the brief says.** §3, DNC-9: "Task **B-14** adds landmarks; it does not restructure headings."

**What is correct.** Landmarks are **B-13** ("Landmarks and skip link — semantic HTML only"). B-14 is "Make the homepage legible without JavaScript".

**Brief amended.** Yes — `B-14` → `B-13` in DNC-9.

**This amendment was made inside the DO-NOT-CHANGE register.** Brief B §0 forbids modifying §3. The convener authorised this specific amendment on 3 September 2026. The reason: DNC-9 is a protective rule that names the task permitted to touch heading structure; naming the wrong task makes the protection unenforceable, because the task actually adding landmarks is not the task the register constrains. The protection itself is unchanged — heading structure remains untouchable, and the same two counts in the same clause were corrected from twelve to thirteen under C-1. No scope was widened.

---

## C-11 — B-13's traces line counts HTML files, not content pages

**What the brief says.** B-13 traces line: "no `<main>` element exists on any page of this property — zero occurrences across all **thirteen** HTML files."

**What the repository contains.** The claim is true — zero `<main>` elements anywhere. But the count is of `.html` files, and there are **fourteen**: thirteen content pages plus `google9d706cf5c30241d2.html`.

Note the direction: this is the one place the brief undercounts by using "thirteen", where everywhere else it undercounts by using "twelve". The two errors are not the same error.

**How counted.** As C-1.

**Brief amended.** Yes — "thirteen HTML files" → "fourteen HTML files" in the B-13 traces line. B-13's own file-affected count and acceptance criteria correctly concern the thirteen content pages and are corrected under C-1, not here. The verification file gets no `<main>` and no skip link.

---

## C-12 — `llms.txt` describes ten content areas, of which two have pages behind them

**What the brief says.** §1 Mission: "The `llms.txt` describes eleven content areas of which two exist."

**What the repository contains.** `llms.txt` has **eleven** `##` headings, but one of them is `## Optional` — a section of the llms.txt format specification itself, not a content area of the site. So the file describes **ten** content areas, of which **two** have pages behind them.

**Brief NOT amended.** The convener ruled on 3 September 2026 that no amendment be made, because the mission-statement sentence is rhetorical rather than an acceptance criterion, and because B-5 will rewrite or remove the file entirely. The corrected figure is recorded here so that it is available when B-5 runs and does not have to be recounted.

**How counted.** `grep -c '^## ' llms.txt` → 11; each heading read and classified.

---

## C-13 — Implementation Brief A was delivered to the repository root

**What the convener's instruction said.** That Brief A was at `docs/zawawi/IMPLEMENTATION-BRIEF-A-swakaadvocates.md`.

**What was found.** It was at the repository root, untracked, and was the only copy in the repository. It was flagged rather than deleted under the "remove root duplicates" instruction, because it was not a duplicate.

**Resolved.** The convener directed on 3 September 2026 that it be moved into `docs/zawawi/`. Done in commit `3626356` (DOC-0), preserving the file unmodified.

**Brief amended.** No.

---

## Standing note — line endings

This machine has `core.autocrlf=true`. `index.html`, `robots.txt`, `sitemap.xml` and the other HTML files are **CRLF in the working tree and LF in the repository**; the markdown under `docs/zawawi/` is LF in both.

This is recorded because B-3 is specified as "a single mechanical pass" across thirteen HTML files plus `robots.txt` and `sitemap.xml`. Any tool that rewrites those files must preserve the existing working-tree line endings, or the diff will show every line of every file as changed and the acceptance criterion "read every changed file to confirm nothing else moved" becomes impossible to satisfy.

Git configuration is not to be changed. The constraint sits on the editing method, not on the repository.

---

## C-14 — B-3's acceptance criterion 1 cannot be met as written, and meeting it would falsify the record

**Date:** 8 September 2026
**Accepted by:** Benta, convener, the same day

**What the brief says.** B-3, acceptance criterion 1: *"`grep -rc 'www\.infoonairesources\.shop' .` returns 0 across the entire repository."*

**Why it cannot be met.** Twelve occurrences of the string live in four documents whose purpose is to record history:

| File | Occurrences | What they are |
|---|---|---|
| `docs/zawawi/site-inventory-v1.md` | 8 | the 28 August 2026 findings baseline, describing the defect |
| `docs/zawawi/IMPLEMENTATION-BRIEF-B-infoonairesources.md` | 2 | B-3's own specification, quoting the string it instructs be removed |
| `docs/machine-layer-changelog.md` | 1 | B-2's entry, recording the host it moved the `Sitemap:` line *from* |
| `docs/zawawi/BRIEF-B-CORRECTIONS.md` | 1 | C-7, recording the `www` → apex 301 |

Rewriting those twelve would make the inventory describe a defect it did not find, and make the changelog say B-2 changed the host from the host it changed it *to*. **A documentary record of a defect must be allowed to quote the defect.** A criterion that forces a document to lie about history is a defective criterion, not a standard to meet.

**Why the criterion is defective rather than the documents wrong.** Brief B was issued **2 September 2026**. The programme documents entered the repository in commit `3626356` (DOC-0) on **3 September 2026**. **The criterion predates DOC-0 by one day.** When it was written, `docs/` held nothing, and "across the entire repository" meant the served property and nothing else. It has not become wrong; the repository has grown a second kind of content that the criterion was never drafted against.

**Corrected criterion, as amended in the brief:**

```bash
grep -rl 'www\.infoonairesources\.shop' . --exclude-dir=.git --exclude-dir=docs
```

returns nothing. The scope is **the served property** — the thirteen content HTML files, `sitemap.xml` and `robots.txt`. Documents under `docs/` are records, not served artifacts, and are excluded by design rather than by oversight.

**What did not change.** All 140 in-scope occurrences were replaced. The correction narrows what is *checked*, not what is *done*.

**How counted.** `git grep -l` across the working tree with and without the `docs` exclusion, cross-checked per file.

**Brief amended.** Yes — B-3 acceptance criterion 1.

---

## What is NOT corrected here

The PRE-TASK checklist items P-1 through P-20 remain **unanswered**. Nothing in this file answers any of them, and no task blocked on them is unblocked by anything recorded here.

No count in this file changes a decision, a permission, a prohibition, or a task's scope, except B-15, whose scope was already "the two unsourced statistics" and remains so — only the denominator was wrong.

---

*Recorded 3 September 2026 under Brief B §0 working method clause 1. Accepted by Benta, convener, the same day.*
