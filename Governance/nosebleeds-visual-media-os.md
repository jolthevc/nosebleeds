# Nosebleeds Visual Media and Image Sourcing OS

**Version 1.3 - Editorial Quality Upgrade - Covers Build Mandate Deliverables 09 (Visual Media and Image Sourcing OS) and the visual portions of 02 and 10.**  
**Inherits:** Brand Bible, Research Standard v2.2, Narrative Architectures v2.2, Voice doctrine, and the current G1-G12 production pipeline. Binds by reference.

**Interfaces with:** Production and Review Standard v2.2 through research visual leads, G3 visual needs, G4/G9 media markers, and the G12 publication package. Production governs orchestration; this OS governs visual sourcing, classification, placement, and readiness.

## Governing ideas

**Every visual proves, shows, or explains, or it is not placed.**

**A real image is found, never described into existence.**

**The system finds, classifies, and recommends. The human licenses and decides.**

**Generated imagery never impersonates evidence.**

## 1. What visuals do

Three functions. A visual that does none is decoration and is not placed.

### Prove

The document, box score, newspaper page, letter, television listing, court filing, rulebook line, ticket, contract, or other artifact that establishes or sharpens a claim.

Proof visuals carry the same epistemic state as the claim they support and are placed where the claim matters.

### Show

The person on that date, crowd, stadium, object, room, place, equipment, or moment.

Show visuals put the reader in the relevant human environment and are placed at the beat where that environment matters.

### Explain

The diagram, map, timeline, reconstruction, measured distance, route, data graphic, or other visual that makes a mechanism legible.

Explain visuals are placed at the explanation point, never before the reader has the question.

### Density

Density is a consequence of function, not a target.

Typical, not mandatory:

- Quick Story: one hero and zero to two inline visuals.
- Core Story: one hero and two to four inline visuals.
- Big Story: one hero and four to seven inline visuals.

A Core Story with one extraordinary proof document and no other useful inline visual is correctly served.

## 2. Where visual work happens

Visual thinking is layered into the existing G1-G12 production pipeline. It is not saved for Packaging.

### 2.1 G1 and G2: visual discovery

Research captures visual evidence as it encounters it:

- photographs
- documents
- box scores
- scoreboards
- newspaper pages
- broadcasts
- maps
- objects
- equipment
- advertisements
- programs
- tickets
- data that wants a chart

For real material, record the URL actually retrieved and the visible credit when one is shown.

Research should also flag honest constructed possibilities such as a diagram, timeline, score reconstruction, route, or chart backed by verified packet data.

### 2.2 G3: Visual Opportunity Map

The compiler identifies where visuals would improve the reading experience.

Each need should state:

```text
visual_need:
  function: PROVE | SHOW | EXPLAIN
  what_needed
  why_it_matters
  ideal_placement
  verified_source_url | CONSTRUCT_FROM_RESEARCH | NEEDS_HUMAN
  hero_candidate: yes | no
```

G3 should ask:

- What evidence should the reader see rather than merely be told?
- What person, place, object, or artifact would make the world of the story tangible?
- What mechanism is easier to understand visually?
- What image embodies the conception rather than merely naming the subject?

The Visual Opportunity Map is editorial planning, not permission to fabricate an asset.

### 2.3 G4 and G9: inline MEDIA INSERT markers

The Writer may place production markers between paragraphs.

Markers are not consumer prose and are ignored when scoring sentence quality.

Use:

```text
[MEDIA INSERT
FUNCTION: PROVE | SHOW | EXPLAIN
NEED: specific visual need
WHY HERE: why the reader wants it at this exact beat
SOURCE_URL: verified URL | N/A - CONSTRUCT_FROM_RESEARCH | NEEDS_HUMAN
]
```

Rules:

- place a marker only where the visual performs narrative work
- do not place visuals at arbitrary intervals
- do not invent a real source URL
- do not describe a fake archival object as if it exists
- revisions may move or remove markers when the prose changes
- a visual should usually arrive after the reader has the question it answers

### 2.4 G5, G6, G8, and G10: editorial visual check

Reviewers may flag:

- a marker that arrives too early or late
- a visual that merely decorates
- a great visual opportunity Research found but the draft ignored
- a visual that would allow explanatory prose to be cut
- a hero idea that illustrates the noun rather than the conception

Visual findings do not excuse prose weaknesses. The article must still read well without the asset loaded.

### 2.5 G12: resolution and packaging

Packaging resolves the final article's visual needs.

It receives the final article, Research visual section, and Visual OS.

It should:

- choose the hero concept
- resolve inline markers to real sources or honest constructed assets
- preserve source, credit, and rights notes
- write captions
- write treatment prompts where useful
- identify unresolved human sourcing work

G12 does not rewrite the article body.

## 3. The hero

Every story gets a hero candidate or a fully specified fallback path.

The hero makes the story feel like an event and serves the story card, newsletter, and social share.

Rules:

- The hero sells the reason the story is irresistible before the reader starts.
- The hero should embody the conception, not merely depict the nominal subject.
- Ask: "What image would make someone want to know what happened even before reading the headline?"
- The hero belongs to the story: person, crowd, object, document, scoreboard, place, or other central visual object.
- Never the mascot.
- Never a generic stadium simply because the story is about sports.
- Real imagery is preferred when the hero is a real person, event, or object and a strong real image can be found.
- A document may be the hero when the document is itself the discovery.
- A typographic, diagrammatic, or illustrated cover is a quality fallback, not filler.
- A mediocre real photograph loses to an excellent constructed cover when the constructed cover tells the truth more clearly.
- The Packager chooses the recommended hero from the G3 hero concepts, Research visual evidence, and the final article conception. The human may overrule at the gate.

Weak hero instinct:
- article about a shot clock -> handsome shot clock
- article about Tiger -> generic Tiger portrait
- article about a GM -> executive at a draft table

Better instinct:
- article about a 19-18 game -> the impossible-looking final score
- article about a rule forcing play -> the behavior the rule had to stop
- article about an athlete changing opponents -> the opponents' altered world
- article about roster valuation -> the expensive position beside the intentionally replaceable one

Literal imagery is allowed when it is genuinely the most compelling conception. It is not the default.

## 4. The candidate contract

For every candidate visual, real or generated. Fields the system cannot fill are left empty and flagged. They are never guessed.

```text
visual_candidate:
  candidate_id
  visual_need_id
  beat_id | hero

  function:
    prove | show | explain

  type:
    photograph | document | newspaper_page | box_score |
    scoreboard | object | map | diagram | timeline | chart |
    illustration | generated

  description:
    exact account of what is depicted, who, where, and when
    using only information supported by the retrieved page or packet

  why_it_works:
    one sentence tying the candidate to the visual need

  placement:
    hero | inline_after_beat | inline_after_paragraph_n | sidebar

  # Real material
  source_url:
    retrieved URL only; empty if not retrieved

  originating_site_or_archive

  visible_credit:
    photographer, agency, publisher, or archive exactly as displayed;
    empty if none visible

  date_of_image:
    only if shown or supported by the page

  alternate_urls:
    other retrieved locations of the same candidate

  rights_classification:
    section 5

  rights_basis:
    what the retrieved page or source actually indicates

  editorial_use_likely:
    yes | no | unknown
    advisory only, never a legal conclusion

  resolution_note:
    sufficient_for_hero | inline_only | unknown

  # Generated or constructed material
  generation_prompt:
    section 6

  data_source:
    packet claim_ids used to build charts, timelines,
    reconstructions, maps, or scoreboards

  interpretive_label_required:
    yes for every generated or constructed visual

  alternatives:
    up to two candidate_ids

  confidence:
    high | medium | low
    with reason
```

### Hard rules for the contract

- `source_url` contains only URLs retrieved in this run. A URL recalled from training or constructed from a site's naming pattern is a terminal failure of the visual pass.
- `visible_credit` contains only text visible on the retrieved page or supplied by a directly retrieved authoritative record. The system does not infer a photographer from style, era, or likelihood.
- `rights_classification` describes what the retrieved page or source appears to indicate. It is not a legal opinion.
- `confidence: low` is acceptable and useful. Uncertainty is surfaced, not hidden.
- A real candidate with missing identity, credit, rights basis, or resolution may still be useful as a reference, but its classification must say so.

## 5. Rights classification

Every real candidate carries one of the following. The classification is the system's reading of the retrieved material and its documented basis. The human licensing step decides whether and how it can be used.

### public_domain_candidate

The retrieved source explicitly identifies the material as public domain, supplies a public-domain marker, or provides a documented statutory or institutional basis the system can quote or summarize accurately.

Record the basis.

Do not hardcode a calendar-year cutoff into evergreen doctrine.

Human confirmation remains required before publication where rights matter.

### licensed_editorial_required

The page shows an agency or wire credit, licensing link, editorial-use reference, or comparable licensing path.

Present the agency, visible reference ID when available, and retrieved source page.

### publisher_permission_required

Newspaper pages, magazine spreads, book scans, broadcast frames, or other publisher-controlled material for which the retrieved source indicates permission or licensing may be required.

The system surfaces the path. It does not decide fair use or publication rights.

### archive_terms_apply

Museum, library, hall-of-fame, university, government archive, or similar collection with stated terms.

Record the relevant terms or link to them from the retrieved page.

### creative_commons_stated

The retrieved page states a Creative Commons license.

Record the exact license and any visible attribution, share-alike, non-commercial, or modification conditions.

### unclear

The retrieved page shows no usable rights information or the system cannot confidently classify it.

Present the candidate as unclear and state what a human could check.

### reference_only

Useful for the human to understand what the image is, but not a current publication candidate because it is watermarked, low-resolution, poorly sourced, or likely reproduced by a secondary site without authority.

### generate_alternative

No suitable real image was found or the idea is better served by a clearly interpretive visual.

The system recommends a generated or constructed alternative and supplies the prompt or spec.

### recreate_as_data

The visual is better built than found: scoreboard, box score, timeline, measurement, map, route, or chart.

The system supplies the data and packet claim IDs.

Image cost is not a pipeline priority. Do not suppress the strongest candidate merely because it may cost money. Present the candidate and let the human decide.

## 6. Generated and constructed imagery

Permitted when:

- a real image does not exist or cannot be found
- an idea is better illustrated than photographed
- the cover is interpretive by design
- a diagram, map, timeline, or reconstruction explains something photography cannot
- a data object such as a scoreboard or measurement is more truthful when rebuilt from verified numbers

### Rules

**Never fake evidence.** No generated imagery may present a fictional image as a real historical photograph, real document, real scan, or real documentary frame.

A fake archival box score is forbidden. A reconstruction built from verified figures and labeled as a reconstruction is allowed.

**Always label interpretive material.** Every generated or constructed visual carries a visible label such as `Illustration`, `Diagram`, or `Reconstruction from the official box score`.

**Do not generate identifiable real-person likenesses for story imagery.** Illustrated covers use objects, typography, non-identifiable silhouettes or crowds, diagrams, or other non-deceptive approaches rather than simulated documentary portraits.

**Data visuals are built from the packet.** Every claim-bearing number in a chart, timeline, map, or reconstruction traces to packet claim IDs.

The generation prompt specifies:

- subject and visual function
- style constraints from the Visual Identity brief
- what must not appear
- aspect ratios for hero, inline, and social crops as needed
- packet-backed data or object details
- required interpretive label

## 7. Captions and credits

Captions are in the Nosebleeds voice and do work. They identify, orient, prove, show, or explain, and they credit.

### Real photograph

Draft form:

```text
[What or who]. [Where, when if supported].
Photo: [visible credit or "credit to be confirmed"].
```

### Document

Draft form:

```text
[What the document is]. [Date]. [Archive or publisher].
```

### Constructed or generated

The interpretive label comes first.

Examples:

```text
Reconstruction from the official box score.
Diagram: Nosebleeds.
Illustration: Nosebleeds.
```

One dry observation is permitted when the image earns it.

Captions never restate body copy, never editorialize beyond what the image supports, and never contain a claim not in the Research Packet.

Draft captions are written by the Packager from the candidate contract and are marked draft until the human confirms credits and licensing details.

## 8. The media manifest

The final G12 package functions as the working media manifest.

It should preserve enough information for a human editor to source or build the visuals without repeating the research.

For the hero and every inline recommendation, preserve:

```text
media_item:
  placement: hero | inline
  marker_text: original MEDIA INSERT marker when applicable
  function: prove | show | explain
  type
  description
  why_it_works
  source_url
  visible_credit
  rights_note
  caption_draft
  treatment_prompt
  status: resolved_real | construct_from_research | needs_human | omit
```

The manifest should make unresolved sourcing explicit.

If a revision moves or removes a `[MEDIA INSERT ...]` marker, G12 resolves only the markers present in the final article.

A removed marker does not create an obligation to use the earlier visual.

A strong unmarked visual discovered in Research may still be recommended if it materially improves the finished package.

Where the publication package supports it, the final package should also state overall visual readiness:

- `VISUAL_READY`
- `VISUAL_NEEDS_HUMAN`
- `VISUAL_BLOCKED`

This status is advisory and separate from article quality.

## 9. Visual Readiness

Visual Readiness is a final-package status, not one of the seventeen article-quality scores.

### VISUAL_READY

A viable hero and every narratively required inline visual function have either:

- a credible retrieved real candidate
- or a fully specified constructed/generated fallback backed by the packet

Any remaining human action is ordinary licensing, credit confirmation, approval, or final selection.

### VISUAL_NEEDS_HUMAN

The system found strong references or a credible direction, but the human must source, replace, choose, or resolve something before publication.

This is expected to be a normal state for many Nosebleeds stories because the human retains the final real-image sourcing and licensing decision.

### VISUAL_BLOCKED

A visual function judged essential to the package has no usable candidate, no honest constructed fallback, and no credible human sourcing path recorded.

The package cannot be called visually complete until the block is resolved or the EIC/Packager decides the visual function is not actually required.

A visual status does not alter the article-quality profile.

## 10. The human handoff

At the final gate, the human receives the manifest inside the publication package and may:

1. license or source the chosen real images
2. confirm or correct credits
3. approve or replace the hero
4. approve any reconstruction's underlying data
5. resolve any `VISUAL_NEEDS_HUMAN` or `VISUAL_BLOCKED` item

The system has done everything short of the transaction and legal judgment.

It has not fabricated a URL, credit, photographer, archive, license, or right.

## 11. Prohibitions

- No fabricated URLs, credits, photographers, agencies, archive names, dates, or license terms.
- No generated imagery presented as documentary evidence.
- No generated likeness of a real person used as simulated documentary story imagery.
- No fake documents, archival scans, box scores, or headlines.
- No visual placed for decoration.
- No visual placed before the reader has the question it answers.
- No mascot in the hero or in any evidence-bearing visual.
- No legal assertion by the system that an image may be published.
- No suppression of a strong candidate merely for cost reasons.

## 12. Runtime implications

The current G1-G12 pipeline can satisfy this OS without adding a new visual agent.

- G1 and G2 collect real visual leads and constructed opportunities during research.
- G3 creates the Visual Opportunity Map and hero concepts.
- G4 places only supported `[MEDIA INSERT ...]` markers.
- G5, G6, G8, and G10 may flag visual placement or missed visual opportunity while keeping prose review separate.
- G9 may move, remove, or add supported markers during revision.
- G12 resolves the final hero and inline visual package from the final article plus Research visual material.
- Real candidate URLs must come from retrieved research. Missing URLs are never guessed.
- Constructed visuals must trace claim-bearing details to Research.
- Visual readiness may remain `VISUAL_NEEDS_HUMAN` when licensing or final sourcing requires a person.
- No additional Generation workflow stage is required merely to comply with this OS.
- A future dedicated Visual Research or Visual Editor stage may be added if the publication later needs more sourcing depth, but it is optional rather than canonical.
- Visual Identity, including logo, typography, color, card system, and layout, remains a separate design brief.

# Change Log

## v1.3 - Editorial Quality Upgrade

- Layered visual thinking into G1-G12 rather than saving it for packaging.
- Added G3 Visual Opportunity Map.
- Added inline MEDIA INSERT marker contract for G4/G9.
- Reframed hero selection around the article conception rather than the nominal subject.
- Preserved proof/show/explain, sourcing, rights, and no-fake-evidence rules.

## v1.2 - Batch Three

- Updated Narrative Architectures interface to v1.2 and Production interface to v1.2.
- Removed circular canonical inheritance between the Visual Media OS and Production Standard. Production inherits this Visual OS for orchestration; the Visual OS now interfaces with Production through explicit contracts rather than inheriting it back.
- Made no substantive change to prove/show/explain, candidate resolution, rights classification, generated-imagery rules, or Visual Readiness.

## v1.1 - Batch Three

- Updated inheritance to Research Standard v1.2 and Narrative Architectures v1.1.
- Added an explicit Architecture visual-needs pass and Visual Research stage between Architecture and Draft.
- Separated `visual_need_id` from `candidate_id`; writers now insert only resolved candidate IDs.
- Formalized the Visual Editor as an advisory diagnostic seat outside the scored article profile.
- Replaced the static public-domain-year rule with `public_domain_candidate` plus documented basis and human confirmation.
- Added `VISUAL_READY`, `VISUAL_NEEDS_HUMAN`, and `VISUAL_BLOCKED` to the media manifest and human handoff.
- Preserved prove/show/explain, retrieved-only URLs, visible-only credits, no fake evidence, no real-person generated likenesses for story imagery, and human licensing control.

## v1.0 - Batch Three

Initial version. Three visual functions with density as consequence; visual workflow; hero rules; candidate contract; rights classifications; generated-imagery rules; caption forms; versioned media manifest; human handoff; prohibitions.
