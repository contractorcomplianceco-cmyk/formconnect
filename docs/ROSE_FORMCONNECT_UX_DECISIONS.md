# FormConnect — Rose UX Decisions Package

**Product:** FormConnect  
**Date:** 2026-08-03  
**Evidence input:** Completed internal staff UX review  
**Overall verdict (review):** PARTIALLY STAFF-READY — WORKFLOW REVISIONS REQUIRED  
**Live / tip:** `https://forms.cagteam.net` · `main` @ `557364d`  
**Status:** PAUSED / HOLDING · Partner share **NO** · Public go-live **NO**  
**RDC-008:** CLOSED (AuditEngine → RoseOS on public prototype) — **preserve**  
**Rose P0 design-flow yes (2026-08-03):** Search=B · Builder=B · Version SoT=A · Assign=A — **prototype honesty UX only** on tip branch `tip/formconnect-p0-ux-2026-08-03`. No live deploy / merge / wiring.

**Implementation:** Tip UX corrections in progress for Rose review (screenshots + SHA). Still **no** live wiring, integrations, schema/auth, deploy, merge, partner share, or public go-live from this pass.

---

## Naming (all decisions)

- **Nova** = client-facing assistant  
- **RoseOS** = intelligence powering Nova  
- **AuditEngine** = never named or described on client / public / staff surfaces  

Unwired behavior → “Ready to Connect” / planned / preview only. No fake success states.

---

## Present to Rose now — P0 only

### UX-P0-01 — Global search

| Field | Content |
|-------|---------|
| **Exact current reality** | Header search accepts input and advertises ⌘K but returns no results, filters, or navigation. |
| **Visible staff impact** | Search looks live; staff expect results and get none — trust break / false affordance. |
| **Rose decision question** | Should FormConnect have real local search now, an honest unavailable state, or remove search from the shell? |
| **Options** | **A)** Real client-side search across Registry/Submissions first (bounded; separate build yes later) · **B)** Visibly unavailable / coming-soon until a later search system · **C)** Search removed from the current shell |
| **Recommendation** | **B** — unless Rose explicitly approves a bounded local-search build. |
| **Why** | Matches paused phase; avoids implying a search system that does not exist. |
| **What remains unavailable** | Result lists, filters, keyboard navigation to records, any search backend. |
| **Future visual preview safe?** | **Yes** — can mock “coming soon” UI without wiring. |
| **Future wiring required?** | **Yes** for A; **No** for B/C beyond copy/affordance honesty. |
| **Related route/surface** | Global header / command palette affordance on prototype shell |
| **Explicit** | **No implementation approved.** |

---

### UX-P0-02 — Builder work-state model

| Field | Content |
|-------|---------|
| **Exact current reality** | Staff can add fields but there is no Save, Publish, Discard, Cancel, Back, or Exit state. |
| **Visible staff impact** | Builder feels editable with no safe exit or review path; risk of believing work is persisted. |
| **Rose decision question** | What is the intended **non-live** Builder workflow? |
| **Options** | **A)** Explicit local design-preview state with discard/review language · **B)** Draft → review-gated approval flow (no persistence/publish implied until separately approved) · **C)** Builder temporarily unavailable until its state model is approved |
| **Recommendation** | **B**, with no persistence or publish behavior implied until separately approved. |
| **Why** | Matches stated review-gated governance direction without wiring storage. |
| **What remains unavailable** | Real save, publish, durable drafts, approvals pipeline, discard persistence. |
| **Future visual preview safe?** | **Yes** — language/states can be previewed without backend. |
| **Future wiring required?** | **Yes** before any real draft/publish; preview-only can ship after separate yes. |
| **Related route/surface** | Builder / form studio on prototype |
| **Explicit** | **No implementation approved.** |

---

### UX-P0-03 — Version source of truth

| Field | Content |
|-------|---------|
| **Exact current reality** | Builder shows Contractor Onboarding Intake as **v4.3 draft**; Registry and Governance → Versions show **v4.2 Published**; no v4.3 in the Versions ledger. |
| **Visible staff impact** | Conflicting version truth; staff cannot tell published vs working draft. |
| **Rose decision question** | Which surface is authoritative, and how should unpublished working drafts vs published versions be named and displayed? |
| **Options** | **A)** Governance Versions = SoT; Builder must visibly label unpublished working draft ≠ published ledger · **B)** Builder draft is SoT until published (ledger lags by design — must say so) · **C)** Freeze Builder version display until ledger and Builder reconcile under an approved model |
| **Recommendation** | **A** (Governance Versions = source of truth; Builder distinguishes unpublished working draft). |
| **Why** | Prevents silent “v4.3 published” implication; ledger remains operational SoT. |
| **What remains unavailable** | Auto-ledger of drafts; publish promotion; true version history wiring. |
| **Future visual preview safe?** | **Yes** — labeling/copy can be previewed. |
| **Future wiring required?** | **Yes** for real version promotion; **No** for honest labels only (after yes). |
| **Related route/surface** | Builder · Registry · Governance → Versions |
| **Explicit** | **No implementation approved.** |

---

### UX-P0-04 — Submission ownership and handoff

| Field | Content |
|-------|---------|
| **Exact current reality** | “Assign owner” self-assigns to Alyssa, offers no picker, shows no persistent owner, and has no acceptance/handoff state. Governance shows the internal staff roster. |
| **Visible staff impact** | Looks like a real assignment happened; operational handoff is fake. |
| **Rose decision question** | Should assignment be a preview, a future real flow, or removed until the ownership model is decided? |
| **Options** | **A)** Review-gated handoff **preview** (do not imply a real assignment) · **B)** Actual persisted staff assignment flow after separate wiring approval · **C)** Unavailable / removed until the operational ownership model is decided |
| **Recommendation** | **A** for the current paused phase. Do not imply a real assignment happened. |
| **Why** | Keeps roster visible as design context without lying about persistence. |
| **What remains unavailable** | Persistent owner, picker, acceptance, notifications, audit of handoff. |
| **Future visual preview safe?** | **Yes** for A; B requires wiring approval first. |
| **Future wiring required?** | **Yes** for B; A is honesty/preview only after separate UI yes. |
| **Related route/surface** | Submissions · Governance staff roster |
| **Explicit** | **No implementation approved.** |

---

## Parked — P1 (do not present until Rose answers P0)

Recorded from staff UX review. **Not asking Rose yet.**

| ID | Topic | One-line reality |
|----|-------|------------------|
| UX-P1-01 | Mobile Builder layout | Builder layout not staff-ready on mobile |
| UX-P1-02 | Registry “View details” | Dead-end control |
| UX-P1-03 | Notification bell | Bell present; no destination |
| UX-P1-04 | Analytics audience-toggle | Scope mismatch vs audience |
| UX-P1-05 | Route/record navigation | Non-linkable navigation patterns |

Each P1 will later get the same decision template. **No implementation approved.**

---

## Stop

Await Rose’s explicit **A/B/C** (or written decision) on UX-P0-01…04 and Adoption Pass product unknowns.  
No application code, schema, routes, roles, permissions, integrations, `main` app tip, or deployment changes from this document.
