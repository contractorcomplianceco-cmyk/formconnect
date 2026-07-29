# Polish + Cleanup + Wow — Form Intelligence Layer Console

**Date:** 2026-07-26
**SHA at survey:** n/a — no VCS in this workspace. Surveyed against `FormIntelligenceLayer.dc.html`, 1,518 lines / 228,929 chars.
**Surveyed by:** Claude (build-side AI)
**Mode:** Report-only. No code was edited. No motion, spacing, or "delight" was added.

**Viewports surveyed:** 1169×754 (live preview, real measurements) and ~1440 effective layout width (root-scaled).
**Coverage caveat, stated up front:** the ≤1180px media queries were still firing during the wide capture, so the *three-column dashboard hero* and the *two-pane Studio / Routing / Submissions / Mapping layouts* could NOT be visually verified at a true 1440. Findings below are limited to layout that does not depend on those breakpoints. This is the same open item carried from the previous pass.

---

## Summary

- **Motion verdict:** `mixed` — screen entry is alive, hover is dead almost everywhere, press state does not exist.
- **Cleanup verdict:** `balanced` visually / `cramped` in the token layer — the console reads well but there is effectively no spacing or type scale underneath it (416 off-scale spacing values, 24 distinct font sizes).
- **Wow verdict:** `competent, with one real idea` — the AI-provenance colour law is genuinely distinctive; everything around it is well-executed standard SaaS.

---

## PASS 1 · MOTION & POLISH

### 1a. Interactive states inventory

| Element type | Default | Hover | Focus | Active/Pressed | Disabled | Loading | Verdict |
|---|---|---|---|---|---|---|---|
| Primary CTA (`accent-grad`) | ✓ | ✓ `filter:brightness(1.07)` + glow | ✗ | ✗ | ✗ | ✓ (spinner, AI generate only) | **fail** — no focus, no press |
| Secondary button | ✓ | ✓ border+colour → accent | ✗ | ✗ | ✗ | n/a | **fail** — no focus, no press |
| Nav link (sidebar) | ✓ | ✓ colour → #FFF (only element with a transition) | ✗ | ✗ | n/a | n/a | **partial** |
| Input field | ✓ | ✗ | ✓ 9 of 32 controls | n/a | ✗ | n/a | **fail** — see below |
| Card (clickable) | ✓ | ✓ (submission rows, table rows) | ✗ | ✗ | n/a | n/a | **partial** |
| Icon button (row menu, revoke, delete) | ✓ | ✓ | ✗ | ✗ | ✗ | n/a | **fail** |
| Tab (builder + governance) | ✓ | ✗ **no hover at all** | ✗ | n/a | n/a | n/a | **fail** |

Measured counts across the file: **`style-hover` × 33 · `style-focus` × 9 · `style-active` × 0 · `:focus-visible` × 0 · `aria-*` × 0.**
Form controls present: 17 `<input>`, 13 `<select>`, 2 `<textarea>` = **32**; 9 carry a focus treatment.
**`outline:none` appears 10×.** Every one of those suppresses the native focus ring; the ones without a paired `style-focus` are keyboard-invisible.
**51 `<button>` elements, 0 focus styles, 0 press states.**

Open Items: (i) no press/active state anywhere in the app; (ii) no focus state on any button; (iii) `outline:none` without a replacement ring; (iv) builder + governance tabs have no hover.

### 1b. Transition audit

Only **4 `transition:` declarations exist in the entire build:**

| Line | Element | Value |
|---|---|---|
| 1254 | sidebar nav item (`navStyle`) | `background .14s, color .14s` |
| 1368 | builder preview card (`previewWrap`) | `box-shadow .12s, border-color .12s` |
| 1372 | toggle track + knob (`tgl`) | `background .15s` / `left .15s` |
| 1435 | analytics funnel bar | `width .4s` |

- **Distinct transition durations: 4** (120 / 140 / 150 / 400 ms). Target 2–4 → **pass on count, fail on intent** — 120/140/150 are three values doing one job.
- **Distinct easings: 2 in use** (`var(--ease-out)`, `linear`) — but **all four `transition` declarations omit the easing entirely**, so they silently run on the CSS default `ease`. Effective easings in the build: **3, one of them unintentional.**
- **Distinct animation durations: 7** (`.14s` menu, `.22s` toast, `.26s` screen entry ×10, `.3s` AI result, `.7s` spinner, `1.4s` AI pulse, `2.4s` status pulse). Combined with transitions: **10 distinct motion durations. Target 2–4 → fail (drift).**
- **Jitter-prone properties: 2.** `transition:'width .4s'` on funnel bars (line 1435) animates layout; `transition:'left .15s'` on the toggle knob (line 1372) animates position. Both should be `transform` if this were being fixed.
- **Sluggish (>500ms on feedback): 0.** The 2.78s AI generate sequence (4 × 620ms + 300ms, line ~1180) is deliberate simulated latency, not feedback lag — not a finding.
- **The dominant finding:** 33 hover states exist, but only 4 elements in the app have a transition. **Every button, tab, icon button and table-row hover snaps instantly with no easing.**

### 1c. Micro-interaction check

| Micro-interaction | Present? | Feels good? | Where it lives | Suggested fix (Rose approves or not) |
|---|---|---|---|---|
| Button press feedback | **N** | — | nowhere | Nothing changes on mousedown across 51 buttons |
| Input focus | Partial | Y where present | topbar search, registry filter, AI textareas, builder settings | 23 of 32 controls have no focus treatment |
| Nav item active state | **Y** | **Y** | `navStyle`, line 1254 | Coral left border + burgundy gradient + white text; the best-resolved state in the build |
| Card hover | Partial | Y | table rows, submission rows, registry rows | Instant — no transition |
| Modal / dialog enter-exit | **N** | skip | no modals in build | — |
| Row-menu enter | **Y** | Y | line 364, `fadeUp .14s` | Enter only; no exit |
| Toast enter/exit | Partial | Y on enter | line 990, `toastIn .22s` | Enter animates; **exit is an instant unmount** after 2800ms |
| Page transitions | **Y** | **Y** | `fadeUp .26s` on all 9 screens | Consistent and correct — note it is `translateY` only, no opacity, so it slides without fading |
| Skeleton loaders | **Y** (AI only) | Y | `aiSteps`, spinner + step ticks | Best moment in the build |
| Empty-state entrance | **N** | — | AI Studio idle state | Appears with no entrance |

### 1d. "Twitchy or dead" check

| Surface | Verdict |
|---|---|
| Dashboard | `mixed` — alive on entry + the pulsing status dot; dead on every card and row hover |
| Registry | `dead` — filters, table rows, row menu all snap |
| AI Studio | `alive` — the only surface with real choreography (spinner → step ticks → `streamIn` result) |
| Builder | `mixed` — preview card has the only easing-correct hover; left list and tabs are dead |
| Routing | `dead` |
| Submissions | `dead` |
| Analytics | `mixed` — funnel bars animate width on mode switch; nothing else moves |
| System Mapping | `dead` |
| Governance | `dead` |
| Design System | `dead` (appropriate — it's a reference surface) |

### 1e. Motion pass summary

```
MOTION & POLISH — Form Intelligence Layer Console
Interactive states complete: 0 / 7 element types (nav is closest, still missing focus + press)
Distinct durations in use: 120/140/150/400ms transitions + 140/220/260/300/700/1400/2400ms animations = 10 (target 2–4)
Distinct easings: 2 declared (--ease-out, linear) + 1 implicit default `ease` on all 4 transitions = 3 (target 1–3, but the third is accidental)
Jitter-prone transitions: 2 (width @1435, left @1372)
Sluggish transitions (>500ms on feedback): 0
Micro-interactions present + feel good: 5 / 10
Surfaces alive / twitchy / dead: 1 alive · 0 twitchy · 6 dead · 3 mixed
Findings: 9 Open Items
```

---

## PASS 2 · CLEANUP & WHITESPACE

### 2a. Spacing scale audit

Measured against a 4/8/12/16/24/32/48/64/96 base scale:

| Property | Distinct values | Off-scale occurrences |
|---|---|---|
| padding | **30** | **192** |
| gap | **18** | **83** |
| margin | **17** | **59** |
| border-radius | **13** | **82** |
| **Total** | — | **416** |

Off-scale padding values in use: `1, 3, 5, 7, 9, 9.5, 11, 13, 14, 15, 17, 18, 19, 22, 26, 30, 34, 36, 44, 60`px.
Off-scale radii: `3, 5, 7, 9, 11, 14, 18`px — sitting alongside on-scale `6, 8, 10, 12`. There are **13 distinct corner radii** where the design-system card says four.
Heaviest single offenders: `9px` (21 paddings + 21 gaps), `11px` (21 paddings + 19 gaps), `15px` (36 paddings), `18px` (39 paddings).

**Type scale: 24 distinct font sizes**, of which **five are half-pixel** (`9.5, 10.5, 11.5, 12.5, 13.5`) accounting for **131 occurrences**. `11.5px` alone is used 54×, `12.5px` 42×. There is no type ramp — sizes were tuned per element.

**Verdict: the visual result is consistent to the eye, but there is no scale underneath it.** Every value is hand-set. This is the single largest cleanup finding in the build and the reason 2d below has so many rows.

### 2b. Alignment audit

| Surface | Left edges consistent | Grid respected | Orphaned element | Crammed element | Optical alignment |
|---|---|---|---|---|---|
| Dashboard | ✓ | ✗ — KPI grid re-flows 4+2 @1169, 5+1 @~1440 | **Yes — 6th KPI tile alone on its own row** (line 221) | — | ✓ |
| Registry | ✓ | ✓ | — | **Yes — the 6 filter selects are ragged;** each sizes to its own content, "All risk" visibly narrowest | ✓ |
| AI Studio | ✓ | not verifiable at 1440 | — | — | ✓ |
| Builder | ✓ | **✗ — `min-width:1024px` (line 446) with no `.fil-panes` collapse; at the user's own 1169px viewport the content area is ~861px, so the whole workspace scrolls horizontally** | — | Left field list truncates most labels to ellipsis at 262px | ✓ |
| Routing | ✓ | ✓ | — | — | ✓ |
| Submissions | ✓ | ✓ | — | — | ✓ |
| Analytics | ✓ | ✓ | — | — | ✓ |
| System Mapping | ✓ | ✓ | — | — | ✓ |
| Governance | ✓ | ✓ | — | — | ✓ |
| Design System | ✓ | ✗ | **Yes — "Clear space & minimum size" alone on row 2 of a 3-up grid** (line 780), two-thirds of the row empty | — | One stray over-indented source line (the 40px mark `<img>`, styleguide "Mark only" card) — cosmetic in source only |
| Topbar (all screens) | — | — | — | **Yes — `⌘K` badge overlaps the search placeholder** | **✗ — measured: input width 210px, `padding-right:12px`, badge starts 36px from the right edge → 24px of typeable/placeholder area runs underneath the badge** (line 141) |
| Sidebar (all screens) | ✓ | — | — | **Yes — measured `nav.scrollHeight 533 > clientHeight 496`; 37px of the nav is clipped at the user's own viewport, with no scroll affordance or fade. "Submissions" is the row cut in half.** | ✓ |

### 2c. Whitespace breathing check

| Surface | Section breathing | Content breathing | Line-height | Max-width | Dead zones | Clusters | Overall |
|---|---|---|---|---|---|---|---|
| Dashboard | 16–20px | 16–22px card padding | ✓ body 1.4–1.6, display 1.05–1.15 | ✓ 1360px | **1 — empty half-row under the KPI grid** | ✓ | **balanced** |
| Registry | 14–16px | 12×16 cells | ✓ | ✓ | — | Filter row | **balanced** |
| AI Studio | 14–18px | 16–20px | ✓ | ✓ | — | ✓ | **airy** |
| Builder | 16px | 13–26px | ✓ | ✓ 640px preview | — | Add-field chip cluster is tight (5px 9px) | **balanced** |
| Routing | 16px | 16–18px | ✓ | ✓ | **1 — "Route preview" card renders header + subtitle over an empty 18px body when no code is selected** (lines 549–554) | ✓ | **unfinished in one place** |
| Submissions | 18px | 20×22px | ✓ | ✓ | **1 — "Missing information" card renders a header over nothing when `missing` is empty** (affects s2, s5, s7; line 619) | ✓ | **balanced** |
| Analytics | 14–16px | 16–18px | ✓ | ✓ | — | ✓ | **airy** |
| System Mapping | 16–18px | 13×16 cells | ✓ | ✓ | — | ✓ | **balanced** |
| Governance | 10–12px between approval cards | 15×18px | ✓ | ✓ 1200px | — | ✓ | **balanced** |
| Design System | 16px | 18–20px | ✓ | ✓ 640px prose / 1120px page | **1 — the orphaned logo card's empty row** | ✓ | **balanced** |

*Note on the 64–96px section-breathing target:* that figure is a marketing-page metric. This is a data console at 14px base; 14–20px between cards is the correct density and I am **not** flagging it. Prose max-widths (560/640px) and data max-widths (1120/1200/1360px) are correctly separated.

### 2d. Orphan + inconsistency sweep

| # | Finding | Evidence | What it should be | Rose's call |
|---|---|---|---|---|
| 1 | **Card header padding differs 10 ways for the same component** | `15px 18px`×12, `15px 20px`×13, `13px 15px`, `13px 18px`, `14px 15px`, `14px 16px`, `14px 18px`, `16px 20px`, `17px 20px`, `22px 26px` | One value (or two: compact / standard) | ☐ |
| 2 | **Table `<td>` padding differs 8 ways** | `12px 16px`×19, `13px 16px`×4, `11px 16px`×4, `12px 10px`×5, `12px 12px`, `12px 14px`, `10px 12px`, `13px 8px` | One value per table density | ☐ |
| 3 | **6th KPI tile orphaned** | line 221, `minmax(184px,1fr)`; measured tops 4+2 @1169px | A grid that resolves to 3×2 or 6×1 | ☐ |
| 4 | **Logo-usage 4th card orphaned** | line 780, `minmax(260px,1fr)` | 2×2 or 4×1 | ☐ |
| 5 | **Registry filter selects are ragged-width** | 6 `<select>` all sized to content; "All risk" narrowest | Uniform min-width (carried open item from previous pass) | ☐ |
| 6 | **Topbar search: 24px of the field sits under the ⌘K badge** | line 141, measured | `padding-right ≈ 46px` | ☐ |
| 7 | **Sidebar nav clips 37px with no affordance** | measured `533 > 496`; "Submissions" cut mid-row | Fade mask, or a shorter footer block | ☐ |
| 8 | **Builder forces horizontal scroll below ~1330px total width** | line 446, `min-width:1024px`, no `.fil-panes` class | Same collapse treatment the other 4 two-pane screens get | ☐ |
| 9 | **Two visually identical row patterns, one clickable and one not** | "Recent Submissions" rows have `style-hover` + `onClick`; "Forms Needing Review" rows above them have neither, and look the same | Either make both interactive or differentiate them | ☐ |
| 10 | **Toast animates in, disappears instantly** | line 990 `toastIn .22s`; `setTimeout(…, 2800)` unmounts with no exit | Symmetric exit | ☐ |
| 11 | **13 distinct border-radii** | 2/3/5/6/7/8/9/10/11/12/14/18/999px | The 4 the Design System page itself documents (6/8/12/16 + pill) — **the build contradicts its own published spec** | ☐ |
| 12 | **131 half-pixel font sizes** | 9.5/10.5/11.5/12.5/13.5px | Whole-pixel ramp | ☐ |

### 2e. Cleanup sweep — code / copy debris

| Check | Result |
|---|---|
| `console.log` | **none** ✓ |
| Commented-out code | **none** ✓ |
| Debug / DEV-MODE UI | **none** ✓ |
| Placeholder copy (`Lorem`, `TODO`, `[COPY TBD]`, "Coming soon") | **none** ✓ |
| Dev URLs / sample credentials | **none** ✓ (all mock data is in-character: `CCA-7H2K-9QX4`, `tok_••••4417`, `59-•••••••` — correctly masked) |
| **Empty `<sc-if>` blocks left behind** | **3 — lines 550, 551, 619.** Residue from the paired-negation fix in the previous pass. They render nothing and are the reason findings 2c/Routing and 2c/Submissions have header-over-nothing cards. |
| **Duplicate method definition** | **`setAiEvt` is defined twice — lines 1166 and 1230.** Identical behaviour; the second silently overwrites the first. |
| **Dead code in the logic class** | `resetAi()` (defined, never referenced) · `anSelStyle` (exposed, template uses `anSelStyleFull`) · `posLive` / `posCompletion` / `posSystems` (exposed, never read by the template — leftovers from the pre-reskin posture panel) · `codesRows[].selected` and `sources[].pctN` / `devices[].pctN` (computed, never read) |
| **Half-implemented UI** | Topbar search input (not wired) · `⌘K` badge (**promises a shortcut that does not exist**) · notification bell with a "6" badge (not wired) · "Add condition" (toast only) · row-menu "View details" (toast only) — *seams are intentionally off per the build brief; the `⌘K` affordance is the one that reads as broken rather than unwired* |
| Stray source formatting | One over-indented `<img>` line in the styleguide "Mark only" card — source-only, no visual effect |

### 2f. Cleanup pass summary

```
CLEANUP & WHITESPACE — Form Intelligence Layer Console
Spacing values on-scale: N — 416 off-scale occurrences across padding/gap/margin/radius
Alignment issues: 5 (KPI orphan, logo-card orphan, ragged filter selects, ⌘K overlap, nav clip)
Breathing verdict: balanced (density is correct for a console; the token layer is not)
Dead zones: 3 (Route preview empty card, Missing-information empty card, KPI half-row)
Orphans / inconsistencies: 12
Code/copy debris: 6 (3 empty sc-if, 1 duplicate method, 6 unused values, 1 stray indent) — no logs, no TODOs, no placeholder copy
Findings: 23 Open Items
```

---

## PASS 3 · WOW FACTOR

### 3a. The "one moment" survey

**The one detail a discerning viewer would notice in 60 seconds:**
> The dashboard hero's **signal wave** — four hairline strokes running coral → magenta → purple on a single gradient, passing *behind* the posture ring and *under* the metric stack rather than being boxed into a chart well. (Lines 172–180.) It is the only element in the build that behaves like graphic design rather than UI.

Honest qualifier: it is decorative. It carries no data. A designer would notice it; a user would not miss it.

### 3b. The "screenshot moment" check

| Surface | Verdict | Why | What would make it screenshot-worthy (Rose decides — NOT implemented) |
|---|---|---|---|
| Dashboard | **screenshot-worthy** | Hero panel: gradient ring, governance statement, signal wave, stacked metrics | Fix the orphaned 6th KPI tile — it's the one thing that breaks the frame |
| Design System | **screenshot-worthy** | Logo-usage board, colour law, the AI-vs-approved comparison cards | Fix the orphaned 4th logo card |
| AI Studio | **screenshot-worthy** (in the `done` state) | The dashed magenta boundary, the AI-DRAFT chip, "not a saved record", the duplicate/missing warning pair | Nothing — this is the strongest surface |
| Governance | professional but forgettable | Clean audit list with kind-coded glyphs; reads like every audit log | The approvals tab has the real drama (5 pending sensitive writes) but opens on the audit tab |
| Registry | professional but forgettable | Competent dense table | Ragged filter row is what stops it |
| Submissions | professional but forgettable | Good list/detail; Rose OS summary block on ink is nice | The empty "Missing information" card undercuts it |
| Analytics | professional but forgettable | Standard funnel + bars | — |
| System Mapping | professional but forgettable | The `→` arrow column turning red on mismatch is a nice touch nobody will notice | — |
| Builder | **functional but rough** | Three panes work, but labels truncate and the whole thing side-scrolls below ~1330px | Fix the horizontal scroll first |
| Routing | **functional but rough** | The empty "Route preview" shell | An empty state |

**Screenshot-worthy: 3 / 10.**

### 3c. The distinctive-element inventory

Scored against the honest bar — *would a designer at Braun or The New Yorker call this distinctive, or just fine?*

1. **The AI-provenance colour law.** Magenta means "a machine made this and it is not yet real": dashed magenta boundary, magenta AI-DRAFT chip, magenta focus ring on AI-filled inputs, pink footer restating "sending to review does not write to Zoho CRM." Codified on the Design System page as a rule, then actually obeyed across four screens. **Genuinely distinctive** — most products render AI output identically to records. This is the build's one real idea.
2. **The signal wave + gradient posture ring.** Distinctive as craft, not as thinking. A good designer would say "nice", not "clever."
3. **The refusal copy.** "Every sensitive write passes human approval." · "Rose OS drafts suggestions only." · "Draft-only · cannot write" as an access-role scope. Anti-promise voice, not SaaS-generic. **Distinctive** — but it is item 1 expressed in words, so I am counting it as 1.5 findings, not 2.

**Honest count: 1 strong distinctive element, 1 supporting craft moment.** Everything else — white cards, 12px radius, dark rail, pill badges, segmented controls — is competent standard SaaS. It is well-executed standard, not distinctive standard.

### 3d. The "would embarrass Rose" check

**One answer:**
> **The `⌘K` badge sitting on top of the search placeholder in the topbar.** It is present on all ten screens, it is in the top-right of every screenshot, it is 24px of measurable overlap, and it advertises a keyboard shortcut that does nothing. A client will read it as "unfinished", not "seams off."

Runner-up (not the answer, but close): the empty **Route preview** card on the Routing screen, which is the first thing a client sees on that screen and looks like a component that failed to load.

### 3e. Wow pass summary

```
WOW FACTOR — Form Intelligence Layer Console
The one detail a discerning viewer would notice: the coral→magenta→purple signal wave running behind the dashboard posture ring
Screenshot-worthy surfaces: 3 / 10
Distinctive elements found: 1 strong (AI-provenance colour law, obeyed across 4 screens) + 1 supporting (hero wave + gradient ring)
Embarrassment risk: the ⌘K badge overlapping the topbar search placeholder on all 10 screens
Overall verdict: competent but not yet memorable — one real idea, three fixable defects standing in front of it
```

---

## All findings, bucketed by severity

### P0 — Would embarrass Rose (fix before any client sees this)
- **⌘K badge overlaps the search placeholder by 24px on all 10 screens.** `padding-right:12px` vs badge at `right:10px`. (§2b, §3d · line 141)
- **"Route preview" renders as an empty card shell** when no code is selected — header, subtitle, then nothing. (§2c · lines 549–554)

### P1 — Visible quality issues (fix if you want to be proud)
- **Builder side-scrolls the entire workspace below ~1330px viewport** — it is the only screen with no responsive collapse. (§2b · line 446)
- **Sidebar nav clips 37px with no scroll affordance**; "Submissions" is cut mid-row at the user's own 1169×754. (§2b)
- **6th KPI tile orphaned on its own row** (4+2 @1169, 5+1 @~1440). (§2b · line 221)
- **"Missing information" card renders a header over nothing** on 3 of 8 submissions. (§2c · line 619)
- **3 empty `<sc-if>` blocks left behind** from the previous pass's negation fix. (§2e · lines 550, 551, 619)
- **`setAiEvt` defined twice** — the second definition silently overwrites the first. (§2e · lines 1166, 1230)
- **No press/active state on any of 51 buttons; no focus state on any button; 23 of 32 form controls have no focus treatment; `outline:none` used 10× without replacement.** (§1a)
- **Registry filter selects are ragged-width** — carried open item. (§2b)

### P2 — Small refinements (nice to fix, safe to defer)
- 33 hover states, 4 transitions — hover snaps everywhere except nav, builder preview, toggles. (§1b)
- All 4 `transition` declarations omit their easing and silently fall back to CSS default `ease`. (§1b)
- 10 distinct motion durations against a target of 2–4. (§1b, §1e)
- Toast animates in, vanishes with no exit. (§1c)
- 2 jitter-prone transitions: `width` on funnel bars, `left` on toggle knobs. (§1b · lines 1435, 1372)
- Builder and Governance tabs have no hover state at all. (§1a)
- "Forms Needing Review" rows look identical to the clickable "Recent Submissions" rows but are inert. (§2d #9)
- Logo-usage 4th card orphaned in a 3-up grid. (§2b · line 780)
- Dead values in the logic class: `resetAi`, `anSelStyle`, `posLive`, `posCompletion`, `posSystems`, `codesRows[].selected`, `pctN` ×2. (§2e)
- `⌘K`, topbar search, and the notification bell are unwired affordances. (§2e)
- Builder left-list labels truncate to ellipsis at 262px. (§2b)

### P3 — Elevation moves (optional — turn "competent" into "screenshot-worthy")
- **Card header padding: 10 different values for one component.** Collapsing to one (or a compact/standard pair) is the single highest-leverage cleanup in the build. (§2d #1)
- **Table `<td>` padding: 8 different values.** (§2d #2)
- **13 distinct border-radii where the build's own Design System page publishes 5** — the product contradicts its own spec on the page that states the spec. (§2d #11)
- **131 half-pixel font sizes across 24 distinct sizes** — no type ramp. (§2a, §2d #12)
- **416 off-scale spacing occurrences.** A real token pass (padding/gap/margin/radius) is the difference between "looks consistent" and "is consistent."
- Governance opens on **Audit trail**; the **Approvals** tab (5 pending sensitive writes, the product's whole thesis) is one click away and unseen.
- The AI Studio `done` state is the strongest surface in the build and is only reachable after a 2.8s generate — nothing on the Dashboard points at it.

### NON-FINDINGS (checked, came back clean)
- No `console.log`, no commented-out code, no `TODO`, no `Lorem`, no placeholder copy, no debug UI, no DEV banners, no dev URLs.
- Mock data is in-character and correctly masked throughout (`tok_••••4417`, `59-•••••••`, `CCA-` code format consistent across all 7 codes).
- Prose max-widths (560/640px) and data max-widths (1120/1200/1360px) are correctly separated.
- Line-height discipline holds: body 1.4–1.6, display 1.05–1.25.
- Screen-entry animation (`fadeUp .26s var(--ease-out)`) is applied identically to all 9 screens — no drift.
- Semantic colour never loses to brand colour; every status badge pairs tint with a written label; connection health pairs dot with status word. The accessibility claim on the Design System page is actually kept.
- Dark theme token set is complete and parallel to light.
- Copy voice is consistent — no SaaS-generic filler found on any surface.
- The real FormConnect logo asset is used as delivered on all 6 placements; no redraw, no recolour.

---

## Rose's decisions needed (batched)

**1. P0 — fix both?**
- ☐ 1a. ⌘K / search overlap
- ☐ 1b. Route preview empty state

**2. P1 — fix or defer, per item?**
- ☐ 2a. Builder horizontal scroll · ☐ 2b. Sidebar nav clip · ☐ 2c. KPI orphan tile
- ☐ 2d. Missing-information empty card · ☐ 2e. 3 empty `sc-if` blocks · ☐ 2f. Duplicate `setAiEvt`
- ☐ 2g. Focus + press states (this is the largest single P1 — ~84 elements) · ☐ 2h. Filter select widths

**3. P3 — any elevation moves you want?**
- ☐ 3a. Card-header padding → one value · ☐ 3b. Table-cell padding → one value
- ☐ 3c. Radii → the 5 the Design System page publishes · ☐ 3d. Whole-pixel type ramp
- ☐ 3e. Full spacing-token pass · ☐ 3f. Governance opens on Approvals

**4. Any finding you disagree with — fine as-is?**
Candidates I'd expect you to wave off: the unwired bell/search (seams off by design), the 64–96px section-breathing target (wrong metric for a console), the builder label truncation (correct at 262px), the AI generate 2.8s delay (deliberate).

**5. Blocking question before any of the above:**
The three-column dashboard hero and the four two-pane screens still have **not** been seen at a true 1440. If you have a 1440 monitor, that check should happen before we spend effort on P1 layout fixes — a real 1440 pass could add findings or retire some.

---

## Approved fixes → RDC log

*Empty pending Rose's decisions. On approval, each row moves to `RDC_LOG_form-intelligence-layer.md` with: surface / file:line · what it was · what Rose changed it to · Rose's authorizing quote · post-fix screenshot filename · token file updated Y/N.*
