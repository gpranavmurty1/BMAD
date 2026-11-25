# Decision Log

A record of significant operating decisions, their rationale, and alternatives considered.

---

## DL-004 · AI PoV Artifact Variants

**Date:** 2026-11-24  
**Status:** Accepted

### Decision
Create three PoV-specific template variants (`intent-pov.md`, `plan-pov.md`, `spec-pov.md`) for use on AI Proof of Value initiatives with a 3–4 week execution window. These do not replace the standard templates — they are used when the goal is hypothesis validation, not production delivery.

### Key Structural Differences from Standard Templates

| Area | Standard Epic | AI PoV |
|---|---|---|
| `intent.md` | Goals + success criteria | Hypothesis + Decision Gate + What we're NOT trying to prove |
| `plan.md` | 8-week flexible phases, RISK-XXX IDs | 4-week fixed phases (Setup / Build / Evaluate / Showcase), informal risk table, Showcase Plan |
| `spec.md` | Full API contracts, NFRs, process flows | AI Approach, Input/Output definition, Eval Methodology, Known Limitations, Scale-up Path |
| Formal IDs | FR-XXX, NFR-XXX, RISK-XXX, DEP-XXX | FR-XXX retained; risks and deps informal; EC-XXX, LIM-XXX, OQ-XXX added |
| Output | Shippable product | Demo + recommendation (Proceed / Pivot / Stop) |

### Rationale
- A 3–4 week PoV produces a **recommendation**, not a product. The artifact structure must reflect that goal.
- The **Decision Gate** in `intent-pov.md` (Proceed / Pivot / Stop) forces upfront alignment on what success means before the PoV begins — avoiding the common failure mode of post-hoc rationalisation.
- The **Go / No-Go check** at the start of W4 in `plan-pov.md` prevents teams from building a showcase for a failing PoV without a deliberate choice to do so.
- The **Scale-up Path** in `spec-pov.md` ensures the PoV output is immediately usable as input to a Phase 1 epic if the Decision Gate returns Proceed.

### Alternatives Considered
- **Use standard templates with reduced content:** Rejected — the standard templates prompt for sections (NFRs, full API contracts, RACI) that are premature for a PoV and create noise.
- **Single PoV document:** Rejected — collapses WHY / HOW / WHAT; the separation is especially valuable in a PoV where the hypothesis (WHY) is the most important thing to get right.

### Template Locations
- `/templates/intent-pov.md`
- `/templates/plan-pov.md`
- `/templates/spec-pov.md`

---

## DL-003 · plan.md Format

**Date:** 2026-11-24  
**Status:** Accepted

### Decision
Adopt the following format for `plan.md`, scoped per epic, written for the human team:

**Sections:**
1. **Approach** — Overarching strategy (1–3 paragraphs); rationale for choices lives in `decision-log.md`
2. **Phases & Milestones** — Phase overview table with entry/exit criteria + week-by-week milestone table (owner, status per week)
3. **Technical Approach** — Architecture pattern, key technology choices, deployment strategy, observability plan
4. **Team & Workstream Ownership** — One owner per workstream; collaborators and notes
5. **Risks & Mitigations** — Formal `RISK-XXX` IDs; Likelihood / Impact / Mitigation / Owner / Status
6. **Dependencies & Blockers** — External dependencies with fallback plans (`DEP-XXX`)
7. **Communication & Checkpoints** — Cadence, format, participants, purpose; escalation path and decision authority
8. **Related Artifacts** — Links to the other five artifacts

### Rationale
- **Workstream owner table** (not RACI) keeps accountability clear and fast to scan; avoids committee ambiguity.
- **Formal `RISK-XXX` IDs** allow risks to be referenced from milestones, tasks, and the decision log — traceable across the full artifact set.
- **Week-by-week milestones** (not phase-only) give the team a weekly heartbeat for status tracking without prescribing daily task-level detail (that lives in `tasks.md`).
- Phase overview and week table are separated so readers can get the big picture or drill into the schedule as needed.

### Alternatives Considered
- **RACI matrix:** More complete but adds overhead; most epics at this scale need an owner, not a full responsibility matrix.
- **Hard date columns only (no week numbers):** Harder to reason about relative distance and slippage across a plan; week numbers are calendar-agnostic.
- **Phase-based milestones without weekly breakdown:** Too coarse — teams lose the weekly rhythm needed to catch slip early.

### Template Location
`/templates/plan.md`

---

## DL-002 · intent.md Format

**Date:** 2026-11-23  
**Status:** Accepted

### Decision
Adopt the following format for `intent.md`, scoped per epic, written for the human team:

**Sections:**
1. **Problem** — Who is affected, what the pain point is, and why now
2. **Goal** — One or two sentence outcome-oriented statement
3. **Success Criteria** — Split into quantitative (metric / baseline / target / measurement method) and qualitative (checklist)
4. **Out of Scope** — Explicit exclusions with reasons
5. **Constraints** — Tabulated by type (Timeline, Tech, Compliance, Budget)
6. **Stakeholders** — Table of name, role (Owner / Approver / Informed), and their specific need
7. **Related Artifacts** — Links to the other five artifacts in the system

### Rationale
- **Per epic** granularity keeps intent focused and actionable without becoming a project-level vision doc.
- **Human team** audience means plain language over machine-readable structure; tables are used for scannability.
- **Both quantitative and qualitative** success criteria prevents the trap of optimizing only for measurable proxies while ignoring harder-to-measure outcomes.

### Alternatives Considered
- **Per feature:** Too granular — intent at feature level tends to repeat itself or become trivial.
- **Per project:** Too broad — teams lose sight of why any individual epic matters.
- **Qualitative only:** Risks no clear definition of done.
- **Quantitative only:** Risks gaming metrics without achieving real outcomes.

### Template Location
`/templates/intent.md`

---

## DL-001 · Artifact Operating Principle

**Date:** 2026-11-23  
**Status:** Accepted

### Decision
Adopt a structured artifact system where each document answers one distinct question:

| Artifact | Question | Purpose |
|---|---|---|
| `intent.md` | **WHY** | The north star — motivation, goals, success criteria |
| `plan.md` | **HOW** | Strategy and approach to achieve the intent |
| `spec.md` | **WHAT** | Precise definition of what gets built |
| `tasks.md` | **DO** | Actionable work items with clear ownership |
| `test-plan.md` | **VERIFY** | How you confirm the spec was met |
| `decision-log.md` | **WHY THIS APPROACH** | Captures tradeoffs and rejected alternatives |

### Rationale
- Prevents the common failure mode of collapsing strategy (HOW) with definition (WHAT), keeping specs stable even as plans evolve.
- Keeping `intent.md` separate ensures the north star is always accessible and prevents re-litigating goals when scope changes.
- `decision-log.md` captures tradeoffs and rejected alternatives, reducing repeated debate on settled questions.
- `tasks.md` as the execution layer keeps implementation details out of the spec, preserving spec integrity.

### Alternatives Considered
- **Single monolithic doc (e.g., one README):** Rejected — collapses concerns, becomes hard to navigate and maintain as complexity grows.
- **PRD-only approach:** Rejected — PRDs typically blend WHY, WHAT, and HOW without clean separation; verification and decisions are often absent.

### Implications
All artifacts produced in this workspace should respect these roles. An artifact should not bleed into another's question. When in doubt, ask which question the content is answering and place it accordingly.

---

## DL-004 · AI PoV Artifact Variants

**Date:** 2026-11-24  
**Status:** Accepted

### Decision
Create three PoV-specific template variants (`intent-pov.md`, `plan-pov.md`, `spec-pov.md`) for use on AI Proof of Value initiatives with a 3–4 week execution window. These do not replace the standard templates — they are used when the goal is hypothesis validation, not production delivery.

### Key Structural Differences from Standard Templates

| Area | Standard Epic | AI PoV |
|---|---|---|
| `intent.md` | Goals + success criteria | Hypothesis + Decision Gate + What we're NOT trying to prove |
| `plan.md` | 8-week flexible phases, RISK-XXX IDs | 4-week fixed phases (Setup / Build / Evaluate / Showcase), informal risk table, Showcase Plan |
| `spec.md` | Full API contracts, NFRs, process flows | AI Approach, Input/Output definition, Eval Methodology, Known Limitations, Scale-up Path |
| Formal IDs | FR-XXX, NFR-XXX, RISK-XXX, DEP-XXX | FR-XXX retained; risks and deps informal; EC-XXX, LIM-XXX, OQ-XXX added |
| Output | Shippable product | Demo + recommendation (Proceed / Pivot / Stop) |

### Rationale
- A 3–4 week PoV produces a **recommendation**, not a product. The artifact structure must reflect that goal.
- The **Decision Gate** in `intent-pov.md` (Proceed / Pivot / Stop) forces upfront alignment on what success means before the PoV begins — avoiding the common failure mode of post-hoc rationalisation.
- The **Go / No-Go check** at the start of W4 in `plan-pov.md` prevents teams from building a showcase for a failing PoV without a deliberate choice to do so.
- The **Scale-up Path** in `spec-pov.md` ensures the PoV output is immediately usable as input to a Phase 1 epic if the Decision Gate returns Proceed.

### Alternatives Considered
- **Use standard templates with reduced content:** Rejected — the standard templates prompt for sections (NFRs, full API contracts, RACI) that are premature for a PoV and create noise.
- **Single PoV document:** Rejected — collapses WHY / HOW / WHAT; the separation is especially valuable in a PoV where the hypothesis (WHY) is the most important thing to get right.

### Template Locations
- `/templates/intent-pov.md`
- `/templates/plan-pov.md`
- `/templates/spec-pov.md`

---

## DL-003 · plan.md Format

**Date:** 2026-11-24  
**Status:** Accepted

### Decision
Adopt the following format for `plan.md`, scoped per epic, written for the human team:

**Sections:**
1. **Approach** — Overarching strategy (1–3 paragraphs); rationale for choices lives in `decision-log.md`
2. **Phases & Milestones** — Phase overview table with entry/exit criteria + week-by-week milestone table (owner, status per week)
3. **Technical Approach** — Architecture pattern, key technology choices, deployment strategy, observability plan
4. **Team & Workstream Ownership** — One owner per workstream; collaborators and notes
5. **Risks & Mitigations** — Formal `RISK-XXX` IDs; Likelihood / Impact / Mitigation / Owner / Status
6. **Dependencies & Blockers** — External dependencies with fallback plans (`DEP-XXX`)
7. **Communication & Checkpoints** — Cadence, format, participants, purpose; escalation path and decision authority
8. **Related Artifacts** — Links to the other five artifacts

### Rationale
- **Workstream owner table** (not RACI) keeps accountability clear and fast to scan; avoids committee ambiguity.
- **Formal `RISK-XXX` IDs** allow risks to be referenced from milestones, tasks, and the decision log — traceable across the full artifact set.
- **Week-by-week milestones** (not phase-only) give the team a weekly heartbeat for status tracking without prescribing daily task-level detail (that lives in `tasks.md`).
- Phase overview and week table are separated so readers can get the big picture or drill into the schedule as needed.

### Alternatives Considered
- **RACI matrix:** More complete but adds overhead; most epics at this scale need an owner, not a full responsibility matrix.
- **Hard date columns only (no week numbers):** Harder to reason about relative distance and slippage across a plan; week numbers are calendar-agnostic.
- **Phase-based milestones without weekly breakdown:** Too coarse — teams lose the weekly rhythm needed to catch slip early.

### Template Location
`/templates/plan.md`

---

## DL-002 · intent.md Format

**Date:** 2026-11-23  
**Status:** Accepted

### Decision
Adopt the following format for `intent.md`, scoped per epic, written for the human team:

**Sections:**
1. **Problem** — Who is affected, what the pain point is, and why now
2. **Goal** — One or two sentence outcome-oriented statement
3. **Success Criteria** — Split into quantitative (metric / baseline / target / measurement method) and qualitative (checklist)
4. **Out of Scope** — Explicit exclusions with reasons
5. **Constraints** — Tabulated by type (Timeline, Tech, Compliance, Budget)
6. **Stakeholders** — Table of name, role (Owner / Approver / Informed), and their specific need
7. **Related Artifacts** — Links to the other five artifacts in the system

### Rationale
- **Per epic** granularity keeps intent focused and actionable without becoming a project-level vision doc.
- **Human team** audience means plain language over machine-readable structure; tables are used for scannability.
- **Both quantitative and qualitative** success criteria prevents the trap of optimizing only for measurable proxies while ignoring harder-to-measure outcomes.

### Alternatives Considered
- **Per feature:** Too granular — intent at feature level tends to repeat itself or become trivial.
- **Per project:** Too broad — teams lose sight of why any individual epic matters.
- **Qualitative only:** Risks no clear definition of done.
- **Quantitative only:** Risks gaming metrics without achieving real outcomes.

### Template Location
`/templates/intent.md`

---
