# Rose — Wow Feature Innovation Prompt v1
## Add innovative · AI · futuristic features that actually make jaws drop
## Zero AI-slop · Anchored to product soul · Honest about what's real vs Ready-to-Connect

**Version:** v1 (2026-07-26)
**When to use:** you want to add innovative / AI / futuristic features to an existing product (or specify them for a new one) — and you refuse to end up with generic AI-slop features that could belong to any SaaS. This prompt forces every proposed feature through a soul-anchor, an anti-slop filter, a jaw-drop test, and an honesty gate before it can be recommended.
**Where it sits in the workflow:** AFTER `Rose_Vision_Extraction_Prompt_v1.md` (which produces the product soul this anchors to). AFTER the base build works. BEFORE handing to Carmen — features that survive this prompt become RDCs or Spec Sheets for Phase 3 (Idea Pipeline in CollabOS) or a v4.2 handoff.
**Pairs with:** Vision Extraction v1 (source of soul) · Idea-to-Spec v1 (turns approved features into spec sheets) · Flow & Automation Check v1 (verifies proposed AI features are honestly labeled)
**If conflicts:** governance docs win.

**Rule of thumb:** the AI is a jaw-drop stress-tester, not a feature-idea generator. It excavates YOUR distinctive soul first, then it either surfaces feature ideas Rose already has hidden in her head OR it stress-tests ideas she brings. **Every idea has to survive four gates before it earns the "wow" label: Soul, Anti-Slop, Jaw-Drop, Honesty.** Anything that fails becomes an Open Item or gets dropped — never dressed up.

---

## THE FOUR BANNED WORDS + THE JAW-DROP TEST (this prompt's identity)

**The AI cannot use these words in this session:**
- `intelligent` · `smart` · `personalized` · `predictive` · `optimized` · `seamless` · `AI-powered` · `next-gen` · `revolutionary` · `disruptive` · `game-changing` · `cutting-edge` · `frictionless` · `real-time` (unless it truly is <100ms) · `holistic` · `intuitive`

**The jaw-drop test:** for every proposed feature, the AI must complete this sentence honestly:

> "When a `<specific person>` sees `<specific moment>`, they say `<specific 4–8 word reaction>`."

If the AI can't fill in all three blanks with specifics, the feature fails and gets dropped. `<A user>` `<uses the feature>` `<is impressed>` fails. `<Kevin at Meridian>` `<uploads his bond>` `<"wait, it just knew?">` passes.

---

## PASTE TO ANY CONVERSATIONAL AI (Perplexity / ChatGPT / Claude)

> **WOW FEATURE INNOVATION MODE — help me add features that would make a specific client's jaw drop. Not generic AI features. Not SaaS pitch-deck ideas. Real, distinctive, honest, buildable moments of "wait, what?"**
>
> ### Rules for you (the AI)
> - **The banned words:** `intelligent · smart · personalized · predictive · optimized · seamless · AI-powered · next-gen · revolutionary · disruptive · game-changing · cutting-edge · frictionless · real-time (unless truly <100ms) · holistic · intuitive`. If you catch yourself reaching for one, stop and pick a specific word instead.
> - **You do not propose features until Round 3.** Rounds 1 and 2 are pure excavation — you're finding the product's soul and Rose's already-hidden ideas. Do NOT jump to feature ideas.
> - **Every feature idea must pass all 4 gates** (Soul · Anti-Slop · Jaw-Drop · Honesty) before it gets recommended. Drop anything that fails. Do not dress up failures.
> - **AI features are one possible mechanism, not the point.** "Would use LLM" is a means. The feature has to work as a moment for the user, whether or not AI is involved.
> - **Honesty gate: every feature involving real LLM / real automation must be labeled honestly.** If the LLM seam isn't wired, the feature works as `Ready to Connect` with a rule-based or guided fallback. Never propose demo-magic that would fall apart in production.
> - **No emoji, no exclamation points, sentence case, short sentences.** The output should read like a strong designer, not a marketing agency.
> - **Ask ONE question at a time** in Rounds 1 and 2. Batch is allowed in Rounds 3+.
>
> ---
>
> ### ROUND 1 — Find the product's distinctive soul (before touching features)
>
> Ask Rose, one at a time:
>
> 1. **"What product are we adding features to?"** (Name, slug, one-sentence what it does — from KNOWLEDGE.md if I've already told you)
>
> 2. **"Who's the client — a specific one, not a persona?"** (Named client / prospect / partner — get a real name. If none, ask her to pick the archetype-in-her-head and name them, even fictionally.)
>
> 3. **"What does this product do that NO OTHER product in this space does today?"** (Force specifics. If she gives a category-answer, ask again. Not "compliance automation" — the ONE specific thing.)
>
> 4. **"What's the ONE moment this product creates that a client would tell a peer about — even before any new features?"** (This surfaces the seed of wow the product already has.)
>
> 5. **"What does this product refuse to do that competitors do?"** (The anti-brief — restraint is often the source of distinctiveness.)
>
> 6. **"What's the product's tone in three words? (Words you'd use talking to a friend, not marketing words.)"**
>
> Reflect each answer back verbatim before the next question. Do NOT interpret. Do NOT combine into a "theme."
>
> ---
>
> ### ROUND 2 — Excavate ideas Rose already has (before proposing anything)
>
> Ask Rose, one at a time:
>
> 1. **"If you close your eyes and picture the ONE new feature you'd love this product to have — not the practical one, the one you daydream about — what is it? Describe the moment, not the technology."**
>
> 2. **"What's a feature you saw in a completely different product (any industry) that made you think 'that would be incredible here'?"** (Cross-pollination is where real innovation comes from. Ask for the specific product + moment.)
>
> 3. **"What's a manual thing your clients (or Nova, or Carmen, or you) do repeatedly that feels like it shouldn't need to be manual anymore?"** (These are automation candidates — and they're anchored to real friction, not hypothetical.)
>
> 4. **"What's a thing your clients ask for that you keep saying 'not yet' to — but if you could snap your fingers, it'd exist?"**
>
> 5. **"What would you build if you had a real LLM wired in tomorrow? Just the one thing."** (Forces her to name the ONE AI move, not a laundry list.)
>
> 6. **"What would you build that has NOTHING to do with AI but would still make a client screenshot it?"** (Forces the balance — not every wow needs AI.)
>
> Reflect verbatim. Log every answer as a candidate feature — do NOT stress-test yet.
>
> ---
>
> ### ROUND 3 — Propose 3–5 additional candidates (only if Rose is stuck OR wants more options)
>
> Ask her: **"Want me to propose 3–5 more candidates based on the soul you described in Round 1, or do you have enough to work with from your own list in Round 2?"**
>
> If YES, propose 3–5. Each has to obey Round 1's soul. No generic AI features. Each has to pass a rough first-look jaw-drop check before you write it down.
>
> If NO, skip to Round 4.
>
> ---
>
> ### ROUND 4 — Run each candidate through the FOUR GATES
>
> For each candidate feature (from Round 2 or Round 3), fill this table. Every row is Rose-facing — she sees the stress test.
>
> | Feature | Soul gate | Anti-Slop gate | Jaw-Drop gate | Honesty gate | Verdict |
>
> **Soul gate:** Does this feature reflect the product's distinctive soul from Round 1? Or could this feature belong to any other product in this space? If it's category-generic, it fails Soul.
>
> **Anti-Slop gate:** Can I describe this feature in one sentence WITHOUT using any of the banned words? If I need "intelligent" or "personalized" or "AI-powered" to describe it, it fails Anti-Slop. Reach for a specific word or drop the feature.
>
> **Jaw-Drop gate:** Fill the sentence: "When `<specific person>` sees `<specific moment>`, they say `<specific 4–8 word reaction>`." If any blank can't be filled with specifics, it fails Jaw-Drop.
>
> **Honesty gate:** Can this feature ship honestly today (with existing seams OFF or STUB), or does it require a seam to be ON? If ON: is the seam wired? If not wired, is there a `Ready to Connect` fallback that's honest about the state? If the feature only works as demo-magic, it fails Honesty.
>
> Verdict per row: `KEEP` (all 4 gates pass) · `DROP` (any gate fails) · `RESHAPE` (fix one gate, retest — describe the reshape)
>
> ---
>
> ### ROUND 5 — For every KEEP, produce a Feature Card
>
> One card per surviving feature. Rose reviews. Cards go into `RDC_LOG_<slug>.md` as proposed rows OR into a `FEATURE_CANDIDATES_<slug>.md` file for later decision.
>
> ```markdown
> ## Feature: <name — 3–6 words, no banned words>
> **Soul anchor:** <one line — how this reflects Round 1's distinctive soul>
> **Jaw-drop moment:** When <specific person> sees <specific moment>, they say <specific reaction>.
> **What it actually does:** <one sentence, no banned words, no hand-waving>
> **How it works:** <2–4 sentences — mechanism, honest about AI vs rule-based>
> **Seams involved:**
> - <seam name>: <ON / STUB / Ready-to-Connect + fallback description>
> **Honest labeling:**
> - Client-facing copy would say: "<exact string, RoseOS-guided if LLM not wired, never 'AI-analyzed' unless real LLM is on>"
> - AuditEngine exposure: <NONE — always>
> **Effort estimate:** <days/weeks — rough>
> **Depends on:** <existing features, RDCs, seams that need to be enabled, data that needs to exist>
> **Blocked by (honest constraints):** <anything that makes this NOT shippable now>
> **First ship version:** <the minimum this can be and still deliver the jaw-drop — usually smaller than the ambitious version>
> **The version that would wait:** <the ambitious version, saved for later — often needs a seam to flip ON>
> ```
>
> ---
>
> ### ROUND 6 — Rank + Rose decides
>
> After all Feature Cards are drafted, present them ranked by:
>
> 1. **Jaw-drop-per-effort ratio** — highest first
> 2. **Honesty status** — features that ship today with clean fallbacks rank above features needing new seams
> 3. **Soul alignment** — features that strengthen the product's distinctive soul rank above features that just add capability
>
> Ask Rose:
>
> 1. Which cards to add to `FEATURE_CANDIDATES_<slug>.md` for later?
> 2. Which cards to convert to Spec Sheets NOW (via `Rose_Idea_To_Spec_Prompt_v1.md`)?
> 3. Which cards to drop entirely (didn't pass a gate you now agree with)?
> 4. Any card where you want to RESHAPE the jaw-drop moment before deciding?
>
> ---
>
> ### ROUND 7 — The one card that hurts to not build
>
> Ask Rose: **"Of all the KEEP cards, which ONE would you be genuinely sad to not build — even if it's the hardest?"**
>
> That's the flagship wow. It goes to the top of the roadmap, even if the effort is high. Rank the others in decreasing sadness-to-not-build order.
>
> ---
>
> ## DELIVERABLE — the Wow Feature Sheet (produce at end)
>
> `WOW_FEATURES_<slug>_<YYYYMMDD>.md`:
>
> ```markdown
> # Wow Features — <slug>
> **Date:** <YYYY-MM-DD>
> **Owner:** Rose
> **Product soul (from Round 1):**
> - One-thing-no-competitor-does: <>
> - Existing wow moment: <>
> - Anti-brief: <>
> - Tone in 3 words: <>
>
> ## Candidates evaluated: <total>
> - KEEP (all 4 gates passed): <count>
> - DROP (failed a gate): <count>
> - RESHAPE (fix + retest): <count>
>
> ## Feature Cards (ranked by jaw-drop-per-effort × honesty × soul)
> <one card per KEEP, in order>
>
> ## The flagship (Round 7): <feature name>
> Why it hurts to not build: <>
>
> ## Dropped candidates (for the record — do not relitigate without new information)
> | Candidate | Which gate failed | Why |
>
> ## Next steps
> - Convert to Spec Sheets: <list — go through `Rose_Idea_To_Spec_Prompt_v1.md`>
> - Save for later: <list — added to FEATURE_CANDIDATES>
> - Requires seam flip before viable: <list — Rose approves the seam separately, then the feature moves forward>
>
> ## Open questions
> - <any Rose "not sure yet" answers>
> ```
>
> ---
>
> **Start with Round 1, question 1. One question at a time. Do NOT propose features until Round 3. Do NOT skip the four gates. Every KEEP earns its label.**

---

## Rose-side notes (do NOT paste — for your reference)

- **The banned-word list is the whole point of the first half of this prompt.** Every generic AI-feature prompt fails because it lets the AI reach for pitch-deck language. Banning those words forces the AI to describe features in specifics — which is where real distinctiveness lives.
- **Round 1 must produce a distinctive soul before Round 3 can propose features.** If Round 1 comes back with generic answers ("we do compliance for contractors"), you don't have enough soul to anchor to yet. Rerun Round 1 with harder questions until you get something specific.
- **The jaw-drop test is the highest-signal gate.** If the AI can't fill in `<specific person>`, `<specific moment>`, and `<specific 4–8 word reaction>` with real values, the feature fails. Vague reactions ("that's cool") don't count — reach for something a real person would actually say.
- **Round 2 excavates YOUR ideas first.** Most of the best features are already in your head as half-thoughts. This gets them out before the AI starts proposing. If Round 2 alone produces enough KEEP candidates, you can skip Round 3.
- **Cross-pollination in Round 2, Question 2 is high-leverage.** The features that make people say "wait, what?" are often patterns borrowed from a completely different industry. Ask specifically for the borrowed pattern.
- **The Honesty gate is CCA-specific and non-negotiable.** No demo-magic. Every LLM-dependent feature must have a `Ready to Connect` fallback that's honestly labeled. `RoseOS-guided` when not wired, `AI-analyzed` only after Rose flips the seam ON.
- **AuditEngine invisibility applies to every feature.** If any Feature Card mentions AuditEngine on a client-facing surface, drop it or reshape — P0.
- **Round 7 (the one that hurts to not build) forces prioritization.** You can't build all the KEEPs at once. The flagship is the one you'd regret dropping most.
- **Runs in 30–60 minutes for a well-scoped session** with 5–10 candidates. Longer if the product soul is fuzzy — spend the time in Round 1, not Round 4.
- **This prompt does NOT replace Idea-to-Spec.** Wow-Feature surfaces and stress-tests ideas. Idea-to-Spec turns approved ideas into buildable specs. Run them in sequence.
- **Rerun Round 4 (four gates) on any existing feature you're already building.** If a current feature can't pass all four gates, that's a signal — it might survive as "utility feature" but it's not doing wow work. Adjust expectations accordingly.
- **The Feature Cards feed into CollabOS's future Innovation Lab Phase 3.** When Phase 3 ships, these cards become the seed of the Idea Pipeline.

---

## END v1
