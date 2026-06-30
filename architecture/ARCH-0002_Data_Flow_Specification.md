# MKS-HAI-ARCH-0002 Data Flow Specification

**Version:** 1.0 Freeze Candidate  
**Status:** Approved  
**Depends on:** MKS-HAI-ARCH-0001 v1.0  
**Milestone:** Platform Architecture Freeze

---

## 1. Purpose

This specification defines data flow and layer contracts between MKS-HAI layers.

Each layer receives only the defined input and returns only the defined output.

Layers do not depend on internal implementation of other layers.

---

## 2. Data Flow

```text
User Input
↓
RaceContext
↓
KnowledgeContext
↓
AnalysisResult
↓
DecisionResult
↓
ReviewResult
↓
ConfidenceResult
↓
FinalResponse
```

Data flows one direction.

Each layer may reference only previous layer outputs defined by contract.

---

## 3. Layer Contract Overview

### User Layer

Input:

- User Request

Output:

- RaceContext

Examples:

- Race information
- Race date
- Venue
- Race number
- User conditions

---

### Knowledge Layer

Input:

- RaceContext

Output:

- KnowledgeContext

Examples:

- Charter
- Course dictionary
- Surface dictionary
- MKS Premium
- MKS-L
- Evaluation rules

---

### Analysis Layer

Input:

- RaceContext
- KnowledgeContext

Output:

- AnalysisResult

Examples:

- Ability evaluation
- Pace evaluation
- Distance suitability
- Course suitability
- Running style
- Jockey
- Weight
- Popularity
- Expected value

---

### Decision Layer

Input:

- AnalysisResult

Output:

- DecisionResult

Examples:

- Axis candidate
- Opponent candidate
- Eliminate candidate
- Skip decision
- Recommended bet type

---

### Review Layer

Input:

- DecisionResult

Output:

- ReviewResult

Examples:

- Contradiction check
- Evaluation omission
- Pace consistency
- Betting Review
- Feedback requirement

---

### Confidence Layer

Input:

- ReviewResult

Output:

- ConfidenceResult

Examples:

- Confidence grade
- Confidence score
- Bet strength

---

### Output Layer

Input:

- DecisionResult
- ConfidenceResult

Output:

- FinalResponse

Examples:

- Marks
- Reasons
- Confidence
- Bet selections
- Budget allocation
- Skip decision

---

## 4. Data Ownership

Each data contract is owned by the layer that generates it.

| Data | Owner |
| --- | --- |
| RaceContext | User Layer |
| KnowledgeContext | Knowledge Layer |
| AnalysisResult | Analysis Layer |
| DecisionResult | Decision Layer |
| ReviewResult | Review Layer |
| ConfidenceResult | Confidence Layer |
| FinalResponse | Output Layer |

Other layers may reference data but must not modify owned data.

---

## 5. Immutability Rule

Layer outputs are immutable.

If a change is required, generate a new result or snapshot.

- Review cannot modify AnalysisResult.
- Confidence cannot modify DecisionResult.
- Output only displays final data.

---

## 6. Contract over Implementation

MKS-HAI layers do not know engines.

They know contracts only.

For example:

- Analysis Engine can be AI, Python, SQLite, MKS, or API.
- Decision Layer only reads AnalysisResult.

---

## 7. Stable Contract Rule

Contracts are version-controlled.

Example:

```text
AnalysisResult v1.0
AnalysisResult v2.0
```

Future changes must consider compatibility.

---

## 8. Immutable Result Rule

AnalysisResult must not be changed.

If Review finds a contradiction, DecisionResult may be regenerated.

Example:

```text
Analysis
↓
Decision v1
↓
Review
↓
Decision v2
↓
Review
↓
Decision v3
```

Analysis remains unchanged.

---

## 9. Definition of Done

ARCH-0002 is completed when:

- All layer inputs and outputs are defined
- Data ownership is clear
- Data flow is one directional
- Immutable Rule is defined
- Layer Contract is fixed
- Engine implementation can use this document as a basis
