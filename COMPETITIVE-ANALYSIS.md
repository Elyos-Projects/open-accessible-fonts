# Competitive + Improvement Analysis — `open-accessible-fonts`

> Scope: rigorous review of PLAN.md (v0.1.0) and TASKS.md for the Elyos good-deed project
> "open-accessible-fonts" (OFL fonts for under-served scripts + low-vision/dyslexia legibility).
> Competitor claims below are grounded in cited web sources. Guardrails in focus: OFL compliance,
> evidence-based legibility (dyslexia-font claims are contested — cited carefully), Unicode/script
> coverage, font-engineering quality, attribution, and scope realism.

---

## 1. Correctness & completeness review of PLAN.md

The plan is unusually mature and self-aware. It is one of the strongest drafts in the program: it
already internalizes the two hardest truths (dyslexia-font evidence is contested; type design is
slow and unforgiving) and wires honest constraints (clean-room, community veto, non-medical
framing, `verifiedNeed=false`) into the artifacts rather than the prose. Findings below are
refinements, not rescues.

**1a. Evidence / contested dyslexia-font claims — CORRECT, and the plan's biggest strength.**
The plan repeatedly refuses to over-claim (O8 honesty clause; §3 non-goal "will not claim
clinical/medical efficacy"; risk row escalating any efficacy claim to high-risk). This matches the
literature precisely:
- The widely cited Rello & Baeza-Yates and later controlled studies find **no reading-speed or
  accuracy benefit** from OpenDyslexic vs. Arial/Times; one alternating-treatment study found it
  *reduced* speed/accuracy ([PMC, Annals of Dyslexia 2017](https://pmc.ncbi.nlm.nih.gov/articles/PMC5629233/)).
- Dyslexie similarly **did not benefit reading** in children with or without dyslexia
  ([Springer, Annals of Dyslexia 2017](https://link.springer.com/article/10.1007/s11881-017-0154-6)).
- The British Dyslexia Association recommends *plain, evenly-spaced sans-serif* (Arial, Verdana,
  Tahoma) — i.e. general legibility, not a "dyslexia font" — and notably **does not cite research**
  to substantiate even that advice
  ([BDA style guide](https://www.thedyslexia-spldtrust.org.uk/media/downloads/69-bda-style-guide-april14.pdf)).
- **Refinement (important):** the plan should extend the same skepticism to its *low-vision*
  framing. Even Atkinson Hyperlegible — the project's lodestar prior art — has design-time testing
  with low-vision readers but **limited published peer-reviewed evidence that it outperforms good
  standard fonts** ([Wikipedia](https://en.wikipedia.org/wiki/Atkinson_Hyperlegible);
  [Letterform Archive talk: "challenging assumptions about legibility"](https://letterformarchive.org/events/view/atkinson-hyperlegible-challenging-assumptions-about-legibility-and-accessibility/)).
  Luciole's own study found only ~half of low-vision participants *preferred* it — a preference
  signal, not a comprehension win
  ([ScienceDirect / Acta Ophthalmologica 2023](https://www.sciencedirect.com/science/article/pii/S0001691823001026)).
  The evidence brief (fonts-research-005) should state plainly: **for low vision the strongest,
  best-evidenced levers are size, contrast, and spacing — not typeface identity** — so the family's
  value proposition is "openly licensed + designed to legibility principles + wide language reach,"
  not "clinically better than Verdana."

**1b. Scope vs. creating fonts from scratch — the single biggest realism risk.** The plan
acknowledges "type design is slow" (High-likelihood risk) but the *ambition* still under-prices it.
Drawing a production-quality, multi-weight, variable, fully-kerned, hinted Latin family with
GF-Core + differentiation coverage is typically **months of expert type-design labor**, and a
correctly-shaping complex-script font (GSUB/GPOS for Adlam/N'Ko/Tifinagh) is a specialist
sub-discipline. M1's "draw core Latin glyph set" (one `large` task) compresses an enormous craft
effort. **Recommendation:** explicitly offer a lower-effort, higher-certainty alternative path —
*extend/repair existing OFL faces* (Atkinson Hyperlegible Next, Andika, Lexend, Luciole) and
*curate/guide* — and treat from-scratch drawing as the exception requiring a committed expert
designer. Open Question Q4 raises "new vs. extend" but defers it to M1; given the labor asymmetry,
**extend-first should arguably be the default**, with the project's differentiated value in
language-coverage extension, QA, provenance, and guidance.

**1c. Font-engineering quality — well-covered, two gaps.** Hinting, kerning, Unicode coverage,
variable axes, and shaping are all addressed with real tools (fontmake/gftools/fontTools,
FontBakery, HarfBuzz diffs, hyperglot/gflanguages). FontBakery + GF-layout-from-day-one is exactly
right for cheap upstreaming ([gf-guide onboarding](https://googlefonts.github.io/gf-guide/onboarding.html)).
Gaps: (i) **hinting** is largely punted to autohinting (reasonable, but legacy low-DPI Windows
rendering is a real low-vision concern — the very users targeted may be on old hardware; keep
fonts-hint-307 closer to mainline for the a11y family); (ii) **"byte-stable reproducible build"**
(fonts-infra-001) is an admirable but technically fragile acceptance bar — font binaries embed
timestamps/tool versions and are notoriously hard to make byte-identical; recommend relaxing to
*deterministic-content* reproducibility (normalized/`ttx`-diff equality) to avoid a self-inflicted
red CI.

**1d. OFL compliance — strong.** OFL-1.1 for fonts, MIT for tooling, CC-BY-4.0 for docs;
mandatory FONTLOG.txt (correctly flagged as OFL-*required*, commonly forgotten); Reserved Font Name
discipline; the US "typeface designs aren't copyrightable but font *software* is" nuance is
correctly cited *and* declined in favor of the stricter clean-room global-safe standard. The
prohibited-inputs allow/deny list and `provenance.json` per-glyph schema are best-in-class. Minor:
add an explicit **OFL Reserved Font Name collision check** to CI/release (name search) since RFN
trademark conflict is listed as a risk but has no automated gate.

**1e. Script coverage for under-served languages — correct posture, watch the "gap" claim.** The
review-before-draw lock, community veto, and "no invented orthographies" are exactly the right
ethics. **However**, the plan should sharpen its needs analysis against the fact that **Noto now
covers 162 of 168 Unicode scripts and ~1,000 languages**, including Adlam (co-designed with its
inventors), N'Ko, Tifinagh, Vai, etc.
([Wikipedia: Noto](https://en.wikipedia.org/wiki/Noto_fonts);
[Google blog: endangered languages](https://blog.google/outreach-initiatives/accessibility/preserving-endangered-languages-noto-fonts/)).
The genuine remaining gaps are mostly **not "no font exists"** but **"only one weight / no italic /
no variable / missing language-specific orthographic forms / weak shaping for a specific
orthography / no display or text-optimized option."** fonts-research-004 must frame the shortlist in
those precise terms or risk duplicating Noto. This is a correctness issue: §2 says "missing weights,
missing diacritic coverage… broken shaping" — good — but the executive summary's "a script with no
open font" framing overstates the 2026 reality and should be softened.

**1f. Testing with users — honestly scoped, possibly too conservative to validate the premise.**
Deferring human-subjects trials to partners (avoiding IRB/PII burden) is defensible and the PII
treatment (disability status = sensitive) is excellent. But the project's entire accessibility
premise rests on legibility benefit it then declines to measure. Recommend M0 explicitly plan a
**lightweight, partner-run, preference/comprehension proofing protocol** (not a clinical trial) so
O8 can produce a real signal rather than defaulting to "rely on published research" that, for the
specific shipped font, doesn't exist.

**1g. Completeness:** All 17 sections present; metadata header, Appendix A (25 applied
improvements), and self-review are thorough. TASKS.md is schema-mapped, sizing is honest,
`verifiedNeed=false` is applied correctly everywhere a partner is unsecured, and the example Task
JSON is schema-valid. No major omissions.

---

## 2. Competitive landscape (cited)

**Low-vision / high-legibility, openly licensed:**

- **Atkinson Hyperlegible (Braille Institute + Applied Design Works)** — the category leader and the
  project's closest prior art. OFL, free for any use; 2025 **Atkinson Hyperlegible Next** adds a
  variable weight axis, monospace, and expands from 27 to **150+ languages**
  ([Braille Institute](https://www.brailleinstitute.org/freefont/);
  [Braille Institute Next launch](https://www.brailleinstitute.org/about-us/news/braille-institute-launches-enhanced-atkinson-hyperlegible-font-to-make-reading-easier/)).
  *Strength:* brand, distribution (Google Fonts), maximal letterform differentiation, now
  multilingual. *Weakness:* peer-reviewed efficacy evidence is thinner than its reputation
  ([Wikipedia](https://en.wikipedia.org/wiki/Atkinson_Hyperlegible)); design-led, not study-led.
- **Luciole (typographies.fr + CTRDV, France)** — OFL, designed by a multidisciplinary team
  (ophthalmologist, orthoptist, psychologist, typographer) and *actually studied* against Arial,
  OpenDyslexic, Verdana, Eido, Frutiger in 145 readers. *Strength:* rare real study + medical
  collaborators. *Weakness:* result was a **preference** signal (~half of low-vision readers), not a
  comprehension/speed win; Latin/French-centric
  ([ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0001691823001026)).
- **APHont (American Printing House for the Blind)** — purpose-built for large-print low vision
  (even spacing, high crossbars, heavier/wider letters). *Strength:* institutional pedigree,
  embodies large-print research. *Weakness:* **not OFL** (restrictive APH license), limited
  weights/scripts, dated distribution
  ([APH large-print guidelines](https://www.aph.org/resources/large-print-guidelines/);
  [Perkins School roundup](https://www.perkins.org/resource/my-eight-favorite-free-fonts-print-disabilities/)).

**Dyslexia-targeted:**

- **OpenDyslexic** — free, weighted-bottom letters; *hugely popular but evidence-thin/negative*
  ([PMC 2017](https://pmc.ncbi.nlm.nih.gov/articles/PMC5629233/)). *Strength:* mindshare, free.
  *Weakness:* no proven benefit; some studies show harm.
- **Dyslexie** — proprietary, similar concept; **no reading benefit** in controlled study
  ([Springer 2017](https://link.springer.com/article/10.1007/s11881-017-0154-6)). Cautionary tale
  for over-claiming.
- **Lexend (Shaver-Troup + Thomas Jockin; Google Fonts)** — OFL, variable, designed around
  reading-science principles (expansion + spacing to reduce crowding); the developers report
  proficiency gains in a large student sample
  ([Google Design case study](https://design.google/library/lexend-readability)). *Strength:*
  measures proficiency not just speed; strong distribution. *Weakness:* the headline study is
  largely developer-authored / not independently replicated — treat as promising, not settled.

**Broad legibility / literacy / coverage:**

- **Andika (SIL)** — OFL, designed for literacy learners with extensive extended-Latin coverage for
  African/Asian/American languages; explicitly notes it may also help low-vision/visual-stress
  readers ([SIL](https://software.sil.org/andika/andika-and-the-visually-impaired/)). Direct
  overlap with both project goals; a strong "extend, don't duplicate" candidate.
- **Inter (Rasmus Andersson)** — OFL, tall x-height, 140+ languages, variable, ubiquitous UI face
  ([GitHub](https://github.com/rsms/inter)). High legibility but UI-optimized, not accessibility-
  positioned — a quality bar to clear.
- **Noto (Google + Monotype)** — the 800-lb gorilla for script coverage: **162/168 Unicode scripts,
  ~1,000 languages**, Adlam co-designed with its creators; "largest source of fonts for endangered
  languages" ([Wikipedia](https://en.wikipedia.org/wiki/Noto_fonts);
  [Monotype case study](https://www.monotype.com/resources/case-studies/more-than-800-languages-in-a-single-typeface-creating-noto-for-google)).
  *Strength:* coverage, funding, distribution, durability. *Weakness:* harmonized "house style" can
  miss community-preferred forms; uneven weight/italic/variable depth; not accessibility-tuned.

**Infrastructure / methods (not competitors, but the ecosystem to plug into):** FontBakery QA
([repo](https://github.com/fonttools/fontbakery)), Hyperglot language-detection
([Rosetta](https://hyperglot.rosettatype.com/)), and gflanguages
([Google Fonts](https://github.com/googlefonts/lang)) — all already in the plan.

**Net read:** The accessibility-Latin space is **crowded with credible OFL incumbents**
(Atkinson Next, Lexend, Luciole, Andika, Inter). Building *yet another* original a11y Latin face
from scratch is the weakest strategic move available. Script coverage is **dominated by Noto** but
has real depth/specificity gaps. The defensible territory is **evidence-honesty + language-coverage
extension + provenance/QA rigor + community co-design**, not novel glyph drawing.

---

## 3. Gaps we can fill

1. **The honest, navigable map nobody maintains.** A continuously-updated, evidence-graded
   **"which open accessible font for which need/script/language"** resource — citing the contested
   evidence — does not exist in a trustworthy, neutral, open form. This is high-impact and low-craft-risk.
2. **Language-coverage *extension* of proven faces.** Take Atkinson Next / Lexend / Andika /
   Luciole and fill *specific* orthography gaps (extended-Latin African diacritics, a missing
   weight, a missing italic, a variable axis) for a *named* community — measurable via
   hyperglot/gflanguages, cheap to upstream, avoids duplicating Noto.
3. **Shaping/orthography *repair*, not new scripts.** Where Noto exists but a specific orthography
   shapes wrong or lacks community-preferred forms, contribute fixes upstream — a real, under-served,
   verifiable gap.
4. **QA + provenance commons.** A reusable FontBakery+HarfBuzz+coverage CI template and a
   `provenance.json` standard other open-font projects can adopt — infrastructure value independent
   of any single font shipping.
5. **Accessibility *usage* guidance** (size/contrast/line-length/spacing, WCAG-referenced) that is
   evidence-graded and honest that *layout beats typeface* — fills the gap left by vendors who
   over-sell the font itself.

---

## 4. Differentiators to win

1. **Evidence honesty as the brand** — the only open-font effort that publishes the contested
   evidence and reframes (or kills) claims accordingly. Trust is the moat in a field full of
   over-claims.
2. **Community-as-co-author with a real veto** — operationalized (signs the *brief*, not the
   finished font), not tokenized; differentiates from top-down house-style coverage.
3. **Provenance you can audit** — per-glyph clean-room manifest + reproducible builds; a license
   guarantee competitors rarely document.
4. **"Delivered, not merged"** — adoption event required (upstreamed or deployed for a named
   beneficiary), aligning with Elyos's outcome bar vs. repo-dump font releases.
5. **Coverage + accessibility together** — most incumbents do one; the program treats
   under-served-script legibility as a single mandate (fonts-a11y-309, fonts-multiscript-308).

---

## 5. Claude API leverage (and hard limits)

**Where Claude genuinely helps (non-design, verifiable, high-leverage):**

- **The evidence brief & honest claims** (fonts-research-005): synthesize and *grade* the
  legibility literature, draft the reusable non-medical framing text, and red-team specimen/README
  copy for over-claiming. (Every citation human-verified.)
- **Glyph-coverage & language-support analysis**: drive hyperglot/gflanguages to compute and explain
  per-language coverage gaps, generate the M3 coverage dataset, and turn raw FontBakery/HarfBuzz
  diff output into human-readable QA narratives and triage suggestions.
- **Pipeline, CI, and docs scaffolding** (fonts-infra-001/002): generate the fontmake/gftools build
  config, GitHub Actions, FONTLOG/OFL/`provenance.json` templates, specimen HTML, web `@font-face`
  kits, usage guides, and the maintenance playbook.
- **Testing scaffolds**: build HarfBuzz shaping test-string harnesses, proofing pages, and
  diff-report tooling (the *scaffold*, not the verdict on correctness).
- **Curation/guidance**: draft and maintain the "which font for which need" resource and the
  partner-outreach materials.

**Where Claude must NOT decide (wire these as guardrails):**

- **Type design is expert human work.** Claude does not draw production glyphs, set final
  spacing/kerning, or judge drawing quality — that is the type-design reviewer's call.
- **Legibility/efficacy claims must be evidence-based, never asserted by the model.** Claude may
  summarize studies; it must not *generate* a benefit claim. No fabricated or extrapolated efficacy
  numbers — ever (the Dyslexie/OpenDyslexic literature is the cautionary case).
- **OFL/clean-room compliance is human-verified.** Claude can *flag* suspected provenance/RFN issues
  but the maintainer's license audit is authoritative; never let the model autotrace or "start from"
  a proprietary face.
- **Script correctness belongs to native readers / the script authority.** Claude does not validate
  orthographic forms or shaping correctness for a community's script — the community holds the veto.
- **Human-subjects/PII**: Claude never handles identifiable reader/disability data; testing stays
  partner-run, consented, aggregate.

---

## 6. Ten concrete optimizations

1. **Default to "extend a proven OFL face," not "draw from scratch."** Flip Q4: original drawing is
   the exception requiring a committed expert designer. Cuts the largest effort/quality risk (§1b).
2. **Apply the contested-evidence skepticism to low-vision too.** State in the brief that
   size/contrast/spacing outweigh typeface choice; position the family as "open + legibility-
   principled + wide coverage," not "clinically better" (§1a).
3. **Reframe the script shortlist around *specific* deficiencies** (missing weight/italic/variable/
   orthographic form/broken shaping), explicitly differentiating from Noto's 162-script coverage
   (§1e); make "does Noto already cover this adequately?" a required column in fonts-research-004.
4. **Relax "byte-stable" to deterministic-content reproducibility** (normalized `ttx`/diff equality)
   to avoid a fragile, perpetually-red CI gate (§1c).
5. **Add an automated Reserved-Font-Name / trademark name-search gate** to release, closing the RFN
   risk that currently has no automated check (§1d).
6. **Ship the "honest font chooser" guidance resource as an early, partner-light deliverable** (M0/M1)
   — high impact, low craft risk, and seeds outreach/credibility before any font ships (§3.1).
7. **Plan a lightweight partner-run preference/comprehension proofing protocol in M0** so O8 yields a
   real signal for the shipped font instead of defaulting to "cite published research" that doesn't
   cover it (§1f).
8. **Keep the accessibility family's hinting closer to mainline** (don't fully defer fonts-hint-307):
   low-vision users disproportionately run older/low-DPI hardware where hinting matters (§1c).
9. **Prioritize upstream contribution to Noto/Atkinson Next/Andika** as a first-class adoption path,
   not just self-hosting — durability + reach come "free" and align with M4 sustainability.
10. **Add an independent-replication caveat to any Lexend-style proficiency citation** in the brief
    (developer-authored studies flagged as promising-not-settled) to keep the evidence bar uniform.

---

## 7. Parallel & perpendicular spin-offs

- **font-accessibility-guidance** (perpendicular, high-value): the evidence-graded, openly-licensed
  "which font + which layout for which need/script" resource. Lowest craft risk, highest trust
  payoff; can ship before any glyph is drawn.
- **MCP server: `font-coverage` / `font-qa`** (perpendicular): expose hyperglot/gflanguages coverage
  checks, FontBakery summaries, and HarfBuzz shaping diffs as MCP tools so any Elyos agent (or
  external project) can ask "does font X cover language Y, and is it QA-clean?" Reuses the exact
  Claude-leverage tooling from §5.
- **handwriting-practice** (parallel): shares letterform/differentiation design thinking and
  community-orthography data; accessible fonts can drive practice-sheet generation.
- **keyboard-layouts-open** (parallel): a script needs *input* as much as *rendering*; pairing a new
  font with an open keyboard layout makes a language genuinely typeable — strong co-delivery story.
- **easy-read-plus** (parallel/downstream): consumes the accessibility family + usage guide for
  easy-read documents; a natural first adoption event for M1.
- **braille-ready-texts** (parallel/downstream): print/large-print companion to braille pipelines;
  large-print legibility guidance feeds both.
- All four named downstream consumers (literacy, decodable-readers, captions, signage) double as
  **built-in adoption-event sources**, de-risking the "delivered, not merged" bar.

---

## 8. Open questions

1. **Extend vs. from-scratch as the *default*** — given the labor asymmetry and crowded a11y-Latin
   field, should the program commit to extend-first and reserve original drawing for genuine gaps?
2. **Is there a real, *unmet* script need** once Noto's 162-script/1,000-language coverage is
   subtracted — and can fonts-research-004 prove it in *specific* (weight/orthography/shaping) terms
   before committing a community partner's time?
3. **Can the project secure even one lightweight partner-run proofing study**, or does it accept that
   O8 will, for the foreseeable future, lean on (non-specific) published research?
4. **Where does the highest-leverage work actually sit** — drawing fonts, or the guidance/QA/coverage
   *commons* (curation, MCP tooling, provenance standard) that helps the whole open-font ecosystem?
5. **Low-vision hinting investment** — how much manual hinting is justified for the legacy/low-DPI
   hardware low-vision users disproportionately run?
6. **Upstream-first adoption** — should contributing to Atkinson Next / Andika / Noto count as a
   *preferred* delivery outcome over standalone releases?
7. **RFN/trademark** — automated name-search gate owner and tooling before first release.

---

## Executive summary (~300 words)

`open-accessible-fonts` is a notably mature, self-aware plan: it already bakes in the field's two
hardest truths and operationalizes honest guardrails (OFL clean-room, community veto, non-medical
framing, `verifiedNeed=false`). My review refines rather than rescues it.

**Top 3 competitors.** (1) **Atkinson Hyperlegible / Atkinson Hyperlegible Next** (Braille
Institute) — the OFL low-vision leader, now variable + 150+ languages, but with thinner
peer-reviewed efficacy evidence than its reputation. (2) **Noto** (Google/Monotype) — 162 of 168
Unicode scripts and ~1,000 languages, Adlam co-designed with its inventors; dominates the
script-coverage premise. (3) **Lexend** (and Andika/Luciole/Inter as the crowded supporting cast) —
OFL, reading-science-driven, well-distributed.

**Single strongest differentiator.** *Evidence honesty as the brand* — the only open-font effort
that publishes the contested legibility evidence and reframes or kills claims accordingly, paired
with auditable per-glyph provenance and community co-authorship. Trust is the moat in a field full
of over-claims.

**Top 3 Claude-API ideas.** (1) Author and *grade* the legibility evidence brief and red-team
specimen/README copy for over-claiming. (2) Drive hyperglot/gflanguages + FontBakery/HarfBuzz to
produce coverage datasets and human-readable QA/shaping reports. (3) Scaffold the build/CI,
provenance/FONTLOG templates, specimens, usage guides, and a `font-coverage` MCP server — never
drawing glyphs or asserting efficacy.

**Two most important plan-correctness findings.** (1) **Contested-evidence dimension:** the plan
handles dyslexia-font skepticism correctly (OpenDyslexic/Dyslexie show no proven benefit; BDA
favors plain sans-serif) but should extend the *same* skepticism to its low-vision framing — even
Atkinson/Luciole lack strong comprehension evidence, and size/contrast/spacing outweigh typeface
choice; position the family accordingly. (2) **Scope realism:** drawing original families from
scratch is the weakest move in a crowded OFL-a11y field largely covered by Noto; *extend-first*
(fill specific weight/orthography/shaping gaps in proven faces) plus curation/QA/coverage commons is
higher-impact and lower-risk.
