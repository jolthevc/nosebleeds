# NOSEBLEEDS
## Batch Four Implementation v2.3
### Simple orchestration, sophisticated editorial intelligence

**Status:** Canonical n8n implementation specification.  
**Supersedes:** Batch Four Implementation v2.2 where conflicts exist.

---

# 0. CORE IMPLEMENTATION PRINCIPLE

> **KEEP THE EDITORIAL INTELLIGENCE SOPHISTICATED. KEEP THE N8N IMPLEMENTATION SIMPLE.**

Detailed markdowns teach models how to think.

n8n primarily:

- fetches context
- calls models
- validates outputs
- moves strong output to the next node
- writes human-readable state

Do not build an orchestration bureaucracy around the editorial system.

---

# 1. TWO WORKFLOWS

Only two editorial workflows are required:

1. **Ideation Workflow**
2. **Generation Workflow**

A lightweight GitHub Pages console may sit on top of the Google Sheet.

No separate editorial-learning workflow.

No automated learnings file.

No hidden memory loop.

---

# 2. GOOGLE SHEET

Canonical human-readable columns:

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

`Story Type` and `Human Carrier` are not required runtime fields.

If old physical columns remain in the Sheet, leave them blank.

Do not add Hook Source URL or Hook Source Support as required human-facing columns. Those are transient I1 to I2 evidence fields.

---

# 3. STATUS VALUES

Allowed statuses:

- READY
- HOLD
- GENERATING
- READY_FOR_REVIEW
- PUBLISHED
- REJECTED
- ERROR

Meaning:

**READY:** commissioned and eligible for Generation.  
**HOLD:** do not generate.  
**GENERATING:** active Generation run.  
**READY_FOR_REVIEW:** machine finished; human review next.  
**PUBLISHED:** human marked published.  
**REJECTED:** human rejected before Generation.  
**ERROR:** operational failure, not ordinary editorial reservation.

---

# 4. PRIORITY

Priority 1 is highest.

Ideation default: 3.

Generate Next Story selects:

1. highest-priority READY row
2. earliest Created Date among ties

If any row is already `GENERATING`, Generate Next Story refuses to start another run.

---

# 5. IDEATION WORKFLOW

## Goal

Return exactly 10 strong candidate conceptions from I1.

Let I2 commission only the ideas that clear the editorial bar.

## Runtime context

Fetch fresh from GitHub:

- Brand Bible
- Ideation and Commissioning Standard
- I1 prompt
- I2 prompt
- universal preamble if used by the implementation

Build a Slate Note from:

- last 10 Working Titles
- last 10 Core Premises
- recent Sport counts
- all existing Working Titles + Core Premises for deduplication

Do not build:

- archetype quotas
- category quotas
- Story Type counts
- era quotas
- human-carrier quotas

---

# 6. I1 CANDIDATE GENERATOR

Provider: OpenAI with web search.

I1 should explore broadly and return exactly 10 candidates.

I1 contract:

```json
{
  "candidates": [
    {
      "working_title": "",
      "core_premise": "",
      "hook": "",
      "hook_source_url": "",
      "hook_source_support": "",
      "why_this_could_work": "",
      "sport": "",
      "source_leads": []
    }
  ]
}
```

Required per candidate:

- `working_title`
- `core_premise`
- `hook`
- `hook_source_url`
- `hook_source_support`
- `why_this_could_work`
- `sport`

`source_leads` must be an array.

An empty `source_leads` array does not kill the candidate if the primary hook URL is valid.

---

# 7. I1 VALIDATION

Validation asks:

> **Did the scout return an intelligible conception and a real sourced hook?**

It does not ask:

> Has the article already been researched and architected?

Do not require:

- narrative_hinge
- human_carrier
- story_type
- archetype
- hinge_year
- living_subject

Malformed candidate count should normally be zero or very low.

---

# 8. I2 COLD COMMISSIONING EDITOR

Provider: Anthropic, no search.

I2 receives:

- Ideation Standard
- Slate Note
- validated candidates
- `IDEA_SCORE_FLOOR`

Current floor:

**8.5**

I2 output:

```json
{
  "passed": [
    {
      "working_title": "",
      "core_premise": "",
      "hook": "",
      "hook_source_url": "",
      "hook_source_support": "",
      "why_it_works": "",
      "sport": "",
      "source_leads": [],
      "idea_score": 0
    }
  ],
  "rejected": [
    {
      "working_title": "",
      "reason": ""
    }
  ]
}
```

I2 does not emit a 14-dimension scorecard.

One holistic idea score is enough.

---

# 9. IDEATION WRITE

For each passing candidate:

- create Idea ID
- map fields into the Sheet
- set Priority = 3 unless configured otherwise
- set Status = READY
- set Created Date
- leave Generation fields blank

Before write:

- dedup primarily against Working Title
- dedup semantically against Core Premise

Do not pass weaker ideas merely to hit a target row count.

Zero writes is valid.

Zero writes because every candidate was malformed is not healthy.

---

# 10. HEALTHY IDEATION RUN REPORT

After each run, report:

- raw I1 candidate count
- malformed candidate count
- I2 received count
- I2 passed count
- dropped below 8.5
- dedup drops
- rows written

For calibration runs, also surface:

- one full raw I1 candidate
- one full I2 passed object or rejection object
- obvious thematic clustering
- obvious era clustering

A healthy run may generate 10 and commission 2 to 5.

The pass count is not a quota.

---

# 11. GENERATION WORKFLOW

When Generate Next Story is triggered:

1. refuse if any row is `GENERATING`
2. select next READY row by Priority then Created Date
3. mark it `GENERATING`
4. create Drive folder
5. run G1 through G12
6. save only permanent Research and Final Article docs
7. mark `READY_FOR_REVIEW`
8. populate Final Article, Final Score, Generated Date

Generation receives the lean commissioned idea.

G1 through G3 are responsible for discovering the final editorial spine, relevant people, mechanisms, hinge if any, and best truthful conception.

---

# 12. GENERATION COMMITMENT

Once Generation begins, do not editorially abort.

Research may:

- correct the hook
- change the person
- change the angle
- change the mechanism
- change the time window
- change the thesis
- change the architecture
- change the narrative hinge
- determine that no hinge is appropriate
- REFRAME

Normal outcomes:

- CONTINUE
- REFRAME

Only exceptional operational failure becomes ERROR.

After two revisions, unresolved editorial reservations still produce `READY_FOR_REVIEW` with a warning.

---

# 13. DRIVE

Folder:

`Nosebleeds > Unpublished > [Idea ID] - [Working Title]`

Only two permanent docs:

1. `01 - Research`
2. `02 - Final Article`

Do not permanently store:

- individual research pass docs
- drafts
- reviewer reports
- EIC reports
- score docs
- orchestration artifacts

Intermediate outputs may remain in n8n execution history.

---

# 14. RESEARCH

G1: Deep landscape and reconstruction.  
G2: Context and adversary.  
G3: Research compiler and final conception.

Research is mode-aware.

A Belief File is conditional.

A narrative hinge is conditional.

The final Research document locks the editorial spine before drafting.

---

# 15. DRAFT AND REVIEW

G4 drafts from Research only.

G5 reviews Story / Reader Experience.

G6 reviews Voice / Nosebleeds / Magic.

G7 reviews Truth / Evidence.

G8 adjudicates.

G9 revises.

G10 cold-scores.

G11 adjudicates a second round if needed.

Maximum two G9 revision rounds.

G12 packages after body copy is stable.

---

# 16. HUMAN NOTES

Human Notes are human and operational.

Do not feed Human Notes into automated learning.

Do not create a learnings file.

Do not infer publication taste from Human Notes automatically.

---

# 17. TIMEOUTS AND RUNTIME

There is no Nosebleeds requirement to complete workflows in 10 minutes.

The current environment may support substantially longer runs, including roughly 40 minute workflows.

Do not:

- reduce candidate quality
- reduce research depth
- remove editorial passes
- downgrade models
- compress search

solely to satisfy a presumed 10 minute ceiling.

Actual node-level or platform-level timeouts remain implementation settings and should be configured to support the workflow.

---

# 18. FRONTEND

The lightweight console may expose:

- Working Title
- Status
- Priority
- Sport
- Idea Score
- Drive Folder
- Final Article
- Generated Date

Summary counts:

- READY
- GENERATING
- READY_FOR_REVIEW
- PUBLISHED

Controls:

- Run Ideation
- Generate Next Story

Editable:

- Priority
- Status
- Human Notes

Do not surface removed required fields such as Story Type or Human Carrier.

---

# 19. ERROR POLICY

ERROR is for:

- technical/API failure
- malformed required runtime output after retry
- unrecoverable source access
- impossible premise with no honest adjacent piece
- legal/safety operational stop

ERROR is not for:

- reviewer dislikes draft
- final score below aspiration
- EIC wants more work after max revisions
- story was reframed
- no narrative hinge exists

---

# 20. FINAL IMPLEMENTATION PHILOSOPHY

The system should be easy to understand.

The models do the editorial thinking.

n8n moves the work.

The Google Sheet tells the human what state the work is in.

Do not add machinery until a real failure mode proves it is necessary.
