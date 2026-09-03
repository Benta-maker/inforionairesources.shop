# EXECUTION SEQUENCE — BOTH PROPERTIES

**Version:** 1.0
**Issued:** 2 September 2026
**Deadline:** 15 September 2026 — 13 days
**Covers:** Implementation Brief A (swakaadvocates.co.ke) and Implementation Brief B (infoonairesources.shop)

---

## THE SEQUENCING RULE

Two positions govern order, and they pull in opposite directions from what the deadline suggests.

**P-23 clause 3, verbatim:** *"Commit no resource that is wasted if the date slips. Every authorised action must be justified by P-13 independently of the deadline."*

**P-13's binding cost rule:** *"No machine-facing artifact is built whose cost exceeds the cost of the level-1 work still undone. Since level-1 work is nowhere complete on any real property, this operates in practice as a prohibition on speculative standards spending."*

Read together: the deadline does not promote work up the queue. It promotes exactly one thing — **observation** — because observation is the only activity whose value is destroyed if it starts late. Everything else is justified by the Consumption Rule or it is not justified at all.

Position Analysis S-4 states the deadline's scope directly: *"The deadline's only operative instruction for either property is D-10: separate ad-carrying pages from fact-carrying pages. Everything else the deadline appears to demand fails P-13's cost rule."* Neither property carries advertising. So on these two properties, the deadline's operative instruction is satisfied by default, and what remains is the observation window.

**Consequence: the deadline-critical block is five items, not thirty.** The rest of both briefs is ordinary engineering that would be correct on 15 October as surely as on 14 September.

---

## PHASE 0 — TODAY THROUGH 5 SEPTEMBER: unblock and observe

Nothing here changes either website.

| # | Task | Property | Why now |
|---|---|---|---|
| 0.1 | **A-1 / B-1 — external observation running** | Both, one instrument | ⏰ **The only genuinely date-destroyed activity in the programme.** P-23 clause 2 requires observation established *before* the date so the post-date state is observed rather than inferred. A baseline started on 14 September is nearly worthless; one started today gives twelve days of before-state. Start this before anything else, including before answering the PRE-TASK checklist. |
| 0.2 | **PRE-TASK checklist, Brief A** — priority P-1 (raw HTML), P-2 (repo), P-3 (origin), P-4–P-13 (Cloudflare) | A | Item P-1 alone unblocks A-5, A-9 and A-10. Inventory §C.2.4 records it as sufficient to resolve every NOT DETERMINABLE item in §B.3 and §B.4 **in one step**. Nothing on the law firm property can be specified precisely until it lands. |
| 0.3 | **PRE-TASK checklist, Brief B** — priority P-1 (phantom paths), P-2 (Formspree), P-3 (WhatsApp), P-4 (MX) | B | P-1 unblocks four tasks at once. P-2/P-3/P-4 unblock the conversion repair, which is the highest-value zero-risk work on either property. |
| 0.4 | **A-2 — version control and untouched baseline** | A | Every subsequent change must be diffable and revertable. If no repository exists, this creates one from the live HTML. |
| 0.5 | ~~Decide OD-L~~ — **resolved 2 Sep: concession accepted** | B | B-2 proceeds. The changelog must record the convener's decision and its date, not just the file change. |

**Gate out of Phase 0:** observation has produced at least three consecutive daily files, and the two priority PRE-TASK items are answered.

---

## PHASE 1 — 5 TO 12 SEPTEMBER: deadline-critical work

Four items. All would be correct regardless of the deadline; they are here because they are cheap, safe, and better done before the boundary than across it.

| # | Task | Property | Deadline-critical? | Reason |
|---|---|---|---|---|
| 1.1 | **A-3 — Cloudflare posture recorded; tier decision taken (OD-B)** | A | ⏰ **Yes** | D-5 binds this property and only this property. The tier decision determines what granularity exists on the day, and D-8 requires it be taken *on the record, with the loss of granularity stated*. Taking it on 20 September is taking it after the fact. |
| 1.2 | **B-2 — `robots.txt` rewrite** | B | ⏰ **Yes, conditionally** | Not because of Cloudflare — this property is unproxied and outside that control plane. It is deadline-adjacent because the current file blocks nine crawlers under a rationale D-1 rules unavailable, and because a change to crawl directives made *during* the observation window contaminates the observation. Land it before 12 September or defer it to after 20 September. Do not ship it on the 14th. |
| 1.3 | **B-8 — conversion repair** (Formspree, WhatsApp, MX) | B | Not strictly | Placed here because it is the highest value-per-risk work in either brief and there is no argument for delay. Both subscribe forms and the WhatsApp link have been non-functional in production since at least March 2026. Every visitor who tried to subscribe was lost silently. |
| 1.4 | **B-3 — canonical host correction** | B | Not strictly | Mechanical, low-risk, and it makes the observation logs cleaner by removing a redirect hop from every measured fetch. Cheap to do now, marginally annoying later. |

**Freeze from 12 September.** No further changes to either property's crawl directives, canonicals, `robots.txt`, `sitemap.xml` or hosting configuration until 20 September. **A moving property cannot be a measured property**, and the paired comparison D-5 authorises is the only natural experiment the programme has.

Content and markup work may continue during the freeze — but record every deploy in the observation log, so that a body-hash change on the 16th can be attributed to your own commit rather than to the intermediary.

---

## PHASE 2 — 12 TO 20 SEPTEMBER: freeze and observe

| # | Activity | Property |
|---|---|---|
| 2.1 | Observation cadence increased to twice daily, 13–18 September | Both |
| 2.2 | No infrastructure change of any kind | Both |
| 2.3 | On 16–20 September: run the boundary diff per Brief A §5.3 and Brief B §5.3 | Both |
| 2.4 | Write `docs/observation-findings-2026-09.md` | Both |

**How to read the result — the discipline matters more than the finding.**

P-23 clause 1 grades the change as *announced policy, not shipped*. No brief in the corpus observed the flip in production, and verifications V-1 and V-3 are dischargeable only on or after the date. Inventory §B.2.7 already models the right caution about its own single fetch: it establishes what one fetcher saw on one date from one network path, and *"establishes nothing about other agent classes."*

So: report what changed, from which user-agent, on which URL, on which date, with the raw log line. Report what the unproxied control arm showed. Do **not** report that the flip did or did not happen. The instrument does not support that sentence.

---

## PHASE 3 — 20 SEPTEMBER ONWARD: the actual engineering

Ordered by P-13's Consumption Rule — documented consumer first, measured effect second, specification-without-consumer last — and within that, by dependency.

### 3A. Level 1: configuration hygiene and truth repair

Documented consumers, Tier 1–2 evidence of parsing. This is where the bulk of the value is, and P-13's cost rule means nothing below it may be built until it is done.

| Order | Task | Property | Depends on |
|---|---|---|---|
| 1 | B-4 — sitemap truth | B | OD-C |
| 2 | B-5 — `llms.txt` truth or removal | B | OD-C, B-4 |
| 3 | B-7 — restore or de-reference about/contact/privacy/terms | B | OD-G |
| 4 | B-6 — navigation repair | B | B-7 |
| 5 | B-11 — decide which dangling references are repaired and which removed | B | P-16, B-7 |
| 7 | B-10 — mark expired listings | B | P-17 |
| 8 | A-4 — `robots.txt` and `sitemap.xml` | A | P-14, P-15, P-16 |
| 9 | A-6 — dead LinkedIn link | A | P-21 |
| 10 | A-7 — stale forthcoming labels | A | P-22 |
| 11 | A-8 — meta-layer hygiene | A | P-24 (image half only) |
| 12 | A-10 — logo anomaly | A | P-1, P-24 |
| 13 | B-15 — source or remove the two unsourced statistics | B | P-14 |

**Note what is no longer in this block.** B-9 (FAQ reconciliation) and B-12 (commercial facts) have moved to 3B, because under the revised OD-J they are outputs of the generator rather than hand-edits. B-11 stays here as a *decision* task — which references are repaired, which removed — and the generator writes the result.

### 3B. Level 1, structural: semantics and description

| Order | Task | Property | Depends on |
|---|---|---|---|
| 14 | A-9 — semantic pass, zero visual change | A | P-1 |
| 15 | B-13 — landmarks, no ARIA | B | — |
| 16 | B-14 — no-JS legibility | B | — |
| 17 | **B-20 — build the machine-layer generator** | B | 3A complete |
| 18 | B-9 — FAQ reconciliation, via generator | B | B-20 |
| 19 | B-11 — regenerate with repaired references | B | B-20 |
| 20 | B-12 — commercial facts, via generator | B | B-20, P-11, OD-H, P-13 |
| 21 | A-16 — checker and declared-values file | A | — |
| 22 | A-5 — the firm's description as structured data | A | A-16, P-1, OD-D, OD-E |
| 23 | A-16 stage 2 — port the generator if the pipeline allows | A | P-3, A-5 |

**Why B-20 sits at 17 and not earlier.** The generator reads the page to produce the markup, so the page has to be true first. Building it before 3A completes would mean generating clean structured data for a site whose navigation points at five destinations that do not exist. Truth repair, then generation, then description.

**Why the firm lags the shop here.** A-16's generator half is conditional on PRE-TASK P-3 — how the site is published, and whether a generation step fits that pipeline. The checker half is unconditional and ships with A-5. See OD-J as resolved.

### 3C. Governance and record

| Order | Task | Property |
|---|---|---|
| 24 | A-13 / B-16 — machine-layer changelogs (opened in Phase 0, backfilled here) | Both |
| 25 | A-12 — provenance-marking convention | Both |
| 26 | B-17 — deliberate non-actions recorded | B |
| 27 | A-11 — human-readable rights reservation and data-protection notice | A |
| 28 | A-14 — `www` decision implemented or recorded | A |

**A-11 is out of order deliberately.** It is a level-1 item by content, but it is blocked on advocate-supplied legal text and there is no point queuing it earlier. It does, however, gate one line of A-4: the `robots.txt` reference to `/legal-notice` must not ship before the page exists.

### 3D. Level 3 and measurement: October onward

| Order | Task | Property |
|---|---|---|
| 29 | A-15 / B-19 — citation probes, first run | Both |
| 30 | B-18 — repository hygiene, second-repo archive, optional CI | B |
| 31 | Standing review per Charter Part IX item 6 | — |

---

## WHAT IS DEADLINE-CRITICAL, IN ONE TABLE

| Task | Property | Genuinely deadline-critical | Why |
|---|---|---|---|
| A-1 / B-1 — observation | Both | **Yes, absolutely** | Value is destroyed by lateness. The only such item in the programme. |
| A-3 — Cloudflare posture and tier | A | **Yes** | D-5 binds this property; the tier decision must be taken before the state it governs changes. |
| B-2 — `robots.txt` | B | **Yes, in the sense of "before the freeze"** | Not because of Cloudflare. Because changing crawl directives mid-observation contaminates the measurement. |
| PRE-TASK P-8 (Brief B) — confirm unproxied | B | **Yes** | The control-case design rests on it. If the zone has been proxied since inspection, the whole §5.3 comparison must be redesigned before the date, not discovered after it. |
| OD-L decision | B | **Yes** | Gates B-2. |
| B-8 — conversion repair | B | No, but do it now | Highest value-per-risk work in either brief. No argument for waiting. |
| B-3 — canonical host | B | No, but do it now | Cheap; removes a redirect hop from every measured fetch. |
| **Everything else** | Both | **No** | Justified by P-13 or not justified. P-23 clause 3 forbids spending against a date that may slip. |

---

## THE ONE THING THAT MUST NOT SLIP

If only one item in this document is executed, it is the observation instrument.

D-5 concedes that the property cannot contest the edge classifier's semantics — *"it can only choose which side of the classifier it sits on, and at the free tier it cannot even do that"* — and then authorises the one thing that remains available: *"the paired observation across 15 September, which converts the concession into the programme's only natural experiment."*

The programme holds two properties under the same DNS provider with opposite proxy postures (§C.1.20). That is a genuinely unusual instrument, and it exists by accident rather than design. It works only if both arms are measured before the boundary and neither is altered across it.

Everything else in both briefs can be done in October. This cannot.

---

*End of Execution Sequence. Sequenced under P-13's Consumption Rule and P-23's fallback posture; deadline-critical designations traced to D-5, P-23 clause 2, and Position Analysis S-4.*
