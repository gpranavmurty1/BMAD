# Intent: [PoV Name] — Proof of Value

> **WHY are we running this PoV?**  
> This document captures the hypothesis, goals, evaluation criteria, and decision gate for this AI Proof of Value. It is written for the human team and the stakeholders who will decide whether to proceed.

---

## Problem

_What problem are we trying to solve? Who experiences it and why does it matter enough to investigate now?_

**Who:** [The person / team / system affected]  
**What:** [The pain point, inefficiency, or gap]  
**Scale:** [How often does this happen? What's the cost — time, money, quality, morale?]  
**Why now:** [The trigger — new capability available, leadership priority, competitive pressure, etc.]

---

## Hypothesis

_The single, testable claim this PoV is designed to validate or invalidate. Be specific and falsifiable._

> **We believe that** [an AI-powered capability / approach]  
> **will** [produce a specific outcome]  
> **for** [a specific actor or process]  
> **as evidenced by** [a measurable or observable result within the PoV window]

**Example:**
> We believe that an LLM-assisted triage agent will reduce first-response time on Tier-1 support tickets by >30% for the support team, as evidenced by a side-by-side comparison on 200 historical tickets during the PoV.

---

## Goal

_What does a successful PoV look like in plain language? One to two sentences._

> [e.g. Demonstrate that AI-assisted document review can surface relevant clauses in legal contracts with accuracy sufficient to reduce manual review time, and produce a recommendation on whether to invest in a production system.]

---

## What We Are Trying to Prove

_The specific capabilities or outcomes this PoV must validate. These map directly to the evaluation criteria below._

- [ ] [Capability 1 — e.g. The model can correctly classify ticket intent with >80% accuracy on the test set]
- [ ] [Capability 2 — e.g. End-to-end latency is acceptable for real-time use (<3s per request)]
- [ ] [Capability 3 — e.g. The output format is interpretable by a non-technical end user without training]
- [ ] [Capability 4 — e.g. The approach works on our data, not just benchmark datasets]

---

## What We Are NOT Trying to Prove

_Explicit scope boundaries. These are not gaps — they are deliberate exclusions. Sets honest expectations with stakeholders._

- **Production-readiness:** This PoV does not validate scalability, uptime SLAs, or enterprise security posture.
- **Full feature coverage:** [e.g. We are only testing the classification step, not the downstream workflow automation.]
- **Cost at scale:** Infrastructure costs are not optimised during the PoV; this is addressed in a follow-on epic if we proceed.
- **[Other explicit exclusion]:** [Reason]
- **[Other explicit exclusion]:** [Reason]

---

## Evaluation Criteria

_How we will judge whether the PoV succeeded. Criteria should be agreed with stakeholders before the PoV begins — not after._

### Quantitative Thresholds

| ID | Metric | Minimum Threshold | Target | Measurement Method |
|---|---|---|---|---|
| EC-001 | [e.g. Classification accuracy] | [e.g. >75%] | [e.g. >85%] | [e.g. Human eval on 200-item held-out set] |
| EC-002 | [e.g. End-to-end latency] | [e.g. <5s] | [e.g. <2s] | [e.g. Timed runs in staging environment] |
| EC-003 | [e.g. False positive rate] | [e.g. <15%] | [e.g. <5%] | [e.g. Reviewer audit of flagged items] |

### Qualitative Thresholds

- [ ] [e.g. Subject matter experts rate the outputs as "useful" or "very useful" in structured feedback]
- [ ] [e.g. The demo is compelling enough for the sponsor to greenlight a Phase 1 investment]
- [ ] [e.g. The team has confidence in the approach and is not recommending a pivot]

> **Minimum bar:** The PoV is considered a pass if ALL quantitative minimums are met AND at least [N] of [M] qualitative criteria are satisfied.

---

## Decision Gate

_The explicit outcome this PoV produces. This is agreed upfront — not discovered after the fact._

| Outcome | Condition | Next Step |
|---|---|---|
| **Proceed** | Minimum bar met. Hypothesis validated. | Commission [Epic Name / Phase 1 build]. Transition `spec-pov.md` → full `spec.md`. |
| **Pivot** | Partial results — some criteria met, hypothesis needs refinement. | Run a focused follow-on PoV on [specific gap]. Document learnings in `decision-log.md`. |
| **Stop** | Minimum bar not met. Hypothesis invalidated. | Document why in `decision-log.md`. Redirect effort to [alternative approach or use case]. |

**Decision owner:** [Name — who has authority to call the outcome]  
**Decision date:** [Target date — typically end of W4]  
**Decision forum:** [e.g. PoV showcase + debrief meeting]

---

## Constraints

_Non-negotiable boundaries this PoV must operate within._

| Type | Constraint |
|---|---|
| **Timeline** | [e.g. Must conclude by [Date] — 4 weeks from kick-off] |
| **Data** | [e.g. Only anonymised historical data may be used; no live production data] |
| **Model / Vendor** | [e.g. Must use approved model vendors only — see approved list] |
| **Budget** | [e.g. Max \$X in API/compute costs for the PoV period] |
| **Compliance** | [e.g. No PII in prompts or model inputs without legal sign-off] |
| **Team** | [e.g. Max 2 engineers + 1 subject matter expert; no additional headcount] |

---

## Stakeholders

_Who cares about this PoV and what does each need from it?_

| Stakeholder | Role | What they need from this PoV |
|---|---|---|
| [Sponsor / Executive] | Decision maker | Confidence to invest (or not) in a production system |
| [Domain SME] | Evaluator | Assurance that the AI output is accurate and trustworthy |
| [Engineering Lead] | Builder | A clear technical direction and feasible scope |
| [End User / Team] | Beneficiary | Evidence that this will make their work easier, not harder |
| [Legal / Compliance] | Approver | Confirmation that data usage and model choices are within policy |

---

## Assumptions

_What we are treating as true without full evidence. If any of these are wrong, the PoV plan changes._

- [ ] [e.g. We will have access to at least [N] labelled examples by Week 1]
- [ ] [e.g. The chosen model API is accessible from our environment without procurement delays]
- [ ] [e.g. Subject matter experts can commit [X hours/week] for evaluation during W3–W4]
- [ ] [e.g. The problem is well-defined enough that we can agree on ground truth labels]

---

## Related Artifacts

| Artifact | Link |
|---|---|
| Plan | `plan-pov.md` |
| Spec | `spec-pov.md` |
| Decision Log | `decision-log.md` |
