# Plan: [PoV Name] — Proof of Value

> **HOW are we going to run this PoV?**  
> This document defines the execution strategy, week-by-week schedule, ownership, risks, and showcase plan. The *what* lives in `spec-pov.md`; the *why* and the hypothesis live in `intent-pov.md`.

---

## Approach

_The overarching execution strategy for this PoV. Cover the method, the key directional choices, and why this is the right way to test the hypothesis in 3–4 weeks. Detailed rationale for specific choices lives in `decision-log.md`._

> [e.g. We will run a human-in-the-loop evaluation on a held-out set of historical data. We are not building a live integration in this PoV — we will simulate the workflow end-to-end using a notebook environment and manual triggers. This keeps setup cost low and allows us to validate the AI quality signal before committing to infrastructure. If the PoV passes, the next epic will productionise the pipeline.]

**Build vs. Buy:** [e.g. Using [Model/API] via API — no fine-tuning in this PoV; prompt engineering only]  
**Live vs. Offline:** [e.g. Offline evaluation on historical data — not a live pilot with real users]  
**Depth vs. breadth:** [e.g. Deep on one use case variant — not testing all edge cases or sub-domains]

---

## PoV Phases

_Four fixed phases mapped to the 3–4 week window. Adjust week counts only if timeline differs._

| Phase | Name | Weeks | Goal | Exit Criteria |
|---|---|---|---|---|
| **Phase 1** | Setup & Baseline | W1 | Environment ready, data accessible, baseline established | Dev environment working, dataset prepared, baseline metric measured |
| **Phase 2** | Build | W2–W3 | Core AI component working end-to-end against the eval set | All inputs processed, outputs generated, no blocking errors |
| **Phase 3** | Evaluate | Start of W4 | Quality measured against evaluation criteria in `intent-pov.md` | EC-001 to EC-00X measured; pass/fail determination made |
| **Phase 4** | Showcase & Decide | End of W4 | Decision gate triggered with evidence | Demo delivered, recommendation documented, go/no-go called |

> **Go / No-Go Check:** A formal pass/fail check against the minimum thresholds in `intent-pov.md` happens at the start of W4, before the showcase is prepared. Do not build a showcase for a failing PoV without a deliberate decision to present findings anyway.

---

## Week-by-Week Milestones

| Week | Dates | Phase | Milestone | Owner | Status |
|---|---|---|---|---|---|
| W1 | [DD Mon – DD Mon] | Setup | Development environment configured and accessible to all team members | [Name] | `Planned` |
| W1 | [DD Mon – DD Mon] | Setup | Dataset sourced, cleaned, split into eval and test sets | [Name] | `Planned` |
| W1 | [DD Mon – DD Mon] | Setup | Baseline metric established (current human / rule-based performance) | [Name] | `Planned` |
| W1 | [DD Mon – DD Mon] | Setup | Model API access confirmed, first call working | [Name] | `Planned` |
| W2 | [DD Mon – DD Mon] | Build | Initial prompt / pipeline producing outputs on full eval set | [Name] | `Planned` |
| W2 | [DD Mon – DD Mon] | Build | Evaluation harness built — automated scoring where applicable | [Name] | `Planned` |
| W3 | [DD Mon – DD Mon] | Build | Prompt / approach iterated based on W2 results | [Name] | `Planned` |
| W3 | [DD Mon – DD Mon] | Build | SME spot-check on sample outputs — qualitative signal captured | [Name] | `Planned` |
| W3 | [DD Mon – DD Mon] | Build | Known failure modes documented in `spec-pov.md` | [Name] | `Planned` |
| W4 | [DD Mon – DD Mon] | Evaluate | Full evaluation run on held-out test set | [Name] | `Planned` |
| W4 | [DD Mon – DD Mon] | Evaluate | Go / No-Go check against `intent-pov.md` thresholds | [Name] | `Planned` |
| W4 | [DD Mon – DD Mon] | Showcase | Demo prepared and rehearsed | [Name] | `Planned` |
| W4 | [DD Mon – DD Mon] | Showcase | Showcase delivered to stakeholders | [Name] | `Planned` |
| W4 | [DD Mon – DD Mon] | Showcase | Recommendation documented in `decision-log.md` | [Name] | `Planned` |

> **Status values:** `Planned` → `In Progress` → `Done` | `At Risk` | `Blocked`

---

## Technical Approach

_Strategy-level technical decisions for this PoV. Detailed input/output definitions and model choices live in `spec-pov.md`. This section captures the shape of the solution._

### AI Method
[e.g. Zero-shot prompting with chain-of-thought reasoning using GPT-4o. No fine-tuning. Prompt templates versioned in `/prompts`.]

### Environment
[e.g. Jupyter notebooks in a local Python environment. No cloud infrastructure deployed — API calls only. All outputs logged to a local CSV for analysis.]

### Evaluation Approach
[e.g. Automated scoring via exact match and F1 for structured outputs. Human evaluation via structured rubric for open-ended outputs. SME panel of 2 reviewers.]

### Data Handling
[e.g. All data anonymised before use. No data sent to external model vendors beyond what is approved in the data handling policy. Eval set stored locally, not in cloud storage.]

### Versioning
[e.g. Prompt versions tracked in git. Output snapshots saved with run ID and timestamp for reproducibility.]

---

## Team & Workstream Ownership

_One owner per workstream. PoV teams are small — it is acceptable for one person to own multiple workstreams._

| Workstream | Owner | Collaborators | Notes |
|---|---|---|---|
| AI pipeline build | [Name] | [Names] | Core builder — owns prompt engineering and evaluation harness |
| Data sourcing & prep | [Name] | [Names] | Coordinates with [data team / SME] for access; blocking W1 |
| Subject matter evaluation | [Name / SME] | [Names] | Commits [X hrs/week] from W3; evaluation rubric agreed in W1 |
| Stakeholder comms & showcase | [Name] | [Names] | Owns demo preparation; liaises with sponsor |
| PoV lead / coordination | [Name] | — | Runs weekly check-ins, tracks milestones, owns the decision gate |

---

## Risks

_Key risks to the PoV succeeding within the 3–4 week window._

| Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|
| Data not accessible or insufficient quality by W1 | High | Critical | Confirm access before kick-off; have a fallback synthetic dataset ready | [Name] |
| Model API rate limits or access issues slow W2 build | Medium | High | Test API access in W1 as a hard gate; identify backup model vendor | [Name] |
| SME availability too low for meaningful evaluation | Medium | High | Agree SME commitment in writing before kick-off; cap review to [N] hours total | [Name] |
| Hypothesis is wrong — results are clearly poor by W3 | Low | Medium | This is information, not failure — pivot or stop decision made early; don't push to showcase | [Name] |
| Scope creep into productionisation concerns | Medium | Medium | Refer all production questions to the scale-up path in `spec-pov.md`; freeze PoV scope | [Name] |

---

## Showcase Plan

_How the PoV results are presented to stakeholders. Agreed before W4 so preparation is not rushed._

**Format:** [e.g. 30-minute live demo + 10-minute Q&A]  
**Audience:** [Sponsor, Domain SMEs, Engineering lead, [others]]  
**Date:** [Target date — end of W4]  
**Location / Format:** [e.g. In-person / Zoom / recorded video]

### Demo Structure

| Segment | Duration | Content | Owner |
|---|---|---|---|
| Context & Hypothesis | 5 min | Recap the problem and what we set out to prove | [Name] |
| Live Demo | 10 min | Walk through the AI pipeline on [N] real examples | [Name] |
| Evaluation Results | 10 min | Present metrics against thresholds; show failure cases honestly | [Name] |
| Recommendation | 5 min | Go / Pivot / Stop with rationale | [Name] |

### What Stakeholders Are Being Asked to Decide
[e.g. Whether to commission a Phase 1 production build, estimated at [X weeks / X team members / \$X budget].]

### Definition of a "Yes"
[e.g. Sponsor verbally commits to funding Phase 1. Engineering lead agrees the approach is sound. SMEs rate outputs as useful enough to change their workflow.]

---

## Related Artifacts

| Artifact | Link |
|---|---|
| Intent | `intent-pov.md` |
| Spec | `spec-pov.md` |
| Decision Log | `decision-log.md` |
