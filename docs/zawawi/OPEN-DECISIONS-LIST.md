# OPEN DECISIONS LIST — IMPLEMENTATION PHASE

**Version:** 1.0
**Issued:** 2 September 2026
**For:** the convener, ZAWAWI Intelligence Practice
**Scope:** decisions the implementation phase requires that the deliberation did not make

---

## HOW THIS LIST RELATES TO WHAT ALREADY EXISTS

Three registers of unresolved matter already exist and are **not** duplicated here:

- **Position Analysis Part G** — H-1 (whose permission an agent carries, hard-blocked on V-10) and H-2 (whether verification occurs inside the assistant).
- **Open Items memo, O-1 through O-16** — sixteen items across five sections, including O-3 (whether to front a Kenyan cPanel property with the free tier, determinant V-5) and O-4 (the payment rail's mandate architecture).
- **Conflict Register** — D-4 in part and D-15 held on verifications; D-7 provisional on V-10.

Everything below is **net-new**: a decision the implementation phase cannot proceed without, which none of those three registers covers. Where an item touches an existing one, the cross-reference is given.

Each item states the decision, why the council did not make it, what turns on it, and its deadline. **None of these is decided in the briefs.** Tasks depending on an undecided item are marked BLOCKED and stay blocked.

---

## SECTION 1 — DEADLINE-BEARING. Decide before 15 September 2026.

### OD-A. Whether to proxy `infoonairesources.shop` through Cloudflare.

**Why unruled.** Related to O-3 but not the same question. O-3 concerns a Kenyan cPanel-hosted property and its determinant is V-5 (whether Cloudflare peering means Kenyan traffic is fronted locally). This property is on GitHub Pages, whose anycast already serves it globally, so O-3's decision rule — *"the free tier buys visibility of machine traffic the local host does not provide at any price"* — applies with a different fact pattern. The council never saw the proxied/unproxied split, because the Blindness Rule kept the properties out of the corpus; the distinction surfaced only at inventory.

**What turns on it.** Everything about this property's crawl posture. Unproxied, it sits outside Cloudflare's bot management, WAF, crawler controls, Pay-Per-Crawl and the 15 September default change entirely (§A.1.3). It also gets no machine-traffic visibility of any kind — GitHub Pages provides no log access at all, which is why P-22 clause 1 is unsatisfiable here.

**The recommendation the briefs act on regardless of the decision: not before 16 September.** D-5 authorises the paired observation across the date as *"the programme's only natural experiment"*, and the experiment requires an unproxied control arm. Proxying before the date destroys the only instrument the programme has for observing whether the flip shipped at all.

**Secondary unknown, flagged in inventory §C.2.2:** whether GitHub Pages custom-domain HTTPS survives proxying. Test on a staging hostname before touching production.

**Deadline: decide by 12 September** — not to act, but to confirm inaction, so the observation design is stable across the boundary.

---

### OD-B. Cloudflare plan tier for `swakaadvocates.co.ke`.

**Why unruled.** D-8 states the principle and expressly hands the decision to the convener: *"The tier decision has stopped being a billing decision and has become a strategy decision, and it should be taken as one, on the record, with the loss of granularity stated."* The council states what the decision is; it does not take it.

**What turns on it.** Below the paid tier the crawler instrument is non-configurable — the property cannot distinguish a wanted retrieval agent from an unwanted training crawler at all. Above it, the distinction available is still not the distinction the property wants, because D-1's coupling operates upstream at the platform. So the tier buys granularity within a range that is already narrowed.

**What must be recorded either way**, per D-8's African-test caveat, which the ruling requires be carried *"on its face"*: most Kenyan operators are not behind a configurable edge at all, so this ruling addresses a minority of Kenyan sites.

**Deadline: before 15 September.** Task A-3 is blocked on the answer.

---

### OD-L. Whether to accept D-1's concession on `infoonairesources.shop`'s training-crawler blocks.

**Why this is here rather than in the briefs.** D-1 is a final ruling and Brief B implements it at task B-2. But it is the only task in either brief that gives something away, and it reverses a posture the property adopted deliberately — the current `robots.txt` carries a reasoned comment reading *"Our content is original human intelligence — not available for training."* That was a considered decision by the convener, and reversing it is also a considered decision by the convener.

**What the ruling holds.** Both properties admit both audiences, because the separation is not available at any price the properties can pay. Blocking training crawlers also blocks Googlebot, Applebot and Bingbot under most-restrictive-wins. The concession is named precisely: the property has lost the ability to price or refuse training ingestion as a condition of human discovery.

**RESOLVED 2 September 2026: the concession is accepted.** B-2 proceeds as written. The changelog entry must record that the convener took this decision knowingly, on the date, with the loss named — not that a script removed nine lines.

**The choice as originally filed.** Implement B-2, or override a final ruling. An override is legitimate — the convener is the final synthesiser under Charter VII.8 — but it must be recorded as an override, with its reason, so the register stays honest.

**Deadline: before B-2 executes**, which is deadline-critical, so effectively before 10 September.

---

## SECTION 2 — BLOCKING NAMED TASKS. No deadline, but work stops.

### OD-C. Are the eighteen phantom paths commitments or artefacts?

**Why unruled.** Purely owner-held; inventory §C.2.7 asks it directly. The council cannot know whether `/brief/`, `/tools/`, `/policy/`, the five `/industry/*` verticals, `/podcasts/`, `/research/`, `/mentors/`, `/advisory/` and `/opportunities/grants/` are aspirational-by-design or stale.

**What turns on it.** Tasks B-4, B-5 and B-6 all resolve the same way — anything not shipping within thirty days comes out of the sitemap, `llms.txt` and navigation now, and goes back in when it ships. But the convener may prefer to ship one or two rather than remove them.

**Note.** Removing a path from a sitemap costs nothing and is fully reversible. Leaving a declared path 404ing is a standing signal, to every crawler and every visitor, that the property's own description of itself is unreliable.

---

### OD-D. Does the firm publish any fee or fee-basis statement?

**Why unruled.** Two independent reasons. D-3 lists fee basis among the facts a self-description should carry, but Position Analysis S-2 bars the council from ruling on the decision layer for this property: *"The corpus contains a regulatory frame at tier 1 and no consumer evidence whatsoever about credentialed professional services… Everything decision-layer awaits the commissioned brief."* And separately, LSK advertising rules govern what a Kenyan advocate may state about fees, and no seat is competent on that.

**What turns on it.** Whether A-5's structured data can carry any pricing signal at all. Currently the site states no price, no range, no hourly or retainer indication, not even "fees on application" (§B.5.4). DNC-4 protects that absence until this is decided.

**Recommendation: leave it absent unless the advocate has an affirmative reason and LSK comfort.** The cost of silence here is low, and the cost of a misstated fee representation by a regulated professional is not.

---

### OD-E. May the LSK practising certificate number be published?

**Why unruled.** Inventory §C.2.7 raises it; no seat is competent on Kenyan professional-conduct publication rules.

**What turns on it.** Whether A-5's `Person` node for John Swaka carries a verifiable credential identifier. Verifiable credentials are among the strongest entity-identity signals available under P-15's thin common core, and the property currently carries the advocate's name only via an email local-part, a LinkedIn caption and a meta `keywords` string (§B.5.4) — which is thin for the central named practitioner of the firm.

---

### OD-F. Should `www.swakaadvocates.co.ke` exist?

**Why unruled.** Owner decision about the firm's own identifiers.

**What turns on it.** Task A-14. The hostname is currently NXDOMAIN on all record types, so *"any inbound link, citation, directory listing, business-profile entry, or printed reference using `www.swakaadvocates.co.ke` fails at resolution — before any HTTP request, before any redirect, before Cloudflare"* (§B.1.5). If the firm's letterhead, cards or directory entries use `www.`, those references currently go nowhere.

**Low cost either way.** A proxied CNAME plus a 301 is a few minutes' work; deciding it will never exist is free. Deciding nothing leaves the failure in place.

---

### OD-G. Disposition of `Benta-maker/infoonairesources-site`.

**Why unruled.** Inventory §C.2.3 asks; not a council matter.

**What turns on it.** Task B-7. The second repository holds working `about.html`, `contact.html`, `privacy.html`, `terms.html`, `resources.html` and `404.html` — four of which the deployed site 404s on — and received maintenance commits on 16–17 June 2026, three months after its CNAME was deleted and it stopped being deployed (§A.7.6, §C.1.9).

**The privacy page matters most.** The live site links to a privacy policy from the footer and from the hero form microcopy, while collecting email addresses through forms that do not work. Whichever route B-7 takes, that combination should not survive the month.

---

### OD-H. Is M-Pesa live, or still "from launch"?

**Why unruled.** Owner-held fact. Related to O-4 (the mandate architecture) but distinct: O-4 asks how agent-initiated payment could work on the rail; this asks whether the rail is connected at all today.

**What turns on it.** Whether B-12 may express `acceptedPaymentMethod` in markup. The FAQ names M-Pesa as available "from launch" — a stated future capability — and no payment integration of any kind exists in the repository (§A.6.2). Asserting current acceptance of a payment method not accepted fails P-14 and creates consumer-protection exposure under P-18(i), which treats site-authored statements as the site's own publication.

---

### OD-I. Who signs off human-visible text changes on `swakaadvocates.co.ke`?

**Why unruled.** A process question, not a finding. But it is load-bearing: every human-visible change on a regulated legal practice's site is an advertising decision under LSK rules, and Brief A's instruction header requires convener confirmation on every task partly for this reason.

**What turns on it.** Execution speed. If the advocate must review each change, tasks batch differently than if the convener holds delegated authority for non-substantive edits.

**Suggested split, for the convener to accept or amend:** structural and markup changes that produce no visible text change (A-4, A-8, A-9, A-10) proceed on convener authority; anything altering displayed words (A-6, A-7, A-11) requires the advocate.

---

## SECTION 3 — METHODOLOGICAL. Not blocking, but they affect whether the record holds.

### OD-J. P-14's propagation test versus hand-authored HTML. — **RESOLVED 2 September 2026**

**Status: decided by the convener. Recorded here rather than removed, because the resolution is a method decision the programme should be able to audit later.**

**The problem as filed.** P-14 states the admissibility test for any machine-facing artifact: *"if a human-facing edit does not propagate automatically, the artifact is a liability and is refused."* Both properties are hand-authored static HTML with no build step. A human-facing edit does not propagate automatically to the structured data on either. Read strictly, P-14 refused the structured-data tasks in both briefs.

**That this is a live failure mode, not a theoretical one, is already in the record.** The homepage FAQ markup on the shop has drifted from the rendered FAQ so far that three marked-up questions appear nowhere on the page and three rendered questions appear nowhere in the markup (§C.1.4). Nobody edited the markup incorrectly. The page changed and the markup did not, because nothing connected them.

**The three options originally filed were: detect drift, build a full templating system, or refuse the structured-data work. None was right.**

**Resolution adopted: generate the machine layer from the page.**

A script parses the finished page and writes the structured data from what it finds there — FAQ questions and answers from the rendered accordion, prices from the tiers block, contact facts from the footer, practice-area names from the services section. The page becomes the single source of truth. Edit an answer and the markup updates, because the markup is derived from the answer.

This **satisfies** P-14 rather than substituting for it. The position asks that the machine layer be *"a projection of the human page rather than a parallel artifact"*; a generator makes it literally that. The FAQ divergence at §C.1.4 could not have occurred under one.

**The residual, stated honestly.** A small set of values cannot be read off a page — `addressCountry: "KE"`, `@type` choices, `foundingDate` normalised from "Established 2016". These live in `data/declared-values.json`, capped at roughly twenty entries on the shop and fifteen on the firm, each with a comment naming its rendered counterpart or stating it has none. **These values remain guarded by detection, not propagation.** That is a substitution, and it is recorded as one — but it now covers a handful of stable facts rather than the entire machine layer.

**Implementation.**
- **Shop:** task **B-20**, buildable now, roughly a day. Runs before B-9, B-11 and B-12, all of which now depend on it. No new dependencies, no templating framework; pages continue to be hand-authored exactly as now.
- **Law firm:** task **A-16**, in two stages. The checker and declared-values file are built unconditionally alongside A-5. The generator is ported only once PRE-TASK P-3 reveals how the site is published and whether a generation step fits that pipeline. If it does not, that is recorded as a finding about the platform — the same logic P-22's African-test amendment applies to absent log access.

**Sequencing consequence.** The generator is built **before** the structured-data tasks, not alongside them, or the markup gets hand-written and then automated a week later. And it comes **after** the truth repair (sitemap, navigation, forms), because there is no sense generating clean data for a page that links to five destinations that do not exist.

**Operating rule adopted, binding on both properties:** after the generator lands, no JSON-LD block is edited by hand. To change what the markup says, change what the page says. Where a needed fact cannot be produced that way, that is a signal the page should state it — which is the outcome P-14 exists to force.

---

### OD-K. Reconcile the cross-reference numbering between the Conflict Register and the Position Analysis.

**The problem.** The Conflict Register cites the Position Analysis by a numbering scheme the Position Analysis does not use. D-5 cites *"Position Analysis IX.3"* for the finding that the concession binds one property and not the other. D-7 cites *"Position Analysis Part XI"* for the five holdings. The Conflict Register's standing qualifier G.6 cites *"Position Analysis Part IX.2"* for the infrastructure-class determination. The Position Analysis as issued is organised as Parts A through J, with the five holdings at Part J and no Parts IX or XI.

**Why it matters.** The programme's whole method is litigation traceability — every task citing the ruling it implements. Both briefs cite D-5's substance, which is unambiguous on its face. But a reader auditing the chain from task to ruling to position will follow D-5's pointer to a section that does not exist.

**What is needed.** Either a corrected Conflict Register with pointers matching the Position Analysis's actual structure, or a one-page concordance recorded alongside both. **Do not renumber the D-IDs** — the register is explicit that future cycles append rather than renumber, and that traceability is worth more than tidy sequence.

**Not blocking.** The briefs proceed. But the discrepancy should be closed before the register is shown to anyone outside the practice, and certainly before the methodology is offered as a product.

---

### OD-M. Standing restriction handling in implementation outputs.

**Why raised.** The Conflict Register creates citation restrictions *"binding on all downstream work"*, and names implementation briefs specifically: no spoof rate (CL-2); no conversion-premium magnitude (CL-4); no D-4 degradation curve (V-4); the CL-5 currency qualifier on every misattribution citation; no A-8 magnitude as a rationale for editorial change; no emission-rate figure without its frame (CL-13); no Cloudflare-derived number as the sole basis of an implementation decision (P-3).

**Both briefs carry these into their instruction headers.** But the restrictions also bind anything produced *downstream of the briefs* — probe reports, client-facing summaries, the observation findings document, and any future marketed methodology.

**The decision:** whether a single standing restrictions sheet is maintained as a practice-level instrument, applied to every output, rather than re-copied into each document where it can drift. **Recommended.** The alternative is that a figure barred in September reappears in November because it was copied from a document that predated the bar.

---

## SUMMARY

| ID | Decision | Deadline | Blocks |
|---|---|---|---|
| OD-A | Proxy the shop through Cloudflare? | 12 Sep (confirm inaction) | Observation design |
| OD-B | Cloudflare plan tier, law firm | 15 Sep | A-3 |
| ~~OD-L~~ | ~~Accept D-1's concession on training blocks?~~ | **RESOLVED 2 Sep** | Accepted; B-2 proceeds |
| OD-C | Phantom paths: commitments or artefacts? | — | B-4, B-5, B-6 |
| OD-D | Publish any fee statement? | — | A-5 (scope) |
| OD-E | Publish LSK certificate number? | — | A-5 (scope) |
| OD-F | Should `www` exist for the firm? | — | A-14 |
| OD-G | Disposition of second repository | — | B-7 |
| OD-H | Is M-Pesa live? | — | B-12 |
| OD-I | Who signs off firm text changes? | — | Execution cadence |
| ~~OD-J~~ | ~~P-14 propagation vs hand-authored HTML~~ | **RESOLVED 2 Sep** | Generator adopted; B-20 / A-16 |
| OD-K | Register/Position numbering concordance | — | Traceability |
| OD-M | Standing restrictions as a practice instrument | — | Downstream outputs |

**Two resolved on 2 September 2026: OD-L (training blocks — concession accepted) and OD-J (propagation — generator adopted). Eleven remain open; two of those are deadline-bearing: OD-A and OD-B.**

---

*End of Open Decisions List. Net-new only; H-1, H-2 and O-1 through O-16 are unaffected and remain open on their own terms.*
