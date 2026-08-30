# Nosebleeds Production and Review Standard

**Version 1.2 - Batch Three - Covers Build Mandate Deliverables 10 (Drafting System), 11 (Editorial Review and Revision System), and the publication-package portion of the Final Human Handoff.**  
**Implements:** forensic bench, EIC conductor, iterative revision, run ledger, and final package.  
**Inherits:** Editorial OS v1.0, Brand Bible v1.3, Voice Bible v0.8 and current Voice Kernel, Ideation and Selection Standard v1.2, Research Standard v1.2, Master Scoring Rubric v1.2, Narrative Architectures v1.2, Visual Media OS v1.2. Binds by reference.

> **Runtime supersession note — Batch Four v2.1.** The editorial principles in this document remain canonical, but Batch Four v2.1 supersedes the runtime orchestration described below wherever they conflict. The current n8n Generation workflow does **not** implement the old freeze/hash system, mechanical scan, eight-specialist bench, dual cold scorers, run ledger, artifact/version graph, or full re-review dependency waves. Runtime uses three independent reviewers, one EIC brief, Writer revision, a fresh Cold Final Review, and at most one additional narrow EIC/revision/cold-review round. n8n should load only the sections explicitly named by the Batch Four implementation spec, especially the EIC doctrine.

The canonical loop is:

**architecture -> visual research -> draft -> freeze -> independent diagnosis -> EIC brief -> revision -> re-diagnosis -> re-score -> verdict -> package**

Revision never happens before diagnosis. Diagnosis never happens on a moving document. Nobody on the specialist bench sees anyone else's report. Cold scorers see no reports or prior scores. The EIC is the only editorial role that sees the full current-round picture.

## 1. Stage map and dependency waves

The runtime uses dependency waves rather than pretending every diagnostic can start at the same instant.

| Stage | Role | Sees | Produces |
|---|---|---|---|
| P1 Architecture | Story Architect | Research Packet, Kernel, Narrative Architectures | Beat plan with visual needs |
| P1.5 Visual Research | Visual Research | Beat plan visual needs, packet visual leads, Visual Media OS | Ranked visual candidates and resolutions |
| P2 Draft | Writer, full-draft mode | Drafting Packet | ARTICLE_ORIGINAL |
| Freeze | Deterministic | ARTICLE_ORIGINAL | Content hash, immutable version |
| P3 Mechanical | Deterministic | Frozen article, resolved candidate set | Hard hits, review flags |
| P4 Verification | Evidence Auditor + deterministic E1 function | Frozen article, Research Packet, source ledger | Verification report, deterministic E1 |
| P5 Editorial Bench | Eight specialists, blind and parallel where dependencies permit | Frozen article, packet, beat plan, assigned module | Eight specialist reports |
| P5V Visual Review | Visual Editor, advisory | Frozen article, beat plan, candidate set, media markers | Visual advisory report |
| P6 Cold Score, split-phase | Two scorers, different families + deterministic score assembler | Phase A: frozen article, packet, mode/register. Phase B: verification report | Phase A judgment scores A1-D4; Phase B finalized score records with imported E1 |
| P7 EIC | Conductor | All current-round outputs | Verdict recommendation, one revision brief if needed |
| P8 Revision | Writer and, when authorized, Story Architect | Revision brief, current version, packet, Kernel | ARTICLE_REVISED_nn and optionally revised beat plan |
| P9 Re-review | Current-version P3-P7 graph again | Revised frozen version | New reports, scores, deltas |
| P10 Package | Deterministic assembly + Packager | Final article, ledger, media manifest | Publication package |
| Human gate | Human | Publication package | Publish, reject, or edit |

### Diagnostic wave A

After a version is frozen, run concurrently:

- P3 Mechanical Scan
- P4 Verification
- P5 Story Doctor
- P5 Hook and Opening Editor
- P5 Momentum and Structure Editor
- P5 Two Readers
- P5 Hindsight Auditor
- P5 Landing Editor
- P5 Contagion and Package Editor
- P5V Visual Editor
- P6 Cold Scorer A, judgment phase on A1 through D4
- P6 Cold Scorer B, judgment phase on A1 through D4

The cold scorers do not wait for verification to begin judgment scoring. They do not score E1 in this phase.

### Diagnostic wave B

Starts when its dependencies exist:

- P5 Voice and Prose Editor starts after P3 so it can inspect mechanical review flags.
- P6 score finalization starts after P4 and both cold judgment passes exist. A deterministic assembler verifies article-version/hash alignment and imports the E1 emitted by verification into both score records. No new editorial judgment occurs in this step.

### Diagnostic wave C

P7 EIC starts only after all required current-round reports and both finalized cold-score records are written to the ledger.

This dependency graph applies again during re-review.

## 2. The Drafting Packet

What the Writer receives in full-draft mode. Nothing else.

The Writer never sees reviewer reports, prior scores, EIC diagnoses, revision history, or the Voice Bible's quarantined reviewer sections.

```text
drafting_packet:
  brief_id
  packet_version
  architecture_version
  article_version_target: ORIGINAL

  title_working
  subtitle_working

  format
  target_words
  register

  hook_fact:
    statement
    epistemic_state: Verified
    outcome_is_hook: yes | no

  hinge:
    statement
    date_or_bounded_period

  beat_plan:
    complete architecture output

  spine:
    named

  people_or_collective:
    [ identity,
      who_they_were_then,
      after,
      living,
      attributed_statements ]

  timeline

  belief_file:
    full | reduced | skipped | inevitability_mode
    with evidence

  hindsight_hazards: []

  discovery_claim:
    statement
    epistemic_state
    required_prose_behavior

  locked_claims_list:
    claims the writer may state flat

  attributed_claims_list:
    claims requiring visible natural attribution

  disputed_claims_list:
    claims whose disagreement or uncertainty must remain visible

  legend_list:
    claims that may appear only as legend or later telling

  prohibited_claims_list:
    claims that may not be asserted

  quote_bank:
    verbatim only, each with speaker, date, context, source,
    and quotation-handling metadata

  statistics:
    authoritative figures and claim_ids

  texture

  explanation_points:
    from Architecture: what to explain, where,
    and maximum necessary scope

  ending_chosen
  ending_fallback

  visual_markers:
    [ { beat_id, visual_need_id, candidate_id } ]
    only resolved inline candidates; no unresolved fake IDs

  calibration_passages:
    two or three register-matched passages,
    marked synthetic/not-for-reuse until production exemplars replace them

  voice_kernel:
    current version

  protected_intent:
    architecture-level facts, relationships, functions,
    discovery, and ending function

  risks
```

The packet is the writer's entire factual world.

A factual claim not in it is an external claim and verification will find it.

A writer who wants a fact the packet does not contain does not invent it.

## 3. The drafting prompt: full-draft mode

Production-ready. Served with the current Kernel and Drafting Packet. Written to give a creative identity, not a reviewer checklist.

> You are writing a Nosebleeds story. You are a sports fan who did the reading: you found this story, you read everything in the packet, and you cannot wait to tell it. You are in the stands with the reader, not above them. The story is the star, not you.
>
> Everything factual you may assert is in the packet. State locked claims plainly. Attribute attributed claims naturally so the reader can see whose account it is, usually in the sentence or immediate context. Keep disputed claims disputed. Tell legends as legends or later tellings. Prohibited claims do not exist. If you reach for one, that is evidence the packet does not support the sentence.
>
> Quotes come from the quote bank, verbatim, or not at all. Claim-bearing numbers come from the statistics list or locked claims. If the packet does not contain something you want, you do not have it. Do not invent dialogue, thoughts, scenes, presence, reporting, motives, or people. Nothing you write becomes evidence because you wrote it. The packet is the evidence boundary.
>
> Follow the beat plan for order, purpose, and pull. Within each beat, write freely. The plan tells you where the hook belongs, where the hinge is, where the story slows, where explanation becomes necessary, and where the story ends. It does not tell you how to write sentences.
>
> Put the hook fact where the plan says, usually in the first sentence or first paragraph. Do not hide why the reader clicked. Preserve the uncertainty that matters. If the outcome is the payoff, the people inside the story do not know it until it happens, and neither does the prose. The hindsight-hazards list is what nobody in the scene knows yet. Introduce people as who they were then.
>
> Use contemporaneous evidence from the Belief File when the story calls for it. If the Belief File is in inevitability mode, do not manufacture doubt. Say what people actually expected and find the tension inside the certainty.
>
> Write in the assigned register. Calibration passages are demonstrations of restraint and rhythm, not material to reuse. Never reuse their sentences or facts. If the material turns serious, let wit leave and precision stay. If the material is funny, let the facts carry the joke. Ordinary sentences are required. Let exact numbers replace adjectives when the number is the fact. Show a reaction and trust it. Explain a rule or mechanism only where the plan marks the explanation point, in the minimum scope required to preserve the stakes.
>
> The narrator is never first-person singular. The mascot is not in the article body. The article is continuous prose by default: no bullets, no lists, no bold run-in labels, and no section headers unless the beat plan explicitly calls for them. Use no em dashes anywhere.
>
> End on the ending the architecture chose. Do not append a paragraph explaining what it means.
>
> Where the packet contains a resolved inline visual marker, insert it on its own line as `[MEDIA: candidate_id]` at the marked beat. Never invent a marker. Do not describe the visual merely to compensate for the marker.
>
> Output the article only: title, subtitle, then body. No preamble, notes, source commentary, or explanation of choices. The title and subtitle may improve on the working versions. Keep the headline concrete, clear, intriguing, and free of adjectives that tell the reader how impressed to be. There is no mandatory headline syntax.

Target length is a target, not a quota.

The prompt is versioned in the prompt pack. This is canonical full-draft prompt v1.1.

## 4. Freeze and versioning

`ARTICLE_ORIGINAL` is written to the ledger with a content hash and is immutable.

Every reviewer, scorer, and the EIC reads the same bytes for a given version.

Revisions create:

- `ARTICLE_REVISED_01`
- `ARTICLE_REVISED_02`
- rarely `ARTICLE_REVISED_03`

Each version is frozen on creation and receives its own hash.

Revisions never edit a prior frozen version in place.

A rearchitecture may also create:

- `BEAT_PLAN_REVISED_01`

The old beat plan remains in the ledger.

## 5. Mechanical scan: P3

Deterministic, no model.

Produces two lists for the ledger and the Prohibitions Gate.

### Hard hits

Gate fails until fixed:

- em dash in article prose
- first-person singular pronoun outside quoted material when the use is narrator voice rather than a legitimate quoted source
- templated contrast explicitly prohibited by Voice Bible v0.8
- mascot name or mascot-voice marker in article body
- `[MEDIA: candidate_id]` whose candidate ID is not in the resolved candidate set for this article version
- a quoted string that does not map to the quote bank, routed to verification for confirmation
- a claim-bearing number not mapped to statistics or locked claims, routed to verification rather than automatically declared false

### Review flags

Surfaced, not automatically failed:

- watchlist phrases
- bullet or list formatting
- bold run-in labels
- rhetorical-question reliance
- one-sentence-paragraph runs
- fragment density
- word count outside target band
- headline syntax match against recent headlines
- suspicious repeated paragraph openings

The mechanical scanner finds patterns.

It does not decide whether a non-hard pattern is guilty.

## 6. Verification: P4 Evidence Auditor and deterministic E1

The Evidence Auditor sees:

- the frozen article
- Research Packet
- source ledger

It does not see the beat plan, specialist reports, cold scores, or EIC diagnosis.

Its job is mapping, not literary judgment.

The Evidence Auditor maps each article claim to the packet and emits the verification inputs required by Master Scoring Rubric v1.2.

```text
verification_report:
  article_version
  verification_report_version

  claims_found:
    - claim_text
      location
      mapped_packet_claim_id | EXTERNAL
      packet_state
      prose_state
      load_bearing: yes | no
      result:
        ok | wrong_state | material_error |
        external | prohibited

  quotes:
    - text
      location
      quote_bank_id | EXTERNAL
      verbatim_match: yes | no
      source

  statistics:
    - figure
      location
      packet_stat_id | EXTERNAL
      authoritative_match:
        yes | no | discrepancy_noted

  hindsight_leaks:
    - passage
      hazard_id

  deterministic_inputs:
    fabrication_count
    invented_source_count
    invented_quote_count
    prohibited_claim_asserted_count

    external_load_bearing_claim_count
    load_bearing_state_mismatch_count
    load_bearing_material_error_count

    non_load_bearing_external_unresolved_count
    non_load_bearing_state_mismatch_count
    non_load_bearing_material_error_count

    quote_verbatim_mismatch_count
    statistic_mismatch_count

    metadata_only_warning_count

  E1_computed:
    exact output of the shared Master Scoring Rubric v1.2
    deterministic verification function

  fixes_required:
    - location
      what
      from_packet_claim_id

  escalations:
    claims the auditor believes the Research Packet itself may have wrong;
    routed to a research follow-up loop, never fixed by the writer
```

### Deterministic E1 rule

Production does not define a second set of E1 bands.

After model-assisted claim mapping, the shared deterministic function from Master Scoring Rubric v1.2 computes E1 from `deterministic_inputs`.

Cold scorers import that E1.

They do not rescore truth.

If the Evidence Auditor believes the packet itself is wrong, the run routes to research before prose revision.

## 7. The diagnostic bench: P5 and P5V

The editorial bench contains eight specialists. The Visual Editor is a ninth advisory specialist outside the scored article dimensions. The Evidence Auditor is the separate truth audit in P4.

The EIC therefore receives ten diagnostic inputs before cold scores:

- Evidence Auditor
- eight editorial specialist reports
- Visual Editor

Each editorial specialist receives:

- frozen article
- Research Packet
- beat plan
- assigned register and mode
- its own compact module

Each is blind to every other report and to all scores.

The Visual Editor additionally receives the resolved visual-candidate set and media markers.

### 7.0 Specialist report contract

```text
specialist_report:
  specialist
  article_version
  module_version

  dimensions_owned: []

  findings:
    - id
      severity: critical | major | minor
      location
      what
      why_it_matters
      evidence
      recommended_fix
      fix_type:
        structural | prose | factual | cut | visual

  strengths:
    - location
      what
      protection_recommendation:
        none | PROTECT_EXACT | PROTECT_SUBSTANCE | PROTECT_FUNCTION

  recommended_scores:
    dimension: score with one-line justification
    advisory only; cold scorer decides judgment dimensions

  verdict_on_mandate:
    strong | acceptable | needs_revision | failing

  one_sentence:
    single most important thing about this article from this seat
```

### Protection meanings

`PROTECT_EXACT`: rare. Exact wording itself is unusually valuable and should remain byte-identical unless the EIC explicitly resolves a conflict.

`PROTECT_SUBSTANCE`: preserve the fact, image, joke, observation, emotional beat, or idea. Minimal wording changes are allowed when continuity requires them.

`PROTECT_FUNCTION`: preserve what the passage or beat accomplishes, though structure or wording may change.

Locked facts remain governed by the Research Packet and are not a prose-protection category.

### 7.1 Story Doctor

Owns A2 Story, A3 Human Stakes, A5 Originality.

Questions:

- Is there a real hinge or bounded before-and-after?
- Who or what carries it?
- Are the human stakes concrete?
- If the carrier is a collective, is it genuinely the subject or a missing protagonist?
- Does the piece materially depart from the standard telling?
- Could this be reduced to a reference entry?

Does not comment on prose style.

### 7.2 Hook and Opening Editor

Owns A1 Hook and the first 250 words.

Questions:

- Why does someone click?
- Why do they read the second paragraph?
- Is the hook fact in the first paragraph unless a justified exception exists?
- Is the outcome given away when it should be preserved, or hidden when the outcome itself is the hook?
- Is there throat clearing?
- Is the first person introduced as who they were then?

The report stops at word 250 except to identify where the hook actually appears if later.

### 7.3 Momentum and Structure Editor

Owns B1 Momentum, B2 Structure.

Reads the beat plan against the draft.

Questions:

- Where does the piece stall, and why?
- Is each beat's pull delivered?
- Is context placed where the reader has the question?
- Is the hinge slowed without being preempted?
- Do section headers help if present?
- Is the architecture visible as machinery?
- Did approximate beat weights turn into a repetitive template?

Names every stall by location and proposes structural fixes such as move, cut, merge, compress, or re-sequence, not sentence polish.

### 7.4 The Two Readers

Owns A4 Discovery and B3 Accessibility.

Reads twice.

**General sports reader:** Can they feel the stakes early? Is a specialized rule explained only when needed? Is anyone made to feel like an outsider?

**Lifelong fan of the sport:** What did they actually learn? Is the discovery load-bearing or decorative? Is the supposed discovery merely the first search result or standard fan knowledge?

Two sub-reports inside one contract.

### 7.5 Voice and Prose Editor

Owns C1 Voice, C2 Prose.

This is the only editorial specialist that receives:

- Voice Bible v0.8 quarantined diagnostics
- P3 mechanical review flags

Questions:

- Does it sound like a fan who did the reading?
- Is the register right for this material?
- Does the register change naturally rather than through announcement?
- Are there interchangeable sentences?
- Has any device become a metronome?
- Does mascot personality leak into body copy?
- Which watchlist hits are actually guilty in context?
- Which flags are innocent?
- Does the prose feel written rather than generated?

Proposes prose fixes only, never structural fixes.

Dismissed flags are logged so the scanner can later be tuned.

### 7.6 Hindsight Auditor

Owns C3 Restore Uncertainty.

Receives the Belief File and hindsight-hazards list.

Questions:

- Does anyone know something they could not know yet?
- Does the prose use a later title, nickname, scandal, diagnosis, or outcome before it existed?
- Is expectation reconstructed from contemporaneous evidence?
- Is a plausible alternative concrete where one genuinely existed?
- In inevitability mode, is the prose manufacturing doubt?

Reports N/A with the logged Research Standard reason when the mode was validly skipped.

### 7.7 Landing Editor

Owns D1 Emotional Payoff, D2 Sports Magic, D3 Ending.

Questions:

- Does the hinge land without emotion words doing the scene's work?
- Is reaction shown where the story gives us one?
- Is sport alive on the page through the appropriate story material, with no mandatory crowd beat?
- Does every outward thread return to the game, fan, athlete, team, or competition?
- Does the piece pass the different-industry test?
- Does the ending perform the function architecture chose?
- Would the piece be better if the final paragraph vanished?

Names the exact sentence where a swell begins if one does.

### 7.8 Contagion and Package Editor

Owns B4 Entertainment, D4 Contagion, headline, and subtitle.

Questions:

- Would anyone send this?
- What would they say when they did?
- What facts, arguments, images, feelings, or lines escape the piece?
- Is it a pleasure in its assigned register or dutiful?
- Is the headline concrete and intriguing without telling the reader how impressed to be?
- Does the subtitle orient without merely repeating the title or needlessly spoiling the payoff?
- Does the headline repeat recent syntax?

May propose up to three alternative headline/subtitle pairs.

### 7.9 Visual Editor: advisory

Owns no scored article dimension.

Uses the Visual Media OS.

Questions:

- Is every media marker tied to a real narrative function?
- Is any visual decorative or premature?
- Does the selected candidate actually satisfy its visual need?
- Is the hero the strongest available package image or object?
- Did revision move the prose away from the visual?
- Is any constructed visual insufficiently backed by packet data?

Recommendations are candidate swaps, marker moves, visual-need changes, or packaging flags.

### 7.10 Evidence Auditor

Section 6.

Owns E1 and Truth Gate through deterministic verification.

It is not an editorial style seat.

### Rubric coverage

The eight editorial specialists cover A1 through D4 without score overlap:

- A1: Hook and Opening
- A2, A3, A5: Story Doctor
- A4, B3: Two Readers
- B1, B2: Momentum and Structure
- B4, D4: Contagion and Package
- C1, C2: Voice and Prose
- C3: Hindsight
- D1, D2, D3: Landing

E1 comes from deterministic verification.

The Visual Editor advises package quality without entering the article profile.

## 8. Cold scoring: P6

Cold scoring is split-phase so verification does not sit unnecessarily on the critical path.

### Phase A: judgment scoring

Two cold scorers from different model families independently score the frozen article on judgment dimensions A1 through D4 under Master Scoring Rubric v1.2.

They receive:

- frozen article
- Research Packet
- story mode and register

They do not receive:

- verification report
- bench reports
- each other's scores
- EIC diagnosis
- prior-round scores
- revision history

They do not score, estimate, or speculate about E1.

Each Phase A record is bound to the frozen article version and content hash.

### Phase B: deterministic finalization

When P4 verification finishes, a deterministic score assembler:

1. confirms the verification report belongs to the same frozen article version and hash
2. imports the deterministic E1 exactly as emitted
3. attaches the truth-gate result
4. preserves the two scorers' A1 through D4 judgments unchanged
5. writes two finalized score records to the ledger

No model may override E1 upward or downward.

A disagreement of 1.5 or more on any non-E1 gating dimension is flagged.

Under the conservative launch policy, the lower gating score governs.

The EIC receives both finalized records.

## 9. The EIC conductor: P7

The EIC receives:

- frozen article
- Research Packet
- beat plan
- resolved visual candidates
- mechanical scan
- verification report
- eight editorial specialist reports
- Visual Editor report
- both cold score records

The EIC is the only editorial role that sees everything from the current round.

It produces a verdict recommendation and, if REVISE, exactly one coherent revision brief.

### 9.1 What the EIC does, in order

1. **Gates first.** If Truth fails on a load-bearing claim and verification escalated to research, pause for research before prose revision. Editing a paragraph whose facts may change is waste.
2. **Adjudicate disagreement.** When specialists conflict, decide and explain why. When cold scorers disagree on a gating dimension, note that the lower governs and whether diagnostic evidence supports the concern.
3. **Separate critical from polish.** Re-tier findings into must fix, should fix, and may fix. Gates, load-bearing facts, structural failures, meaningful hindsight leaks, and swell endings usually become must-fix. Optional polish never overrides protected work.
4. **Find root causes.** Ten findings may share one cause. Name the cause and the smallest coherent fix rather than forwarding ten symptoms.
5. **Order the work.** Truth, then structure, then sound, then words. Do not polish a paragraph that is about to move or disappear.
6. **Protect strengths.** Compile protections from specialist recommendations plus architecture-level protected intent and locked facts. Assign the correct protection type. Resolve any conflict between a must-fix and a protected item explicitly.
7. **Choose the revision mode.** Targeted Patch, Structural Revision, Polish, or the one-time Rearchitecture + Redraft escape hatch defined below.
8. **Name targets.** State which dimensions must move and to what approximate level so delta reporting can judge whether the revision worked.
9. **Protect the article's best thing.** The revision brief must name the single feature of the current version that makes the piece worth saving, if one exists.

### 9.2 Revision brief

```text
revision_brief:
  brief_id
  from_version
  to_version
  eic_model_id

  verdict_recommendation:
    REVISE

  gate_status: []

  root_causes:
    - cause
      evidence_from_reports
      fix

  must_fix:
    - id
      location
      instruction
      fix_type
      source_finding_ids
      from_packet_claim_ids

  should_fix: []
  may_fix: []

  protected:
    - location_or_claim_id
      protection_type:
        PROTECT_EXACT | PROTECT_SUBSTANCE | PROTECT_FUNCTION
      what
      why

  locked_facts_reminder:
    pointer to Locked Claims List

  order_of_work:
    truth | structure | sound | words

  revision_mode:
    targeted | structural | polish | rearchitecture_redraft

  target_dimensions:
    - dimension
      current
      target

  register_reminder

  do_not:
    specific temptations this piece has shown

  best_thing_to_preserve:
    one sentence

  one_paragraph_to_the_writer:
    plain prose: what is good, what is wrong, what to do
```

The Writer receives the brief, current article version where the mode requires it, Research Packet, and Kernel.

It never receives the raw specialist reports.

## 10. Revision: P8 Writer modes

One Writer role operates under the same Kernel and packet discipline.

### Full draft

Section 3. Used for ORIGINAL and for the fresh prose pass inside an authorized Rearchitecture + Redraft.

### Targeted patch

Receives exact locations and instructions.

Edits only those locations plus the minimum surrounding text required for continuity.

Every changed paragraph is reported.

### Structural revision

Rebuilds only the beats named in the revision brief.

Carries unaffected beats forward except where continuity or a must-fix requires a local adjustment.

Reports changed beats and paragraphs.

### Polish

Sentence-level only.

No paragraph is moved, added, or removed unless the EIC explicitly authorizes a microscopic continuity repair.

No claim changes epistemic state.

### Rearchitecture + Redraft

Exceptional escape hatch.

Permitted once per run only when the EIC concludes all four are true:

1. the underlying Story Brief remains strong
2. the Research Packet remains strong enough to support the story
3. the primary failure is architecture or draft execution rather than the premise itself
4. patching would preserve too much of a broken shape

This mode is not generic "try again."

Process:

1. Freeze and keep the failed article and original beat plan.
2. EIC creates a rearchitecture section inside the revision brief naming the failed structural assumptions and what must change.
3. Story Architect receives the Research Packet, current beat plan, Narrative Architectures, and EIC architecture diagnosis. It does not receive raw specialist reports.
4. Story Architect produces `BEAT_PLAN_REVISED_01` with new visual needs if necessary.
5. Visual Research reruns only for new or changed visual needs.
6. Writer receives a fresh Drafting Packet built from the revised architecture plus a compact `carry_forward_assets` list containing approved PROTECT_EXACT wording and PROTECT_SUBSTANCE material from the failed version. The Writer does not receive the old article as a template.
7. Writer produces the next `ARTICLE_REVISED_nn` as a fresh draft from the new plan.
8. The new version goes through the full current-version diagnostic graph from scratch.

Rearchitecture + Redraft counts as a substantive revision against the loop budget.

A second rearchitecture is not allowed in the same run.

If the rearchitected version still fails because the story has no workable shape, KILL.

### Rearchitecture and convergence semantics

A rearchitecture replaces the passage structure rather than patching it. Prior passage-level findings therefore cannot be treated as though the same locations still exist.

When a Rearchitecture + Redraft occurs:

- prior passage-level editorial findings are marked `RETIRED_BY_REARCHITECTURE`, not `CLOSED`
- unresolved truth, legal, packet, and source issues carry forward normally
- architecture-level failure reasons and dimension-level weaknesses remain in the ledger for comparison
- the delta from the pre-rearchitecture article to the new article is computed at the dimension and gate level, not by attempting location-by-location closure
- the rearchitected article begins a fresh specialist-finding sequence for the three-consecutive-rounds escalation rule
- findings on the new version receive new finding IDs even when they resemble an old symptom
- protection still applies to any `PROTECT_EXACT`, `PROTECT_SUBSTANCE`, or `PROTECT_FUNCTION` asset explicitly carried into the fresh Drafting Packet

The rearchitecture counts as a substantive revision, but it resets the consecutive-finding streak because the relevant passages and shape have been superseded.

This prevents a stale finding from being counted as unresolved merely because the new article addresses the same dimension in a different structure.

### Patch semantics and protection

The default revision principle is **patch, do not regenerate**.

But protection is typed:

- `PROTECT_EXACT` must remain byte-identical unless the EIC explicitly resolves a conflict.
- `PROTECT_SUBSTANCE` may receive minimal wording changes for continuity, but its fact, image, joke, observation, or emotional work must remain.
- `PROTECT_FUNCTION` may move or be recast, but the function must survive.

Only exact protection is verified mechanically by byte diff.

Substance and function protection are checked in re-review and delta analysis.

A targeted patch that changes far more of the article than the brief authorized is rejected and rerun. The runtime may use a configurable diff-size warning, but no fixed percentage belongs in doctrine.

Revision may not introduce a factual claim outside the packet.

If a necessary fix requires a fact the packet lacks, insert:

```text
[NEEDS: description]
```

and route to a research follow-up loop.

The writer does not guess.

## 11. Re-review: P9 and convergence

The revised version is frozen and re-enters the P3-P7 dependency graph.

Every specialist and cold scorer is blind to prior reports, prior scores, and prior verdicts.

The EIC alone sees current and prior rounds for delta analysis.

For ordinary targeted, structural, and polish revisions, a finding is closed only when the originating specialist no longer raises it on the new version, or when the specialist's mandate confirms that the finding has become inapplicable because the relevant passage no longer performs that function.

The EIC may not simply declare a still-present finding closed.

After Rearchitecture + Redraft, the special convergence rule above applies: prior passage-level findings are retired, not closed, and the new version begins a fresh finding sequence. Dimension and gate deltas still compare the pre- and post-rearchitecture versions.

Delta analysis records:

- targeted dimensions that improved or failed to improve
- protected dimensions that regressed
- protected exact wording changed or preserved
- protected substance/function preserved or lost
- untargeted dimensions that moved unexpectedly
- new findings introduced by revision

### Loop bounds

Runtime-configured default:

- up to two substantive revisions
- one of those may be the single Rearchitecture + Redraft
- a third revision is permitted only in Targeted Patch or Polish mode for a very small remaining set of must-fix items

If the piece has not reached PUBLISH after the bound, the EIC issues:

- KILL
- or `ESCALATE_TO_HUMAN` when every remaining issue is one the human could reasonably overrule or directly fix

The same materially unchanged finding raised in three consecutive rounds within one continuous architecture lineage triggers automatic escalation or kill. A Rearchitecture + Redraft starts a new finding lineage while preserving dimension-level history.

The system does not attempt the same failed fix indefinitely.

### Fail-closed statuses

```text
RESEARCH_BLOCKED
ARCHITECTURE_FAILED
LOOP_EXHAUSTED
LEGAL_FLAGGED
VISUAL_BLOCKED
ESCALATE_TO_HUMAN
```

A run in any fail-closed status terminates with the full ledger and last frozen version.

Nothing publishes automatically.

## 12. The run ledger

Per run, the ledger holds:

- Story Brief version
- Research Packet version
- every beat plan version
- Visual Research candidate sets and resolutions
- every article version with content hash
- every mechanical scan
- every verification report and deterministic E1 input set
- every editorial specialist report
- every Visual Editor report
- every cold-score record with version metadata
- every EIC verdict and revision brief
- every diff and exact-protection verification
- every substance/function protection check
- every delta report
- every research follow-up trigger and result
- every visual follow-up trigger and result
- every status transition with timestamp and cause

The ledger is the audit trail for a published piece and the diagnostic record for a killed one.

It also feeds the exemplar corpus:

- Tier A: whole approved pieces
- Tier B: approved passages
- Tier C: real failed passages and critical findings
- Tier D: human final-gate edits and before/after notes

## 13. Packaging: P10 and the publication package

Packaging is assembled from the final frozen article, ledger, and final media manifest.

Deterministic assembly handles fields and IDs.

The Packager writes concise human-facing summaries, captions, newsletter-note draft, and distribution notes.

Packaging does not invent a new editorial thesis or factual claim.

The human should not need to reconstruct how the article was made.

```text
publication_package:
  brief_id
  final_article_version
  run_id

  title_final
  subtitle_final

  article_final:
    clean prose with media markers resolved to manifest references

  scorecard_final:
    full Master Scoring Rubric v1.2 record

  scorecard_original
  delta_original_to_final:
    per dimension

  eic_verdict
  sing_check_sentence

  factual_confidence_report:
    E1
    deterministic_inputs
    plain_language_summary

  source_ledger:
    every source actually used or relied upon,
    with retrieved URL or source identifier where available,
    source-fitness metadata,
    claim_ids supported,
    and epistemic-state relationships

  unresolved_caveats:
    []
    target: empty
    each item states what would resolve it

  legal_flags:
    []
    must be empty or explicitly handled at the human gate

  media_manifest:
    final Visual Media OS artifact

  visual_readiness:
    VISUAL_READY | VISUAL_NEEDS_HUMAN | VISUAL_BLOCKED

  mascot_presentation:
    newsletter_note_draft
    presentation_mode:
      standard | quiet | omitted

  archive_metadata:
    sport
    teams
    people
    city
    country
    era
    hinge_year_or_period
    category
    archetypes
    register
    format
    word_count
    contagion_type
    natural_fanbase
    calendar_windows
    living_subject
    spinoff_leads_filed

  distribution_notes:
    tribal_seeding_targets
    nearest_calendar_window
    contagious_units_in_one_sentence_each

  run_summary:
    one paragraph on what the human should inspect first,
    what was hardest, and what remains unresolved
```

There is no undefined external "Sources block standard" dependency. If a public-facing Sources block is later adopted, it must receive its own explicit specification. Until then, the package carries the complete machine/human source ledger described above.

### Visual package rule

Visual Readiness is not part of the seventeen-dimension article score.

- `VISUAL_READY` can proceed to the human gate normally.
- `VISUAL_NEEDS_HUMAN` can proceed to the human gate because human sourcing/licensing is intentionally part of the final workflow.
- `VISUAL_BLOCKED` is fail-closed until the human or system resolves the missing visual function or explicitly determines it is nonessential.

## 14. Runtime implications

### Roles

Model roles include:

- Story Architect
- Visual Research
- Writer, four task modes plus the rearchitecture-redraft path
- Evidence Auditor
- eight editorial specialists
- Visual Editor
- two cold scorers
- deterministic cold-score finalizer that imports E1
- EIC
- Packager

Mechanical scan, hashing/freeze, deterministic E1 calculation, schema checks, and most package assembly are deterministic.

Do not optimize the architecture around a vanity count of model roles. Optimize for clean responsibility, blindness, and useful independence.

### Blindness

- Editorial specialists receive no other specialist report and no scores.
- Visual Editor receives no editorial reports or scores.
- Cold scorers receive no specialist report, no prior score, and no revision history.
- Writer receives only the packet, Kernel, current article when its revision mode requires it, and the EIC revision brief. It never receives raw bench reports.
- Evidence Auditor receives no beat plan or editorial diagnosis.
- Story Architect in a rearchitecture receives the EIC architecture diagnosis, not the raw report pile.
- EIC receives everything needed for adjudication.

### Model routing

- Cold scorers must use different model families while the dual-scorer launch policy remains active.
- Evidence Auditor and Writer should be different model families where routing permits.
- Myth audit or contradiction search independence remains governed by the Research Standard.
- EIC may use the strongest available model regardless of family.

### Concurrency

Use the dependency waves in section 1.

Cold scorers may begin A1 through D4 judgment immediately after freeze. Do not finalize their score records until P4 E1 exists and article-version/hash alignment has been verified.

Do not launch Voice and Prose before P3 flags exist.

### Fail closed

Every stage writes its required artifact to the ledger before a dependent stage begins.

A stage that cannot produce or validate its contract fails closed.

The drafting prompt, specialist modules, EIC prompt, Packager prompt, verification mapper, and deterministic E1 function are versioned in the prompt/runtime pack.

This document is their governing standard. The full-draft prompt in section 3 is canonical text.

# Change Log

## v1.2 - Batch Three

- Split cold scoring into a Phase A judgment pass on A1 through D4 that can run immediately after freeze and a deterministic Phase B finalization that imports E1 after verification.
- Removed verification from the cold scorers' judgment-phase inputs and required version/hash binding before E1 can be stitched into finalized score records.
- Added explicit Rearchitecture + Redraft convergence semantics: prior passage-level findings are retired rather than falsely closed, dimension/gate deltas carry forward, and consecutive-finding escalation restarts on the new architecture lineage.
- Clarified that truth, legal, packet, and source issues survive rearchitecture normally.
- Updated inheritance to Narrative Architectures v1.2 and Visual Media OS v1.2.
- Preserved dependency-wave review, typed protection, deterministic E1, one-time rearchitecture, blind re-review, EIC root-cause adjudication, and fail-closed packaging.

## v1.1 - Batch Three

- Updated inheritance to Batch Two v1.2 and Batch Three Narrative/Visual v1.1.
- Replaced the impossible P3/P4/P5/P6 all-at-once concurrency rule with dependency waves.
- Added P1.5 Visual Research and separated architecture visual needs from resolved candidate IDs.
- Integrated the Visual Editor as a formal advisory diagnostic input and removed stale nine-report/fifteen-role counting logic.
- Replaced the blanket full-regeneration-is-KILL rule with one bounded Rearchitecture + Redraft escape hatch per run.
- Added typed protection: PROTECT_EXACT, PROTECT_SUBSTANCE, PROTECT_FUNCTION.
- Removed fixed byte-identical protection except for PROTECT_EXACT and removed the fixed 60-percent diff rule from doctrine.
- Replaced the stale E1 bands with the exact deterministic input contract consumed by Master Scoring Rubric v1.2.
- Changed writer-facing "tier" language to `epistemic_state` and natural prose behavior.
- Added Visual Readiness to the publication package and fail-closed statuses.
- Simplified mascot packaging to newsletter note plus standard/quiet/omitted presentation mode.
- Removed the undefined Sources block dependency and defined the source-ledger content directly.
- Preserved immutable versions, blind diagnosis, EIC root-cause adjudication, truth-structure-sound-words ordering, patch-first revision, full cold re-review, convergence, loop bounds, and ledger learning.

## v1.0 - Batch Three

Initial version. Production loop; drafting packet and prompt; freeze; mechanical scan; verification; specialist bench; dual cold scorers; EIC conductor; revision loop; convergence; fail-closed statuses; run ledger; publication package; role and blindness map.
