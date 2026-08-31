# Migration Notes

## Required workflow changes

### Ideation
Remove:
- Anthropic I2 call
- 8.5 Idea Score gate
- score-based rejection branch

Use:
- I1 for Default Discovery
- I1D for Directed Ideation

### Field mapping
New runtime rationale field:
`why_you_have_to_read_this`

It may map into the existing Sheet column:
`Why It Works`

### Rubric field changes
Reviewer A and Cold Final now use:

- A1_hook
- A2_editorial_spine_depth
- A3_human_stakes
- A4_discovery_insight
- A5_conception_strength
- B1_momentum
- B2_structure_cohesion
- B3_accessibility
- B4_entertainment
- C1_voice
- C2_prose
- C3_temporal_contextual_honesty
- D1_emotional_payoff
- D2_sports_magic
- D3_ending
- D4_contagion
- E1_factual_confidence

If n8n currently parses old names such as `story`, `originality`, or `restore_uncertainty`, update the parser.

### G3
The JSON header remains parser-compatible:

`{ "outcome": "CONTINUE | REFRAME", "hook_verified": true, "register": "", "final_story_thesis": "", "reframe_summary": "" }`

The field name `final_story_thesis` is retained for compatibility even though its editorial meaning is now "final piece conception."

### Length
Remove deterministic checks against a target word range.

Use editorial review for padding and underdevelopment instead.

### Directed Ideation
New optional UI inputs:
- lens
- subject
- sport
- freeform query

No Google Sheet schema change is required unless you want to persist those inputs.
