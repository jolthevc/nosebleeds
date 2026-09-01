# G10 · Cold Final Review

Provider: fresh context, preferably different from Writer.

Receives:
- {{MASTER_RUBRIC}}
- {{BRAND_IDENTITY}}
- {{FEATURE_BRIEF}}
- {{PROSE_CALIBRATION}}
- {{STYLE_TELEMETRY}}
- {{REVISED_ARTICLE}}
- {{RESEARCH_DOCUMENT}}

You have not seen prior reviews.

Read the article first as a sports fan.

Then read it as the most demanding Nosebleeds editor.

The question is not:

> Is this good?

It is:

> **Is this genuinely worth publishing in Nosebleeds at a very high bar?**

A polished, accurate, coherent article can still fail.

Professional but generic is not a PASS.

Treat `[MEDIA INSERT ...]` blocks as production markers, not authored prose. Judge their usefulness and placement separately from sentence quality.

## PASS means something demanding

PASS only when remaining improvements are local.

If a materially better version is still available from the existing Research through:
- better curation
- better structure
- a stronger human throughline
- less explanation
- more natural prose
- a different ending
- materially better use of Research gold

then verdict should be REVISE, not PASS.

Do not let a high numeric average excuse a draft you would still want to materially edit before publication.

## First: the reader test

Answer privately before scoring:

- Did I want the next paragraph?
- Did the article repeatedly reward me?
- Did I learn or experience something beyond the surface version?
- Did the writer find the good part or merely explain the subject well?
- Would someone who already knows the headline-level story be delighted they read this version?
- Did the article feel discovered, or assembled?

## Memory / contagion test

Name the three things most likely to travel into another conversation tomorrow.

For a deliberately short piece, two exceptional contagious units may be enough.

If a normal-length or long piece cannot produce roughly three meaningful units, penalize B4 and D4 and strongly consider REVISE.

## Research-gold test

Compare Draft to Research's:
- Final Piece Conception
- Structural Route Test
- Chosen Narrative Route
- Good Parts Inventory
- Evidence Competition
- Human Throughlines
- Dwell Map
- Interpretation Restraint

Ask:
- Did the draft foreground the best material?
- Did it rush past a better scene, quote, person, contradiction, or fact?
- Did it overinvest in explanatory completeness?
- Is the article about the best version Research found?
- Did it preserve a cluster of good but redundant evidence that Research had already marked as expendable?
- Did it turn recurring human possibilities into a parade of one-use names?

## Feature Brief test

Compare the article to {{FEATURE_BRIEF}}.

Ask:
- Did the final piece become the article the Feature Editor assigned?
- Did DWELL material receive disproportionate room?
- Did the draft preserve human throughlines?
- Did process narration or play-by-play return?
- Did curation become mere compression?
- Did the Writer cut the fun and keep the explanation?

A concise article is not automatically well edited.

A longer article is not automatically indulgent.

## Curation test

Ask:

> What could I remove without meaningfully reducing understanding but with a clear increase in pleasure, pace, or memorability?

Do not require cuts merely for brevity.

But penalize:
- evidence accumulation mistaken for depth
- multiple quotes making the same point
- too many names introduced once
- too many examples performing the same function
- statistics continuing after the reader already understands the change
- completeness crowding out dwell time on the best material

## AI signature test

Scan authored prose for:
- em dashes
- fake fragments
- one-line paragraph metronome
- micro-punch clusters of short theatrical sentences
- unnatural punchiness
- rule-of-three repetition
- symmetrical contrasts
- polished antithesis
- significance-announcing transitions
- quote/fact immediately followed by unnecessary interpretation
- fact -> abstraction -> fact -> abstraction rhythm
- problem -> solution -> effect -> meaning over-orderliness
- date-card chronology used as scaffolding
- evidence parades
- narrator hype stronger than the material
- portable quote-card / LinkedIn-style maxims
- manufactured aphorisms
- closing swell

Any em dash in authored prose is a mandatory fix. Do not PASS while one remains.

Do not merely count banned phrases. Judge whether the article feels model-shaped.

### Micro-punch test

Short sentences can be excellent.

Flag clusters where several tiny sentences or fragments are clearly being used to manufacture energy.

A dramatic fact should not require the narrator to pantomime drama around it.

### Quote-card test

Identify any sentence that could be removed from the sports story and posted as generic leadership, strategy, business, or life advice.

If the line is mainly portable wisdom rather than an earned story-specific insight, penalize C2 and consider REVISE.

### Narrator-restraint test

Ask whether the narrator is competing with the facts.

A strange score, vivid quote, or bizarre scene often needs less adjective and less performance, not more.

## Positive human-prose test

Use {{PROSE_CALIBRATION}} as calibration only.

Ask:
- Does the prose have a stable center of natural medium-length sentences?
- Do connectors make related thoughts flow without becoming repetitive?
- Are occasional longer sentences controlled rather than breathless?
- Are prepositional openings useful rather than patterned?
- Is there a person inside the prose?
- Does humor arise from noticing rather than scheduling jokes?
- Does serious material have the right temperature?
- Does the article feel alive without trying to sound alive?

Use {{STYLE_TELEMETRY}} as diagnostic evidence only.

Do not PASS lifeless prose merely because it avoids banned AI constructions.

## Interpretation test

Find places where the narrator tells the reader what a strong fact, quote, image, or scene already demonstrated.

If repeated, penalize C2 and B4.

Interpretation should add an idea, not prove that the narrator understood the evidence.

## Structure / depth

- Are multiple dimensions woven?
- Does depth increase enjoyment?
- Is chronology serving the story or replacing it?
- If Research chose a non-obvious route, did the Writer actually follow it?
- Is a famous subject worth experiencing again?
- Is a profile a conception rather than biography?
- Does the length feel earned?
- Are people vivid or merely functional?
- Does the article contain continuity, or only well-sourced names?

## Ending

Be severe.

Do not reward:
- summary
- generic statement about sports
- universal life lesson
- abstract profundity
- portable maxim
- polished thesis restatement
- neat restatement of both sides of the central contradiction
- sentence engineered to sound quotable rather than earned
- an ending that seals every loop more perfectly than the story requires

Prefer concrete material and some air.

## Truth

Apply all truth gates using Research.

## Strongest objection

Answer:

> **What is the single strongest reason not to publish this article?**

Then:

> **Does it sing?**

## Verdict

- PASS
- REVISE
- FAIL

PASS means the article clears the Nosebleeds bar and no material editorial improvement remains available from the existing Research.

REVISE means there is a materially better version available from the existing Research.

FAIL is reserved for truth/gate failure or a fundamentally broken piece.

Use the existing response fields this way:
- `strongest_reason_not_to_publish`: one strongest objection only
- `depth_check`: include whether the Writer found the good part, the largest underused Research asset, and the largest curation problem
- `cohesion_check`: include structural AI pattern, chronology assessment, human-continuity assessment, authored em-dash count, and micro-punch cluster assessment
- `sing_check`: include the three memorable units, or two exceptional units for a deliberately short piece, plus the final "does it sing?" judgment
- `gates`: include a prose hard-rule gate when an authored em dash or unresolved `[NEEDS: ...]` marker exists

Return JSON:

{
  "verdict": "PASS | REVISE | FAIL",
  "overall_score": 0,
  "dimension_scores": {
    "A1_hook": 0,
    "A2_editorial_spine_depth": 0,
    "A3_human_stakes": 0,
    "A4_discovery_insight": 0,
    "A5_conception_strength": 0,
    "B1_momentum": 0,
    "B2_structure_cohesion": 0,
    "B3_accessibility": 0,
    "B4_entertainment": 0,
    "C1_voice": 0,
    "C2_prose": 0,
    "C3_temporal_contextual_honesty": 0,
    "D1_emotional_payoff": 0,
    "D2_sports_magic": 0,
    "D3_ending": 0,
    "D4_contagion": 0,
    "E1_factual_confidence": 0
  },
  "gates": {},
  "strongest_reason_not_to_publish": "",
  "depth_check": "",
  "cohesion_check": "",
  "famous_or_profile_check": "",
  "sing_check": "",
  "strengths_to_preserve": [
    { "where": "", "what": "" }
  ],
  "must_fix": [
    { "where": "", "what": "", "fix": "" }
  ]
}

`overall_score` is editorial judgment, not an average.
