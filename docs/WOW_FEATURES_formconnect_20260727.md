# Wow Features — formconnect
**Date:** 2026-07-27
**Owner:** Rose
**Product:** FormConnect — Internal Intelligent Form Creator and Management System
**Client anchor:** Jestina (internal) · Kevin at Meridian Roofing (recipient side)

**Product soul (from Round 1 — verbatim):**
- One-thing-no-competitor-does: "It digests information from regular conversation and uploaded documents and fills the form in, it learns and guesses and asks questions that might not be on a regular form."
- Existing wow moment: "Ai form creator studio" — "she doesn't have to map any fields."
- Anti-brief: "be boring."
- Tone in 3 words: "smartest data collection."

## Candidates evaluated: 5
- KEEP (all 4 gates passed): 3
- DROP (failed a gate): 1
- RESHAPE (fixed + retested, now KEEP): 1
- Open (no answer yet): 1 — cross-pollination borrowed pattern

---

## Feature Cards (ranked by jaw-drop-per-effort × honesty × soul)

## Feature: Made-For-Them Forms
**Soul anchor:** Extends "she doesn't have to map any fields" from Jestina's side of the glass to the recipient's — the form arrives already knowing who opened it.
**Jaw-drop moment:** When Kevin at Meridian Roofing opens his renewal form and finds 11 of 14 questions already carrying his own numbers, and the rest asking about his Georgia branch by name, he says "wait, this was made for me?"
**What it actually does:** Every form sent to a company arrives addressed to that company, with the questions it has already answered pre-filled and marked as carried over, and only the genuinely new questions left open.
**How it works:** On send, FormConnect matches the form's fields against the client's stored record and prior submissions, fills what it can, and hides or collapses field groups that don't apply to that company's states, entity type, or domains. Filling is a record lookup, not a guess — no LLM required. Each pre-filled value shows its source and date so the recipient can correct it in one click, and corrections write back to the record after Alyssa approves.
**Seams involved:**
- Client record read: ON — existing stored client data.
- Prior-submission carry-forward: ON — existing submissions data.
- Record write-back on correction: STUB — queued to the governance approval queue; nothing writes downstream unattended.
- Tone/wording tailoring: Ready to Connect — with the seam off, wording comes from the form's own template; no rewriting claimed.
**Honest labeling:**
- Client-facing copy would say: "Pre-filled from your CCA record · last updated 12 Jun 2026 — correct anything that's changed."
- AuditEngine exposure: NONE.
**Effort estimate:** 1–2 weeks.
**Depends on:** Client record completeness; field-to-record mapping on published forms; the existing approval queue for write-backs.
**Blocked by (honest constraints):** Companies with thin records get a mostly empty form — the moment only lands where the record is populated. Needs a minimum-coverage rule before it's promised to anyone.
**First ship version:** Pre-fill plus source-and-date labels on one form type (renewal), with manual send.
**The version that would wait:** Question sets that reshape per recipient — dropping whole sections a company can't be asked about — and wording tailored by the LLM seam.

---

## Feature: Stall-Point Chase
**Soul anchor:** The product asks questions a regular form wouldn't. This applies the same instinct to a stalled form: chase the one question that stopped them, not the form.
**Jaw-drop moment:** When Jestina opens the chase queue and sees "Kevin stopped at bond amount — asked him just that," she says "it chased the right question?"
**What it actually does:** When a form goes quiet, FormConnect names the field the recipient stopped on and sends that single question on its own, rather than resending the whole form.
**How it works:** Partial answers are already captured per field, so the last field touched and the first unanswered required field are both known without any model. A stall rule (no progress for N days, form incomplete) moves the form into a chase queue showing the stall field, how far they got, and a one-question message drafted from a template. Jestina approves or edits before anything sends. Repeat stalls on the same field across clients surface as a form-design problem, which is the second half of the value.
**Seams involved:**
- Per-field partial capture: ON.
- Outbound send: ON — but gated; nothing sends without approval.
- Nudge wording drafted by LLM: Ready to Connect — with the seam off, wording comes from a template library labeled "RoseOS-guided," never "AI-written."
**Honest labeling:**
- Client-facing copy would say: "One quick thing left on your renewal — what's your current bond amount?"
- Internal copy would say: "RoseOS-guided draft — review before sending."
- AuditEngine exposure: NONE.
**Effort estimate:** 1–2 weeks.
**Depends on:** Partial-submission persistence on in-flight forms; the stall threshold being configurable per form; existing notification send path.
**Blocked by (honest constraints):** Requires forms to save progress per field as it's typed; forms that only post on submit have no stall point to name.
**First ship version:** A chase queue with the stall field named and a template message Jestina sends by hand.
**The version that would wait:** Automatic sending on a schedule, and the cross-client "this field stalls everyone" form-design report.

---

## Feature: Next Form Due
**Soul anchor:** "It learns and guesses" pointed forward — the same organ that fills a form in guesses which form is coming.
**Jaw-drop moment:** When Jestina opens Monday's queue and sees a form she hasn't built yet, already carrying Meridian's name and a due date, she says "how did it know that was next?"
**What it actually does:** FormConnect names the forms each client will need next and the date each is due, and stages them before anyone asks.
**How it works:** The six compliance domains already carry dated obligations per client — renewals, annual reports, 300A postings, CE deadlines, registered-agent filings. A rule set walks those dates backward by each form's typical turnaround and stages the matching form template with the client attached. No model needed for the which-and-when. The answer side reuses Made-For-Them pre-fill, so a staged form arrives partly complete. Jestina publishes or dismisses; dismissals train the staging rules by form type.
**Seams involved:**
- Domain deadline data read: ON.
- Form template matching: ON — rule-based mapping from obligation type to form template.
- Answer pre-fill: shares Made-For-Them's seams.
- Guessing forms with no dated obligation behind them: Ready to Connect — with the seam off, FormConnect only stages forms it can point at a real date for, and says so.
**Honest labeling:**
- Internal copy would say: "Staged from Meridian's SOS annual report deadline, 14 Aug 2026."
- Never: "predicted." Every staged form shows the obligation it came from.
- AuditEngine exposure: NONE.
**Effort estimate:** 2–4 weeks.
**Depends on:** Reliable dated obligations per client across the six domains; an obligation-type-to-form-template map; Made-For-Them pre-fill for the answer half.
**Blocked by (honest constraints):** Only as good as the deadline data. Domains with thin coverage stage nothing, and a wrong staged form costs more trust than a missing one — needs a confidence floor and a visible reason line on every staged item.
**First ship version:** One domain (Licensing renewals) staged 45 days out, with the source deadline shown on each item.
**The version that would wait:** All six domains, learned turnaround times per client, and staging for obligations with no date behind them.

---

## The flagship (Round 7): pending Rose's answer
Ask: of these three, which one would you be genuinely sad to not build, even if it's the hardest?

## Dropped candidates (for the record — do not relitigate without new information)
| Candidate | Which gate failed | Why |
|---|---|---|
| Client portal | Soul | A portal belongs to any product in this space, and CCA already has ContractorConnect for contractor-facing status and documents. Capability, not soul — and scoped to the wrong product. Reroute the ask to ContractorConnect. |

## Next steps
- Convert to Spec Sheets: pending Rose's pick — Made-For-Them Forms is the cheapest first ship and the other two depend on its pre-fill.
- Save for later: the two "version that would wait" halves of each card.
- Requires seam flip before viable: LLM wording/tone on Stall-Point Chase and Made-For-Them; undated form staging on Next Form Due.

## Open questions
- Round 2 Q2 (cross-pollination): "not sure." Worth revisiting — the borrowed-pattern answer is where a fourth candidate would come from.
- Does "be boring" extend to the recipient-facing form, or only to the internal console? Made-For-Them assumes boring means quiet and plain, not decorated.
- Minimum record coverage before a Made-For-Them form is allowed to send.
