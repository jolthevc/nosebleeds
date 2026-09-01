# Nosebleeds Editorial v6: Feature + Prose Upgrade

This package is a targeted architecture and craft upgrade built after the v5 Shot Clock regression.

## Diagnosis

The system now researches well and reviews intelligently, but the Writer still tends to turn strong Research into chronological explanation. v5 also showed a second failure: curation was interpreted as compression, so strong human and scene material disappeared while explanatory scaffolding survived.

The new architecture separates three jobs:

1. **G3 Research Compiler:** establishes truth, possibilities, and Research gold.
2. **G3.5 Feature Editor / Story Architect:** decides what article should actually be written and what should be omitted.
3. **G4 Writer + G4.5 Prose & Character Editor:** write the assignment, then improve life, flow, character, jest, and tonal naturalness before forensic review.

## New files

- `Governance/nosebleeds-feature-editor-standard.md`
- `Governance/nosebleeds-story-calibration.md`
- `Governance/nosebleeds-prose-calibration.md`
- `Prompts/G3.5-feature-editor.md`
- `Prompts/G4.5-prose-character-editor.md`

## Core v6 principles

- Curation is not compression.
- The full Research document is a fact vault, not a checklist.
- Process narration is not automatically story.
- A sports article is not automatically play-by-play.
- Editorial space may be asymmetric.
- Positive prose calibration matters as much as anti-AI rules.
- Natural connectors, occasional prepositional openings, character, and jest are welcome when they fit.
- Avoid both staccato AI cadence and breathless run-on prose.
- Calibration examples demonstrate moves and tone. They must never be copied structurally or linguistically.

## New runtime sequence

`G1 -> G2 -> G3 -> G3.5 -> G4 -> Style Telemetry 1 -> G4.5 -> Style Telemetry 2 -> parallel G5/G6/G7 -> G8 -> G9 R1 -> Style Telemetry R1 -> G10 -> optional G11/G9 R2 -> Style Telemetry R2 -> G10 -> G12`

No additional revision round is added.

G4.5 is part of first-draft creation, not a hidden third revision.

## Model experimentation

The package does not hard-code a new G4 provider. G4 should remain configurable so the same Feature Brief can be used for a controlled Writer bakeoff across strong models.

G4.5 should preferably use a provider different from G4 when practical, because its value comes partly from a fresh prose ear.

## n8n changes required

- fetch the three new governance files and two new prompt files
- insert G3.5 between G3 and G4
- pass `FEATURE_BRIEF` to G4, G5, G6, G8, G9, G10, G11
- pass `PROSE_CALIBRATION` to G4, G4.5, G6, G9, G10, G11
- add deterministic Style Telemetry after G4 and after G4.5
- insert G4.5 before G5/G6/G7
- pass post-G4.5 telemetry to G6/G8/G9
- recompute telemetry after each G9 revision and pass the current telemetry to G10/G11 and the next G9 if Round Two runs
- preserve existing truth, Drive, Sheet, revision, packaging, and concurrency behavior

See the accompanying n8n implementation prompt supplied with the ZIP for exact orchestration.
