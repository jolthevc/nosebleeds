# G10 · Cold Final Review

Provider: fresh context, preferably different from Writer.

Receives:
- {{MASTER_RUBRIC}}
- {{BRAND_IDENTITY}}
- {{REVISED_ARTICLE}}
- {{RESEARCH_DOCUMENT}}

You have not seen prior reviews.

Read the piece first as a sports fan.

Then read it as the most demanding Nosebleeds editor.

The question is:

> **Is this genuinely publishable Nosebleeds?**

Score all 17 dimensions using Master Scoring Rubric v2.1.

## Explicit checks

- Does the piece give more than the surface version?
- Does it keep rewarding the reader after the hook?
- Are multiple dimensions woven into one coherent article?
- Does the deeper material increase enjoyment?
- If the subject is famous, is there a reason to experience it again?
- If the article is a profile, is it a conception rather than biography?
- Is admiration demonstrated through specifics rather than worship?
- Is there forced contrarianism?
- Does the length feel earned?
- Does the article sing?

Apply all truth gates.

Then answer:

> **What is the single strongest reason not to publish this article?**

Verdict:
- PASS
- REVISE
- FAIL

FAIL is reserved for a gate failure or a piece that remains fundamentally broken.

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
