# Rose — Polish + Cleanup + Wow Prompt v1
## Motion & polish pass · Cleanup & whitespace check · Wow-factor check
## AI surveys and reports · Rose decides every fix · Zero AI-added anything

**Version:** v1 (2026-07-26)
**When to use:** the build works. You're past feature-complete. Before wrap-up. You want to know: does it move well, does it breathe well, does it have any moments that make someone say "oh."
**Where it sits in the workflow:** AFTER Sanity Check v1 or A1 in Fast Finish · BEFORE Wrap-Up v2.1. Not required — a build can ship without this. But if the build is client-facing or you want to be proud of it, run this pass.
**Pairs with:** Sanity Check v1 · Fast Finish v1 · Wrap-Up v2.1 · Style-From-Mockup v1
**If conflicts:** governance docs win.

**Rule of thumb:** the AI **does not add anything**. No new animations. No new spacing. No new "delight." No AI-initiated motion, palette, or layout ideas. It surveys, reports, and asks. Rose decides every fix. If Rose approves a fix, it becomes an RDC (Rose-Directed Change) and gets logged. Otherwise it becomes an Open Item.

---

## PASTE TO BUILD-SIDE AI

> **POLISH + CLEANUP + WOW MODE — three passes, done in order. You survey the build. You do NOT touch code. You do NOT add motion, spacing, animations, or "delight." You report findings; Rose decides which fixes to make. Every approved fix becomes an RDC and gets logged.**
>
> ### Ground rules (all 3 passes)
> - No code edits during survey. Report-only mode.
> - No AI-initiated design proposals. If you notice something, report it as Open Item or Suggested RDC — Rose decides.
> - Compare against the mockup / design tokens / RDC log for what's intended. If it deviates, that's a finding.
> - Evidence with every finding: file:line, screenshot filename, or specific measurement.
> - Locked lines / palette / naming stay as-is. Don't flag them for "polish."
> - Every seam stays OFF. No live wiring to test transitions.
> - The 9 accuracy floors from Fast Finish stay respected — nothing this pass finds overrides them.
>
> ---
>
> ## PASS 1 · MOTION & POLISH (does it feel alive without being twitchy?)
>
> ### 1a. Interactive states inventory
> For every interactive element, verify all four states are defined and consistent across the app:
>
> | Element type | Default | Hover | Focus | Active/Pressed | Disabled | Loading | Notes |
> |---|---|---|---|---|---|---|---|
> | Primary CTA | | | | | | | |
> | Secondary button | | | | | | | |
> | Nav link | | | | | | | |
> | Input field | | | | | | | |
> | Card (if clickable) | | | | | | | |
> | Icon button | | | | | | | |
> | Tab | | | | | | | |
>
> For each row: pass / fail / missing. If missing → Open Item. If inconsistent across pages → Open Item.
>
> ### 1b. Transition audit
> Grep the codebase for `transition`, `animate`, `duration`, `ease`, `motion`:
> ```
> grep -rniE "transition|animate|duration-|ease-|motion-" --include="*.tsx" --include="*.ts" --include="*.css"
> ```
>
> Report:
> - Total count of transitions used
> - Distinct durations found (should be 2–4 max: e.g. 150ms · 250ms · 400ms — anything else is drift)
> - Distinct easings found (should be 1–3 max)
> - Any transitions on properties that jitter (height, width, top, left — should use transform instead)
> - Any duration over 500ms on user-triggered feedback (usually feels sluggish)
>
> ### 1c. Micro-interaction check
> For each of these, note whether it exists AND whether it feels good (proportional to what triggered it — nothing bounces or overshoots unless intentional):
>
> - Button press feedback (color shift · slight scale · shadow lift)
> - Input focus (ring · border shift · label movement)
> - Nav item active state (underline · background · weight shift)
> - Card hover (lift · border · shadow — subtle, not dramatic)
> - Modal / dialog enter/exit (fade · slide · scale)
> - Toast / notification enter/exit
> - Page transitions (if any)
> - Skeleton loaders (if content is fetched)
> - Empty-state entrance (fade in vs pop in)
>
> Table:
> | Micro-interaction | Present? Y/N | Feels good? Y/N/skip | Where it lives | Fix suggestion (Rose approves or not) |
>
> ### 1d. "Twitchy or dead" check
> Two failure modes for motion:
> - **Twitchy** = too much motion, wiggles on every interaction, animations play when nothing needed to move, bounce/overshoot everywhere
> - **Dead** = no motion at all, feels like a static PDF, no feedback on any interaction
>
> One-line verdict per surface: `alive` · `twitchy` · `dead` · `mixed (list which)`
>
> ### 1e. Motion pass summary
> ```
> MOTION & POLISH — <project>
> Interactive states complete: <N/N element types>
> Distinct durations in use: <list> (target 2–4)
> Distinct easings: <list> (target 1–3)
> Jitter-prone transitions (height/width/top/left animations): <N> (list)
> Sluggish transitions (>500ms on feedback): <N> (list)
> Micro-interactions present + feel good: <N/N>
> Surfaces alive / twitchy / dead: <breakdown>
> Findings: <count of Open Items to surface to Rose>
> ```
>
> ---
>
> ## PASS 2 · CLEANUP & WHITESPACE (does it breathe?)
>
> ### 2a. Spacing scale audit
> Grep for spacing values in styles:
> ```
> grep -rniE "\b(margin|padding|gap|space)-[0-9]+|(m|p|gap|space)-\[[0-9]+" --include="*.tsx" --include="*.ts"
> grep -rniE "'[0-9]+px'|\"[0-9]+px\"" --include="*.tsx" --include="*.ts" --include="*.css"
> ```
>
> Report:
> - Distinct spacing values found (should follow the base scale from `Rose_Style_From_Mockup_Prompt_v1.md` — typically 4/8/12/16/24/32/48/64/96)
> - Any magic numbers (13px, 21px, 37px, etc.) — off-scale, list them
> - Vertical rhythm consistency across pages (do sections 96px apart everywhere, or does it vary?)
>
> ### 2b. Alignment audit
> For every page, visually check (screenshot each and note in a table):
>
> | Surface | Left edge alignment across sections consistent? | Grid alignment (12-col or whatever) respected? | Any element orphaned / floating alone? | Any element crammed against another? | Optical alignment issues (icon vs text baseline)? |
>
> ### 2c. Whitespace breathing check
> For each surface, one line per criterion:
>
> - **Section breathing** — enough space between distinct content sections? (target: 64–96px min on desktop)
> - **Content breathing** — enough space inside cards/containers? (target: 24–32px padding min on cards)
> - **Line-height breathing** — body text `line-height: 1.5–1.7`, headings tighter (1.1–1.25)?
> - **Max-width discipline** — text columns capped (60–75ch for prose, wider for data)?
> - **Dead zones** — any large empty areas that make the surface feel unfinished? (different from breathing — dead zones look like a mistake)
> - **Cluster density** — any group of controls / cards that look cramped together?
>
> Format:
> | Surface | Section breathing | Content breathing | Line-height | Max-width | Dead zones | Clusters | Overall verdict |
>
> ### 2d. Orphan + inconsistency sweep
> - **Orphan elements** — buttons/icons/labels sitting alone with no relationship to nearby content
> - **Inconsistent spacing between similar surfaces** — e.g. `/app/dashboard` has 32px card gaps, `/app/billing` has 24px
> - **Inconsistent padding on same component across pages** — e.g. `<Card>` has 24px padding in one place, 20px in another
> - **Text baseline misalignment** — labels not vertically centered with their inputs, icons not aligned to text
>
> One row per finding: file:line + what · what it should be · Rose's decision needed
>
> ### 2e. Cleanup sweep — code / copy debris
> - Any `console.log` still in code
> - Any commented-out code blocks
> - Any test/debug UI still visible (e.g. debug panels, "DEV MODE" banners)
> - Any placeholder copy (`Lorem ipsum`, `[COPY TBD]`, `TODO`) still on client-facing surfaces
> - Any dev-only URLs, sample credentials, or seed data leaked into production paths
> - Any half-implemented UI (a button that goes nowhere, a tab with `Coming soon` on a client-facing page in a non-PROP build)
>
> Table per finding.
>
> ### 2f. Cleanup pass summary
> ```
> CLEANUP & WHITESPACE — <project>
> Spacing values on-scale: Y / N (off-scale: N found)
> Alignment issues: N (list)
> Breathing verdict: <airy / balanced / cramped / mixed>
> Dead zones: N (list)
> Orphans / inconsistencies: N (list)
> Code/copy debris: N (list)
> Findings: <count of Open Items>
> ```
>
> ---
>
> ## PASS 3 · WOW FACTOR (would a designer screenshot this?)
>
> ### 3a. The "one moment" survey
> Look at every surface. Answer:
>
> **"If a designer or a discerning user saw this build for 60 seconds, what's the ONE detail they'd notice? Not overall — one specific detail."**
>
> If your answer is "nothing in particular," that's a signal — write "no distinguishing detail found." That's data.
>
> If you found one, describe it in one sentence, with file:line or screenshot.
>
> ### 3b. The "screenshot moment" check
> For each surface, one-line verdict:
> - `screenshot-worthy` — a designer would grab this
> - `professional but forgettable` — clean, competent, unremarkable
> - `functional but rough` — works, could look better
> - `unfinished` — obviously not done
>
> Table:
> | Surface | Verdict | Why | If not screenshot-worthy: what would make it? (Rose decides, do NOT implement) |
>
> ### 3c. The distinctive-element inventory
> Every build should have 1–3 things that don't feel like every other product. Not "innovative" — just distinctive. Examples:
> - A specific piece of typography (a custom letterform, an unusual weight pairing)
> - A restrained accent color used in one meaningful place
> - A specific micro-interaction that surprises without annoying
> - A specific piece of copy that isn't SaaS-generic ("Your value report is being prepared" vs "Loading…")
> - A specific empty-state that's charming instead of blank
> - A specific navigation choice (a persistent element, a clever hierarchy)
> - A specific piece of visual restraint (one dominant color, one dominant font weight, one hero image)
>
> List the 1–3 you found. If you found 0, that's a wow-factor finding — Rose decides whether to add one (via RDC, not AI-initiated).
>
> ### 3d. The "would embarrass Rose" check (repeat from Sanity Check, updated)
> **"If Rose sent this to a real client tomorrow, what's the ONE thing that would embarrass her?"** Force a single answer. If nothing embarrasses, say "nothing" — that's a valid signal that this is ready.
>
> ### 3e. Wow pass summary
> ```
> WOW FACTOR — <project>
> The one detail a discerning viewer would notice: <finding or "none">
> Screenshot-worthy surfaces: N/N
> Distinctive elements found: <list of 1–3 or "none">
> Embarrassment risk: <one thing or "none">
> Overall verdict: <would be proud to send / competent but not memorable / needs a moment to elevate / not ready>
> ```
>
> ---
>
> ## COMBINED REPORT (produce at end)
>
> Produce a single markdown block: `POLISH_REPORT_<slug>_<YYYYMMDD>.md`
>
> ```markdown
> # Polish + Cleanup + Wow — <project>
> **Date:** <YYYY-MM-DD>
> **SHA at survey:** <sha>
> **Surveyed by:** <AI name/model>
>
> ## Summary
> - Motion verdict: <alive / mixed / twitchy / dead>
> - Cleanup verdict: <airy / balanced / cramped / mixed>
> - Wow verdict: <proud to send / competent / needs elevation / not ready>
>
> ## All findings, bucketed by severity
>
> ### P0 — Would embarrass Rose (fix before any client sees this)
> - <finding> (source: pass §)
>
> ### P1 — Visible quality issues (fix if you want to be proud)
> - <finding>
>
> ### P2 — Small refinements (nice to fix, safe to defer)
> - <finding>
>
> ### P3 — Elevation moves (turn "competent" into "screenshot-worthy" — optional, Rose's call)
> - <finding>
>
> ### NON-FINDINGS (things I checked that came back clean)
> - <>
>
> ## Rose's decisions needed (batched)
> 1. Which P0 items to fix? (per-item)
> 2. Which P1 items to fix vs defer? (per-item)
> 3. Any P3 elevation moves you want to add? (per-item)
> 4. Any findings you disagree with — this is fine as-is? (per-item)
>
> ## Approved fixes → RDC log
> For every fix Rose approves, add a row to `RDC_LOG_<slug>.md` with:
> - Surface / file:line
> - What it was
> - What Rose changed it to
> - Rose's quote authorizing the fix
> - New screenshot filename (post-fix)
> - Token file updated? Y/N
> ```
>
> ---
>
> **Start with Pass 1a. Do all three passes in order. Do not touch code. Do not add anything. Report and wait.**

---

## Rose-side notes (do NOT paste — for your reference)

- **The AI-adds-nothing rule is the whole point.** Motion / polish / whitespace prompts usually turn into "AI redesigns your build under the banner of quality." This one is survey-only. Every fix is your call, logged as an RDC.
- **Pass 1 (Motion) has the highest failure rate for AIs.** They love to suggest "add a subtle animation here" — which is exactly the drift you're avoiding. If it starts proposing motion, reset: "You're proposing. Survey only. Reset to 1b."
- **Pass 2 (Cleanup/Whitespace) has the highest catch rate.** This is where you'll find the most real findings — off-scale spacing, orphaned elements, inconsistent padding between similar surfaces. Worth running even if you skip 1 and 3.
- **Pass 3 (Wow) is the hardest to score honestly.** The AI will overclaim distinctive elements to please you. Push back: "Would a designer at Apple / Braun / The New Yorker say this is distinctive, or just fine? Answer honestly."
- **The "one detail" question in 3a is diagnostic.** If the AI can name it, the build has a soul. If it can't, that's data — you either add elevation (a distinctive move via RDC) or ship as "competent but not memorable" (which is fine for internal tools, less fine for client-facing).
- **The "embarrass" question repeats from Sanity Check on purpose.** Running it twice at different stages catches things that pass early but appear once the build is more complete.
- **Every approved fix is an RDC.** This keeps the trail clean for Carmen's Phase 1 acknowledgment.
- **Runs in 30–60 minutes for a medium build.** Longer if there are lots of surfaces.
- **When to skip this pass:** internal-only builds where "functional and clean" is enough. Definitely don't skip for `PUB`, `DEMO-PROD`, `PRIV` client-facing types.

---

## END v1
