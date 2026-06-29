# open-accessible-fonts — PLAN

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) ·
> Lane: donated · Risk tier: **medium** · Track: 4 (Language, translation & accessibility)

**Positioning (one line):** Letters are infrastructure. A script with no open, well-made font is a
language that cannot be typed, taught, or read on a screen — and a reader with low vision or
dyslexia who is handed a font built for no one in particular is being quietly excluded. Elyos
**open-accessible-fonts** produces a small number of *excellent*, openly licensed (OFL) type
families that (a) give under-served scripts a free, correct, shapable font and (b) apply published
legibility research so low-vision and dyslexic readers get a fair chance — with provenance on every
glyph and the affected language/reading communities in the driver's seat, not the footnotes.

**Who this is for, in one breath:** a teacher in a Fulfulde classroom whose textbook has to be set
in a script (Adlam) that most devices ship no font for; an older reader losing central vision who
needs letterforms that don't collapse into each other at 14pt; a dyslexic student for whom `b`,
`d`, `p`, `q` are four shapes of the same anxiety. None of them should have to pay, and none of them
should have to accept a guess made *about* them rather than *with* them.

**The constraint that is the identity:** we ship **OFL-only, clean-room, community-reviewed** type,
or we do not ship. We never trace a proprietary font, never over-claim a clinical/medical benefit,
and never design an under-served script *for* a community instead of *with* it. Those three refusals
are the product.

---

## 1. Executive summary

open-accessible-fonts is a donated-compute Elyos good-deed project that designs, builds, QAs, and
releases a focused portfolio of **openly licensed (SIL OFL 1.1) fonts** addressing two
under-served audiences that overlap more than people assume:

1. **Under-served scripts** — writing systems with poor or no free font coverage (e.g. Adlam,
   N'Ko, Tifinagh, Vai, Osage, Ol Chiki, Canadian Aboriginal Syllabics, and extended-Latin
   African orthographies). Without a font, a script cannot be rendered, taught digitally, or used
   online — a hard digital-inclusion barrier.
2. **Low-vision and dyslexia/reading accessibility** — Latin (and, later, multi-script) type
   designed to published legibility principles (clear letter differentiation, generous spacing,
   open apertures, large x-height), shipped as static and variable fonts.

The deliverable of each "deed" is **font source + built binaries + QA report + type specimen +
provenance record**, released under OFL with code/tooling under MIT. The bar is Elyos's
"delivered, not merged": a font is done when it passes automated QA (FontBakery + shaping diff),
passes **expert + community/lived-experience review**, and is *actually adopted* — handed to the
requesting community, accepted upstream (e.g. Google Fonts / Noto), or deployed in a real document.

This is honestly a **medium-risk, craft-heavy** program. Type design is slow and unforgiving;
script correctness errors can harm a community; and accessibility benefit claims are scientifically
**contested** (especially for "dyslexia fonts"). The plan treats all three as first-class risks:
clean-room provenance, native-reader review for every script, and a disciplined **"designed using
legibility research; not a medical device, not a treatment, not a diagnosis"** stance for the
accessibility work.

**No partner, requestor, or script community is secured yet.** Every "verified need" in TASKS.md is
`false` until a named community/partner signs on. This is the single most important human decision
gate (see §16).

---

## 2. Problem & beneficiaries

### The problem

- **Script invisibility.** Unicode encodes hundreds of scripts; far fewer have a *free, complete,
  correctly shaping* font. Where Noto and a handful of community fonts have filled gaps, real holes
  remain: missing weights, missing diacritic/orthography coverage for specific languages, broken or
  absent OpenType shaping (GSUB/GPOS) for complex scripts, and no italic/variable options. The
  practical effect: a language cannot be set in a textbook, an app shows tofu (□□□), and an entire
  speech community is pushed onto a colonizing script or off digital text entirely.
- **Accessibility as an afterthought.** Most default UI/body fonts are not designed for readers with
  low vision (macular degeneration, cataract, diabetic retinopathy) or for dyslexic readers. Cheap
  failures — `I`/`l`/`1`, `O`/`0`, `rn`/`m`, mirror pairs `b`/`d`/`p`/`q` — cause real reading
  errors. A small number of openly licensed accessibility faces exist (e.g. Atkinson Hyperlegible),
  proving demand; coverage and language reach are still thin.

### Beneficiaries (who is actually helped)

| Beneficiary | Harm today | What this project gives them |
|---|---|---|
| Speakers/learners of under-served-script languages | Can't render/type/teach their script digitally | A free, correct, shapable OFL font for their orthography |
| Teachers & OER authors (overlaps `literacy-from-zero`, `decodable-readers`) | Can't typeset materials in the target script or in a legible face | Fonts they can embed in open educational materials |
| Low-vision readers | Glyph confusion, fatigue, reading errors at body sizes | A legibility-first family tuned to differentiation & spacing |
| Dyslexic readers | Mirror/rotation confusion, crowding | A family applying (honestly-scoped) legibility principles |
| Downstream Elyos projects | Need embeddable fonts for documents/signage/captions | A reusable, license-clean font commons |

### Verified need & partner status — **TO BE SECURED**

There is **no secured partner, requesting community, or formal needs assessment yet.** This is a
gating constraint, not a detail:

- For **under-served scripts**, a font designed without the affected community is at best wasted and
  at worst harmful (wrong forms enshrined as "the open font"). We will **not** begin glyph drawing
  on a script until a **named script authority / language community partner** is secured and has
  co-defined the orthography and design brief.
- For **accessibility**, we require **lived-experience reviewers** (low-vision and dyslexic readers)
  and an **accessibility/vision specialist** (e.g. low-vision optometry, accessibility org) before
  any benefit framing is published.

Candidate partners to approach (all **TO BE SECURED**, none contacted): SIL Global / Non-Roman
Script Initiative; the Noto / Google Fonts program; script-specific communities (e.g. Adlam /
Winden Jangen, N'Ko literacy groups); accessibility orgs (RNIB, Braille Institute, Bureau of
Internet Accessibility); and university type-design programs. **Listing a candidate is not a
commitment from them.**

---

## 3. Goals and non-goals

### Goals

1. Ship a small number of **excellent**, OFL-licensed font families — quality over catalog size.
2. Give at least one **under-served script** a free, correct, community-validated font with working
   complex-script shaping.
3. Ship at least one **accessibility-first** family grounded in published legibility research, with
   honest, non-medical framing and lived-experience validation.
4. Make **provenance and licensing** auditable: every glyph traceable to a clean-room or OFL/PD
   source; no proprietary derivation.
5. Build a **reusable, reproducible font pipeline** (source → build → QA → specimen → release) so
   each subsequent family is cheaper than the last.
6. Achieve **real adoption**, not just a repo: upstream acceptance (Google Fonts/Noto) and/or
   deployment in a real document handed to the beneficiary community.

### Non-goals (explicit — what this project will NOT do)

- **Will not trace, autotrace, or derive from proprietary fonts.** No "clean up a commercial face."
- **Will not claim clinical/medical efficacy.** Not a treatment for dyslexia or any vision
  condition; not a medical device; not a diagnosis. We claim *design intent grounded in legibility
  research*, nothing more.
- **Will not design an under-served script without that community.** No extractive, "we know best"
  type design. No new/invented orthographies.
- **Will not pursue breadth-first coverage** of dozens of scripts. Depth on a few beats tofu-removal
  theater on many.
- **Will not build font-editing apps or a web foundry** as a primary deliverable (tooling is glue,
  not the product). Source format and CLI build only.
- **Will not handle controlled/identifiable data.** Any reading/legibility testing with humans uses
  consented, aggregate, de-identified results only (see §7, §14) — and is preferred to be deferred
  to partner-run studies rather than run by this project.
- **Will not ship a font that fails QA or lacks community/expert sign-off** to hit a date.

---

## 4. Success metrics (outcomes)

Outcome-based (beneficiary impact), not vanity. Baselines are mostly **unknown until a partner +
target script/audience are chosen**; targets are stated as the shape of success.

| # | Outcome metric | Baseline | Target |
|---|---|---|---|
| O1 | Under-served scripts given a complete, correctly-shaping OFL font | 0 | ≥1 by M2, ≥2 by M4 |
| O2 | Language orthographies covered (per `gflanguages`/Hyperglot) by shipped fonts | 0 | ≥1 script's primary language fully covered; ≥3 languages by M4 |
| O3 | Accessibility families shipped with expert + lived-experience sign-off | 0 | ≥1 by M1 |
| O4 | Real adoption events (upstreamed to GF/Noto, or deployed in a delivered document) | 0 | ≥1 by M2, ≥3 by M4 |
| O5 | Community/native-reader review pass rate before release | n/a | 100% (release gated on it) |
| O6 | Provenance completeness (glyphs/sources with recorded provenance) | n/a | 100% |
| O7 | Automated QA (FontBakery Universal/GF profile) pass on every release | n/a | 100% (no `FAIL`; `WARN` triaged) |
| O8 | Legibility validation: comprehension/error-rate or preference signal from low-vision/dyslexic readers (partner-run, consented, aggregate) | unknown | Documented, honest result — even if null/mixed |

**Honesty clause for O8:** if validation shows no measurable accessibility benefit, we **report that
truthfully** and reframe the font as "high-legibility, openly licensed" rather than suppressing the
result. A null result is a delivered outcome, not a failure to hide.

---

## 5. Scope

### In scope

- Font **source** in UFO + designspace, version-controlled, human-readable, diffable.
- Reproducible **build** to static OTF/TTF, **variable** fonts, and **WOFF2** for web.
- Glyph design for: an accessibility-first Latin family; ≥1 under-served script (community-led).
- **OpenType layout** (GSUB/GPOS) for complex-script shaping; kerning; mark positioning.
- **QA**: FontBakery, HarfBuzz shaping diffs, Unicode coverage & language-support reports,
  cross-platform/cross-renderer rendering checks.
- **Type specimens**, web-delivery kits, and an **accessibility usage guide** (size, contrast,
  line-length recommendations — referencing WCAG, framed as guidance not compliance certification).
- **Provenance & licensing** artifacts: `OFL.txt`, `FONTLOG.txt`, `provenance.json`, designer/source
  attribution, glyph-source manifest.
- Governance: community co-design protocol, reviewer roster, release checklist.

### Out of scope

- Designing/standardizing **new scripts or orthographies** (defer to Unicode/ScriptSource/community
  processes; we implement what is already encoded and community-accepted).
- **Hinting at the level of bespoke per-glyph TrueType instructions** for legacy low-DPI Windows
  (we use autohinting / `gftools` defaults; manual hinting only if a partner requires and resources).
- **Font hosting/CDN service**, font-management apps, or a web font foundry product.
- **Right-to-left/bidi UI app** development; we ship fonts + shaping, not editors.
- **Proprietary-format deliverables** (e.g. Glyphs-only `.glyphs` as the canonical source — UFO is
  canonical so the source is fully open-tool buildable).
- **Human-subjects legibility trials run by this project** (we rely on partner-run or
  published research; if any data is gathered, see §7/§14 consent constraints).
- **Medical, optometric, or educational-diagnostic advice.**

---

## 6. Solution approach & architecture

This is a **content/craft pipeline** project (type design) wrapped in a reproducible
software toolchain. The architecture is the pipeline plus the QA/provenance gates around it.

### Pipeline (source → release)

```
 design brief + glyph set spec
        │  (community + accessibility review at the brief stage, not after)
        ▼
 UFO sources (.ufo) + designspace  ──► version-controlled in git (canonical, open-tool)
        │
        ├─ build: fontmake → static OTF/TTF + variable .ttf
        ├─ post: gftools (fix-* , autohint), fontTools subset → WOFF2
        ▼
 build artifacts (OTF/TTF/variable/WOFF2)
        │
        ├─ QA gate: FontBakery (Universal + GF profile)            ── must pass (no FAIL)
        ├─ shaping gate: HarfBuzz shaping diff (diffenator/fontproof) for complex scripts
        ├─ coverage gate: Unicode + gflanguages/Hyperglot language-support report
        ▼
 review gate: community/native-reader sign-off (scripts) + expert/lived-experience (a11y)
        │
        ▼
 release: tagged version + specimen PDF + provenance.json + OFL.txt + FONTLOG.txt
        │
        ▼
 adoption: hand to community / upstream PR to Google Fonts/Noto / deploy in a document
```

### Components & tech stack

- **Canonical source format:** UFO 3 + designspace (open, tool-agnostic, diffable). `.glyphs` may be
  used by individual designers but **UFO is the committed source of truth.**
- **Build:** `fontmake` (UFO→binaries, variable fonts), `gftools` (fixes, autohinting, packaging),
  `fontTools` (subsetting, WOFF2, manipulation). Python, pinned via a lockfile.
- **QA:** `fontbakery` (Universal + Google Fonts profiles), `diffenator2`/`fontproof` for shaping &
  rendering diffs, HarfBuzz for shaping ground truth, `hyperglot`/`gflanguages` for language coverage.
- **Shaping/layout:** OpenType features authored in `.fea` (FEZ/feaLib), validated against HarfBuzz.
- **Specimens & proofs:** `gftools` proofing / `diffenator2` HTML proofs; specimen as reproducible
  HTML→PDF.
- **CI:** GitHub Actions runs build + FontBakery + shaping/coverage reports on every PR; artifacts
  attached. (Elyos donated-lane: the human runs their agent locally; CI verifies — the CLI never
  runs a coding agent itself, per CLAUDE.md.)
- **Repo layout (per family):** `sources/`, `fonts/` (built, generated), `documentation/`
  (specimen, ARTICLE), `OFL.txt`, `FONTLOG.txt`, `provenance.json`, `METADATA` (GF-compatible),
  `.fontbakery` config — mirroring Google Fonts upstream conventions for cheap upstreaming.

### Data model (provenance & metadata)

- `provenance.json` (project-defined, see §7): per source — origin, license, designer(s), whether
  clean-room original, references consulted, date, reviewer, community sign-off record.
- `FONTLOG.txt`: OFL-required changelog/acknowledgements (a hard OFL convention).
- `METADATA` / `gflanguages` language declarations for coverage truth.

### Key decisions (locked)

1. **OFL 1.1 for all fonts; MIT for tooling/code; CC-BY-4.0 for docs/specimens.** No exceptions.
2. **UFO is the canonical, committed source** (no proprietary-only source of truth).
3. **Clean-room only.** Every glyph is an original drawing or derived from an OFL/PD source whose
   license permits derivatives; **no proprietary tracing/autotracing, ever.**
4. **Variable-first where sensible** (weight axis at minimum), with static instances exported.
5. **Review-before-draw for scripts:** community + orthography sign-off on the *brief*, not just the
   finished font.
6. **Accessibility framing is non-medical, evidence-honest** (the "not a treatment" stance is wired
   into the specimen, README, and usage guide as standard text).
7. **Reproducible builds:** anyone can rebuild identical binaries from source with pinned tooling.

---

## 7. Data, licensing & compliance  *(CRITICAL — conservative by default)*

Type design has unusually sharp IP and cultural edges. This section is binding.

### Licensing of outputs

- **Fonts:** SIL **Open Font License 1.1 (OFL)** — the de-facto standard for open fonts; permits
  use, study, modification, and redistribution, including bundling, with reserved font names and a
  no-standalone-sale clause. Each family ships `OFL.txt` + `FONTLOG.txt` (required) and declares a
  **Reserved Font Name** policy.
- **Code/tooling/build scripts:** **MIT**.
- **Documentation, specimens, usage guides:** **CC-BY-4.0**.

### Permissible *input* sources (allow-list)

Reference and derivation material is restricted to:

- **Original clean-room drawing** (preferred; default for all glyphs).
- **OFL-licensed fonts** whose license permits modification/derivation (with FONTLOG attribution and
  Reserved Font Name compliance).
- **Public-domain** letterform references (historical specimens out of copyright) — with the
  jurisdictional caveat below.
- **CC0 / CC-BY / PD** script charts, Unicode code charts (used as encoding reference, not artwork),
  and community-provided reference forms **with explicit permission**.

### Prohibited inputs (hard refusals)

- Proprietary/commercial fonts as a tracing, autotracing, or "starting point" source.
- Glyph outlines copied from any source whose license forbids derivatives.
- Scraped/uncertain-license imagery of letterforms.
- Any reference whose provenance cannot be established → **excluded**.

### Font-IP nuance (recorded, handled conservatively)

Jurisdictions differ: in the US, **typeface *designs* are generally not copyrightable**, but **font
*software* (the outline program, hinting, naming) is**, and some jurisdictions (and design/patent
regimes) protect designs. We do **not** rely on the US carve-out — our rule is the stricter
clean-room standard above, so the output is safe to redistribute globally. Trademark on font
*names* is respected via Reserved Font Name discipline.

### Provenance model

Every release carries `provenance.json` proving the clean-room/allow-list chain:

```jsonc
{
  "family": "TBD",
  "license": "OFL-1.1",
  "reservedFontNames": ["TBD"],
  "glyphSources": [
    { "scope": "Latin core", "origin": "original-clean-room",
      "designer": "TBD", "references": ["Unicode code charts (encoding only)"],
      "license": "n/a (original)", "date": "TBD", "reviewer": "TBD" }
  ],
  "scriptAuthority": { "name": "TO BE SECURED", "signOff": null },
  "accessibilityReview": { "expert": "TO BE SECURED", "livedExperience": "TO BE SECURED",
                           "claims": "legibility-design-intent-only; non-medical" },
  "fontbakeryReport": "path/to/report",
  "buildToolingLock": "requirements.lock"
}
```

### Privacy / PII

- The fonts themselves contain no personal data.
- **Contributor/reviewer data:** names credited only with consent (FONTLOG attribution is
  opt-in-by-consent; pseudonyms honored).
- **Legibility testing data (if any):** strongly prefer partner-run or published studies. If this
  project ever gathers reader feedback, it must be **consented, aggregate, de-identified**, with no
  health/disability status tied to an identifiable person (a disability self-identification is
  sensitive PII). Default stance: **don't collect; cite published research.**

### Cultural & attribution requirements (scripts)

- The affected **script/language community is credited as co-designer**, not "consulted."
- Orthographic choices follow community + Unicode/ScriptSource consensus; **no invented forms.**
- Right to be **named or anonymous** respected; right to **request changes** documented in
  governance.

---

## 8. Quality, review & risk gates

**Risk tier: medium** (per ROADMAP and the good-deed definition). Rationale: requires *domain
accuracy* (script correctness; legibility design), carries *cultural-harm* risk (wrong script
forms), and touches *accessibility claims* that border on health (handled by hard non-medical
framing). It is **not "high"** because we publish **no medical/clinical advice**; if any
accessibility claim drifted toward clinical efficacy, that specific work would escalate to **high**
and require credentialed expert sign-off before merge.

### Required reviews before a deed is "done"

| Work type | Automated gate | Human gate (required) |
|---|---|---|
| Any font release | FontBakery (no FAIL) + reproducible build | Maintainer review |
| Under-served script | + shaping diff (HarfBuzz) + coverage report | **Native-reader / script-authority sign-off** (medium) |
| Accessibility family | + coverage report | **Accessibility/vision specialist + lived-experience reviewer(s)** sign-off; non-medical framing verified |
| Any benefit/efficacy claim | — | **Escalate to high**: credentialed expert sign-off, or remove the claim |
| Provenance | provenance.json present & complete | Maintainer license/provenance audit |

### Definition of Shipped (project-level)

A font is **Shipped/Delivered** when: acceptance criteria met **and** automated QA green **and**
required human/community/expert sign-off recorded **and** OFL/FONTLOG/provenance complete **and**
the artifact is *actually adopted* — handed to the requesting community, accepted upstream
(GF/Noto), or deployed in a delivered document. Merged ≠ done.

---

## 9. Roadmap & milestones

Phased, with measurable **exit criteria**. M0 is a thin, partner-independent cold-start;
script work is explicitly **blocked on securing a community partner**.

### M0 — Foundation & cold-start (no partner required)
**Goal:** stand up the reproducible pipeline, QA/provenance gates, governance, and the two research
spines (script-gap analysis; accessibility-evidence review) so later phases are de-risked.
**Exit criteria:**
- Repo builds a trivial test UFO → OTF/TTF/variable/WOFF2 reproducibly in CI.
- FontBakery + shaping + coverage reports run automatically on PR.
- Licensing/provenance framework (`OFL.txt`/`FONTLOG.txt`/`provenance.json` templates + clean-room
  policy) merged and documented.
- Under-served-script **prioritization shortlist** + accessibility **evidence brief** (honest on
  contested dyslexia-font claims) published.
- Governance + community co-design protocol + reviewer roster (roles, even if names TBD) merged.

### M1 — Accessibility-first Latin family (pilot deliverable)
**Goal:** ship one excellent, legibility-driven Latin family with honest framing and lived-experience
review. Chosen first because it is **partner-light** (no script community gate) and proves the
pipeline end-to-end.
**Exit criteria:**
- Design brief + glyph set spec approved (covers GF Latin Core + accessibility-critical
  differentiation set: `Il1`, `O0`, `bdpq`, `rn/m`, etc.).
- Core glyph set drawn in UFO; builds clean; FontBakery green.
- Legibility proofing + **accessibility specialist + ≥2 lived-experience reviewers** sign-off; the
  **non-medical framing** verified in README/specimen/usage guide.
- v1.0 released (static + variable + WOFF2 + specimen + provenance) under OFL; **≥1 adoption event**
  (GF submission opened or deployed in a real document).

### M2 — First under-served script (community co-designed) — **BLOCKED on partner**
**Goal:** give one under-served script a free, correct, shapable OFL font, co-designed with its
community.
**Entry gate:** a named script authority / language-community partner secured; orthography &
brief co-signed. *(Until then this milestone does not start; verifiedNeed=false.)*
**Exit criteria:**
- Orthography spec + glyph set + shaping requirements co-signed by the community.
- Glyphs + OpenType GSUB/GPOS implemented; HarfBuzz shaping diff clean against community test
  strings; coverage report shows the primary language fully covered.
- **Native-reader correctness review** passed (100%).
- Released under OFL with specimen + provenance + FONTLOG crediting the community; **≥1 adoption
  event** (community use or Noto/GF upstreaming).

### M3 — Scale & delivery
**Goal:** broaden weight/optical coverage, harden web delivery, and add a coverage dataset; begin a
second script *only if* a second partner is secured.
**Exit criteria:**
- Variable axes (≥ weight; optical size where justified) consolidated and QA-green.
- Web delivery kit (WOFF2 + `@font-face` + accessibility usage guide) published.
- Language-support matrix dataset (Hyperglot/gflanguages) published as an open dataset.
- ≥3 total adoption events across the portfolio.

### M4 — Sustainability & handoff
**Goal:** ensure the fonts outlive the project — upstream homes, maintenance playbook, outcome
tracking.
**Exit criteria:**
- ≥1 family accepted into a durable upstream (Google Fonts / Noto) or a committed community
  maintainer named.
- Maintenance playbook (issue triage, re-release, Unicode/tooling updates) published.
- Outcome-tracking ledger live (adoption + any legibility findings, including null results).

---

## 10. Work breakdown

The itemized, schema-mapped backlog lives in **TASKS.md**, organized by the M0–M4 milestones above.
Each task maps to an Elyos Task JSON (donated lane unless noted), with type, riskTier, deliverable,
acceptance criteria, and `verifiedNeed` set **honestly** (`false` wherever no partner/requestor is
secured — i.e. all script tasks and any benefit-claim tasks today). TASKS.md also carries the
milestone Definitions of Done and one full schema-valid example Task JSON.

---

## 11. Governance, roles & stakeholders

| Role | Responsibility | Status |
|---|---|---|
| **Maintainer / project owner** | Roadmap, release sign-off, license/provenance audit | TBD |
| **Type design reviewers (rotation)** | Drawing quality, spacing, OpenType correctness | TBD (≥1 experienced type designer) |
| **Script authority / community partner** | Orthography, glyph forms, native-reader review, co-design | **TO BE SECURED** (per script) |
| **Accessibility/vision specialist** | Legibility design review; non-medical claim boundary | **TO BE SECURED** |
| **Lived-experience reviewers** | Low-vision & dyslexic reader feedback (consented) | **TO BE SECURED** (≥2) |
| **Steward (last-mile owner)** | Drives actual adoption: upstreaming, community handoff, deployment | TBD |
| **Requestor / beneficiary** | The community/org that asked for the script/face | **TO BE SECURED** |
| **Elyos governance/board** | Edge-case rulings, COI/veto, risk-tier escalation | Existing Elyos process |

Co-design principle (binding): for any under-served script, **the community holds an effective veto**
on forms and naming, and is credited as co-author. Decisions and change-requests are logged
publicly.

---

## 12. Dependencies & integrations

- **Tooling:** fontmake, fontTools, gftools, fontbakery, diffenator2/fontproof, HarfBuzz,
  hyperglot, gflanguages (all open-source, Python). Pinned via lockfile.
- **Upstream homes:** Google Fonts repo conventions; Noto project; (optionally) a community-hosted
  repo. Acceptance criteria for upstreaming are external and must be met.
- **Encoding references:** Unicode code charts (encoding reference only), ScriptSource (community
  orthography reference).
- **Elyos platform:** task schema (`packages/schema`), CLI workspace prep (donated lane — never runs
  the agent), registry entry, CI/governance workflows.
- **Cross-project:** `literacy-from-zero`, `decodable-readers`, `open-childrens-books`,
  `caption-commons`, `easy-read-plus`, `braille-ready-texts`, `multilingual-signage-templates` are
  downstream consumers of these fonts.
- **People dependencies (the real critical path):** script communities, accessibility/vision
  experts, lived-experience reviewers — **all unsecured**.

---

## 13. Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|
| Designing a script *without* its community → wrong/harmful forms | Med | High | Hard entry gate: no glyph drawing before community partner + co-signed brief; community veto | Maintainer |
| Accessibility benefit over-claimed (esp. dyslexia, where evidence is contested) | Med | High | Standard "non-medical, design-intent-only" framing; expert + lived-experience review; escalate any efficacy claim to high-risk | A11y specialist |
| Proprietary-font IP contamination (tracing/derivation) | Low | High | Clean-room policy; provenance.json on every glyph source; maintainer license audit; reject unknown-provenance refs | Maintainer |
| No partner/community ever secured → script lane stalls | Med | Med | M1 (accessibility) is partner-light and ships first; script lane explicitly blocked, not faked; verifiedNeed=false | Steward |
| Complex-script shaping bugs (GSUB/GPOS) render text wrong | Med | High | HarfBuzz shaping-diff CI gate + native-reader test strings; no release on shaping FAIL | Reviewers |
| Type design slower than estimated (craft is slow) | High | Med | Narrow scope (Latin core first); variable-first reuse; honest sizing; quality over count | Maintainer |
| Cross-platform rendering inconsistencies (old Windows/hinting) | Med | Med | gftools autohint + diffenator2 rendering checks; document known limits | Reviewers |
| Reviewer/lived-experience PII or disability status exposed | Low | High | Consent-only credit; no disability data tied to identity; aggregate-only feedback | Maintainer |
| Reserved Font Name / trademark conflict | Low | Med | RFN discipline; name search before release | Maintainer |
| Null legibility result tempts suppression | Med | Med | Honesty clause (O8): report null/mixed results; reframe as "high-legibility" | Steward |
| Upstream (GF/Noto) rejects submission | Med | Low | Treat repo + community handoff as valid adoption; meet upstream specs early | Steward |

---

## 14. Security & privacy

- **Threat surface is small** (no service, no user data store) but non-zero: malicious font files,
  supply-chain (Python deps), and reviewer PII.
- **Secrets:** none in fonts/receipts/logs (per CLAUDE.md). CI tokens scoped minimally; no API keys
  committed. (Funded lane not used here; if ever used, hard per-task budget cap applies.)
- **Supply chain:** pin all build tooling via lockfile; CI builds in a clean environment;
  reproducible-build check detects tampering.
- **Font-file safety:** validate built binaries (FontBakery includes structural checks); no embedded
  scripts; subsetting via fontTools only.
- **PII:** contributor/reviewer names only by consent; pseudonyms honored; **no disability status or
  health data tied to an identifiable person**; any reader feedback aggregate + de-identified +
  consented, and preferably partner-run, not project-run.
- **Misuse prevention:** fonts are content with low abuse potential; the main misuse is
  misattribution — mitigated by RFN/OFL discipline and provenance. Refuse any request to derive from
  proprietary type or to falsify provenance.

---

## 15. Sustainability & maintenance

- **Upstream-first durability:** preferred end state is acceptance into Google Fonts / Noto, which
  provides long-term hosting, distribution, and a maintenance culture. Failing that, a **named
  community maintainer** must be committed before a script font is considered sustainably delivered.
- **Maintenance playbook (M4):** how to triage issues, re-build/re-release with updated tooling,
  respond to Unicode/orthography updates, and handle community change-requests.
- **Outcome tracking:** a public ledger records adoption events (upstream acceptance, document
  deployments, community usage) and any legibility findings — **including null/mixed results**.
- **Reproducibility guarantees** the font can be rebuilt by anyone, decoupling longevity from any
  one contributor.

---

## 16. Open questions

1. **Which under-served script first?** Decided *with* the first secured community, not pre-chosen
   here. (Prioritization shortlist is M0 research; selection requires a partner.)
2. **Who are the accessibility experts and lived-experience reviewers?** **TO BE SECURED** before any
   M1 benefit framing is published.
3. **Should we run our own legibility validation or rely solely on published/partner research?**
   Default: rely on published/partner research (avoid human-subjects/PII burden). Needs a human
   decision if a partner offers to run a study.
4. **New original accessibility face vs. extend an existing OFL face (e.g. Atkinson Hyperlegible)?**
   Trade-off: clean-room originality vs. faster, proven base. Decide at M1 brief, license permitting.
5. **Variable axis strategy** — is an explicit "legibility/accessibility" treatment an axis, a
   separate family, or just the default? Decide at M1 brief.
6. **Manual hinting** — invest for legacy low-DPI, or rely on autohinting? Resource-dependent.
7. **COI / naming** — confirm Reserved Font Names against trademark before each release.

**Headline human-decision gate:** No script work starts until **Q1/Q2** are resolved (a real
community partner + accessibility experts secured). Until then, `verifiedNeed=false` everywhere it
applies, and only the partner-light M0/M1 lane proceeds.

---

## 17. References

- SIL Open Font License 1.1 (OFL) and FONTLOG conventions.
- SIL Global / Non-Roman Script Initiative; ScriptSource (script/orthography reference).
- Unicode Standard & code charts (encoding reference only).
- Google Fonts / Noto project repository conventions and onboarding specs.
- Tooling: fontmake, fontTools, gftools, fontbakery, diffenator2/fontproof, HarfBuzz, hyperglot,
  gflanguages.
- Atkinson Hyperlegible (Braille Institute) — prior art for an openly licensed low-vision face.
- WCAG (for usage-guidance references on size/contrast/line-length — guidance, not certification).
- Published legibility/readability research (low vision; and the **contested** dyslexia-font
  literature — to be summarized honestly in the M0 evidence brief).
- Elyos: `CLAUDE.md`, `docs/good-deed-definition.md`, `packages/schema/src/schemas.ts`,
  `planning/ROADMAP.md`.

---

## Appendix A — Improvements applied

Twenty-five specific improvements identified against the first draft and **applied above** (not
merely proposed):

1. **Added an "honesty clause" (O8)** requiring null/mixed legibility results to be reported, not
   suppressed — closing the most likely integrity gap in an accessibility project.
2. **Wired the "not a medical device / not a treatment" framing into artifacts** (README, specimen,
   usage guide) as standard text, not just a non-goal — making the refusal operational.
3. **Made "review-before-draw" a locked decision** (community signs the brief, not the finished
   font) — preventing sunk-cost pressure to ship wrong forms.
4. **Sequenced the accessibility Latin family (M1) before any script work** because it is
   partner-light, de-risking pipeline proof without blocking on unsecured communities.
5. **Explicitly blocked M2 on a partner entry-gate** and set `verifiedNeed=false` for all script
   tasks — honest per the spec instead of inventing a community.
6. **Added the US "typeface design not copyrightable" nuance and then explicitly declined to rely on
   it**, adopting the stricter clean-room standard for global redistribution safety.
7. **Specified UFO as canonical committed source** (not `.glyphs`) so the source is fully buildable
   with open tools — a real open-source guarantee.
8. **Added reproducible-build requirement + tooling lockfile** as both a quality and a supply-chain
   security control.
9. **Added HarfBuzz shaping-diff as a hard CI gate** for complex scripts — the specific failure mode
   (broken GSUB/GPOS) that silently corrupts text.
10. **Added language-coverage truth via hyperglot/gflanguages** so "covered a language" is
    measurable (O2), not asserted.
11. **Defined a concrete `provenance.json` schema** with glyph-source granularity, script-authority
    sign-off, and accessibility-claim scope.
12. **Mandated FONTLOG.txt** (an actual OFL requirement people forget) and Reserved Font Name
    discipline to avoid trademark conflicts.
13. **Added cross-platform rendering checks (diffenator2)** to catch old-Windows/hinting regressions
    that QA-on-one-renderer would miss.
14. **Separated "delivered" from "merged" with an explicit adoption event** (upstream or deployed
    document) in the Definition of Shipped — aligning with Elyos's quality bar.
15. **Added a steward (last-mile owner) role** distinct from maintainer, because adoption/upstreaming
    is the step most likely to be dropped.
16. **Listed candidate partners but flagged "listing ≠ commitment"** to avoid implying secured
    relationships.
17. **Tightened PII stance to treat disability self-identification as sensitive PII** and defaulted
    to *not collecting* reader data, preferring published/partner research.
18. **Added a risk-tier escalation trigger:** any efficacy/clinical claim escalates the work to
    high-risk (credentialed sign-off) — making the medium/high boundary explicit.
19. **Scoped out human-subjects legibility trials run by the project** to avoid IRB/consent burden,
    with a clear human-decision point if a partner offers one.
20. **Made variable-first an explicit decision** with static export, reducing per-weight drawing cost
    (addresses the "type design is slow" risk).
21. **Mapped downstream Elyos consumers** (literacy, decodable-readers, captions, braille, signage)
    so the font commons has named demand and isn't built in a vacuum.
22. **Adopted Google Fonts repo layout from day one** to make eventual upstreaming cheap rather than
    a costly reformat.
23. **Added a community veto + public change-request log** to the governance section — operationalizing
    co-design instead of tokenizing it.
24. **Stated baselines as "unknown until partner/target chosen"** rather than fabricating baseline
    numbers — honest metrics.
25. **Added a positioning + "constraint is the identity" frame** (OFL-only, clean-room,
    community-led) matching the exemplar's depth and making the refusals the brand.

---

## Review sign-off

**Reviewer pass (self-review against PLAN_SPEC, CLAUDE.md, good-deed-definition, and the schema):**

- **Completeness:** All 17 required H2 sections present and ordered per PLAN_SPEC; metadata header
  present; Appendix A (25 applied improvements) and this sign-off added per the task. ✔
- **Guardrails:** License/provenance handled conservatively (OFL/MIT/CC-BY only; clean-room;
  prohibited inputs enumerated; provenance schema). Privacy/PII addressed (consent-only credit;
  disability status as sensitive PII; no project-run human trials by default). Non-medical framing
  for accessibility wired into artifacts with a high-risk escalation trigger. Cultural co-design with
  community veto. ✔
- **Honesty:** No partner/requestor/community invented — all marked **TO BE SECURED**;
  `verifiedNeed=false` mandated for script and benefit-claim tasks; baselines marked unknown; null
  results required to be reported. ✔
- **Risk tier:** Medium, with explicit rationale and the medium→high escalation boundary defined. ✔
- **Lane discipline:** Donated lane; CLI never runs the agent; CI verifies. Funded lane not used; cap
  noted if ever used. ✔
- **Correctness fixes applied during review:** (a) clarified that FONTLOG is OFL-*required*, not
  optional; (b) ensured every script milestone carries an explicit entry gate so no script task can
  start partner-less; (c) aligned Definition of Shipped with Elyos "delivered, not merged" by
  requiring an adoption event; (d) confirmed all output licenses are concrete (OFL-1.1 / MIT /
  CC-BY-4.0) for the schema's `outputLicense` field in TASKS.md.

**Outstanding human decisions before execution:** secure a script community partner (Q1/Q2) and
accessibility experts + lived-experience reviewers; decide original-vs-extend for the accessibility
face. Until secured, only M0 and M1's partner-light steps may proceed.

**Status:** Draft v0.1.0 — ready for maintainer and Elyos governance review.
