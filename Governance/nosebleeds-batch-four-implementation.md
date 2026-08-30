# Nosebleeds Batch Four (Simplified): Implementation Specification

**Version 2.1** - supersedes Runtime Architecture v1.0 through v1.2 and Prompt Pack v1.0 through v1.2 wherever they conflict; inherits Batches One through Three editorial doctrine unchanged.

## 1. System at a glance

Two n8n workflows. Ideation (Sunday 12:00 PM Pacific, plus manual) and Generation (Sunday 2:00 PM Pacific, plus manual). One Google Sheet, the editorial queue, human-readable. One Google Drive tree. Nosebleeds > Unpublished > [Idea ID] - [Working Title] , holding two permanent documents per article: 01 - Research and 02 - Final Article .

One GitHub Pages frontend, the Nosebleeds Console, cloned from the Pretty Penny Console and rebranded. One GitHub repo holding the canonical markdowns, the prompts, and the frontend. Roughly eleven AI calls per article (fourteen with a second revision round), zero human intervention until the final article is waiting. What is deliberately not built: leases, lineage, schema registry, context manifests, module compilation, artifact versioning, diff validators, per-node Drive artifacts, automated learning. The Sheet’s Status column is the only coordination mechanism, and the n8n execution

history is the only intermediate record.

### 1.1 Universal search-call preamble

`Prompts/universal-preamble.md` is prepended by the workflow to the **search-enabled calls only**: I1 Candidate Generator, G1 Research Pass 1, and G2 Research Pass 2. It is not prepended to I2, G3 through G12, or any non-search model call. The preamble exists only to enforce source/instruction separation and anti-fabrication behavior during retrieval.

## 2. The Google Sheet

Spreadsheet `Nosebleeds`, tab `Queue`. One row per idea.

| Column | Type | Written by | Notes |
|---|---|---|---|
| Idea ID | text | Ideation | `NB-YYYYMMDD-nn` |
| Working Title | text | Ideation | Nosebleeds headline taste; provisional |
| Core Premise | text | Ideation | 1 to 3 sentences: the actual story |
| Hook | text | Ideation | The specific fact, contradiction, decision, number, or image that earns the click |
| Why It Works | text | Ideation | Human stakes, discovery, Nosebleeds fit, emotional or entertainment potential |
| Sport | text | Ideation |  |
| Story Type | text | Ideation | `canon`, `unknown-known`, `discovery`, `myth-vs-record`; plus one archetype word |
| Human Carrier | text | Ideation | Named person, or the documented collective and why it is the subject |
| Source Leads | text | Ideation | Up to five URLs actually opened during ideation, one per line |
| Idea Score | number | Ideation | Evaluator's 0 to 10 judgment |
| Priority | number | Ideation, human | 1 highest. Ideation sets 3 by default; human edits freely |
| Status | text | workflows, human | See section 3 |
| Drive Folder | url | Generation |  |
| Final Article | url | Generation |  |
| Final Score | number | Generation | Cold review overall judgment, optional |
| Created Date | date | Ideation |  |
| Generated Date | date | Generation |  |
| Human Notes | text | human | Free-form human operational/editorial notes |

Three columns beyond the minimal queue materially help editorial judgment: Human Carrier, Final Score, and Generated Date.

## 3. Statuses

READY , HOLD , GENERATING , READY_FOR_REVIEW , PUBLISHED , REJECTED , ERROR .

Ideation writes new rows as READY . Generation selects the first row where Status is READY , ordered by Priority ascending then Created Date ascending, and immediately sets it to GENERATING . On success, Generation sets READY_FOR_REVIEW and fills Drive Folder, Final Article, Final Score, Generated Date. On an unrecoverable failure, Generation sets ERROR , writes a one-line reason to Human Notes (appending, never overwriting), and stops. Whatever was saved to Drive stays. HOLD , PUBLISHED , REJECTED are human-set. HOLD means do not generate.

A row in GENERATING for more than six hours is assumed stuck; the human resets it to READY or ERROR from the Console. No automatic recovery at launch.

## 4. Ideation Workflow

Trigger: Sunday 12:00 PM Pacific, plus a Manual Trigger from the Console webhook. Purpose: put only high-quality Nosebleeds story conceptions into the Sheet. Twenty to thirty candidates in, five to ten rows out is the expected ratio, and zero rows out is an acceptable result.

### 4.1 Node sequence

1. **Trigger.** Schedule or webhook.
2. **Read Sheet.** Pull every row's Working Title, Core Premise, Sport, Story Type, Status, and Created Date. This is the slate context.
3. **Fetch doctrine from GitHub.** Brand Bible and Ideation and Selection Standard.
4. **Build slate note.** Code node, no model. From the Sheet: counts by Sport and Story Type over the last twelve rows, the last ten Working Titles, and all Working Titles/Core Premises for dedup. Output one short text block.
5. **AI: Candidate Generator.** OpenAI with web search. Receives Brand Bible, Ideation Standard, and slate note. Produces 20 to 30 story conceptions. Each includes premise, hook, hinge, carrier, why readers care, sport, story type, source leads actually opened, `hook_source_url`, and `hook_source_support`.
6. **AI: Cold Idea Evaluator.** Anthropic, no search. Receives Ideation Standard, slate note, and candidate array. Does not receive generator self-assessments. Scores each candidate and returns only ideas at or above the 8.5 launch bar that it would be genuinely exciting to spend a full generation run on.
7. **Dedup.** Code node. Drop any passed candidate whose Working Title or Core Premise substantially matches an existing row using a simple normalized token-overlap threshold. Log the drops.
8. **Write rows.** Append each survivor as `READY`, Priority 3, Created Date now, and generated Idea ID. Preserve Source Leads from the generator card.
9. **Notify.** Optional email or Console flag: `Ideation added N ideas.`

The Candidate Generator is the only search-enabled call in Ideation. The evaluator is deliberately a different provider and remains search-blind, using the generator's retrieved hook source and support sentence as evidence rather than re-researching the candidate.

### 4.2 Why the evaluator sees the slate note but has no quota

Slate awareness is context. The evaluator may prefer an underrepresented sport or type between two candidates of comparable quality and must not pass a weaker candidate to fill a gap. The note is one paragraph; it is not a rule.

### 4.3 Idea Score

One number, 0 to 10 in half points, the evaluator’s judgment of whether this is a real Nosebleeds story, formed against the fourteen dimensions in the Ideation Standard but not computed from them. The evaluator names the two strongest and the single weakest dimension in its reasoning. Passing floor at launch: 8.5. The floor is a config value in the prompt; adjust only after comparing the first month of ideas against the human’s PUBLISHED and REJECTED decisions. The evaluator should pass an idea only if it would be genuinely exciting to spend a full Nosebleeds generation run on. Three exceptional ideas are better than nine merely good ones.

### 4.4 Structured outputs

Generator returns { candidates: [ { working_title, core_premise, hook, hook_source_url, hook_source_support, narrative_hinge, human_carrier, why_readers_care, sport, story_type, source_leads: [urls] } ] } . Evaluator receives the source URL and support sentence but remains search-blind. Evaluator returns { passed: [ { ...same fields, idea_score, why_it_works } ], rejected: [ { working_title, reason } ] } . Parse with the n8n

structured-output parser; on parse failure, retry the call once with the parse error appended, then stop the run with a notification. Nothing is written on a failed run.

## 5. Generation Workflow

Trigger: Sunday 2:00 PM Pacific, plus a Manual Trigger from the Console webhook (“Generate Next Story”). Purpose: turn the highest-priority READY idea into a deeply researched, polished Nosebleeds article. One story per run.

### 5.1 The commitment rule

Ideation is where ideas are killed. Generation is where accepted ideas are made great. Research may change the hook, the hinge, the carrier, the register, and the thesis. It may not decide the story is not worth writing. The post-research outcome is CONTINUE or REFRAME, and the workflow proceeds either way. Only operational failures or a genuinely impossible premise with no honest adjacent story produce ERROR, and those are rare.

### 5.2 Node sequence

1. **Trigger.** Schedule or manual webhook.
2. **Select story.** Read Sheet, filter `Status = READY`, sort Priority ascending then Created Date ascending, take the first. If none, end quietly.
3. **Claim.** Set that row to `GENERATING`.
4. **Fetch doctrine from GitHub.** Research Standard, Voice Kernel, Narrative Architectures, Voice Bible calibration passages, Master Scoring Rubric, Production and Review Standard EIC section, Visual Media OS functions/rights sections, and Brand Bible identity. Heading extraction is a simple Code node; if a heading is not found, pass the whole document.
5. **Create Drive folder.** `Nosebleeds/Unpublished/[Idea ID] - [Working Title]`. Write its URL to the Sheet.
6. **AI: Research Pass 1, Reconstruction.** OpenAI with web search. Research landscape, standard telling, hook verification, hinge, chronology, people as they were then, authoritative statistics, verbatim quotes with URLs, rules/context, texture, visual leads actually found, human consequences, and ending material. Tag claims by epistemic state.
7. **AI: Research Pass 2, Belief and Adversary.** OpenAI with web search in fresh context. Receives the idea and Pass 1 claim list without Pass 1 state conclusions. Reconstruct what people knew and expected before the hinge; identify doubters/believers; test inevitability; trace myths; deliberately search for contradiction; record opposing accounts.
8. **AI: Research Compiler and Thesis.** Anthropic, no search. Reconcile both passes under the Research Standard. Apply fact lock, preserve contradictions, write Claims We Should Not Make, decide `CONTINUE` or `REFRAME`, write the Final Story Thesis, and compile `01 - Research`.
9. **Guard.** Code node. If there is no verified hook and no verified alternative hook supporting a truthful adjacent reframe, set `ERROR` with `no verifiable hook` and stop. This should be rare.
10. **Save `01 - Research`.** Write the compiled Research document to the article Drive folder as a Google Doc.
11. **AI: Writer, first draft.** Anthropic. Receives the idea context, Final Story Thesis, Research document, Voice Kernel, Narrative Architectures, two or three register-matched calibration passages, and Brand identity. Output title, subtitle, body, and `[MEDIA: description]` markers where a visual would prove, show, or explain.
12. **AI: Reviewer A, Story and Reader Experience.** Anthropic, fresh context. Receives draft, Research document, Rubric.
13. **AI: Reviewer B, Voice, Nosebleeds, Magic.** Anthropic, fresh context. Receives draft, Belief File/Hindsight Hazards, Voice Bible, Kernel, Rubric.
14. **AI: Reviewer C, Truth and Evidence.** Fresh context, preferably a provider different from the Writer when quality testing supports it. Receives draft, Research document, Research epistemic-state guidance, and canonical E1 rubric bands.
15. **AI: EIC.** Anthropic, strongest tier. Receives draft, Research document, Reviewers A/B/C, Rubric, Production Standard EIC section. Produces one Revision Brief.
16. **AI: Writer, revision.** Anthropic. Receives current draft, Research document, Revision Brief, Kernel. If the EIC calls for architecture regeneration, rewrite from the Research document rather than blindly patching.
17. **AI: Cold Final Review.** Fresh context. Receives revised article, Research document, Rubric, Brand identity. Scores all seventeen dimensions, names the strongest reason not to publish, lists `strengths_to_preserve`, and returns `PASS | REVISE | FAIL`.
18. **Branch on verdict.** `PASS` goes to Packaging. First-round `REVISE` or `FAIL` triggers EIC round 2, Writer revision 2, and Cold Final Review 2. A second-round `REVISE` or `FAIL` does not become a workflow error: continue to Packaging with the best current article and append a warning to Human Notes that the automated publication bar was not cleared, including the strongest reason. The human decides.
19. **Maximum two revision rounds.** Enforced by the branch structure, not a counter.
20. **AI: Packaging.** Anthropic. Generates five title/subtitle pairs and selects one. Recommends hero and supporting visuals from the Research visual leads where possible. Optional house-style treatment prompts use the locked Nosebleeds painterly gouache + subtle ink-line + restrained halftone/print texture + warm paper treatment, leaning deep navy, faded athletic red, warm cream, white, and dark golden yellow. Ordinary article art gets no baked-in logo or heavy border.
21. **Assemble `02 - Final Article`.** Code node. Recommended title, subtitle, article body, resolved Visuals block, alternate title pairs, and Sources block.
22. **Save `02 - Final Article`.** Write Final Article URL, Final Score, Generated Date, and `READY_FOR_REVIEW` to the Sheet. If the second Cold Review did not clear the bar, preserve the warning in Human Notes.
23. **Notify.** `[Working Title] is ready for review.`

AI calls: 3 research, 1 draft, 3 reviewers, 1 EIC, 1 revision, 1 cold review, 1 packaging = 11. A second revision round adds 3, for 14 maximum.

### 5.3 The one added node, and why

Step 7, Research Pass 2 as a fresh context, is the only place this specification adds a call beyond the minimum. Restore-uncertainty and the myth audit are the two things a single research pass reliably under-works, because a model that has just verified a claim is a poor adversary to it. A second pass that does not inherit the first pass’s conclusions produces the Belief File and the contradictions honestly. It is the cheapest insurance in the system and it directly protects the publication’s two signature qualities.

### 5.4 Retry and error behavior

Every AI call retries once on a provider error or a parse failure, with the error appended. A second technical failure sets ERROR with the node name in Human Notes and stops. Drive writes retry twice. Sheet writes retry twice. Editorial reservations after the maximum revision rounds are not technical errors: the best current article is saved and the row reaches READY_FOR_REVIEW with a warning in Human Notes. The Drive folder and 01 - Research persist on technical error so the human can see how far it got.

## 6. Google Drive

Nosebleeds/ Unpublished/ NB-20260906-01 - The Game That Ended 19 to 18/ 01 - Research 02 - Final Article

Moving a folder to Published/ is a human act after publication; the workflow never touches it. Nothing else is saved.

## 7. The Research document

Sections, in order. The compiler writes all of them; empty sections say “none found” rather than being omitted. Working Story Thesis (from the idea) · Final Story Thesis · Research Outcome: CONTINUE or REFRAME, with the reframe explained · Verified Hook · Narrative Hinge · Why This Story Matters · Human Carrier(s) · Full Timeline · What People Knew Then (Belief File: known, expected with numbers, doubters and believers named and dated, plausible alternatives, not knowable then, inevitability note) · Key Verified Facts · Important Numbers and Statistics (with the authoritative source and any contemporaneous discrepancy) · Useful Quotes (verbatim, speaker, date, context, URL; recalled-later quotes marked) · Myths, Legends, and Repeated Anecdotes (each with its traced origin and verdict) · Contradictions and Disputed Claims · Claims We Should Not Make · Hindsight Hazards · Human Stakes · Important Rules and Context (explained in the fewest words, with where in the story each becomes plot) · Scenes, Texture, and Specific Details · Potential Visuals (with URLs actually found and visible credit; function: prove, show, explain) · Hero Image Recommendation · Potential Endings · Researcher’s Recommended Story Conception (shape, register, spine, where the hook goes, where to slow down) · Sources (one per line: publisher, title, date, URL, and the state it carried). Every fact in the document carries one of six tags: Verified, Attributed, Disputed, Legend, Inference, Unverified. The Writer states Verified flat. Attributed material is attributed naturally and close enough that the reader cannot mistake the account for documented fact; source names should not be repeated mechanically when attribution remains clear. Disputed material carries the dispute honestly. Legend is presented as legend. Inference is never load-bearing, and Unverified material does not appear. Reviewer C checks the draft against exactly this.

## 8. Doctrine each node receives

| Node | Markdowns from GitHub |
|---|---|
| Candidate Generator | Brand Bible; Ideation and Selection Standard |
| Cold Idea Evaluator | Ideation and Selection Standard |
| Research Pass 1 | Research Standard |
| Research Pass 2 | Research Standard belief and adversary sections |
| Research Compiler | Research Standard; Narrative Architectures section 1 |
| Writer, draft | Voice Kernel; Narrative Architectures; Voice Bible calibration passages; Brand Bible identity |
| Reviewer A | Master Scoring Rubric dimensions A and B, D3 |
| Reviewer B | Voice Bible; Voice Kernel; Rubric C, D1, D2, D4 |
| Reviewer C | Research Standard epistemic states; Master Scoring Rubric v1.2 E1 section |
| EIC | Rubric; Production and Review Standard EIC section; Kernel |
| Writer, revision | Voice Kernel |
| Cold Final Review | Rubric; Brand Bible identity |
| Packaging | Voice Bible headline/subtitle sections; Visual Media OS functions/rights sections |

Whole documents are passed where listed without a section. Sections are extracted by heading in a Code node. No compiled modules.

### 8.1 Runtime prompt filenames

The n8n build fetches the following files from `Prompts/`. These basenames are stable runtime contracts and should not be renamed:

- `I1-candidate-generator.md`
- `I2-cold-idea-evaluator.md`
- `G1-research-pass-1.md`
- `G2-research-pass-2.md`
- `G3-research-compiler.md`
- `G4-writer-draft.md`
- `G5-reviewer-a-story.md`
- `G6-reviewer-b-voice.md`
- `G7-reviewer-c-truth.md`
- `G8-eic.md`
- `G9-writer-revision.md`
- `G10-cold-final-review.md`
- `G11-eic-round-two.md`
- `G12-packaging.md`

`Prompts/universal-preamble.md` is a separate prepend-only runtime file for I1, G1, and G2 as specified in §1.1.

## 9. Reviewer output shape

All three reviewers return the same JSON: { overall_assessment, strengths: [ { where, what, protect: true|false } ], must_fix: [ { where, what, why, fix } ], should_fix: [...], optional: [...], scores: { dimension: score }, verdict: PASS |

REVISE | FAIL } . Reviewer C’s must_fix items carry the Research document’s tag for the

claim in question. The EIC reads all three; the Writer never sees any of them.

## 10. Model routing

| Work | Launch provider | Note |
|---|---|---|
| Candidate Generator, Research Pass 1, Research Pass 2 | OpenAI, web search enabled | Use a mode that returns cited URLs; the Research document depends on them |
| Cold Idea Evaluator, Research Compiler, Writer, Reviewers A/B, EIC, Packaging | Anthropic | EIC on strongest available tier |
| Reviewer C, Cold Final Review | Prefer provider different from Writer if testing supports it; otherwise Anthropic in fresh context | Independence matters most here |
| Conversation scanning | Perplexity, optional | Not part of launch workflows |

Provider choice is per-node configuration, not doctrine. Expect to swap after dry runs.

## 11. Frontend: the Nosebleeds Console

Clone the Pretty Penny Console repository into the Nosebleeds repo’s console/ directory and change only: Sheet ID and tab name; column mapping to §2. Status set to §3, with colors: READY blue, GENERATING golden yellow, READY_FOR_REVIEW red, PUBLISHED cream on dark, HOLD and REJECTED grey, ERROR red outline.

Branding: Nosebleeds wordmark, Lou avatar, palette (red, blue, warm cream, white, dark golden yellow), retro sports editorial type direction. Displayed columns: Working Title, Status, Priority, Sport, Story Type, Idea Score, Drive Folder, Final Article, Generated Date. Summary counts: READY, GENERATING, READY_FOR_REVIEW, PUBLISHED. Controls: “Run Ideation”, “Generate Next Story”, each a POST to an n8n webhook with the shared-secret header, same pattern as Pretty Penny. Editable fields: Priority, Status, Human Notes, each a POST to an update webhook. Webhooks (n8n, Header Auth with a shared secret, same as Pretty Penny): GET /nosebleeds/queue (read rows), POST /nosebleeds/update (row id, field, value), POST /nosebleeds/run-ideation , POST /nosebleeds/generate-next . Four webhooks. The two

run webhooks call the respective workflow’s Manual Trigger path.

Security note: reuse the Pretty Penny Console's secure server-side or proxy pattern for authenticated n8n calls. Do not embed a reusable n8n shared secret directly in public GitHub Pages JavaScript. If the Pretty Penny implementation already solves this, copy that mechanism unchanged.

## 12. Schedules and manual triggers

Ideation: Sunday 12:00 PM America/Los_Angeles, plus webhook. Generation: Sunday 2:00 PM America/Los_Angeles, plus webhook. The two-hour gap lets Ideation refresh the queue first. Manual “Generate Next Story” checks for any row in GENERATING before starting; if one exists, it returns “a story is already generating” and does nothing. This is the entire concurrency mechanism. Manual “Run Ideation” runs regardless.

## 13. n8n build sequence

1. Sheet and Drive. Create the Sheet with the §2 columns and the Unpublished folder. Hand-enter one READY row: the shot clock (see the Prompts document’s dry-run brief). 2. GitHub. Nosebleeds repo with doctrine/ (all canonical markdowns), prompts/ (the Prompts document, split one file per node), console/ (cloned from Pretty Penny). Confirm raw-content fetch works for one file. 3. Generation workflow, research half. Steps 1 to 10. Run it on the shot clock row. Read 01 - Research in full. Fix prompts until the Research document is something you would

hand a writer. 4. Generation workflow, writing half. Steps 11 to 23. Run end to end. Read 02 - Final Article . This is Dry Run 1.

5. Ideation workflow. Steps 1 to 9. Run it. Read every row it wrote. Tighten the evaluator until you would generate any row it passes. 6. Console. Clone, rebrand, wire the four webhooks. 7. Dry Runs 2 and 3. A myth-versus-record story (tests Legend, Disputed, Claims We Should Not Make, and Reviewer C) and a recent-past story with living subjects (tests attribution, the legal caution in the Research Standard, and the package). Both handentered as READY. 8. Schedules on. Only after the three dry runs produce articles you would publish or could see how to fix. Nothing in steps 1 to 4 depends on Ideation existing; that is the point of the order.

## 14. What this keeps from the prior Batch Four

The three ideas worth keeping survived intact: independent critique that the Writer never sees, consolidated by one EIC into one brief; facts locked before drafting, with the Research document as the Writer’s entire factual universe and Reviewer C checking against it; and a cold final review in a fresh context that is asked the single strongest reason not to publish. Everything else that was infrastructure is now either the Sheet’s Status column, the n8n execution history, or a sentence in a prompt.

## CHANGE LOG

v2.1: final launch simplification and editorial-quality patch. Raised the Ideation floor to 8.5 and made READY a stronger commitment; added hook-source support for search-blind idea evaluation; changed second-round editorial failure from ERROR to flagged READY_FOR_REVIEW; aligned attribution and Reviewer C with canonical E1 doctrine; tightened the visual treatment to the locked Nosebleeds gouache/ink house style; added the public-frontend secret handling note.

v2.0: architectural reset. Two workflows, one Sheet, one Drive tree with two permanent documents, one cloned Console, eleven to fourteen AI calls per article, CONTINUE/REFRAME with no editorial kill inside Generation, three reviewers plus EIC plus cold review, two-round maximum, no schemas, no leases, no modules, no lineage.
