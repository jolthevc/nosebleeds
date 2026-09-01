# NOSEBLEEDS
## Runtime Prompt Registry v2.2
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
Landscape, verification, discovery, visual leads, 3-5-way conception divergence, and Good Parts inventory.

Provider:
OpenAI with web search.

## G2-research-pass-2.md
Adversarial deepening, missed-gold search, conception challenge, competing explanations, and visual challenge.

Provider:
OpenAI with web search.

## G3-research-compiler.md
Canonical Research document, 3-5-way final conception comparison, Good Parts inventory, Dwell Map, and Visual Opportunity Map.

Provider:
Anthropic or strongest non-browsing editorial model.

## G4-writer-draft.md
First draft with editorial-abundance, anti-over-orderliness, human-texture, and inline MEDIA INSERT guidance.

Provider:
Anthropic or strongest long-form writing model.

## G5-reviewer-a-story.md
Story, depth, cohesion, reader experience, underused Research gold, entertainment, and over-orderliness.

Provider:
Fresh-context editorial model.

## G6-reviewer-b-voice.md
Voice, human prose, AI-signature detection, contextual honesty, emotional payoff, sports magic, and contagion.

Provider:
Fresh-context editorial model.

## G7-reviewer-c-truth.md
Truth and evidence.

Provider:
Prefer a provider different from the Writer.

## G8-eic.md
Round One EIC synthesis with competence ceiling, stronger reframe authority, Research-gold comparison, and entertainment audit.

Provider:
Strongest editorial model.

## G9-writer-revision.md
Targeted revision.

Provider:
Writer model.

## G10-cold-final-review.md
Fresh-context final review with competence ceiling, memory/contagion test, AI-signature audit, and Research-gold comparison.

Provider:
Prefer provider different from Writer.

## G11-eic-round-two.md
Narrow Round Two brief.

Provider:
Strongest editorial model.

## G12-packaging.md
Integrated title/subtitle/hero front door plus MEDIA INSERT resolution and supporting visual package.

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


# EDITORIAL V4 QUALITY SHIFT

The central upgrade is:

> Find the good part, give it room, and do not confuse clean explanation with great storytelling.

Runtime implications:

- the commission defines territory, not the final frame
- G1/G2 diverge across roughly 3-5 materially different conceptions before G3 converges
- G3 explicitly compares multiple possible articles
- G3 identifies Research gold and where the Writer should dwell
- chronology is a tool, not a default
- explanatory completeness does not outrank entertainment
- people should not function merely as evidence delivery
- professional but generic is not a PASS
- structural AI-isms matter as much as banned phrases
- authored em dashes are mandatory fixes
- G4/G9 may place inline MEDIA INSERT markers
- visual thinking begins in Research, not Packaging
- title, subtitle, and hero are one front-door problem
- the hero embodies the conception rather than the nominal subject
- Writer titles are provisional; G12 owns final title/subtitle packaging
