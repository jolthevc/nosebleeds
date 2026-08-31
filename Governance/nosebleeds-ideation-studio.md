# NOSEBLEEDS
## Ideation Studio Product & Runtime Standard v1.0
### Discover, explore, refine, compare, and commission without turning brainstorming into a production workflow.

**Status:** Canonical product and runtime behavior for interactive ideation  
**Scope:** Nosebleeds Console + n8n brainstorming workflows  
**System of record:** Google Sheet only after explicit human commissioning

---

# 0. PURPOSE

The Ideation Studio is the human-controlled creative workspace inside the Nosebleeds Console.

It exists for one reason:

> **Help the editor find, shape, and commission better sports pieces without forcing every exploratory thought into the production queue.**

The Ideation Studio is not the autonomous Ideation workflow.

The autonomous Ideation workflow searches broadly and returns commissioned ideas.

The Ideation Studio is interactive.

It should let the human:

- explore a blank slate
- constrain by sport
- constrain by editorial lens
- combine sport and lens
- provide rough directional thoughts
- inspect multiple conceptions
- compare alternatives
- converse with the AI
- refine or fork a concept
- commission only when satisfied

The human editor owns the final decision.

---

# 1. THE PRODUCT MODEL

The Ideation Studio has five stages:

1. **Discover**
2. **Explore Framings**
3. **Refine**
4. **Compare**
5. **Commission**

These stages should feel connected, not like separate tools.

The system should progressively spend more model effort only as human interest increases.

---

# 2. SEARCH INPUTS

Interactive discovery accepts three optional inputs.

## Sport

Examples:

- NFL
- NBA
- MLB
- college football
- golf
- tennis
- soccer

Sport may be blank.

## Editorial Lens

Suggested lenses:

- Profile
- Game / Moment
- Season / Era
- Team / Organization
- League / Institution
- Business / Commercial
- Strategy / Tactics
- Culture / Fandom
- Media
- Money / Contracts
- Rules / Innovation
- Myth / Memory
- Rivalry
- Politics / Society
- Place / Stadium
- Object / Artifact

Lens may be blank.

A lens is a search constraint.

It is not a required article template.

## Freeform Direction

The editor may provide rough thoughts such as:

> Something around how NFL teams decide which positions are actually worth paying for.

or:

> I want something on Tiger, but not another greatness profile.

or:

> The 2016 cap spike, KD, and unintended consequences.

Freeform direction may be blank.

---

# 3. SUPPORTED SEARCH MODES

The same interface must support:

## Blank slate

No sport.  
No lens.  
No direction.

The model searches freely for strong Nosebleeds concepts.

## Sport only

Example:

NFL

## Lens only

Example:

Profile

## Sport + lens

Example:

NBA + Business / Commercial

## Direction only

Example:

Something around teams overpaying for positions that are not actually scarce.

## Any combination

Example:

NFL  
Strategy / Tactics  
Something around offensive line scarcity and tackle versus guard value.

Do not create separate workflows for each mode.

One search contract should support all combinations.

---

# 4. DISCOVERY OUTPUT

Interactive discovery should normally return approximately six Concept Cards.

This is intentionally smaller than the autonomous Ideation slate.

The user is actively evaluating options.

Quality and legibility matter more than volume.

Each Concept Card should contain:

- Working Title
- Core Conception
- Why You Have to Read This
- Sport
- Lens, when useful
- Audience Gravity
- What It Opens Up
- Editorial Promise
- Depth Runway
- Research Confidence
- Initial Source Leads
- approximately three possible Framings

---

# 5. AUDIENCE GRAVITY

Audience Gravity is directional metadata.

Use:

- **Core**
- **Crossover**
- **Wildcard**

It answers:

> **How much reader interest likely exists before sentence one?**

It does not determine whether a concept can be commissioned.

A Wildcard may be exceptional.

A Core subject may be mediocre.

Do not implement quotas or hard logic from this field.

---

# 6. EDITORIAL PROMISE

Interactive concepts may receive a directional Scout Grade or Editorial Promise score.

This is not the final article rubric.

This is not an automated commissioning threshold.

Recommended dimensions:

- Audience Pull
- Entertainment Potential
- Conception Strength
- Depth Potential
- Nosebleeds Fit
- Research Promise, when useful

The model may also provide one overall Editorial Promise score from 0 to 10.

The score exists to help the human compare possibilities.

It must never block commissioning.

Do not run a second evaluator model merely to generate this score.

The same discovery model should return it.

---

# 7. DEPTH RUNWAY

Use:

- **Short**
- **Substantial**
- **Deep**

Depth Runway is not a word-count estimate.

It answers:

> **How much rewarding material appears to exist beneath the hook?**

A Short idea can be excellent.

A Deep idea can still be badly conceived.

The field should help the editor understand likely research and narrative surface.

---

# 8. RESEARCH CONFIDENCE

Use:

- **Strong**
- **Moderate**
- **Needs Work**

This reflects how confidently the model can see a responsible research path from initial discovery.

It does not mean the piece is already verified.

Full Research happens after commissioning.

---

# 9. WHAT IT OPENS UP

Concept Cards should identify a small number of promising dimensions.

Examples:

- strategy
- psychology
- business
- money
- culture
- mythology
- fandom
- media
- politics
- identity
- technology
- memory
- relationships
- institutional incentives

These are descriptive tags.

They are not requirements.

They should help the editor see where the story might deepen.

---

# 10. FRAMINGS

Each broad concept should usually return approximately three legitimately different ways into the subject.

A framing is a conception, not a cosmetic title variation.

Good framing alternatives may differ by:

- central question
- perspective
- narrative spine
- whose experience carries the piece
- what consequence matters most
- what contradiction organizes the story
- whether the event, person, institution, or mechanism is foregrounded

Do not force three fixed buckets such as:

- business
- culture
- psychology

The model should find the best three framings for that subject.

---

# 11. CONCEPT WORKBENCH

Selecting a Concept Card or framing opens the Concept Workbench.

The Workbench should display:

## Current Conception

The current best version of the piece.

## Conversation

A freeform editor-to-AI thread.

The editor may say:

- I like this, but make it more Falcons-driven.
- Can we combine A and C?
- This feels too psychological. Make it more football-first.
- Does the business angle actually make this better?
- Give me three completely different framings.
- Make this broader.
- Make this narrower.
- This feels too worshipful.
- What are we missing?
- Challenge the premise.
- Could the real piece be about something adjacent?

The AI should respond conversationally.

When useful, it may propose revised conceptions.

The human explicitly adopts a revision before it replaces Current Conception.

---

# 12. QUICK REFINEMENT ACTIONS

The Console may offer convenience actions such as:

- Different framings
- Go deeper
- Broaden appeal
- Make it more sports-first
- Find the business angle
- Find the human angle
- Find the cultural angle
- Make it less obvious
- Narrow the piece
- Challenge the premise

These are prefilled instructions to the same refinement workflow.

Do not create separate backend endpoints or prompts for each button.

Freeform conversation remains primary.

---

# 13. FORKING

The editor may fork a concept.

Example:

- Original
- Version A
- Version B

Forks allow exploration without destroying earlier thinking.

Fork state is brainstorming state.

It does not belong in the Google Sheet.

For v1, browser or session memory is acceptable.

Persistent cloud storage is not required.

---

# 14. COMPARE

The editor may select two or three concepts or framings and request a comparison.

The comparison should address:

- Audience Pull
- Conception Strength
- Entertainment Potential
- Depth Runway
- biggest weakness
- similarity to recent commissions
- how each might be improved

Do not simply declare a winner.

The purpose is human decision support.

Comparison normally does not require web search.

---

# 15. PREFLIGHT

Before commissioning, the system should produce a clean Preflight.

Recommended fields:

- Working Title
- Core Premise / Conception
- Hook
- Why You Have to Read This
- Sport
- Lens, if useful
- Audience Gravity
- Source Leads
- Open Questions for Research

The final field is important.

Ideation should hand Research unresolved questions rather than pretending the article has already been solved.

Example:

> Research should determine whether the strongest explanation for Atlanta's collapse is play calling, execution, changing incentives, or the interaction among all three.

Preflight may use a stronger web-search call because the human has indicated serious commissioning interest.

---

# 16. COMMISSIONING

Nothing enters the Google Sheet until the editor explicitly selects:

> **Add to Queue**

At that point, the selected conception becomes a normal Nosebleeds idea.

The server should assign:

- Idea ID
- Status = READY
- Created Date
- Priority using existing behavior

The Google Sheet remains the source of truth after commissioning.

Discarded concepts, conversation, comparisons, and forks remain outside the Sheet.

---

# 17. EXISTING READY IDEAS

Every READY or HOLD idea should support:

> **Open in Workbench**

The existing queued conception becomes Current Conception.

The editor may refine it conversationally.

A separate explicit action:

> **Replace Queued Conception**

may update:

- Working Title
- Core Premise
- Hook
- Why It Works
- Sport
- Lens, if stored
- Source Leads

Only allow this when status is READY or HOLD.

Once status becomes GENERATING, the conception is locked.

Do not widen the generic field-update endpoint for this purpose unless there is a strong implementation reason.

A dedicated conception-update action is safer.

---

# 18. SLATE AWARENESS

Interactive Ideation may receive compact recent-slate context.

The UI may show soft warnings such as:

- Similar recent concept
- Recent NFL concentration
- Several recent business pieces
- Similar subject already commissioned

These are informational.

Never block an idea because of them.

Never enforce sport, lens, or era quotas.

Slate context should prevent accidental repetition, not force artificial diversity.

---

# 19. MODEL AND TOKEN DISCIPLINE

The Ideation Studio should progressively spend compute.

## Discover

Use one web-search-capable model call.

Input:
- Ideation Kernel
- editorial calibration when needed
- sport
- lens
- direction
- compact recent slate context

Output:
- approximately six Concept Cards
- framings
- directional metadata
- initial sources

## Refine

Normally use a lightweight capable model without web search.

Input:
- Ideation Kernel
- Current Conception
- editor message
- compact recent Workbench context

Do not resend:
- full Brand Bible
- full Research Standard
- full Production Standard
- all discarded concepts
- entire historical slate
- unlimited conversation history

If the editor explicitly asks for fresh factual investigation, the same refinement endpoint may request web-enabled mode or route to a search-capable model.

## Compare

Use a lightweight model.

No web search by default.

Input only:
- Ideation Kernel
- selected concepts
- compact recent-slate context if relevant

## Preflight

Use a stronger search-capable call.

This is the point where stronger source verification is justified.

The editor has shown real interest.

---

# 20. RUNTIME CONTEXT

The Ideation Studio should use a compact runtime context.

Primary runtime document:

`Governance/nosebleeds-ideation-kernel.md`

The full Brand Bible and downstream production documents should not be injected into every conversational turn.

Default Discovery may also use:

`Governance/nosebleeds-editorial-calibration-examples.md`

when useful for taste calibration.

Calibration examples are not templates.

---

# 21. WEBHOOK ARCHITECTURE

Prefer a small number of generic endpoints.

Recommended shape:

## `POST /nosebleeds/brainstorm-search`

Purpose:
Interactive discovery.

Input:
- sport
- lens
- direction
- optional count
- compact slate context or server-derived slate context

Web search:
Yes.

## `POST /nosebleeds/brainstorm-refine`

Purpose:
Workbench conversation and reframing.

Input:
- current_conception
- editor_message
- compact_thread
- optional use_web

Web search:
No by default.

## `POST /nosebleeds/brainstorm-compare`

Purpose:
Compare two or three concepts or framings.

Web search:
No by default.

## `POST /nosebleeds/brainstorm-preflight`

Purpose:
Turn a selected conception into a clean, source-aware, queue-ready idea.

Web search:
Yes.

Existing:

## `POST /nosebleeds/add-idea`

remains the explicit persistence action.

Add:

## `POST /nosebleeds/update-conception`

Purpose:
Replace editorial fields for an existing READY or HOLD row.

Server must reject updates when status is GENERATING or later.

Do not create separate endpoints for individual refinement buttons.

---

# 22. WHAT NOT TO BUILD

Do not build:

- a separate agent for every Lens
- sport-specific prompts
- category quotas
- a second ideation evaluator
- a separate score model
- persistent storage for discarded brainstorming in v1
- full article editing inside Ideation Studio
- article research inside every Workbench turn
- a taxonomy that every finished article must fit
- automatic replacement of queued concepts without human confirmation

---

# 23. SUCCESS TEST

The Ideation Studio is working when the editor can:

1. start with nothing or with a rough idea
2. find several strong possibilities
3. see why each might work
4. inspect several ways into the same subject
5. talk through a concept with the AI
6. fork or compare alternatives
7. refine a queued idea before Generation
8. commission only when satisfied
9. do all of this without turning every interaction into an expensive research run

The experience should feel like an editor's desk, not a chatbot and not an admin form.
