# PROVENANCE-MARKING CONVENTION — infoonairesources.shop

**Adopted:** 3 September 2026, task B-16
**Effective:** from the commit that adds this file, forward
**Authority:** D-14, ADAPT prospectively
**Specified by:** Implementation Brief A, task A-12, as incorporated by Implementation Brief B, task B-16
**Approved by:** Benta, convener

**Related:** [`machine-layer-changelog.md`](machine-layer-changelog.md) — which records *who decided* each machine-facing change. This file records *how the text was produced*. Neither substitutes for the other.

---

## Why this exists, and why now

D-14, ADAPT prospectively, verbatim:

> *"any synthetic or assisted content on either property carries its marking from creation, before any duty attaches, because retrofitting marking across a site is expensive and adopting it early is nearly free."*

That is the whole argument, and it is an argument about cost, not about compliance. **No legal duty currently requires this of this property.** It is adopted ahead of any such duty because the cost of adopting it today is a commit-message line, and the cost of adopting it after a duty attaches is a retrospective audit of every page on the site — an audit that, as recorded below, could not now be completed honestly.

Among the material facts behind D-14: Kenya's Bill expresses a human-dignity interest through a machine-legible marking duty. This convention is not written to satisfy that Bill, whose final form is not known. It is written because the reasoning is sound independently of it.

---

## The rule

**Any AI-assisted or AI-generated text, image or asset entering this property carries a marking from creation.**

"From creation" is the operative phrase. The marking attaches when the content is made, not when it is published, and not when someone asks.

### Minimum marking, always

**A commit-message declaration.** Every commit introducing AI-assisted or AI-generated content states so in its message. This is the floor and it is never optional.

### Additional marking, where the content is published as an article or image

**An on-page statement**, in the form the convener approves.

**The approved form, as at 3 September 2026:**

> Parts of this page were drafted with AI assistance. Editorial responsibility rests with Benta, InfoOnAIResources.

**Why the second sentence names a person and not the property.** D-9's principle is that a machine-facing signal must be attributable to a **named human decision**. "InfoOnAIResources" is an entity; an entity cannot hold editorial responsibility, and a statement that assigns it to one discharges nothing. The name is what makes the sentence mean something. Ruled by the convener, 3 September 2026.

### A note on the specified form

Brief A task A-12 reads *"in the form the advocate approves"*. Here it reads **"in the form the convener approves"**.

A-12 was drafted for a regulated legal practice, where the advocate holds sign-off. This property has no advocate, so the convener holds it. **Same structure, different holder.** Ruled by the convener, 3 September 2026. No other substitution has been made to A-12's text.

---

## Scope in time

**This convention binds from its own commit forward.** It does not reach backward, with one exception recorded immediately below.

### The one retrospective note

The two commits that precede this file — `3626356` (DOC-0) and `c5d141e` (DOC-1) — introduced the programme documents under `docs/zawawi/` and `docs/zawawi/BRIEF-B-CORRECTIONS.md`. **The corrections file and the amendments to Implementation Brief B were AI-assisted**, drafted by the implementing agent under the convener's direction and accepted by the convener on 3 September 2026. The four programme documents themselves were committed unmodified as issued.

This note is recorded here rather than by amending those commit messages. **The history is not rewritten.** A convention that begins by falsifying the record of what came before it is not worth adopting.

### The existing site content — an honest silence

**This convention makes no claim about the authorship of the thirteen content pages that existed before its adoption.**

Whether any of them was AI-assisted is not recorded anywhere in the repository, and the convener has stated they are not able to answer it reliably. Marking them as AI-assisted would assert a fact not known to be true. Marking them as human-authored would do the same in the other direction. Both are inventions, and inventing a fact is the one thing this programme forbids without exception.

So nothing is asserted. A reader of this repository should take the absence of a marking on a pre-adoption page as **absence of a record**, not as a claim of human authorship. That is a weaker position than a complete audit would give, and it is stated plainly here rather than papered over — which is precisely the cost D-14 predicts for retrofitting, arriving on schedule.

---

## What this convention is not

- **It is not a disclaimer of responsibility.** The on-page statement assigns editorial responsibility to a named human. It does not diffuse it.
- **It is not a content policy.** It says how content is marked, not what content may be published. Accuracy, sourcing and the prohibition on inventing facts bind independently and are not softened by a marking.
- **It is not a substitute for the change log.** A machine-facing change still requires its entry in `machine-layer-changelog.md`, naming the human who decided it, whether or not AI assisted in producing it.

---

*Adopted 3 September 2026 under D-14, ahead of any legal duty. Approved by: Benta, convener.*
