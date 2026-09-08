# CONVENER DECISIONS — reasoning, not just outcomes

**Opened:** 8 September 2026, task DOC-2
**Convener:** Benta
**Status:** appended to, never rewritten

---

## Why this file exists

*Recorded in the convener's words:*

> The reasoning behind my decisions has lived in a chat conversation that will end. The changelog records **what** changed; it does not record **why** it was decided. This file closes that gap.

`docs/machine-layer-changelog.md` answers *what changed, and who decided it*. It does not answer *why*, and a decision whose reasoning is lost is a decision that cannot be revisited, defended or correctly overturned by whoever comes next. Several of the decisions below gave something up deliberately. A later reader who cannot see the trade will read the loss as an oversight and try to "fix" it.

**This file is appended to, never rewritten.** A decision later reversed is recorded as a new dated row saying so; the original row stays. That is the same discipline `machine-layer-changelog.md` runs under, and for the same reason.

**Related records:**

| File | Answers |
|---|---|
| `docs/machine-layer-changelog.md` | what changed to the machine layer, and who decided |
| `docs/zawawi/BRIEF-B-CORRECTIONS.md` | where the brief and the repository disagreed, and which won |
| `docs/provenance-convention.md` | how AI-assisted content is marked |
| `docs/DO-NOT-CHANGE.md` | what may not be altered |
| `../../zawawi-observation/deploys.md` | every deploy that reached a live property |
| `../../zawawi-observation/observation/README.md` | the observation series and what it cannot establish |

---

## SECTION 1 — DECISIONS

| Date | Decision | Reasoning | What it unblocked | Where implemented |
|---|---|---|---|---|
| **2 Sep 2026** | **OD-L — accept D-1's concession; remove the nine training-crawler blocks from `robots.txt`.** | The block never achieved refusal. Under most-restrictive-wins it also excluded Googlebot, Applebot and Bingbot, so it cost search visibility while achieving nothing. **What is given up is the appearance of refusal, not the fact of it.** | **B-2.** | `425f2e7`, deployed 8 Sep 2026. Changelog entry B-2. Deploy log entry 1. |
| **2 Sep 2026** | **OD-J — resolve the P-14 propagation problem by generating the machine layer from the page, rather than checking it for drift.** | Three options were filed — detect drift, build a templating system, or refuse the structured-data work — and none was right. **A generator satisfies P-14 rather than substituting for it:** the position asks that the machine layer be a projection of the human page, and a generator makes it literally that. The FAQ divergence at inventory §C.1.4 could not have occurred under one. **Residual, recorded as a substitution:** values with no rendered counterpart live in `data/declared-values.json`, capped at about 20 entries, and those remain guarded by detection rather than propagation. | Created **B-20** and **A-16**. **B-9**, **B-11** and **B-12** became generator outputs rather than hand-edits. | **Not yet implemented.** B-20 is sequenced after block 3A completes. |
| **3 Sep 2026** | **Accept all thirteen of Claude Code's corrections to Brief B.** | The August inventory contradicts itself on page count, saying thirteen in some sections and twelve in others, and I propagated the wrong number into the brief rather than counting. Claude Code counted the files. **The files win.** | Made every acceptance criterion in the brief checkable against the repository. | `c5d141e`. `BRIEF-B-CORRECTIONS.md` C-1 to C-13. |
| **3 Sep 2026** | **Amend line 145, inside the DO-NOT-CHANGE register**, which §0 forbids modifying — twelve → thirteen, and B-14 → B-13. | Both edits corrected my own drafting errors and **neither weakened a protection**. DNC-9 named the wrong task as the one permitted to touch heading structure, which made the protection unenforceable against the task actually adding landmarks. Recorded as amended on convener authority, with the reason, rather than done silently. | Made DNC-9 enforceable against the task it was written to constrain. | `c5d141e`. `BRIEF-B-CORRECTIONS.md` C-10. Copy in `docs/DO-NOT-CHANGE.md` carries a note that DNC-9 reflects the correction, not the text as issued. |
| **3 Sep 2026** | **The provenance on-page statement names Benta, not the property.** | D-9's principle is that a machine-facing signal must be attributable to a **named human decision**. An entity cannot hold editorial responsibility. The site currently has no named individual anywhere — its structured data types a team as a `Person` — so **this is the one place naming a human costs nothing and discharges something**. | **A-12 / B-16.** | `be71786`. `docs/provenance-convention.md`, "The approved form". |
| **3 Sep 2026** | **The provenance convention binds from adoption forward and makes no claim about content authored before it.** | I cannot reliably say which of the thirteen existing pages were AI-assisted, and **a wrong answer recorded as fact is worse than an honest silence**. One retrospective note names DOC-0 and DOC-1 as AI-assisted; no history is rewritten. | **A-12 / B-16**, without waiting on an audit that could not be completed honestly. | `be71786`. `docs/provenance-convention.md`, "Scope in time". |
| **7 Sep 2026** | **Merge the three document branches to `main` in order, rather than stacking further work on parallel branches.** | Three open branches each unaware of the others made every cross-reference **true of the repository but false of the branch it was read from**. That compounds with each task, and **the record has to be checkable by someone who was not here.** | Every cross-reference in `DO-NOT-CHANGE.md` and the changelog now resolves within `main`. B-2 and B-3 branched from a base containing the whole record. | `c1c1f98` (merge). Both source branches deleted so no later commit can land on a stale base. |
| **8 Sep 2026** | **Run the observation baseline before deploying B-2, rather than deploying first.** | Claude Code's ordering, accepted. **Capturing the true pre-B-2 state and then watching a known change land proves the instrument detects something you already know about, before you ask it to detect something you don't.** | Gave the series a validated first test rather than an untested instrument pointed at 15 September. | `observation/2026-09-08.jsonl` — 224 records across two passes. `robots.txt` shows two distinct `body_sha256` values, 2,061 B then 888 B; the other seven URLs show one each. |
| **8 Sep 2026** | **C-14 — scope B-3's acceptance criterion 1 to the served property, excluding `docs/`.** | **A documentary record of a defect must be allowed to quote the defect.** A criterion that forces a document to lie about history is a defective criterion, not a standard to meet. Twelve occurrences of the `www.` host live in four files that record the defect, B-2's change and the 301. The criterion was written 2 September and **predates DOC-0 by one day** — when it was drafted, `docs/` held nothing and "the entire repository" meant the served property. | **B-3**, without falsifying the inventory or the changelog. | `d6be32c`. `BRIEF-B-CORRECTIONS.md` C-14. Brief B, B-3 acceptance criterion 1, amended. |

---

## SECTION 2 — STANDING GUIDANCE THAT SHAPED THE WORK BUT LIVES NOWHERE ELSE

### a. The line-endings hazard

`core.autocrlf=true` on this machine. Files are **CRLF in the working tree and LF in the repository**.

Any tool that rewrites a file wholesale reports **every line as changed**, which makes B-3's *"read every changed file to confirm nothing else moved"* uncheckable — the signal drowns in a diff where everything moved.

**The standing rule, applied from DOC-1 onward:** every file-editing task preserves existing line endings, states an **expected changed-line count in advance**, and **stops and shows the diffstat rather than committing** if it exceeds that count. B-3 went further and used byte-level substitution, which cannot alter a line ending at all.

**This has already produced two wrong byte figures, both self-caught:**

1. `deploys.md` entry 1 predicted `robots.txt` at 2,150 B → 907 B. Those were working-tree CRLF figures. Served figures are **2,061 B → 888 B**, because the repository stores and GitHub Pages serves LF. Corrected before the after-run, so prediction and observation were compared on the same footing.
2. An earlier count of B-3's scope gave 141 lines across 15 files and claimed the occurrence count would be higher because some lines carried the string twice. Both wrong: **140 occurrences across 140 lines in 14 files**, one occurrence per line, and `robots.txt` held zero because B-2 had already moved it.

**Git configuration is not to be changed.** The constraint sits on the editing method, not on the repository.

### b. The bare-token limitation — for reading the 16 September results

The observation instrument sends **bare tokens** — `GPTBot`, `ClaudeBot`, `Googlebot` — where real crawlers send full documented strings such as `Mozilla/5.0 … compatible; GPTBot/1.1; +https://openai.com/gptbot`.

`robots.txt` matches on the product token, **so for the robots question the token is right.** But an edge classifier may key on the full string, on the absence of browser-shaped headers, or on IP reputation — signals this instrument does not reproduce.

**A null result on 16 September therefore has two causes that look identical in the data:**

1. nothing changed, or
2. the classifier ignored a bare token it would have acted on.

**The honest finding is "this instrument, sending these tokens, from this network path, saw no change."** Never "the flip did not happen." P-23 clause 1 already grades the change as announced policy, not shipped, and V-1 and V-3 are dischargeable only on or after the date. The instrument does not support the stronger sentence and no amount of clean data will make it.

Also recorded in `../../zawawi-observation/observation/README.md`, deliberately with the data rather than only with the operating instructions, so that a later reader of the logs meets it without having to find a second file.

### c. The observation series began late

Started **8 September 2026**, not the 5th the Execution Sequence intended: **seven days of before-state, not twelve.**

Those days cannot be recovered by any later work. This is the one cost in the programme that no subsequent effort buys back, and it is recorded so that a seven-day baseline is never later mistaken for the twelve the sequence assumed.

Cross-reference: `../../zawawi-observation/observation/README.md`, "Known gap in the series".

### d. The control-browser user agent was a placeholder

`observe.py` shipped with a placeholder Chrome UA string, flagged in its own header, in the file it writes, and by `check.py` on every run.

**Affected runs:** both passes of **8 September 2026** — 224 records, every `control-browser` row carrying `"control_ua_is_placeholder": true`.

**Date corrected: _not yet corrected as of 8 September 2026._**

Verified directly rather than taken as reported: `observe.py` still reads `CONTROL_UA_IS_PLACEHOLDER = True`, and the string is still `Chrome/140.0.0.0`, a version this programme has not confirmed exists. **Fill in the date on the line above when it is actually changed, and name the first run that used the real string.** Until then, the control arm of the series is measuring a browser that may not exist, and every comparison drawn against it inherits that.

---

## SECTION 3 — PENDING ANSWERS

**All twenty PRE-TASK items P-1 to P-20 are unanswered as of 8 September 2026.**

This is the programme's bottleneck. It is recorded here so that a future session sees it immediately rather than reconstructing it from the brief.

Dependencies below are taken from the brief's own **"Depends on"** lines, not inferred, except where the row says otherwise.

### Blocking a named task

| Item | What it asks | Blocks |
|---|---|---|
| **P-1** | Which of the eighteen phantom sitemap paths are real commitments, and when | **B-4** (sitemap truth), **B-5** (`llms.txt` truth or removal), **B-6** (navigation repair). One answer unblocks three tasks. |
| **P-2** | Formspree form ID, or a decision to change provider or remove the forms | **B-8** |
| **P-3** | WhatsApp number, or a decision to remove the link — it is live in production today | **B-8** |
| **P-4** | Mail routing for `info@infoonairesources.shop` — no MX exists while thirteen pages advertise it | **B-8** |
| **P-6** | Disposition of the second repository, which holds working versions of four pages the deployed site 404s on | **B-7**, and **B-6** if pages are being ported |
| **P-11** | What "Launching Month 4" counts from | **B-12** |
| **P-12** | Whether M-Pesa is live or still "from launch" | **B-12** |
| **P-13** | Legal entity behind InfoOnAIResources | **B-12**, and B-11 item 6 (`legalName`, `address`) |
| **P-14** | Sources for the two unsourced homepage statistics | **B-15** |
| **P-16** | Whether `/assets/logo.png` and `/assets/og-image.jpg` exist anywhere | **B-11** |
| **P-17** | Whether the three expired job listings and the course are closed or renewed | **B-10** |

### Deadline-critical, blocking no task but conditioning the experiment

| Item | What it asks | Why it matters now |
|---|---|---|
| **P-8** | Confirm the apex and `www` records are DNS-only / unproxied | **The control-arm design rests on this.** If the zone has been proxied since inspection, the §5.3 paired comparison must be redesigned **before** 15 September, not discovered after it. The instrument's own evidence is consistent with unproxied — `server: GitHub.com`, no `cf-ray` on any shop record across 224 requests — but that is inference from outside; the dashboard is the only place it is confirmed. |
| **P-9** | Whether any Cloudflare feature is active on the zone at all | Same. |

### Not blocking, but unanswered

| Item | What it asks | Note |
|---|---|---|
| **P-5** | GitHub Pages source branch and folder, "Enforce HTTPS" state, custom-domain verification | Informational. Inventory grades the hosting conclusion inferred. |
| **P-7** | Whether `Super45` is a second operator account or a collaborator | Feeds **B-18** (repository hygiene, post-deadline). |
| **P-10** | Why the zone publishes no MX — the DNS-side form of P-4 | Answered together with P-4. |
| **P-15** | Whether the three `Organization.sameAs` social profiles exist and are active | Feeds **B-11**. They are asserted only inside markup and linked from no visible page. |
| **P-18** | Whether the weekly-Monday-brief cadence claim is still accurate — one issue exists, dated 21 March 2026 | **No task in the brief names this as a dependency.** It is a truth-of-copy question that will need an owner. |
| **P-19** | Google Search Console verification state, and what Coverage reports about the eighteen non-existent sitemap URLs | Would supply evidence for **B-4**. |
| **P-20** | Confirm GitHub Pages provides no log access at all | **Not a gap to close — a finding to record.** P-22's African-test amendment governs. |

### What is not blocked, and could proceed today

**B-13** (landmarks, no ARIA) and **B-14** (no-JS legibility) carry **no "Depends on" line at all**. **B-17** (deliberate non-actions, recorded) likewise. These are the only substantive tasks currently executable without an answer from the convener.

Everything else in block 3A waits on P-1, P-6, P-14, P-16 or P-17, and everything in 3B waits on B-20, which the Execution Sequence sequences after 3A completes.

---

*Opened 8 September 2026, task DOC-2. Appended to, never rewritten. Decided by: Benta, convener.*
