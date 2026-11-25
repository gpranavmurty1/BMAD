# Plan: [Epic Name]

> **HOW are we going to do this?**  
> This document defines the strategy, phasing, ownership, and risk posture for this epic. The *what* lives in `spec.md`; the *why* lives in `intent.md`.

---

## Approach

_The overarching strategy for this epic. One to three paragraphs covering the method, key trade-offs made, and any significant directional choices. Rationale for choices lives in `decision-log.md`._

> [e.g. We will use a strangler fig pattern to migrate incrementally, keeping the legacy system live until Week 6 when the new system reaches feature parity. We are building rather than buying because...]

---

## Phases & Milestones

_The work staged into phases. Each phase has a clear goal and exit condition before the next begins._

### Phase Overview

| Phase | Goal | Weeks | Exit Criteria |
|---|---|---|---|
| **Phase 1** | [e.g. Foundation] | W1–W2 | [e.g. Infra provisioned, CI/CD green, contracts agreed] |
| **Phase 2** | [e.g. Core Build] | W3–W5 | [e.g. All FR-XXX implemented, internal demo passed] |
| **Phase 3** | [e.g. Hardening] | W6–W7 | [e.g. Load tests pass, NFR-XXX met, security review signed off] |
| **Phase 4** | [e.g. Launch] | W8 | [e.g. Canary at 100%, runbook approved, on-call handed over] |

### Week-by-Week Milestones

| Week | Dates | Phase | Milestone | Owner | Status |
|---|---|---|---|---|---|
| W1 | [DD Mon – DD Mon] | Phase 1 | [e.g. Repo scaffolded, local dev env documented] | [Name] | `Planned` |
| W2 | [DD Mon – DD Mon] | Phase 1 | [e.g. Infra provisioned in staging, CI/CD pipeline green] | [Name] | `Planned` |
| W3 | [DD Mon – DD Mon] | Phase 2 | [e.g. FR-001 and FR-002 implemented and reviewed] | [Name] | `Planned` |
| W4 | [DD Mon – DD Mon] | Phase 2 | [e.g. API-001 to API-003 integrated and tested] | [Name] | `Planned` |
| W5 | [DD Mon – DD Mon] | Phase 2 | [e.g. Internal demo to stakeholders, feedback captured] | [Name] | `Planned` |
| W6 | [DD Mon – DD Mon] | Phase 3 | [e.g. Load test run, NFR-001 and NFR-002 verified] | [Name] | `Planned` |
| W7 | [DD Mon – DD Mon] | Phase 3 | [e.g. Security review complete, runbook drafted] | [Name] | `Planned` |
| W8 | [DD Mon – DD Mon] | Phase 4 | [e.g. Production launch, canary at 100%] | [Name] | `Planned` |

> **Status values:** `Planned` → `In Progress` → `Done` | `At Risk` | `Blocked`

---

## Technical Approach

_The strategy-level technical decisions for this epic. Detailed contracts (schemas, API shapes) live in `spec.md`. This section captures the patterns and choices that shape the build._

### Architecture Pattern
[e.g. Event-driven with async workers behind a REST gateway. No shared database between services.]

### Key Technology Choices
| Decision | Choice | Alternative Considered |
|---|---|---|
| [e.g. Message broker] | [e.g. Kafka] | [e.g. SQS — rejected because cross-region latency] |
| [e.g. Auth mechanism] | [e.g. JWT + refresh tokens] | [e.g. Session cookies — rejected for stateless requirements] |

### Deployment Strategy
[e.g. Blue/green with feature flags. Canary rollout starting at 5% in Week 8.]

### Observability Plan
[e.g. Structured logs to Datadog, traces via OpenTelemetry, alerts defined before launch in Week 7.]

---

## Team & Workstream Ownership

_Who is accountable for each workstream. One owner per workstream — committees own nothing._

| Workstream | Owner | Collaborators | Notes |
|---|---|---|---|
| [e.g. Backend API] | [Name] | [Names] | [e.g. Pairs with frontend on API-001 contract] |
| [e.g. Frontend / UI] | [Name] | [Names] | |
| [e.g. Infrastructure] | [Name] | [Names] | [e.g. Blocking W1 milestone] |
| [e.g. Data / Schema] | [Name] | [Names] | |
| [e.g. QA / Testing] | [Name] | [Names] | [e.g. Owns test-plan.md] |
| [e.g. Stakeholder comms] | [Name] | [Names] | |

---

## Risks & Mitigations

_Identified risks, their likelihood, impact, and the plan to address them._

> **ID format:** `RISK-XXX`  
> **Likelihood:** `Low` | `Medium` | `High`  
> **Impact:** `Low` | `Medium` | `High` | `Critical`

| ID | Risk | Likelihood | Impact | Mitigation | Owner | Status |
|---|---|---|---|---|---|---|
| RISK-001 | [e.g. Upstream team API not ready by W3] | High | High | [e.g. Start with mock contract; escalate to [Name] if no progress by W2] | [Name] | `Open` |
| RISK-002 | [e.g. Load test reveals architecture bottleneck] | Medium | Critical | [e.g. Run spike in W2 to validate approach before full build] | [Name] | `Open` |
| RISK-003 | [e.g. Key engineer unavailable during launch week] | Low | High | [e.g. Cross-train second engineer by W6; runbook must be complete] | [Name] | `Open` |

> **Status values:** `Open` | `Mitigated` | `Accepted` | `Closed`

---

## Dependencies & Blockers

_External dependencies this plan relies on. Items inside the team's control belong in tasks.md._

| ID | Dependency | Needed By | Owner (External) | Fallback if Delayed |
|---|---|---|---|---|
| DEP-001 | [e.g. Security sign-off on data model] | W6 | [Team / Name] | [e.g. Ship with read-only mode; defer write paths] |
| DEP-002 | [e.g. Staging environment access] | W1 | [Infra team] | [e.g. Use local docker-compose; flag as RISK-001] |

---

## Communication & Checkpoints

_How the team stays aligned and how stakeholders are kept informed._

| Checkpoint | Cadence | Format | Participants | Purpose |
|---|---|---|---|---|
| [e.g. Daily standup] | Daily | 15 min sync | Engineering team | Blockers, progress |
| [e.g. Weekly milestone review] | Weekly (Mon) | Async doc update | All workstream owners | Update milestone status table |
| [e.g. Stakeholder demo] | End of Phase 2 (W5) | Live demo | Stakeholders + team | Validate direction before hardening |
| [e.g. Launch readiness review] | W7 | Checklist review | All owners + [Sign-off Name] | Go / No-go decision |

**Escalation path:** [Name] → [Name] → [Name]  
**Decision authority:** [Who has final call on scope changes, delays, or risk acceptance]

---

## Related Artifacts

| Artifact | Link |
|---|---|
| Intent | `intent.md` |
| Spec | `spec.md` |
| Tasks | `tasks.md` |
| Test Plan | `test-plan.md` |
| Decision Log | `decision-log.md` |
