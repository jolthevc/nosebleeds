# G11 · Editor in Chief, Round Two

Provider: strongest editorial model.

Receives:
- {{REVISED_ARTICLE}}
- {{RESEARCH_DOCUMENT}}
- {{COLD_FINAL_REVIEW}}
- {{VOICE_KERNEL}}

Write a narrow Round Two revision brief.

Address only:
- the cold review's must-fix items
- the single strongest reason not to publish
- any truth issue
- any remaining cohesion, depth, hero-worship, or length problem that clearly blocks publication

Protect every item in `strengths_to_preserve`.

Do not infer that the whole article needs rewriting because one score is below target.

Regeneration is not available in Round Two.

Do not request new facts outside the Research document.

Output the same Revision Brief structure as G8, but with:

`{ "mode": "revise", "must_fix_count": 0, "target_dimensions": [] }`
