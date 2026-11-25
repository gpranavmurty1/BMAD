# Spec: [PoV Name] — Proof of Value

> **WHAT are we building and evaluating?**  
> This document defines the AI component, its inputs and outputs, evaluation methodology, known limitations, and the scale-up path. It is the source of truth for what gets built and how quality is measured during the PoV.

---

## Overview

_One paragraph. What does this PoV build, what does it evaluate, and what question does the output answer?_

> [e.g. This PoV builds an LLM-powered triage classifier that takes raw customer support tickets as input and produces a category label, priority score, and suggested routing. It is evaluated offline against 500 historical tickets labelled by the support team. The output is a quality measurement and a recommendation on whether to invest in a production integration.]

---

## Scope

| In Scope | Out of Scope |
|---|---|
| [e.g. Classification and routing suggestion for Tier-1 tickets] | [e.g. Automated response generation — separate use case] |
| [e.g. Offline evaluation on historical data] | [e.g. Live integration with ticketing system] |
| [e.g. English-language tickets only] | [e.g. Multi-language support] |
| [e.g. Accuracy, latency, and interpretability assessment] | [e.g. Cost optimisation or infrastructure sizing] |

---

## Functional Requirements

_What the PoV build must do. Kept intentionally narrow — this is not a production spec._

> **ID format:** `FR-XXX`

### FR-001: [Core AI Capability]

**Description:** [What the AI component must do — the central function being tested]  
**Actor:** [Who or what triggers it — user, batch job, API call, etc.]  
**Input:** [What goes in]  
**Output:** [What comes out]  
**Acceptance Criteria:**
- [ ] [e.g. Processes all items in the eval set without error]
- [ ] [e.g. Output schema matches the defined format for every item]
- [ ] [e.g. No hard-coded or rule-based shortcuts — must use AI inference]

---

### FR-002: [Evaluation Harness]

**Description:** Automated or semi-automated system to score AI outputs against ground truth.  
**Actor:** PoV engineer  
**Input:** AI outputs + ground truth labels  
**Output:** Metric scores per evaluation criterion (EC-XXX from `intent-pov.md`)  
**Acceptance Criteria:**
- [ ] [e.g. Scores EC-001 to EC-003 automatically]
- [ ] [e.g. Produces a human-readable report with per-item and aggregate scores]
- [ ] [e.g. Flags items for SME review when confidence is below threshold]

---

### FR-003: [Human Evaluation Interface]

**Description:** A lightweight interface or structured rubric for SME reviewers to score outputs they cannot be automated.  
**Actor:** Subject matter expert  
**Input:** AI output + source item  
**Output:** Structured rating per rubric dimension  
**Acceptance Criteria:**
- [ ] [e.g. Rubric has no more than 5 dimensions to prevent reviewer fatigue]
- [ ] [e.g. SME can complete one review in <3 minutes]
- [ ] [e.g. Ratings are captured in a format that can be aggregated]

---

## AI Approach

_The model, method, and design choices that define how the AI component works._

### Model

| Property | Value |
|---|---|
| **Model / API** | [e.g. GPT-4o via OpenAI API / Gemini 1.5 Pro via Vertex AI] |
| **Access method** | [e.g. REST API / SDK / Local inference] |
| **Approved vendor?** | [Yes / Pending approval from [Name]] |
| **Fine-tuning?** | [e.g. No — prompt engineering only in this PoV] |
| **Context window used** | [e.g. Max 8k tokens per request] |

### Method

| Property | Value |
|---|---|
| **Technique** | [e.g. Zero-shot / Few-shot / Chain-of-thought / RAG / Agent loop] |
| **Prompt strategy** | [e.g. System prompt + user message; templates versioned in `/prompts`] |
| **Output format** | [e.g. Structured JSON / free text / classification label] |
| **Determinism** | [e.g. Temperature 0 for classification tasks; seed fixed for reproducibility] |

### Prompt Design

_High-level description of the prompt structure. Full prompt templates live in `/prompts`._

```
[System prompt summary — e.g. "You are an expert support triage agent. 
Classify the ticket into one of [N] categories and assign a priority 
score from 1-5. Return JSON only."]

[User message structure — e.g. "Ticket: {ticket_text}\nCategory options: {categories}"]
```

**Iteration approach:** [e.g. Prompt versions will be iterated in W2–W3 based on failure analysis. Each version is git-committed with a run log.]

---

## Input / Output Definition

_The contract the PoV validates. Exact formats that producers and evaluators rely on._

### Input

```yaml
# Source: [e.g. Historical ticket export from Zendesk / CSV file]
# Format: [e.g. JSON / CSV]

ticket_id:    string   # Unique identifier for traceability
ticket_text:  string   # Raw ticket content (may include subject + body)
created_at:   datetime # Timestamp of original submission
metadata:     object   # Optional: channel, language, account tier
```

**Preprocessing steps:**
1. [e.g. Strip PII — names, emails, phone numbers — using regex before sending to model]
2. [e.g. Truncate to max 2000 tokens if input exceeds context limit]
3. [e.g. Normalise encoding to UTF-8]

### Output

```yaml
# Format: JSON per item

ticket_id:        string   # Echoed from input for traceability
category:         string   # One of: [Category A, Category B, Category C, ...]
priority:         integer  # 1 (low) to 5 (critical)
confidence:       float    # 0.0–1.0; items below [threshold] flagged for human review
reasoning:        string   # Optional: chain-of-thought explanation (for SME review)
model_version:    string   # Model identifier and prompt version for reproducibility
processed_at:     datetime # Timestamp of inference
```

**Output validation:**
- [ ] `category` must be one of the defined enum values
- [ ] `priority` must be integer 1–5
- [ ] `confidence` must be float 0.0–1.0
- [ ] Items failing validation are logged and excluded from metric calculation

---

## Dataset & Evaluation Methodology

_How the PoV measures whether the AI component works._

### Dataset

| Property | Value |
|---|---|
| **Source** | [e.g. Zendesk export, 6-month historical window] |
| **Total items** | [e.g. 700 labelled tickets] |
| **Eval set** | [e.g. 500 items — used for iterative development in W2–W3] |
| **Test set** | [e.g. 200 items — held out, only used in W4 final evaluation] |
| **Labelling source** | [e.g. Ground truth labels applied by support team leads; inter-rater agreement >85%] |
| **Known biases** | [e.g. Over-represented: billing tickets; Under-represented: escalations] |
| **Data handling** | [e.g. Anonymised before use; stored locally; not uploaded to any external service] |

### Automated Metrics

| ID | Metric | Formula / Tool | Applied To |
|---|---|---|---|
| EC-001 | [e.g. Classification accuracy] | [e.g. Exact match; `sklearn.metrics.accuracy_score`] | [e.g. `category` field] |
| EC-002 | [e.g. Weighted F1 score] | [e.g. `sklearn.metrics.f1_score(average='weighted')`] | [e.g. `category` field] |
| EC-003 | [e.g. Mean absolute error on priority] | [e.g. `sklearn.metrics.mean_absolute_error`] | [e.g. `priority` field] |
| EC-004 | [e.g. P95 inference latency] | [e.g. Timed per-request; measured over 200-item test set] | [e.g. End-to-end pipeline] |

### Human Evaluation Rubric

_For outputs that cannot be automatically scored. Used by SME reviewers._

| Dimension | Description | Scale |
|---|---|---|
| [e.g. Accuracy] | [Is the classification correct based on the ticket content?] | 1 (Wrong) – 5 (Correct) |
| [e.g. Interpretability] | [Is the reasoning explanation clear and trustworthy?] | 1 (Confusing) – 5 (Clear) |
| [e.g. Usefulness] | [Would you act on this output without further review?] | 1 (No) – 5 (Yes, immediately) |

**Reviewer assignment:** [e.g. Each SME reviews 100 items; 20 items reviewed by both for inter-rater reliability check]  
**Aggregation:** [e.g. Mean score per dimension; flag items with disagreement >2 points for discussion]

### Failure Analysis

_Beyond aggregate metrics — understanding where and why the model fails._

- [ ] Generate a confusion matrix for classification outputs
- [ ] Sample and tag 20–30 failure cases by failure type (e.g. ambiguous input, missing context, model hallucination)
- [ ] Document failure patterns in the **Known Limitations** section below
- [ ] Use failure analysis to drive prompt iteration in W3

---

## Known Limitations

_What this PoV build deliberately does not handle. These are expected gaps, not bugs. They inform the scale-up path._

| ID | Limitation | Impact | Addressed in Scale-up? |
|---|---|---|---|
| LIM-001 | [e.g. Non-English tickets not supported] | [e.g. ~15% of ticket volume excluded from PoV] | [e.g. Yes — multi-language model or translation pre-step in Phase 1] |
| LIM-002 | [e.g. Confidence scores are not calibrated] | [e.g. Threshold for human review flag is heuristic, not principled] | [e.g. Yes — calibration step added in production build] |
| LIM-003 | [e.g. No handling of tickets with attachments or images] | [e.g. Text-only; ~8% of tickets excluded] | [e.g. Partial — multimodal model evaluated in Phase 2] |
| LIM-004 | [e.g. Latency not optimised] | [e.g. P95 ~4s; acceptable for async PoV, not for real-time] | [e.g. Yes — batching and caching in production build] |

---

## Edge Cases Tested

_Edge cases explicitly included in the eval set to understand model robustness._

| ID | Scenario | Expected Behaviour | Result (filled in W4) |
|---|---|---|---|
| EC-001 | [e.g. Very short ticket (<10 words)] | [e.g. Model still returns valid output; confidence flagged low] | — |
| EC-002 | [e.g. Ticket in multiple languages] | [e.g. Model processes primary language; limitation noted in output] | — |
| EC-003 | [e.g. Ticket with no clear category] | [e.g. Returns lowest-confidence category; flagged for human review] | — |
| EC-004 | [e.g. Duplicate ticket] | [e.g. Processed independently; no deduplication in PoV scope] | — |

---

## Scale-up Path

_If the PoV passes, what does productionising this look like? This becomes the input to the next epic._

### What changes in a production system

| PoV Approach | Production Equivalent |
|---|---|
| [e.g. Notebook / script runner] | [e.g. Containerised microservice with API endpoint] |
| [e.g. Offline batch on historical data] | [e.g. Real-time inference triggered by ticket creation webhook] |
| [e.g. No auth or rate limiting] | [e.g. mTLS between services, API key management, rate limiting] |
| [e.g. Local file storage for outputs] | [e.g. Database write with audit log] |
| [e.g. Manual SME review of flagged items] | [e.g. Integrated review queue in [tool]] |
| [e.g. No monitoring or alerting] | [e.g. Drift detection, accuracy monitoring, PagerDuty alerts] |

### Estimated lift to productionise

| Area | Estimated Effort | Notes |
|---|---|---|
| Infrastructure | [e.g. 2 weeks] | [e.g. Containerisation, cloud deploy, secrets management] |
| Integration | [e.g. 3 weeks] | [e.g. Webhook from ticketing system, write-back of results] |
| Reliability & monitoring | [e.g. 1 week] | [e.g. Logging, alerting, model drift dashboards] |
| Human review workflow | [e.g. 2 weeks] | [e.g. Review queue UI or integration with existing tooling] |
| **Total** | **[~8 weeks]** | [Rough order of magnitude — not a commitment] |

### Open questions for Phase 1

- [ ] [e.g. Which model tier / deployment option minimises cost at production volume?]
- [ ] [e.g. What is the acceptable false positive rate for routing to a human agent?]
- [ ] [e.g. How do we handle model version upgrades without breaking the production pipeline?]

---

## Open Questions

_Unresolved items that must be answered during the PoV._

| ID | Question | Owner | Due | Status |
|---|---|---|---|---|
| OQ-001 | [e.g. Can we get access to labelled data by W1?] | [Name] | W1 | `Open` |
| OQ-002 | [e.g. Is the model vendor approved by security?] | [Name] | W1 | `Open` |
| OQ-003 | [e.g. What is the inter-rater agreement threshold for the SME rubric?] | [Name] | W2 | `Open` |

> Resolved questions move to `decision-log.md`.

---

## Related Artifacts

| Artifact | Link |
|---|---|
| Intent | `intent-pov.md` |
| Plan | `plan-pov.md` |
| Decision Log | `decision-log.md` |
