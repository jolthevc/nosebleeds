# Nosebleeds Editorial Quality Upgrade v4

## Purpose

This package is a targeted post-dry-run upgrade to the Nosebleeds Generation editorial system.

It responds to the first real Shot Clock article, which proved the pipeline and research system worked but exposed a quality ceiling downstream:

- too explanatory
- too chronological and orderly
- too model-shaped in prose and structure
- insufficient human texture
- insufficient entertainment
- strong Research material underused
- post-research framing too conservative
- ending too eager to manufacture meaning
- titles too explanatory
- hero too literal
- visual thinking too late in the process

This is not a pipeline redesign.

It strengthens the existing G1-G12 system.

## Core editorial changes

### 1. The commission is territory, not a prison

G1/G2/G3 now make post-research reframing much more explicit.

G3 considers roughly 3-5 materially different articles before choosing.

Useful prompts include the obvious, narrative, surprising, human, and broadly irresistible versions, but they are not quotas or templates.

The goal is to stop the first clean explanation from winning automatically without manufacturing cosmetic alternatives.

### 2. Good Parts Inventory + Dwell Map

Research now explicitly identifies the best material:

- strangest fact
- absurd detail
- human moment
- scene
- quote
- contradiction
- emotional material
- proof object
- contagious fact

G3 tells the Writer where to dwell and where to compress.

The Writer is instructed to allocate space by reader value rather than abstract importance.

### 3. Explanation is not story

The system now explicitly penalizes:

problem -> background -> solution -> implementation -> effects -> deeper meaning

when that structure is merely the cleanest explanation.

Chronology remains available but is no longer treated as the natural shape of historical material.

### 4. Stronger anti-AI doctrine

The update attacks both surface AI-isms and structural AI behavior.

Hard authored-prose rule:

- no em dashes

Also targeted:

- fake fragments
- unnatural punchy sentences
- one-line paragraph metronome
- rhetorical-question cadence
- rule-of-three repetition
- symmetrical contrasts
- significance-announcing transitions
- immediate explanation after a fact or quote already landed
- manufactured aphorisms
- closing swell
- suspiciously perfect chronology
- over-orderliness

The point is not to swap banned phrases for synonyms.

The point is to make the prose and structure feel more human.

### 5. Competence ceiling

G5, G8, G10, the Rubric, and Production Standard now state directly:

A polished, accurate, coherent, professional article can still fail Nosebleeds.

Review asks:

> Did the Writer find the good part, or merely explain the subject well?

and:

> Would someone who already knows the surface story still be delighted they read this?

The system also asks for three memorable / contagious units.

### 6. Human texture

People should not function merely as evidence delivery.

G4 and reviewers now give more weight to:

- behavior
- complaints
- choices
- relationships
- reactions
- physical detail
- jokes
- quotes allowed to sit without immediate interpretation

### 7. Endings

The system is much more hostile to manufactured transcendence.

It prefers:

- fact
- quote
- image
- action
- object
- irony
- return
- unresolved tension

A final paragraph does not have to tell the reader what the story means.

### 8. Titles, subtitles, and hero as one front door

G12 now treats packaging as an integrated editorial problem.

Core rule:

> Do not title or illustrate the category. Sell the irresistible thing inside it.

Calibration examples distinguish rule-history / "X changed Y" packaging from stranger, more concrete, more clickable front doors.

Writer titles are provisional.

G12 owns final public title/subtitle.

Final artifact assembly should display the G12 title/subtitle once and not stack it above the Writer's provisional title.

### 9. Visuals are layered upstream

The Visual Media OS is aligned to the actual G1-G12 pipeline.

- G1/G2 collect real visual leads and constructed opportunities.
- G3 creates a Visual Opportunity Map.
- G4/G9 can place inline MEDIA INSERT markers.
- G5/G6/G8/G10 can flag bad placement or missed visual opportunity.
- G12 resolves hero and inline media.

MEDIA INSERT syntax:

```text
[MEDIA INSERT
FUNCTION: PROVE | SHOW | EXPLAIN
NEED: specific visual need
WHY HERE: why the reader wants it at this beat
SOURCE_URL: verified URL | N/A - CONSTRUCT_FROM_RESEARCH | NEEDS_HUMAN
]
```

No visual is placed merely to decorate.

Hero principle:

> The hero should embody the conception, not merely depict the nominal subject.

## Files updated

### Governance

- `Governance/nosebleeds-editorial-calibration-examples.md`
- `Governance/nosebleeds-master-scoring-rubric.md`
- `Governance/nosebleeds-narrative-architectures.md`
- `Governance/nosebleeds-production-review-standard.md`
- `Governance/nosebleeds-prompts.md`
- `Governance/nosebleeds-research-standard.md`
- `Governance/nosebleeds-visual-media-os.md`
- `Governance/nosebleeds-voice-bible.md`
- `Governance/nosebleeds-voice-kernel.md`

### Runtime prompts

- `Prompts/G1-research-pass-1.md`
- `Prompts/G2-research-pass-2.md`
- `Prompts/G3-research-compiler.md`
- `Prompts/G4-writer-draft.md`
- `Prompts/G5-reviewer-a-story.md`
- `Prompts/G6-reviewer-b-voice.md`
- `Prompts/G8-eic.md`
- `Prompts/G9-writer-revision.md`
- `Prompts/G10-cold-final-review.md`
- `Prompts/G11-eic-round-two.md`
- `Prompts/G12-packaging.md`

G7 remains unchanged because the Shot Clock dry run suggested truth/evidence review was not the bottleneck.

## Runtime compatibility

No new `{{MARKER}}` dependencies were added to G1-G12.

The existing Generation workflow can continue fetching the same prompt markers.

The explicit structured-output contracts remain backward-compatible at the top level for G5, G6, G8, G10, and G12.

However, after GitHub replacement, verify three orchestration details before the next production article:

1. final document assembly should show only G12's recommended title/subtitle, not the Writer's provisional title/subtitle above or below it
2. editor-facing Final Article documents should preserve `[MEDIA INSERT ...]` markers until the visual package is resolved for publication
3. the workflow should not finalize an article with an authored em dash, unresolved `[NEEDS: ...]` marker, or exact prohibited "It wasn't just X. It was Y." construction. If one survives Round Two, allow only a narrow mechanical compliance repair, not a third editorial rewrite

No new editorial reviewer is required.

## Recommended next test

Run the same Shot Clock commission again from the same Research territory after updating GitHub.

The useful comparison is not whether the new article uses different adjectives.

It should show structural improvement:

- more aggressive post-research framing
- less rule-history feel
- more time on the absurd / human material
- less chronological neatness
- more natural prose
- zero authored em dashes
- stronger contagious moments
- no manufactured ending
- better title/subtitle/hero package
- useful inline media markers
