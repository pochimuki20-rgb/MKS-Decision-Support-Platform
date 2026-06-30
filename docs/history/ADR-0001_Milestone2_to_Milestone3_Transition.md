# ADR-0001: Milestone 2 to Milestone 3 Transition

**Status:** Accepted  
**Project:** MKS Decision Support Platform  
**Context:** Platform Foundation v1.0 / Milestone 3 Schema Design  

---

## 1. Purpose

This ADR records the architectural transition from Milestone 2 to Milestone 3.

It does not define the current specification itself.

It records why the current specification evolved into its present form.

---

## 2. Positioning

This document is a historical architecture decision record.

The current specification remains the GitHub repository's formal Platform Foundation, Architecture, Contract, and Schema documents.

This ADR explains the decision path that led to them.

---

## 3. Key Transition Points

### 3.1 Horse AI to Platform

The project began as MKS Horse AI.

During architecture review, the structure was elevated to:

```text
MKS Decision Support Platform
└── MKS Horse AI
    └── GPT UI / Conversation Frontend
```

Horse AI is now understood as the first interface of the Platform, not the Platform itself.

---

### 3.2 Contract Maturity

The project moved from treating contracts as simple data containers to treating them as responsibility boundaries.

Input Contracts:

- RaceContext
- RaceData
- RaceCondition
- UserContext

Output Contracts:

- AnalysisResult
- DecisionResult
- ReviewResult
- ConfidenceResult
- FinalResponse

This separation enabled later schema design to proceed without mixing identity, snapshots, evaluation, decision, review, and presentation concerns.

---

### 3.3 Snapshot Principle

RaceData and RaceCondition were defined as snapshots.

They are not updated in place.

New states generate new snapshots:

```text
RaceData v1
RaceData v2
RaceData v3
```

This supports history, review, validation, replay, and future API integration.

---

### 3.4 GitHub as SSOT

GitHub was adopted as the Single Source of Truth for approved specifications.

The operating model became:

```text
Proposal
↓
Discussion
↓
PM Review
↓
Approved
↓
GitHub (SSOT)
↓
Specification
↓
Implementation
↓
Validation
```

Chat remains the design and review space.

GitHub remains the official specification space.

HAI follows the approved specification.

---

## 4. Current Maturity Model

The current formal structure is:

```text
Platform Foundation
↓
Information Model
↓
Platform Records
↓
Contracts
↓
Schemas
↓
Engines
↓
Interfaces
```

Earlier discussions were contract-centered.

The current design is record-centered and schema-driven.

This is treated as a natural maturity step, not a contradiction.

---

## 5. Current Project Status

```text
Platform Foundation
Status: Established

Information Model
Status: Established

Platform Record Model
Status: Established

Context Contracts
Status: Completed

Schema Design
Status: In Progress
```

Current deliverable sequence:

```text
RaceEvaluation v1.0
↓
HorseEvaluation v1.0
↓
EvaluationMetadata v1.0
↓
AnalysisResult v1.0
```

---

## 6. Decision

The uploaded transition discussion is not treated as the current specification.

It is treated as historical design evidence explaining why the current specification exists.

Therefore, it is recorded as an ADR under `docs/history/`.

---

## 7. Consequences

Future work shall use the current specification as the authoritative source.

Historical discussions may be referenced to understand design intent, but they do not override current specifications.

Milestone 3 proceeds under Working Agreement v1.0:

- Semantic Correctness
- Responsibility
- Consistency
- Implementability

The next formal task remains:

```text
MKS-HAI-ARCH-0003-B
RaceEvaluation v1.0 Schema
```
