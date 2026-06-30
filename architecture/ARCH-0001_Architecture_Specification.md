# MKS-HAI-ARCH-0001 Architecture Specification

**Version:** 1.0  
**Status:** Approved for Freeze  
**Milestone:** MKS-HAI Milestone 2 - Platform Architecture Freeze

---

## 1. Core Principle

MKS Horse AI does not implement prediction engines before architecture is frozen.

Prediction Engine, Decision Engine, and Betting Strategy Engine must not be implemented before the architecture is defined.

This specification defines the structural foundation of MKS Horse AI within MKS Decision Support Platform.

---

## 2. Upper Structure

```text
MKS Decision Support Platform
└── MKS Horse AI
    └── GPT UI / Conversation Frontend
```

MKS Horse AI is a user-facing interface of the platform. The core concept is Decision Support Platform.

---

## 3. Architecture Overview

```text
User Layer
↓
Knowledge Layer
↓
Analysis Layer
↓
Decision Layer
↓
Review Layer
↓
Confidence Layer
↓
Output Layer
```

Data flow is one directional by default.

Reverse flow is prohibited except for explicitly defined review feedback.

---

## 4. Layer Responsibilities

### 4.1 User Layer

Responsibilities:

- Conversation with user
- Race selection
- Paddock image input
- Result input
- Additional user conditions

Prohibited:

- Do not predict
- Do not decide bet strategy
- Do not finalize evaluation

---

### 4.2 Knowledge Layer

Responsibilities:

- MKS Charter
- Course dictionaries
- Surface dictionaries
- MKS Premium
- MKS-L
- Evaluation rules

Prohibited:

- Do not calculate
- Do not predict
- Do not decide bets

---

### 4.3 Analysis Layer

Responsibilities:

- Ability evaluation
- Distance suitability
- Course suitability
- Surface suitability
- Running style evaluation
- Pace analysis
- Jockey evaluation
- Weight evaluation
- Popularity / odds / expected value evaluation

Prohibited:

- Do not decide buy / skip / eliminate
- Do not decide confidence
- Do not add reasons only for display

---

### 4.4 Decision Layer

Responsibilities:

- Buy
- Eliminate
- Use as opponent
- Use as saver
- Skip
- Decide whether a horse can be the axis

Important Principle:

Decision Layer does not choose the strongest horse. It decides the most rational action under the current conditions.

---

### 4.5 Review Layer

Responsibilities:

Technical Review:

- Pace contradiction check
- Evaluation omission check
- Score contradiction check

Betting Review:

- Bet type check
- Budget allocation check
- Skip validity check

Prohibited:

- Do not restart prediction from scratch
- Do not directly modify AnalysisResult
- Do not justify a conclusion after the fact

If required, Review Layer may return feedback to Decision Layer only.

---

### 4.6 Confidence Layer

Responsibilities:

- Evaluate confidence of DecisionResult
- Assign S / A / B / C
- Organize bet strength

Prohibited:

- Do not modify AnalysisResult
- Do not justify DecisionResult
- Do not change bet selections directly

---

### 4.7 Output Layer

Responsibilities:

- Generate final response
- Show marks
- Explain reasons
- Show Confidence
- Show bet strategy
- Explain expected value and risk
- Clearly state skip decision when applicable

Prohibited:

- Do not add new analysis
- Do not change decision for display convenience

---

## 5. Dependency Rule

```text
User
↓
Knowledge
↓
Analysis
↓
Decision
↓
Review
↓
Confidence
↓
Output
```

Review may send feedback to Decision Layer only when major contradiction is detected.

Confidence cannot modify Analysis.

Output cannot modify Decision.

---

## 6. Layer Independence Principle

Each layer owns only its own responsibility.

- Knowledge provides knowledge but does not predict.
- Analysis evaluates but does not decide bets.
- Decision decides actions but does not justify results.
- Review checks quality but does not restart prediction.
- Confidence evaluates reliability but does not alter analysis.
- Output displays but does not change decisions.

---

## 7. Design Rationale

MKS-HAI separates analysis, decision, review, confidence, and output into independent layers.

Reasons:

- Future API integration
- Knowledge replacement
- Independent Decision Engine improvement
- Stronger Review function
- Output format changes without analysis impact
- Long-term extensibility

---

## 8. Definition of Done

ARCH-0001 is completed when:

- Architecture diagram is fixed
- Layer responsibilities are clear
- Data flow is one directional
- Dependencies are defined
- Design does not contradict Charter
- Decision Engine can be implemented later
- Knowledge Layer can be expanded
- API integration can be accepted
- Review / Confidence / Output can be improved independently

---

## 9. Architecture Freeze Statement

The goal of Milestone 2 is not engine implementation.

The goal is Platform Architecture Freeze.

MKS Horse AI is designed first, then improved.
