# open-accessible-fonts — TASKS

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) ·
> Lane: donated · Risk tier: medium
>
> Itemized, schema-mapped backlog for the M0–M4 roadmap in `PLAN.md`. Sizing is honest; type
> design is slow. `verifiedNeed=false` wherever no partner/requestor/community is secured — which,
> today, is **everywhere it applies** (all script tasks; any benefit-claim task).

---

## How these tasks map to Elyos

Each task below becomes an Elyos **Task JSON** validated against
`packages/schema/src/schemas.ts`. Field mapping:

- **id** — stable slug `fonts-<area>-NNN`.
- **title / project** — human title; `project` = `"open-accessible-fonts"`.
- **type** — `code` (pipeline/build/shaping), `research` (gap/evidence analysis),
  `writing` (specimens, guides, governance docs), `data` (coverage datasets),
  `design-spec` (glyph design briefs + drawn sources — closest schema type for type-design craft),
  `maintenance` (upstreaming, playbooks).
- **lane** — `donated` for all (no `funded` tasks; if any were funded, `fundedBudgetUsd` is required
  by the schema's conditional).
- **priority** — high / medium / low.
- **domain** — string array, e.g. `["typography","accessibility","i18n","open-source"]`.
- **riskTier** — `low` | `medium` | `high`. Script & accessibility-claim work = `medium`; any
  efficacy claim escalates to `high` (credentialed sign-off) — we instead keep claims non-medical.
- **urgent** — boolean (all `false`; this is craft work, not incident response).
- **deliverable** — schema enum `pr | dataset | document | translation`. Font source/binaries ship
  via `pr`; specimens/guides/briefs via `document`; coverage data via `dataset`. (No `translation`
  deliverables here.)
- **tokenEstimate** — `small | medium | large`.
- **status** — all `open` at planning time.
- **context / objective / acceptanceCriteria[] / output** — task narrative + checkable criteria +
  the concrete artifact.
- **resources[]** — tooling/specs/standards links.
- **requestor** — the securing community/org, or omitted/`"TO BE SECURED"`.
- **verifiedNeed** — `false` until a partner/requestor confirms the need.
- **outputLicense** — `OFL-1.1` (fonts), `MIT` (code/tooling), `CC-BY-4.0` (docs/datasets/specimens).

---

## Milestone M0 — Foundation & cold-start (no partner required)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| fonts-infra-001 | Repo scaffold + reproducible build pipeline (UFO→fontmake→OTF/TTF/variable/WOFF2) | code | M | low | pr | — | Maintainer |
| fonts-qa-002 | CI QA gate: FontBakery + HarfBuzz shaping diff + coverage report | code | M | low | pr | fonts-infra-001 | Maintainer |
| fonts-legal-003 | Licensing & provenance framework (OFL.txt / FONTLOG.txt / provenance.json + clean-room policy) | writing | S | medium | document | — | Maintainer |
| fonts-research-004 | Under-served-script gap analysis + prioritization shortlist | research | M | medium | document | — | Maintainer + (community advisor TBD) |
| fonts-research-005 | Accessibility/legibility evidence brief (low-vision + honest on contested dyslexia-font claims) | research | M | medium | document | — | A11y specialist (TO BE SECURED) |
| fonts-gov-006 | Governance + community co-design protocol + reviewer roster | writing | S | low | document | fonts-legal-003 | Maintainer + governance |

### Acceptance criteria (key M0 tasks)

**fonts-infra-001 — build pipeline**
- A minimal placeholder UFO + designspace builds to static OTF + TTF, a variable TTF, and WOFF2 via
  a single documented command.
- Build tooling pinned in a lockfile; a clean-environment rebuild produces byte-stable artifacts
  (reproducible-build check passes).
- Repo follows Google Fonts upstream layout (`sources/`, `fonts/`, `documentation/`, `OFL.txt`,
  `FONTLOG.txt`, `METADATA`).
- README documents prerequisites and the build command; no proprietary tools required.

**fonts-qa-002 — CI QA gate**
- On every PR, CI runs FontBakery (Universal + GF profiles) and fails the build on any `FAIL`;
  `WARN`s are surfaced for triage.
- HarfBuzz shaping diff runs against a test string set and reports diffs as artifacts.
- A Unicode + language-coverage (gflanguages/hyperglot) report is generated and attached.
- No secrets/tokens written to logs or artifacts.

**fonts-legal-003 — licensing & provenance framework**
- `OFL.txt` and a populated `FONTLOG.txt` template included; Reserved Font Name policy documented.
- `provenance.json` schema defined with per-glyph-source granularity (origin, license, designer,
  references, reviewer, community sign-off).
- Clean-room policy + prohibited-inputs allow/deny list documented; proprietary tracing explicitly
  banned.
- Output-license matrix documented: OFL-1.1 (fonts) / MIT (code) / CC-BY-4.0 (docs/data).

**fonts-research-005 — accessibility evidence brief**
- Summarizes published legibility evidence for low vision and **honestly reports the contested,
  mixed evidence for dyslexia-specific fonts** (no over-claiming).
- Defines the standard **non-medical framing** text ("designed using legibility research; not a
  treatment/diagnosis/medical device") to be reused in all artifacts.
- Lists the accessibility-critical differentiation set (`Il1`, `O0`, `bdpq`, `rn/m`, etc.) to drive
  the M1 design brief.

**M0 Definition of Done:** pipeline builds reproducibly with QA in CI; licensing/provenance &
governance frameworks merged; script-prioritization shortlist and accessibility evidence brief
published. No fonts shipped yet; foundation proven.

---

## Milestone M1 — Accessibility-first Latin family (pilot deliverable)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| fonts-design-101 | Design brief + glyph set spec for low-vision/dyslexia-informed Latin | design-spec | M | medium | document | fonts-research-005, fonts-gov-006 | Maintainer + A11y specialist (TBS) |
| fonts-design-102 | Draw core Latin glyph set (UFO source, GF Latin Core + differentiation set) | design-spec | L | medium | pr | fonts-design-101, fonts-infra-001 | Type design reviewer |
| fonts-test-103 | Legibility proofing + accessibility-expert + lived-experience review | research | M | medium | document | fonts-design-102 | A11y specialist + ≥2 lived-experience reviewers (TBS) |
| fonts-ship-104 | Release v1.0 family (static + variable + WOFF2 + specimen) under OFL | code | M | medium | pr | fonts-test-103, fonts-qa-002 | Maintainer + Steward |

### Acceptance criteria (key M1 tasks)

**fonts-design-102 — draw core Latin glyph set**
- UFO source covers GF Latin Core plus the accessibility differentiation set with distinct,
  non-confusable forms for `I/l/1`, `O/0`, `b/d/p/q`, `r n / m`.
- Builds clean through the M0 pipeline; FontBakery green (no FAIL); spacing/kerning reviewed.
- `provenance.json` records every glyph as original clean-room (or OFL/PD-derived with attribution);
  no proprietary derivation.
- Variable weight axis builds; static instances export correctly.

**fonts-test-103 — legibility & lived-experience review**
- Accessibility/vision specialist sign-off recorded; **non-medical framing verified** present in
  README/specimen/usage guide.
- ≥2 lived-experience reviewers (low-vision and/or dyslexic readers) provide consented, aggregate
  feedback; no disability status tied to an identifiable person.
- Any feedback-driven glyph changes logged; if validation is null/mixed, result reported honestly and
  the family reframed as "high-legibility" per the PLAN honesty clause.

**fonts-ship-104 — release v1.0**
- Tagged release with static + variable + WOFF2 + specimen PDF + complete OFL.txt/FONTLOG.txt/
  provenance.json.
- All QA gates green; reproducible build verified.
- **≥1 adoption event**: a Google Fonts submission opened OR the font deployed in a real delivered
  document (e.g. a downstream Elyos OER artifact).

**M1 Definition of Done:** one accessibility-first OFL family shipped with expert + lived-experience
sign-off, non-medical framing verified, and ≥1 real adoption event. Pipeline proven end-to-end.

---

## Milestone M2 — First under-served script (community co-designed) — **BLOCKED on partner**

> **Entry gate:** a named script authority / language community partner must be secured and the
> orthography + design brief co-signed before any drawing starts. Until then every task here has
> `verifiedNeed=false` and remains `open` but unstarted.

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| fonts-script-201 | Secure script community partner + co-sign orthography & design brief | research | M | medium | document | fonts-research-004, fonts-gov-006 | Maintainer + community (TBS) |
| fonts-script-202 | Draw glyphs + author OpenType GSUB/GPOS shaping for the script | design-spec | L | medium | pr | fonts-script-201, fonts-infra-001 | Type design reviewer + community |
| fonts-script-203 | Native-reader shaping & correctness review | research | M | medium | document | fonts-script-202 | Native readers / script authority (TBS) |
| fonts-script-204 | Release script font + specimen + language-coverage report under OFL | code | M | medium | pr | fonts-script-203, fonts-qa-002 | Maintainer + Steward |

### Acceptance criteria (key M2 tasks)

**fonts-script-201 — secure partner + co-signed brief**
- A named community/script-authority partner confirms the need (flips `verifiedNeed` to `true` once
  real) and is credited as co-designer.
- Orthography spec, target language(s), glyph repertoire, and shaping requirements co-signed.
- Community veto + change-request process acknowledged; naming/Reserved Font Name agreed.

**fonts-script-202 — glyphs + shaping**
- Glyph set covers the agreed repertoire; OpenType GSUB/GPOS implements required contextual forms,
  marks, and ligatures.
- HarfBuzz shaping diff is clean against community-provided test strings; FontBakery green.
- Provenance recorded; no proprietary or invented forms.

**fonts-script-204 — release**
- Coverage report shows the primary language fully covered (gflanguages/hyperglot).
- Native-reader correctness review passed (100%); FONTLOG credits the community.
- **≥1 adoption event**: community use OR Noto/Google Fonts upstreaming initiated.

**M2 Definition of Done:** one under-served script has a free, correct, community-validated OFL font
with working shaping, native-reader sign-off, and ≥1 adoption event. *Does not start until the entry
gate is met.*

---

## Milestone M3 — Scale & delivery

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| fonts-var-301 | Consolidate variable axes (weight; optical size where justified) across families | code | M | low | pr | fonts-ship-104 | Type design reviewer |
| fonts-web-302 | Web delivery kit (WOFF2 + @font-face) + accessibility usage guide | writing | S | low | document | fonts-ship-104 | Maintainer + A11y specialist (TBS) |
| fonts-data-303 | Language-support matrix dataset (Hyperglot/gflanguages) for shipped fonts | data | S | low | dataset | fonts-ship-104 | Maintainer |

### Acceptance criteria (key M3 tasks)

**fonts-web-302 — web kit + usage guide**
- WOFF2 + ready-to-use `@font-face` snippets published.
- Accessibility usage guide gives size/contrast/line-length **guidance referencing WCAG** (framed as
  guidance, not a compliance certification) and repeats the non-medical framing.

**fonts-data-303 — coverage dataset**
- Machine-readable language-support matrix per shipped family, CC-BY-4.0, with methodology noted.

**M3 Definition of Done:** variable coverage consolidated and QA-green; web delivery kit + usage
guide published; coverage dataset published; ≥3 total adoption events across the portfolio.

---

## Milestone M4 — Sustainability & handoff

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| fonts-maint-401 | Upstream onboarding (Google Fonts / Noto) or named community-maintainer handoff | maintenance | M | low | pr | fonts-ship-104, fonts-script-204 | Maintainer + Steward |
| fonts-maint-402 | Maintenance playbook + outcome-tracking ledger (incl. null results) | writing | S | low | document | fonts-maint-401 | Maintainer |

### Acceptance criteria (key M4 tasks)

**fonts-maint-401 — durable home**
- ≥1 family accepted into a durable upstream (GF/Noto) OR a named community maintainer committed in
  writing.
- Repo meets upstream specs (METADATA, license, FONTLOG, build).

**fonts-maint-402 — playbook + ledger**
- Maintenance playbook covers issue triage, re-release with updated tooling, Unicode/orthography
  updates, and community change-requests.
- Public outcome-tracking ledger records adoption events and any legibility findings, **including
  null/mixed results**.

**M4 Definition of Done:** at least one family has a durable upstream/maintainer; maintenance
playbook and outcome ledger live; the fonts can outlive the project.

---

## Backlog / future (sized, unscheduled)

| ID | Title | Type | Size | Risk | Deliverable | Notes |
|---|---|---|---|---|---|---|
| fonts-script-205 | Second under-served script | design-spec | L | medium | pr | Needs a second secured community |
| fonts-italic-306 | Italic / true-cursive styles for shipped families | design-spec | L | medium | pr | After uprights stable |
| fonts-hint-307 | Manual TrueType hinting for legacy low-DPI Windows | code | L | low | pr | Only if a partner requires |
| fonts-multiscript-308 | Multi-script harmonization (Latin + script in one family) | design-spec | L | medium | pr | Advanced; needs both communities |
| fonts-a11y-309 | Accessibility face for a non-Latin script | design-spec | L | medium | pr | Combines both program goals |
| fonts-eval-310 | Partner-run legibility validation study (consented, aggregate) | research | M | medium | document | Only if a partner offers; PII constraints apply |

---

## Example task JSON

Complete, schema-valid Task JSON for the first M0 task (`fonts-infra-001`). `verifiedNeed=false`
(no partner/requestor secured); `outputLicense=MIT` (tooling/pipeline code; fonts themselves are
OFL-1.1).

```json
{
  "id": "fonts-infra-001",
  "title": "Repo scaffold + reproducible build pipeline (UFO -> fontmake -> OTF/TTF/variable/WOFF2)",
  "project": "open-accessible-fonts",
  "type": "code",
  "lane": "donated",
  "priority": "high",
  "domain": ["typography", "open-source", "accessibility", "i18n", "tooling"],
  "riskTier": "low",
  "urgent": false,
  "deliverable": "pr",
  "tokenEstimate": "medium",
  "status": "open",
  "context": "open-accessible-fonts produces OFL-licensed fonts for under-served scripts and low-vision/dyslexia accessibility. Before any glyph work, the project needs a reproducible, open-tool build pipeline and a Google-Fonts-compatible repo layout so every later family is cheaper to build, QA, and upstream. No partner or requesting community is secured yet; this foundation task is partner-independent.",
  "objective": "Stand up a version-controlled font repo whose minimal placeholder UFO + designspace builds reproducibly to static OTF/TTF, a variable TTF, and WOFF2 via a single documented command, using only open-source tooling pinned by a lockfile.",
  "acceptanceCriteria": [
    "A minimal UFO + designspace builds to static OTF, static TTF, variable TTF, and WOFF2 via one documented command (fontmake + gftools + fontTools).",
    "All build tooling is pinned in a lockfile; a clean-environment rebuild yields byte-stable artifacts (reproducible-build check passes).",
    "Repo follows Google Fonts upstream layout: sources/, fonts/, documentation/, OFL.txt, FONTLOG.txt, METADATA.",
    "README documents prerequisites and the build command; no proprietary tools are required to build.",
    "No secrets, tokens, or API keys are written to logs, build artifacts, or committed files."
  ],
  "resources": [
    "https://github.com/googlefonts/fontmake",
    "https://github.com/googlefonts/gftools",
    "https://github.com/fonttools/fonttools",
    "https://unifiedfontobject.org/",
    "PLAN.md (sections 6-7: architecture, licensing & provenance)"
  ],
  "output": "A pull request adding the font repo scaffold and reproducible build pipeline, with a placeholder UFO that builds to OTF/TTF/variable/WOFF2 and a README documenting the open-tool build.",
  "requestor": "TO BE SECURED",
  "verifiedNeed": false,
  "outputLicense": "MIT"
}
```

---

## Notes on honesty & gating (read before execution)

- **All script tasks carry `verifiedNeed=false`** until a real community partner is secured (M2
  entry gate). Do not start drawing a script without it.
- **Accessibility tasks must keep claims non-medical**; any efficacy/clinical claim escalates the
  task to `riskTier: high` and requires credentialed expert sign-off before merge — we instead keep
  the framing to "legibility design intent."
- **Every font release** requires complete OFL.txt/FONTLOG.txt/provenance.json and an adoption event
  to count as *delivered* (not merely merged), per the Elyos quality bar.

---

## Generated task index

> Auto-generated by Elyos task decomposition · 2026-06-29 · All 25 tasks validated against
> `packages/schema` (draft-07, additionalProperties:false). Seed task `fonts-infra-001` was
> pre-existing; 24 new task JSON files were generated. No fan-out dimensions (all tasks are
> explicitly enumerated in the TASKS.md backlog; no combinatorial expansion applied).

| File | Title | Type | Priority | Deliverable | Token | verifiedNeed | outputLicense |
|---|---|---|---|---|---|---|---|
| fonts-infra-001.json | Repo scaffold + reproducible build pipeline | code | high | pr | medium | false | MIT |
| fonts-qa-002.json | CI QA gate: FontBakery + HarfBuzz + coverage | code | high | pr | medium | false | MIT |
| fonts-legal-003.json | Licensing & provenance framework | writing | high | document | small | false | CC-BY-4.0 |
| fonts-research-004.json | Under-served-script gap analysis + prioritization | research | high | document | medium | false | CC-BY-4.0 |
| fonts-research-005.json | Accessibility/legibility evidence brief | research | high | document | medium | false | CC-BY-4.0 |
| fonts-gov-006.json | Governance + community co-design protocol | writing | high | document | small | false | CC-BY-4.0 |
| fonts-design-101.json | Design brief + glyph set spec (Latin accessibility) | design-spec | high | document | medium | false | CC-BY-4.0 |
| fonts-design-102.json | Draw core Latin glyph set (UFO + differentiation set) | design-spec | high | pr | large | false | OFL-1.1 |
| fonts-test-103.json | Legibility proofing + accessibility + lived-experience review | research | high | document | medium | false | CC-BY-4.0 |
| fonts-ship-104.json | Release v1.0 Latin accessibility family under OFL | code | high | pr | medium | false | OFL-1.1 |
| fonts-script-201.json | Secure script community partner + co-sign brief | research | medium | document | medium | false | CC-BY-4.0 |
| fonts-script-202.json | Draw script glyphs + OpenType GSUB/GPOS shaping | design-spec | medium | pr | large | false | OFL-1.1 |
| fonts-script-203.json | Native-reader shaping & correctness review | research | medium | document | medium | false | CC-BY-4.0 |
| fonts-script-204.json | Release script font + specimen + coverage report | code | medium | pr | medium | false | OFL-1.1 |
| fonts-var-301.json | Consolidate variable axes across shipped families | code | medium | pr | medium | false | OFL-1.1 |
| fonts-web-302.json | Web delivery kit (WOFF2 + @font-face) + usage guide | writing | medium | document | small | false | CC-BY-4.0 |
| fonts-data-303.json | Language-support matrix dataset (Hyperglot/gflanguages) | data | medium | dataset | small | false | CC-BY-4.0 |
| fonts-maint-401.json | Upstream onboarding or community-maintainer handoff | maintenance | low | pr | medium | false | OFL-1.1 |
| fonts-maint-402.json | Maintenance playbook + outcome-tracking ledger | writing | low | document | small | false | CC-BY-4.0 |
| fonts-script-205.json | Second under-served script (full M2 cycle) | design-spec | low | pr | large | false | OFL-1.1 |
| fonts-italic-306.json | Italic / true-cursive styles for shipped families | design-spec | low | pr | large | false | OFL-1.1 |
| fonts-hint-307.json | Manual TrueType hinting for legacy low-DPI Windows | code | low | pr | large | false | MIT |
| fonts-multiscript-308.json | Multi-script harmonization (Latin + script) | design-spec | low | pr | large | false | OFL-1.1 |
| fonts-a11y-309.json | Accessibility face for a non-Latin community script | design-spec | low | pr | large | false | OFL-1.1 |
| fonts-eval-310.json | Partner-run legibility validation study | research | low | document | medium | false | CC-BY-4.0 |
