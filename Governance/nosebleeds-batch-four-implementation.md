# NOSEBLEEDS
## Batch Four Implementation v2.4
### Simple orchestration, sophisticated editorial judgment

**Status:** Canonical n8n implementation guidance

---

# 0. CORE IMPLEMENTATION PRINCIPLE

Keep orchestration simple.

Put editorial intelligence in prompts and governance, not in a forest of deterministic gates.

The system has two primary workflows:

1. Ideation
2. Generation

A third UI action, Directed Ideation, may reuse the Ideation workflow with a different prompt.

---

# 1. GOOGLE SHEET

Canonical columns:

- Idea ID
- Working Title
- Core Premise
- Hook
- Why It Works
- Sport
- Source Leads
- Idea Score
- Priority
- Status
- Drive Folder
- Final Article
- Final Score
- Created Date
- Generated Date
- Human Notes

`Idea Score` may remain for compatibility.

The new Ideation workflow does not depend on it and should not manufacture a numeric score.

Optional future metadata:

- Ideation Mode
- Requested Lens
- Requested Subject

These are not required for the current schema.

---

# 2. STATUS VALUES

Use:

- READY
- HOLD
- GENERATING
- READY_FOR_REVIEW
- PUBLISHED
- REJECTED
- ERROR

Meaning:

## READY
Commissioned and eligible for Generation.

## HOLD
Human wants to retain idea but not generate yet.

## GENERATING
Locked by active Generation run.

## READY_FOR_REVIEW
Machine editorial process is complete or has reached the two-round limit.

## PUBLISHED
Published.

## REJECTED
Human rejection or explicit manual retirement.

## ERROR
Technical failure, not editorial hesitation.

---

# 3. PRIORITY

Priority 1 is highest.

Generation selects:

1. highest-priority READY row
2. then oldest Created Date

No numeric idea score is required for ordering.

---

# 4. DEFAULT IDEATION WORKFLOW

Goal:

Create exactly 10 commissioned Nosebleeds ideas.

Flow:

Trigger
↓
Load compact Brand + Ideation context
↓
Load recent slate note
↓
OpenAI I1 with web search
↓
Parse JSON
↓
Deterministic schema validation
↓
Deterministic deduplication
↓
Create IDs / metadata
↓
Write 10 READY rows
↓
Run summary

There is no Anthropic I2 gate.

There is no 8.5 commissioning threshold.

There is no second LLM pass/fail evaluator.

The creative model is responsible for exploring widely before returning only its best 10.

---

# 5. DEFAULT IDEATION CONTEXT

Pass:

- compact brand identity
- current Ideation Standard or concise derivative
- I1 prompt
- recent slate context

Do not pass:

- full Research Standard
- full Production & Review Standard
- full Narrative Architectures
- reviewer prompts
- visual system
- scoring machinery

Creative ideation benefits from taste and freedom.

---

# 6. IDEATION VALIDATION

Mechanical checks only:

- valid JSON
- exactly 10 ideas
- required fields
- non-empty title
- non-empty premise
- non-empty hook
- hook source URL
- hook support text
- valid source list structure
- exact duplicates
- obvious near-duplicates of the same underlying piece

Do not enforce:

- sport quotas
- era quotas
- archetype quotas
- protagonist
- hinge
- story type
- numeric score
- number of business stories
- number of famous subjects

If output formatting fails, retry once with a formatting repair instruction.

If editorial quality is disappointing, fix the prompt rather than layering a second gate.

---

# 7. DIRECTED IDEATION

UI may call Directed Ideation with:

- lens
- subject
- sport
- freeform query
- combinations

Examples:

- Profile
- Tiger Woods + Profile
- NBA + Business
- NFL + Strategy
- Olympics + Politics

Flow is the same as Default Ideation except it uses `I1D-directed-ideation.md`.

Directed Ideation returns conceptions, not generic category results.

If the requested subject is Tiger Woods, ten results should be ten different compelling pieces about Tiger, not ten chronological summaries.

Directed output may be written to the Sheet or shown first for human selection depending on UI design.

---

# 8. AUDIENCE GRAVITY IN IMPLEMENTATION

Do not encode 70/20/10 as hard logic.

It belongs in editorial guidance.

The model should understand:

- broad audience interest matters
- core U.S. sports should naturally dominate the archive
- lower-gravity sports need stories that travel
- sport diversity is not a goal by itself

Do not implement deterministic sport filters.

---

# 9. GENERATION WORKFLOW

Flow:

Select highest-priority READY
↓
Atomic status update to GENERATING
↓
Create / confirm Drive folder
↓
G1
↓
G2
↓
G3
↓
Write canonical Research doc
↓
G4
↓
G5 + G6 + G7
↓
G8
↓
G9
↓
G10
↓
If PASS -> G12
If REVISE -> G11 -> G9 -> G10
↓
G12
↓
Write Final Article
↓
Update Sheet
↓
READY_FOR_REVIEW

Maximum two revision rounds.

---

# 10. GENERATION COMMITMENT

Ideation is where ideas are selected.

Generation is where the system makes the idea great.

Research may REFRAME.

Do not return an idea to Ideation because:

- the best piece changes shape
- the angle becomes more or less commercial
- the piece becomes a profile
- a famous story needs a different reason to retell
- a game remains the main spine
- the article is naturally short or long

Only true evidence, legal, safety, or technical failure should stop Generation.

---

# 11. DRIVE

Canonical path:

`Nosebleeds > Unpublished > [Idea ID] - [Working Title]`

Permanent docs:

1. `01 - Research`
2. `02 - Final Article`

Intermediate reviewer output does not need permanent storage unless useful for debugging.

---

# 12. RESEARCH

G1 and G2 use web search.

G3 compiles the factual universe.

The Research document should include:

- final conception
- final editorial spine
- reason to retell when relevant
- what the story opens up
- tapestry map
- epistemic states
- claims not to make

The Writer does not browse.

---

# 13. LENGTH

Do not implement a target word-count gate.

Do not fail a draft because it is shorter or longer than a nominal center.

The system should evaluate:

- depth
- momentum
- completeness
- padding
- whether the material earned its length

The best piece may be 900, 1,800, 3,000, or 4,000-plus words.

---

# 14. REVIEW

Reviewer A:
story, depth, cohesion, reader experience.

Reviewer B:
voice, prose, contextual honesty, magic, contagion.

Reviewer C:
truth.

EIC:
root-cause synthesis.

Cold Final:
fresh publishability test.

---

# 15. HUMAN NOTES

`Human Notes` is human-owned.

Automation should never overwrite it.

Notes may be supplied to Generation as editorial context where appropriate.

---

# 16. TIMEOUTS

Editorial quality outranks an artificial runtime ceiling.

Do not impose a 10-minute maximum on a full Generation run.

Use sensible technical timeouts per node.

If web research is slow but functioning, allow the workflow to complete.

---

# 17. FRONTEND

The UI may expose:

## Discover
Runs Default Ideation.

## Directed Search
User selects or types:
- lens
- subject
- sport
- query

## Queue
Shows READY / HOLD / GENERATING / READY_FOR_REVIEW.

## Generate
Triggers Generation for selected or highest-priority READY idea.

## Review
Opens Final Article and research metadata.

Avoid exposing implementation complexity as editorial UI.

---

# 18. ERROR POLICY

Use ERROR for technical failure.

Do not use ERROR for:

- editorial reservations
- imperfect scores
- a piece that needs human review after two rounds
- a research reframe

After maximum revision rounds, unresolved editorial reservations go to READY_FOR_REVIEW with warning.

---

# 19. MIGRATION FROM V2.3

Remove or disable:

- Anthropic I2 Ideation call
- 8.5 idea threshold
- pass / fail idea parsing
- score-gated Sheet write
- I2-specific retry path

Add:

- I1 v3 default ideation prompt
- optional I1D directed prompt
- mapping from `why_you_have_to_read_this` to Sheet field `Why It Works`
- no word-count gate
- new Research fields for opening-up and tapestry map

Do not change downstream status semantics.

---

# 20. FINAL IMPLEMENTATION PHILOSOPHY

The workflow should be simple enough to understand at a glance.

The editorial system should be sophisticated enough that the output does not feel simple.

> **Do not solve taste problems with more nodes. Solve them with better taste.**
