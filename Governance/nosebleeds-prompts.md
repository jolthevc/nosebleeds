# NOSEBLEEDS
## Runtime Prompt Registry v2.4
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
Canonical Research document, 3-5-way final conception comparison, Structural Route Test, Good Parts inventory, Evidence Competition, Human Throughlines, Dwell Map, and Visual Opportunity Map.

Provider:
Anthropic or strongest non-browsing editorial model.

## G3.5-feature-editor.md
Feature Editor / Story Architect. Converts canonical Research into a selective Feature Brief and Writer Source Packet. Explicitly separates DWELL / MOVE / COMPRESS / OMIT, rejects process narration and play-by-play by default, and protects the best human material from compression.

Provider:
Strong fresh-context editorial model, no web.

## G4-writer-draft.md
First draft written from the Feature Brief, with Research treated as a fact vault rather than a checklist. Uses positive Prose Calibration in addition to anti-AI rules. Uses explicit TITLE / SUBTITLE / ARTICLE_BODY delimiters.

Provider:
Configurable strongest long-form writing model.

## G4.5-prose-character-editor.md
Single pre-review Prose & Character Editor pass. Improves flow, sentence diversity, character presence, jest, warmth, and naturalness without reframing or inventing facts. Receives deterministic style telemetry.

Provider:
Strong fresh-context writing/editorial model. Prefer provider independence from G4 when practical.

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
Targeted revision with curation, human-continuity, and anti-AI behavior repair. Uses the same explicit ARTICLE_BODY delimiter contract as G4.

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
Integrated title/subtitle/hero front door plus MEDIA INSERT resolution and supporting visual package. Hero should communicate one dominant visual idea; supporting visuals must add distinct value.

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


# EDITORIAL V5 CRAFT SHIFT

The central upgrade is:

> Great Research must be edited, not displayed. Great material should sound interesting without the narrator performing interest around it.

Runtime implications:

- G3 makes chronological and energy-driven structures compete before choosing
- Research assets compete for article space through ANCHOR / SUPPORT / OMIT decisions
- G3 identifies recurring Human Throughlines rather than merely listing people
- G4 and G9 prefer fewer memorable people over one-use-name accumulation
- evidence parades and completeness are explicit failure modes
- micro-punch sentence clusters are treated as structural AI behavior
- narrator hype is penalized when facts are already dramatic
- portable quote-card / LinkedIn-style maxims are treated as synthetic prose risk
- interpretation must add understanding rather than restate evidence
- endings may remain slightly open instead of sealing the argument into a final lesson
- G10 PASS means no material editorial improvement remains available from existing Research
- subtitles favor concrete human intrigue over abstract analytical language when possible
- heroes favor one dominant visual idea over overloaded infographic treatment
- G4/G9 output delimiters support clean title/body separation and paragraph preservation in n8n

# EDITORIAL V6 FEATURE / PROSE SHIFT

The central upgrade is:

> Research finds possibilities. The Feature Editor chooses the article. The Writer writes that assignment. The Prose Editor makes it feel alive without changing what is true.

Runtime implications:

- add G3.5 Feature Editor between G3 and G4
- add a selected Writer Source Packet so Research does not behave like a coverage checklist
- add G4.5 Prose & Character Editor before forensic review
- add deterministic style telemetry before and after G4.5
- curation is explicitly different from compression
- process narration and play-by-play are not default story shapes
- editorial asymmetry is allowed when the best material deserves room
- positive prose calibration teaches flow, connectors, prepositional texture, personality, jest, and tonal range
- positive examples are calibration only; overfitting to wording, jokes, structures, titles, or sentence shapes is prohibited
- reviewers judge both staccato AI cadence and breathless over-connected prose
- the final system should feel like a smart friend telling an extraordinary sports story, not a model processing a Research packet
