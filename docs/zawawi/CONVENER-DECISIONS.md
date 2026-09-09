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

**Date corrected: 8 September 2026.** `Chrome/140.0.0.0` (placeholder) → `Chrome/152.0.0.0`, supplied by the convener, and `CONTROL_UA_IS_PLACEHOLDER` set to `False`. Verified byte-identical to the string supplied, and the two-line diff verified before commit.

**First run using the real string: the run of 9 September 2026** — the first scheduled run after the change. **No run on 8 September used it.** All three passes of 8 September, 336 records, carry `"control_ua_is_placeholder": true` and were sent with the placeholder.

**So the boundary between the two states falls inside the series, not before it.** Any comparison that spans 8 September is comparing control-browser rows sent with two different user-agent strings, and the `control_ua_is_placeholder` field on each record is what separates them. The thirteen declared-agent rows are unaffected — their tokens never changed.

### e. A failed scheduled run leaves only a missing file as evidence

**Confirm each day's run the same day, until 20 September.**

On **9 September 2026** the 08:00 scheduled run **failed and produced zero records**. It was registered with `-Execute "python"`, which resolves in a shell only through a Windows Store app-execution alias on the *user* PATH; the *machine* PATH has no Python entry, and the alias does not resolve under Task Scheduler. The task returned `0x80070002`, file not found, before `observe.py` was ever reached. The defect was in the runbook command, not the machine.

**The failure was invisible.** It wrote nothing, warned nobody, and left its exit code in Task Scheduler where no one looks. The only symptom was a file that did not exist. It was caught because the convener asked for the run to be confirmed — not by any alarm.

`check.py` criterion 1 would have caught the missing file, **but not until the following day**. Between now and 15 September that is a day too late, and a day lost before the boundary cannot be recovered by any later work.

**The rule:** each day, check that `LastTaskResult` is `0` and that the day's `.jsonl` holds **112 records** — 224 on the twice-daily days, 13–18 September. Procedure in `../../zawawi-observation/RUNBOOK.md` §1.

`StartWhenAvailable`, set on 8 September, did work: it re-fired the missed 08:00 slot at 09:29. The setting did its job; the command it launched was broken. **Note also that a Python reinstall or upgrade changes the interpreter path and breaks the task the same silent way.**

**Second timing irregularity in the series.** 9 September's 112 records were captured **07:38–07:42 UTC from the manually triggered fixed run**, not at the 08:00 local slot. Together with 8 September's control-UA split at 2(d), the series now carries two irregularities in its first two days, both inside the before-state window:

| Date | Irregularity |
|---|---|
| 8 Sep | Control-browser rows sent with the **placeholder** UA. Three passes, 336 records, all flagged `control_ua_is_placeholder: true`. |
| 9 Sep | Records captured from a **re-triggered** run after the 08:00 slot failed, not at the scheduled time. First run using the real UA. |

Neither invalidates the series. Both must be stated in any finding drawn from it, because a reader comparing capture times or control-arm rows across 8–9 September is comparing across a change in the instrument itself.

---

## SECTION 3 — PRE-TASK ITEMS, ANSWERED

**All twenty items P-1 to P-20 stood open from the brief's issue on 2 September until 8–9 September 2026, when the convener answered every one.** They are recorded here with the answer as given, and with the effect on the tasks each was blocking.

Where an answer creates a new missing input, or changes what a task does rather than merely unblocking it, that is stated in the row. Those are consequences of the answers, not challenges to them.

### The answers

| Item | Answer | Date | Effect |
|---|---|---|---|
| **P-1** | **All eighteen phantom paths are real commitments.** Content ships within **thirty days of 8 September 2026** — by **8 October 2026**. The declarations stay. | 8 Sep | **Changes what B-4, B-5 and B-6 do.** They become **verification** tasks run *after* content lands, not removal tasks. See "What this reverses" below. |
| **P-2** | **Formspree**, form ID `xjyvaqnb`, endpoint `https://formspree.io/f/xjyvaqnb`. Both homepage forms use it. Free tier, **50 submissions/month**. | 8 Sep | Unblocks **B-8**, first of three. |
| **P-3** | **WhatsApp `0703308873`.** Confirmed by the convener as the shop's number, **knowingly shared** with the Swaka Advocates site. | 8 Sep | Unblocks **B-8**, second of three. |
| **P-4 / P-10** | **Google Workspace** on `infoonairesources.shop`. MX `smtp.google.com` priority 1, at Cloudflare. `info@` is an **alias on `benta@`**, not a second user. **Test message received 8 September.** DKIM TXT `google._domainkey` added 8 September; Cloudflare shows DKIM in use. **SPF and DMARC not yet published** — the convener rules this a follow-up, not a PRE-TASK. | 8 Sep | Unblocks **B-8**, third of three. **B-8 is now fully unblocked.** The advertised address receives mail, so it stays on the site. Open follow-up: SPF and DMARC. |
| **P-5** | Source **"Deploy from a branch"**, `main`, `/` (root). Custom domain `infoonairesources.shop`, **DNS check successful** (OBSERVED, dashboard, 9 September). **Enforce HTTPS: OFF.** | 9 Sep | **Hosting finding recorded: `http://` is served without redirect to `https://`.** Convener ruling: **do not change inside the freeze.** Added to the post-freeze list beside B-18/B-19, to be enabled **on or after 21 September**, with a `deploys.md` prediction written first. |
| **P-6 / OD-G** | **Convener Ruling.** Port the four working pages from `infoonairesources-site` into this repository under **B-7**, verify they render, then **archive — not delete** — the second repository. | 8 Sep | Unblocks **B-7**, and **B-6**'s ported-pages branch. Archive step joins **B-18**. |
| **P-7** | **`Super45` is not the convener.** Identity and access disposition **deferred to B-18**. | 8 Sep | Does not block. Recorded as an **open access question**: an account that is not the convener has access to the repository, and who it is remains unestablished until B-18. |
| **P-8** | **CONFIRMED OBSERVED** in the Cloudflare dashboard, 8 September: **all apex A records DNS-only (grey cloud)**. AI Crawl Control shows **zero requests**, consistent with unproxied. | 8 Sep | **The control-arm design holds.** The §5.3 paired comparison needs no redesign. This was the one item whose value expired at the boundary; it is answered with four days to spare. |
| **P-9** | Plan **Free**. DNSSEC **off**. Email Routing **not configured**. **Managed `robots.txt` is switched ON in AI Crawl Control.** | 8 Sep | **STANDING HAZARD, attached to OD-A.** Inert while the zone is unproxied — but **if the shop is ever proxied, it would reinstate the training-crawler blocks that B-2 removed under D-1**, silently and at the edge, over the file the property serves. Not changed. See the hazard note below. |
| **P-11** | **There is no Month 4. Launch is immediate.** "Launching Month 4" is **false copy**. | 8 Sep | **B-12** replaces it. Also engages **DNC-3**, which protects the stated prices and the PPP ladder — the badge is not a price and is not protected. |
| **P-12** | **M-Pesa is live.** | 8 Sep | Partially unblocks **B-12**. **Still missing: paybill/till number and account name.** B-12 cannot write payment facts into markup until the convener supplies them, and must not infer them. |
| **P-13** | Legal entity is **Iman Holdings Ltd**, registered in **Kenya**. | 8 Sep | Unblocks `legalName` for **B-11 item 6** and the entity half of **B-12**. **Still missing: registration number and registered address.** B-11 item 6 asks for an `address` as a `PostalAddress`; P-14 binds, so no address enters markup that the page does not state. |
| **P-14** | **Remove both unsourced homepage statistics.** | 8 Sep | Unblocks **B-15**, and **changes it from a sourcing task to a removal task**. The stat block goes from four statistics to two, both sourced. |
| **P-15** | **Instagram `@infoonairesources`** and **X `@info_onai`** exist as live pages. B-11 may reference them. **Any third profile asserted in current markup is unconfirmed and must be dropped** unless the convener names it. | 8 Sep | Unblocks the `sameAs` half of **B-11**. Current markup (`index.html:67`) asserts **three**: Instagram, **LinkedIn**, **TikTok**. Instagram is confirmed; **LinkedIn and TikTok are dropped**. **X `@info_onai` is not in the markup today** and may be added. |
| **P-16** | Assets supplied by the convener. | 9 Sep | **Both verified present on disk**, so nothing is PENDING: `assets/logo.png` (PNG, 1254×1254, 639 KB) and `assets/og-image.jpg` (JPEG, **1200×630**, 52 KB — the standard Open Graph dimension). Unblocks the image half of **B-11**, and with it the `twitter:` tag decision at B-11 item 2. |
| **P-17** | **All expired listings are closed, not renewed.** | 8 Sep | Unblocks **B-10**. Under **DNC-8 / D-16** they are **marked closed, not withdrawn**. |
| **P-18** | **The weekly Monday brief begins 14 September 2026.** Recorded as a commitment; copy may state the cadence from that date. | 8 Sep | No task named this as a dependency. It is now a dated commitment, and the copy claim becomes true on 14 September rather than being false today. |
| **P-19** | **Not verified in Search Console. Convener Ruling:** verify via **DNS TXT record now**; **do not submit the sitemap until after 20 September.** | 9 Sep | The sitemap submission is deliberately held until after the freeze and the boundary. Feeds **B-4** once verification lands. |
| **P-20** | **Finding, not a question.** GitHub Pages provides **no log access at all**. Recorded. | 8 Sep | Not a gap to close. P-22's African-test amendment governs. The observation instrument in `../../zawawi-observation/` exists because of this. |

### What this reverses — P-1 and task B-4

**B-4's change specification, as written, says: *"Remove all eighteen phantom entries."*** Its acceptance criterion 1 says *"Every `<loc>` corresponds to a file present in the repository."*

**The convener's ruling on P-1 keeps them.** So until content lands — by 8 October 2026 — the sitemap continues to declare **eighteen URLs that return 404**, and **B-4's acceptance criteria as written cannot pass.** The same holds for **B-5**: `llms.txt` describes ten content areas of which two have pages behind them (see `BRIEF-B-CORRECTIONS.md` C-12).

This is recorded, not contested. The ruling is the convener's to make, and the reasoning — that these are real commitments with a date rather than abandoned paths — is a different factual claim from the one the brief was drafted against. But two consequences follow and should be visible:

1. **B-4, B-5 and B-6 cannot be marked complete before the content ships.** They are now verification tasks with a **dependency on a date, 8 October 2026**, not on an answer.
2. **The gap between declaration and reality persists for thirty days**, and D-9 and P-14 both speak to it. Nothing in this programme forbids declaring a commitment; what P-14 forbids is asserting in markup a fact the page does not state. A sitemap entry for a page that does not yet exist sits closer to the first than the second, but it is not free of tension, and a reader of the record should see that it was noticed rather than missed.

### Standing hazard — P-9, attached to OD-A

**Cloudflare's Managed `robots.txt` is switched ON in AI Crawl Control.**

It is **inert today**, because the zone is unproxied and confirmed so under P-8. But **OD-A** contemplates proxying this zone after 16 September. If that happens with this setting left on, Cloudflare would serve a managed `robots.txt` at the edge that **reinstates the training-crawler blocks B-2 removed under D-1** — undoing a recorded convener decision, invisibly, without a commit, and without a changelog entry.

**Not changed.** Recorded here and to be re-read at the moment OD-A is decided, not before.

### What is now unblocked, and what still is not

**Fully unblocked and executable:**

| Task | Was blocked on | Note |
|---|---|---|
| **B-8** — conversion repair | P-2, P-3, P-4 | All three answered. **Highest value-per-risk work in either brief.** |
| **B-7** — restore the missing standard pages | P-6, OD-G | Port from the second repo, verify, then archive it. |
| **B-10** — mark expired listings | P-17 | Mark closed; do not withdraw (DNC-8). |
| **B-15** — the two unsourced statistics | P-14 | Now a **removal** task. |
| **B-13**, **B-14**, **B-17** | never blocked | Landmarks, no-JS legibility, deliberate non-actions. |

**Unblocked but constrained by sequence or freeze:**

| Task | Constraint |
|---|---|
| **B-11** — dangling references | Image and `sameAs` halves unblocked. Executed **by the generator** under OD-J, so it waits on **B-20**, which waits on block 3A. Also carries the inherited dangling `@id` recorded in the changelog. |
| **B-6** — navigation repair | Depends on **B-7** landing first. |
| **B-4**, **B-5** | Now verification tasks; wait on content, **by 8 October 2026**. |
| **Enforce HTTPS** | Post-freeze, **on or after 21 September**, with a `deploys.md` prediction written first. |

**Still carrying a missing input:**

| Task | Missing |
|---|---|
| **B-12** — commercial facts as structured data | **M-Pesa paybill/till number and account name.** Also **Iman Holdings Ltd's registration number and registered address**, if an `address` is to be expressed. |

**Nothing in the freeze window changes.** From **12 to 20 September** no crawl directive, canonical, `sitemap.xml`, `robots.txt` or hosting setting moves — Enforce HTTPS included. Content and markup work may proceed, with every deploy recorded in `../../zawawi-observation/deploys.md`.

---

*Section 3 answered 8–9 September 2026 by Benta, convener, and recorded under task DOC-3. Section 1 and Section 2 are appended to, never rewritten.*
