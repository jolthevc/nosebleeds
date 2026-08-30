# Nosebleeds Editorial v2

This package contains the full replacement files for the Editorial v2 reset.

## Core change

Nosebleeds is entertainment for people who cannot get enough sports.

It roams the entire world of sports and finds the most interesting, entertaining, surprising, moving, funny, revealing, or irresistible pieces inside it. The publication is unified by taste, not by a narrow subject category, historical period, or mandatory narrative structure.

History is a surface, not the identity. Business is a surface, not the identity. Fame is an asset when the conception earns discovery. Obscurity earns no credit by itself.

The consumer promise remains stories. The internal operating unit is the piece. A piece may be a narrative reconstruction, profile, character study, explanation, argument, mystery, anatomy, business story, cultural story, or another form appropriate to the material.

## Files in this package

### Governance replacements

- `Governance/nosebleeds-brand-bible.md`
- `Governance/nosebleeds-voice-bible.md`
- `Governance/nosebleeds-voice-kernel.md`
- `Governance/nosebleeds-ideation-selection-standard.md`
- `Governance/nosebleeds-research-standard.md`
- `Governance/nosebleeds-narrative-architectures.md`
- `Governance/nosebleeds-master-scoring-rubric.md`
- `Governance/nosebleeds-production-review-standard.md`
- `Governance/nosebleeds-batch-four-implementation.md`
- `Governance/nosebleeds-prompts.md`

### Runtime prompt replacements

- `Prompts/universal-preamble.md`
- `Prompts/I1-candidate-generator.md`
- `Prompts/I2-cold-idea-evaluator.md`
- `Prompts/G1-research-pass-1.md`
- `Prompts/G2-research-pass-2.md`
- `Prompts/G3-research-compiler.md`
- `Prompts/G4-writer-draft.md`
- `Prompts/G5-reviewer-a-story.md`

## Files intentionally not replaced

The following existing runtime prompts should remain as they are unless you separately choose to revise them:

- G6 Voice / Nosebleeds / Magic reviewer
- G7 Truth / Evidence reviewer
- G8 EIC
- G9 Writer Revision
- G10 Cold Final Review
- G11 EIC Round Two
- G12 Packaging

Their roles remain sound. The revised governance documents they receive should broaden their judgment without requiring a new orchestration contract.

Visual identity files are also intentionally unchanged.

## n8n note

The current Ideation workflow should generate exactly 10 I1 candidates, then let I2 commission only the candidates that clear the 8.5 threshold.

There is no Nosebleeds rule requiring a 10 minute execution ceiling. Workflows may run substantially longer when needed. Do not reduce research quality, model quality, or editorial passes to satisfy an artificial 10 minute assumption.

## Manual replacement

Replace the matching repository paths with the files in this ZIP.

Because the I1 and I2 contracts changed earlier, make sure the n8n validators and parsers still match the schemas in the included prompt files.

The later Generation workflow should continue using its existing orchestration. The changes here broaden what G1 through G5 are allowed to discover and build, rather than adding workflow complexity.
