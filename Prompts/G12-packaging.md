# G12 · Packaging

Provider: strong editorial model.

Receives:
- {{VOICE_BIBLE_HEADLINE_GUIDANCE}}
- {{VISUAL_OS}}
- {{RECENT_TITLES}}
- {{FINAL_ARTICLE}}
- {{RESEARCH_VISUALS_SECTION}}

The article is final.

Do not change a word of it.

Package the piece.

## Titles

Write five title and subtitle pairs.

The title should reflect the best conception, not merely the broad subject.

Optimize for:
- curiosity
- clarity
- broad appeal
- emotional pull
- truthfulness
- memorability
- the actual reading experience

Famous names are useful when they increase pull.

Do not avoid a famous subject to sound original.

Do not rely on:
- "the untold story"
- "you never knew"
- generic "history of"
- generic "rise of"
- empty greatness language
- prestige vagueness

Questions, colons, and "how X changed Y" constructions are allowed when they are genuinely the best title.

Do not use them mechanically.

Avoid repeating the syntax of recent Nosebleeds titles.

Choose one recommended pair and explain why in one sentence.

## Visuals

Recommend:

- one hero
- two to four supporting visuals where useful

Prefer real images or documents from Research when rights permit.

For each real source:
- source URL
- visible credit
- rights note
- function: prove, show, explain
- draft caption

Where house-style treatment is appropriate, use grounded gouache with subtle ink-line definition, restrained halftone / print texture, warm paper character, and the Nosebleeds palette.

Preserve:
- athlete
- action
- composition
- era cues
- recognizability
- factual truth

Do not invent:
- people
- objects
- documents
- historical detail

Ordinary article art should not bake in a Nosebleeds logo or heavy border.

## Output

Return JSON:

{
  "recommended": {
    "title": "",
    "subtitle": "",
    "why": ""
  },
  "alternates": [
    { "title": "", "subtitle": "" }
  ],
  "hero": {
    "description": "",
    "source_url": "",
    "visible_credit": "",
    "rights_note": "",
    "treatment_prompt": ""
  },
  "supporting": [
    {
      "marker_text": "",
      "function": "prove | show | explain",
      "description": "",
      "source_url": "",
      "visible_credit": "",
      "caption_draft": "",
      "treatment_prompt": ""
    }
  ]
}
