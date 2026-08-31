# Nosebleeds Editorial v3

This package is the full editorial rewrite following the August 31, 2026 Nosebleeds calibration.

It replaces the prior Editorial v2 doctrine wherever the new philosophy materially changes runtime behavior.

## Central editorial correction

Nosebleeds is not optimizing for the most obscure, surprising, or untold sports story.

It is optimizing for the most compelling sports pieces and the best reading experience.

The new center is:

> **Start with something worth caring about. Find everything interesting inside it. Choose the version that produces the best reading experience.**

Key consequences:

- appeal before novelty
- famous subjects are assets
- lower-gravity sports face context tax
- core U.S. sports should naturally dominate the archive without hard quotas
- pure sports stories are valid
- recap is insufficient
- strong pieces should open beyond the surface without forcing an academic thesis
- depth should increase enjoyment
- multi-dimensional research is encouraged
- finished pieces must remain cohesive, like a tapestry
- profiles are a callable lens, not biographies
- admiration is allowed, hero worship is not
- article length follows the material
- Anthropic I2 is removed from Ideation
- Directed Ideation is added for UI category and subject search

## Files in this package

### Governance
- nosebleeds-brand-bible.md
- nosebleeds-ideation-selection-standard.md
- nosebleeds-research-standard.md
- nosebleeds-narrative-architectures.md
- nosebleeds-master-scoring-rubric.md
- nosebleeds-production-review-standard.md
- nosebleeds-voice-bible.md
- nosebleeds-voice-kernel.md
- nosebleeds-prompts.md
- nosebleeds-batch-four-implementation.md

### Prompts
- universal-preamble.md
- I1-candidate-generator.md
- I1D-directed-ideation.md
- I2-cold-idea-evaluator.md (deprecated stub)
- G1-research-pass-1.md
- G2-research-pass-2.md
- G3-research-compiler.md
- G4-writer-draft.md
- G5-reviewer-a-story.md
- G6-reviewer-b-voice.md
- G7-reviewer-c-truth.md
- G8-eic.md
- G9-writer-revision.md
- G10-cold-final-review.md
- G11-eic-round-two.md
- G12-packaging.md

## Not changed

The visual identity and visual media operating system are not included because this editorial reset does not change the house visual system.

## Migration

1. Replace matching files in the repository with the files in this package.
2. Add `Prompts/I1D-directed-ideation.md`.
3. Remove I2 from the n8n Ideation runtime. The included I2 file is a deprecation marker only.
4. Update any n8n field mapping from `why_this_could_work` or similar to `why_you_have_to_read_this`, while continuing to write into the Sheet column `Why It Works` if desired.
5. Do not require Idea Score for READY.
6. Do not enforce a draft word-count target.
7. Update Reviewer A and Cold Review score-field parsing if the implementation expects the old rubric names.
