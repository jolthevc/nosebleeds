# NOSEBLEEDS
## Runtime Prompt Registry v2.1
### Source-of-truth map for live prompt files

**Status:** Canonical registry  
**Important:** The individual files in `/Prompts` are the runtime source of truth. This document maps roles and dependencies. It should not duplicate full prompt text.

---

# IDEATION

## I1-candidate-generator.md
Default Discovery and commissioning.

Provider:
OpenAI with web search enabled.

Returns:
Exactly 10 commissioned ideas.

Key doctrine:
- appeal before novelty
- audience gravity
- famous is welcome
- no second-model taste gate
- no numeric idea score
- find the interesting version
- default discovery does not fill categories

## I1D-directed-ideation.md
Directed Ideation for UI requests.

Provider:
OpenAI with web search enabled.

Supports:
- profile
- business / commercial
- strategy / tactics
- game / moment
- season / era
- team / organization
- league / institution
- culture / fandom
- media
- money / contracts
- rules / innovation
- myth / memory
- rivalry
- politics / society
- place / stadium
- object / artifact
- subject-specific or sport-specific combinations

Returns:
Exactly 10 conceptions unless UI overrides the count.

## I2-cold-idea-evaluator.md
Deprecated.

Do not call in the live Ideation workflow.

The previous Anthropic 8.5 commissioning gate is removed.

---

# GENERATION

## G1-research-pass-1.md
Landscape, verification, discovery, and opening-up research.

Provider:
OpenAI with web search.

## G2-research-pass-2.md
Context, adversary, competing explanations, and deeper-layer testing.

Provider:
OpenAI with web search.

## G3-research-compiler.md
Canonical Research document and final conception.

Provider:
Anthropic or strongest non-browsing editorial model.

## G4-writer-draft.md
First draft.

Provider:
Anthropic or strongest long-form writing model.

## G5-reviewer-a-story.md
Story, depth, cohesion, reader experience.

Provider:
Fresh-context editorial model.

## G6-reviewer-b-voice.md
Voice, prose, contextual honesty, emotional payoff, sports magic, contagion.

Provider:
Fresh-context editorial model.

## G7-reviewer-c-truth.md
Truth and evidence.

Provider:
Prefer a provider different from the Writer.

## G8-eic.md
Round One EIC synthesis.

Provider:
Strongest editorial model.

## G9-writer-revision.md
Targeted revision.

Provider:
Writer model.

## G10-cold-final-review.md
Fresh-context final review.

Provider:
Prefer provider different from Writer.

## G11-eic-round-two.md
Narrow Round Two brief.

Provider:
Strongest editorial model.

## G12-packaging.md
Titles, subtitles, hero and supporting visual package.

Provider:
Strong editorial model.

---

# UNIVERSAL

## universal-preamble.md
Compact runtime identity and truth rules.

Use only where useful.

Do not overload creative Ideation with full downstream production doctrine.

---

# RUNTIME CONTEXT PRINCIPLE

Default Ideation needs:

- compact brand identity
- Ideation Standard or compact derivative
- I1
- relevant recent slate context

Directed Ideation needs:

- compact brand identity
- Ideation Standard or compact derivative
- I1D
- requested lens / subject / sport / query
- recent slate context where useful

Research and Generation may load deeper governance.

Creative discovery should not carry the full production operating system.

---

# EDITORIAL V3 SHIFT

The central change is:

> Start with something worth caring about. Find everything interesting inside it. Choose the version that produces the best reading experience.

Runtime implications:

- audience appeal outranks novelty
- famous subjects are assets
- lower-gravity sports face context tax
- pure sports stories remain valid
- recap is insufficient
- every strong piece should open beyond the surface where useful
- no smoking gun is required
- multi-dimensional research is encouraged
- finished articles must remain cohesive
- profiles are lenses, not biographies
- hero worship is prohibited
- article length follows the material
