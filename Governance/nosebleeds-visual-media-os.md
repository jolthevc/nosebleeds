# Nosebleeds Visual Media and Image Sourcing OS

**Version 1.2 - Batch Three - Covers Build Mandate Deliverables 09 (Visual Media and Image Sourcing OS) and the visual portions of 02 and 10.**  
**Inherits:** Master Handoff sections 16 and 17, Editorial OS sections 19 and 20, Build Clarification (Visual Research), Brand Bible v1.3 section 20, Research Standard v1.2 Stage 10, Narrative Architectures v1.2. Binds by reference.

**Interfaces with:** Production and Review Standard v1.2 through the `visual_need`, candidate-resolution, media-marker, Visual Editor, and publication-package contracts. Production governs orchestration; this OS governs visual sourcing, classification, placement, and readiness. This is deliberately an interface rather than inheritance so the canonical documents do not depend on each other circularly.

> **Runtime supersession note — Batch Four v2.1.** The prove/show/explain framework, source integrity rules, rights posture, hero judgment, and generated-imagery truth rules remain canonical. Batch Four v2.1 supersedes the old standalone Visual Research role, candidate-ID orchestration, media-manifest lifecycle, Visual Editor runtime seat, schema validators, and other visual runtime mechanics below wherever they conflict. At launch, research captures real visual leads; the Writer places descriptive `[MEDIA]` needs; Packaging recommends the hero and supporting visuals and may provide house-style treatment prompts.

> **Sourced stylization rule — current.** Nosebleeds may create a clearly illustrative house-style transformation of a real sourced sports image, including an identifiable real athlete, when the transformation preserves the actual person, action, moment, composition, and era cues of the source. This is stylization of a real reference, not fabrication of a documentary moment. The treatment must be visibly interpretive rather than presented as a photograph or archival record. A transformation does **not** erase the underlying source image's copyright, license, credit, permission, or other rights considerations. Synthetic "historical" scenes or fake documentary images generated without a truthful source moment remain forbidden.

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

Four passes. None invents evidence.

### 2.1 Research Stage 10: leads

During the research loop, the research model captures visual leads as it encounters them: a photograph on a retrieved page, scanned newspaper, document in a court record, box score, program, letter, map, or object.

Each lead is recorded with the URL actually retrieved and the credit visible on the page when one is visible.

Leads are cheap. Research records generously.

### 2.2 Architecture: needs

After the Research Packet is locked, the Story Architect identifies visual needs rather than final images.

Each need has:

```text
visual_need:
  visual_need_id
  beat_id | hero
  function: prove | show | explain
  what_needed
  research_lead_ids: []
  preferred_real: yes | no
```

A visual need is a narrative request, not an assertion that an image exists.

### 2.3 Visual Research: candidates

Visual Research runs after Architecture and before Draft.

It reads:

- the beat plan's `hero_need` and `visual_need` objects
- the Research Packet's visual leads
- the current Visual Media OS

It searches specifically for what each need requires and produces ranked candidates.

This role may search.

It may not assert a URL, credit, photographer, archive, date, licensing state, or image identity it did not actually retrieve or verify from the retrieved page.

Each visual need resolves to:

```text
resolution:
  visual_need_id
  selected_candidate_id | UNRESOLVED
  ranked_candidate_ids: []
  resolution_note
```

The Drafting Packet receives only selected inline candidate IDs and their beat placements. The writer never invents a candidate ID.

If a need is unresolved, the draft proceeds without a fake marker. The unresolved need remains in the media manifest and affects Visual Readiness.

### 2.4 Visual Editor: advisory bench seat

After the draft is frozen, the Visual Editor checks:

- each `[MEDIA: candidate_id]` marker sits where the visual does narrative work
- the selected candidate still matches the beat after prose exists
- the hero ranking reflects the story's strongest available image or visual object
- no visual is decorative, premature, redundant, or misleading
- a required explanatory visual has enough underlying packet data to be constructed honestly

The Visual Editor owns no article-score dimension.

It produces an advisory specialist report to the EIC. Findings enter the revision brief as marker moves, candidate swaps, or visual-needs changes, not as prose criticism unless visual dependence has made the prose incomplete.

The Visual Editor is separate from the eight editorial specialists and from the Evidence Auditor.

## 3. The hero

Every story gets a hero candidate or a fully specified fallback path.

The hero makes the story feel like an event and serves the story card, newsletter, and social share.

Rules:

- The hero belongs to the story: person, crowd, object, document, scoreboard, place, or other central visual object.
- Never the mascot.
- Never a generic stadium simply because the story is about sports.
- Real imagery is preferred when the hero is a real person, event, or object and a strong real image can be found.
- A document may be the hero when the document is itself the discovery.
- A typographic, diagrammatic, or illustrated cover is a quality fallback, not filler.
- A mediocre real photograph loses to an excellent constructed cover when the constructed cover tells the truth more clearly.
- The Packager chooses the recommended hero from the Visual Editor's ranking. The human may overrule at the gate.

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

**Do not fabricate identifiable real people into simulated documentary moments.** A clearly illustrative transformation of a real sourced image is allowed under the Sourced Stylization Rule above, including when the athlete remains identifiable. If there is no real source moment, use objects, typography, non-identifiable silhouettes or crowds, diagrams, or other non-deceptive approaches rather than inventing a fake historical scene.

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

The versioned artifact that carries visual decisions through revision and into the final package.

One manifest exists per article version. The final version is what the human receives.

When a revision moves or removes a `[MEDIA: candidate_id]` marker, the manifest is regenerated. Candidates that no longer fit are flagged, not silently dropped.

```text
media_manifest:
  brief_id
  article_version
  manifest_version

  hero:
    visual_need_id
    candidate_id | UNRESOLVED
    ranked_alternatives: []
    visual_editor_note

  inline:
    - visual_need_id
      beat_id
      marker_position
      candidate_id | UNRESOLVED
      function
      ranked_alternatives: []
      caption_draft
      credit_status:
        confirmed | to_confirm | none_visible | not_applicable

  generated:
    - candidate_id
      generation_prompt
      data_table
      interpretive_label

  rights_summary:
    counts_by_classification
    licensing_candidates: []

  flags:
    [ no_hero_real_image_found |
      hero_is_document |
      hero_is_typographic_fallback |
      unresolved_visual_need |
      synthetic_documentary_real_person_scene_forbidden |
      retrieved_url_missing_for_real_candidate ]

  visual_readiness:
    VISUAL_READY | VISUAL_NEEDS_HUMAN | VISUAL_BLOCKED

  visual_readiness_reason

  human_actions_required: []
```

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
- No synthetic likeness of a real person presented as a simulated documentary or historical moment. Clearly illustrative sourced transformations are allowed under the Sourced Stylization Rule.
- No fake documents, archival scans, box scores, or headlines.
- No visual placed for decoration.
- No visual placed before the reader has the question it answers.
- No mascot in the hero or in any evidence-bearing visual.
- No legal assertion by the system that an image may be published.
- No suppression of a strong candidate merely for cost reasons.

## 12. Runtime implications

- Visual leads are captured inside Research Stage 10 and stored with retrieved URLs only.
- Architecture creates visual needs, not final candidate IDs.
- Visual Research runs after Architecture and before Draft and resolves each need to ranked candidates or `UNRESOLVED`.
- The Drafting Packet receives only resolved inline candidate IDs and placements.
- The Visual Editor is an advisory diagnostic seat with no scored dimension and reports to the EIC.
- Visual Research may rerun after a rearchitecture or any revision that creates a new visual need.
- The Packager assembles the media manifest from candidate records, article markers, Visual Editor ranking, and final article version.
- Schema validation rejects a real candidate whose non-empty URL was not retrieved in the run.
- Legacy schema logic, if reused, must reject synthetic simulated-documentary depictions of identifiable real people but must not reject a clearly illustrative transformation tied to a real sourced image.
- Visual Identity, including logo, typography, color, card system, and layout, remains a separate design brief. This OS governs story-image sourcing and use within that identity.

# Change Log

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
