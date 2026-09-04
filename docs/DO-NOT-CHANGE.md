# DO-NOT-CHANGE REGISTER — infoonairesources.shop

**Copied:** 3 September 2026, task B-16

> **This file is a copy. The brief is the source.**
>
> The authoritative register is **§3 of `docs/zawawi/IMPLEMENTATION-BRIEF-B-infoonairesources.md`**. This file exists so that the register is findable from `docs/` without opening a 700-line brief. Where the two disagree, **the brief governs** and this copy is wrong and must be corrected.
>
> Copied from the brief at commit `c5d141e`.
>
> **DNC-9 below reflects the C-10 correction, not the text as originally issued.** As issued, DNC-9 read "all twelve content pages" and named **B-14** as the task adding landmarks. Landmarks are **B-13**. Both were corrected on 3 September 2026 on the convener's authority, recorded at `docs/zawawi/BRIEF-B-CORRECTIONS.md` C-10. Do not read this file as evidence of what the register originally said — read git for that.

---

## The register

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

## Two standing constraints that are not in the register but bind the same way

Recorded here because they are easy to violate mechanically and the register is where an implementer looks first.

**Barred figures.** Do not cite **78.33 / 41.67 / 28.33** (D-4, barred pending V-4). Do not cite any spoof rate (D-10 / CL-2). Do not cite **"+115.1%"** or **"up to 40%"** as rationale (D-6).

**Infrastructure.** Do not touch DNS, Cloudflare or GitHub repository settings. DNC-10 covers the proxy state specifically; this covers the rest of the control plane.

---

## How to change something in this register

You do not change it here. **§3 of the brief is amended first**, on the convener's explicit authority, with the reason recorded in `docs/zawawi/BRIEF-B-CORRECTIONS.md`. This copy is then updated to match, in the same commit.

Brief B §0 forbids modifying §3. That prohibition has been lifted exactly once, for C-10, and the lifting was recorded. Treat any further amendment the same way.

---

*Copied 3 September 2026 under task B-16. Source: Brief B §3 at commit `c5d141e`. Decided by: Benta, convener.*
