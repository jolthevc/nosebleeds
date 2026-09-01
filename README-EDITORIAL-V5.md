# Nosebleeds Editorial v5 Craft Upgrade

## Purpose

v4 fixed the biggest editorial failure: the system began finding a better article after Research instead of merely explaining the nominal subject.

The second Shot Clock run proved the remaining weakness was craft and curation.

The article had a strong conception, strong Research, stronger human material, a better title, and a better hero. It still felt visibly model-shaped because it:

- relied too heavily on chronology
- used too many good Research findings rather than choosing the best ones
- introduced many one-use human voices
- over-interpreted evidence that already landed
- performed drama through short punchy sentences
- produced portable aphoristic lines
- occasionally out-hyped already dramatic material
- sealed the ending too neatly
- used an over-analytical subtitle
- overloaded the hero with secondary proof
- leaked provisional Writer front matter into the final article body

v5 is a surgical craft upgrade. It does not add agents, research passes, scoring gates, or revision rounds.

## Core v5 doctrine

> Great Research must be edited, not displayed.

> Strong facts do not need the narrator to perform excitement around them.

> The best article is not the one that uses the most Research. It is the one that chooses the right Research and gives it the right amount of room.

## Main changes

### 1. Structural Route Test

G3 now explicitly compares:

- the clean chronological / explanatory route
- an energy-driven route based on curiosity, contradiction, people, or consequence
- additional routes when useful

Chronology may win, but it has to create story energy rather than merely make the subject easy to explain.

### 2. Evidence Competition

G3 classifies overlapping Research as:

- ANCHOR
- SUPPORT
- OMIT FROM ARTICLE

The Writer is explicitly permitted to leave excellent verified material unused.

This addresses the v4 tendency to turn deep Research into lists of coaches, players, examples, and statistics.

### 3. Human Throughlines

G3 identifies:

- THROUGHLINE
- GUEST VOICE
- REFERENCE ONLY

No protagonist is required. The goal is continuity and memorability rather than a parade of one-use names.

### 4. Stronger curation in G4/G9

Writer prompts now make material compete for space.

They explicitly prefer:

- fewer vivid people
- fewer redundant quotes
- fewer examples making the same point
- more room for exceptional scenes
- less completeness for its own sake

### 5. Micro-punch detection

v5 names the synthetic rhythm directly.

Example:

> He waited. Nothing happened. That was the problem.

Short sentences remain allowed. Repeated theatrical short-sentence clusters are now treated as AI-shaped prose.

### 6. Narrator restraint

The Writer and reviewers now flag cases where the narrator is trying harder than the material.

A 19-18 NBA score does not need to be called a "crime against entertainment" before the reader experiences it.

### 7. Quote-card / portable-maxim test

Lines that could be removed from the sports story and posted as generic leadership, strategy, business, or life advice are now treated with suspicion.

This targets synthetic lines that convert a specific sports story into polished universal wisdom.

### 8. Interpretation discipline

The Writer now asks whether an interpretive sentence actually changes understanding.

If it merely explains what the preceding fact, quote, image, or scene already demonstrated, it should be cut.

### 9. Harder G10 PASS standard

PASS now means remaining improvements are local.

If a materially better version is still available from the existing Research through better curation, structure, human continuity, prose, or ending, the verdict should be REVISE.

A high numeric score cannot substitute for this judgment.

### 10. Ending restraint

The system now explicitly rejects endings that restate both sides of the article's contradiction and resolve them into a polished final lesson.

A little unresolved air is allowed.

### 11. Subtitle naturalness

G12 now favors concrete, conversational intrigue over abstract analytical language when both are truthful.

Example:

More analytical:

> One rule changed what rational basketball looked like.

More human:

> Fort Wayne won by barely shooting. The strange part was that its strategy made perfect sense.

### 12. Hero simplicity

The hero should usually communicate one dominant idea in under two seconds.

For the Shot Clock story, `19-18 / FINAL` is a stronger hero core than an infographic containing score, attendance, field-goal attempts, and Mikan's scoring share.

Supporting visuals carry secondary proof.

### 13. Visual non-redundancy

Hero and supporting visuals should perform distinct jobs.

Do not repeat the same box score at two levels of detail unless the second treatment adds meaningful understanding.

### 14. Clean Writer output contract

G4 and G9 now output:

```text
TITLE: ...
SUBTITLE: ...
<<<ARTICLE_BODY>>>
...
<<<END_ARTICLE_BODY>>>
```

The article body must not contain the provisional title, subtitle, `# Article`, or duplicate front matter.

This is the only v5 prompt change that requires a small n8n parser update.

## Files modified in v5

Governance:

- `Governance/nosebleeds-voice-kernel.md`
- `Governance/nosebleeds-voice-bible.md`
- `Governance/nosebleeds-master-scoring-rubric.md`
- `Governance/nosebleeds-production-review-standard.md`
- `Governance/nosebleeds-narrative-architectures.md`
- `Governance/nosebleeds-editorial-calibration-examples.md`
- `Governance/nosebleeds-visual-media-os.md`
- `Governance/nosebleeds-prompts.md`

Prompts:

- `Prompts/G3-research-compiler.md`
- `Prompts/G4-writer-draft.md`
- `Prompts/G5-reviewer-a-story.md`
- `Prompts/G6-reviewer-b-voice.md`
- `Prompts/G8-eic.md`
- `Prompts/G9-writer-revision.md`
- `Prompts/G10-cold-final-review.md`
- `Prompts/G11-eic-round-two.md`
- `Prompts/G12-packaging.md`

Unchanged intentionally:

- G1
- G2
- G7
- Research Standard

Research and truth were not the primary failure in the v4 comparison.

## n8n changes required after GitHub upload

No architecture rebuild is needed.

Keep the same G1-G12 pipeline, model routing, parallel G5/G6/G7, two-round ceiling, Research Questions handoff, Drive behavior, and Sheet behavior.

Only refine existing production points:

1. Update G4 parser for the explicit `TITLE`, `SUBTITLE`, `<<<ARTICLE_BODY>>>`, and `<<<END_ARTICLE_BODY>>>` contract.
2. Update both G9 parsers to use the same contract.
3. Pass only parsed `ARTICLE_BODY` into downstream article-review/revision body fields, while retaining provisional title/subtitle separately if needed.
4. Preserve paragraph breaks exactly from `ARTICLE_BODY` when creating the Final Article Google Doc.
5. Final assembly must strip any accidental leading Markdown title/subtitle/`# Article` front matter from the body as a defensive normalization step.
6. Continue using G12 as the sole final public title/subtitle source.
7. Preserve MEDIA INSERT markers exactly as editor-facing blocks.
8. No new AI node, reviewer, model call, or revision round is required.

## What not to change

Do not:

- add more agents
- add a third revision round
- add another research pass
- add a separate style-rewrite node
- add numerical automatic PASS thresholds
- add deterministic rules for structural AI prose beyond the existing hard mechanical compliance scan
- weaken truth review
- force non-chronological structure on every article
- force a protagonist

The goal is better editorial judgment inside the nodes that already exist.

## Success test for v5

On the next same-territory or regression test, look for:

- less visible chronological scaffolding
- fewer one-use names
- fewer redundant quotes/examples
- more memorable recurring people
- less interpretation after evidence
- substantially fewer micro-punch sentence clusters
- calmer narrator around dramatic facts
- no portable generic maxims
- a less sealed ending
- more natural subtitle language
- simpler hero conception
- non-redundant visual package
- clean final document with one public title/subtitle and preserved paragraphing

The target is not merely a higher automated score.

The target is an article that a demanding human editor would stop wanting to materially rewrite.
