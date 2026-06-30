# MKS-HAI-ARCH-0003 Contract Specification

**Status:** In Progress  
**Scope:** Contract Specification  
**Depends on:** ARCH-0001 / ARCH-0002

---

## 1. Purpose

This document defines the Contract model used by MKS Decision Support Platform and MKS Horse AI.

ARCH-0003 is divided into:

- ARCH-0003-A: Input Contracts
- ARCH-0003-B: Output Contracts

Input Contracts define race identity, race participant data, day-of-race conditions, and user decision conditions.

Output Contracts define evaluation results, decision results, review results, confidence results, and final presentation.

---

## 2. Contract Taxonomy

Contract Taxonomy defines how each Contract should be understood and classified.

| Category | Purpose |
| --- | --- |
| Identity Contract | Identifies the target uniquely. |
| Snapshot Contract | Holds state at a specific point in time. |
| Context Contract | Holds assumptions and decision context. |
| Evaluation Contract | Holds analysis and evaluation results. |
| Decision Contract | Holds decision results. |
| Review Contract | Holds quality check and consistency review results. |
| Presentation Contract | Holds final user-facing output. |

### Current Contract Categories

| Contract | Category |
| --- | --- |
| RaceContext | Identity Contract |
| RaceData | Snapshot Contract |
| RaceCondition | Snapshot Contract |
| UserContext | Context Contract |
| AnalysisResult | Evaluation Contract |
| DecisionResult | Decision Contract |
| ReviewResult | Review Contract |
| ConfidenceResult | Review Contract / Decision Quality |
| FinalResponse | Presentation Contract |

### Future Extension Note

ConfidenceResult is treated as a Review-related Contract in v1.0.

In future versions, it may be separated as an Assessment Contract if uncertainty, data quality, or model applicability are evaluated independently.

---

## 3. Common Principles

### Minimal Context Principle

Context Contracts hold identity and context only.

They do not hold actual analysis target data.

### Snapshot Principle

Contracts whose state changes are not updated in place.

A new snapshot is generated instead.

Example:

```text
10:00 RaceData v1
12:00 RaceData v2
15:20 RaceData v3
```

### Contract over Implementation

Each layer depends on Contracts, not implementation.

### Immutable Contract Rule

Contracts are immutable after generation.

If a change is required, create a new version or snapshot.

---

## 4. ARCH-0003-A Input Contracts

| Contract | Type | Status |
| --- | --- | --- |
| RaceContext v1.0 | Identity / Context | Approved Draft |
| RaceData v1.0 | Snapshot | Approved Draft |
| RaceCondition v1.0 | Snapshot | Approved Draft |
| UserContext v1.0 | Context | Approved Draft |

---

## 5. RaceContext v1.0

**Owner Layer:** User Layer  
**Purpose:** Identify the race to be analyzed and provide the base context for downstream layers.  
**Version:** 1.0  
**Immutable:** Yes  
**Status:** Approved Draft

### Required Fields

- race_id
- race_date
- venue
- race_number
- race_name
- surface
- distance

### Optional Fields

- course_layout
- grade
- season
- source
- locale

### Out of Scope

RaceContext does not hold entrants, jockeys, frame numbers, horse numbers, weights, popularity, odds, track condition, weather, paddock information, or user settings.

These belong to RaceData, RaceCondition, or UserContext.

---

## 6. RaceData v1.0

**Type:** Snapshot  
**Owner Layer:** User Layer / Data Provider  
**Purpose:** Hold a snapshot of entrants and race participant data corresponding to RaceContext.  
**Version:** 1.0  
**Immutable:** Yes  
**Status:** Approved Draft

### Required Fields

- race_context_id
- snapshot_id
- snapshot_time
- entrants

### Optional Fields

- source
- data_completeness

### Entrants Required Fields

- horse_number
- horse_name

### Entrants Optional Fields

- frame_number
- jockey
- weight
- trainer
- sex_age
- running_style
- odds
- popularity
- body_weight
- body_weight_diff
- previous_results
- marks

### Responsibility

RaceData holds only race participant data.

It does not hold weather, track condition, paddock data, user preferences, or analysis results.

---

## 7. RaceCondition v1.0

**Type:** Snapshot  
**Owner Layer:** User Layer / Data Provider  
**Purpose:** Hold a snapshot of day-of-race condition data corresponding to RaceContext.  
**Version:** 1.0  
**Immutable:** Yes  
**Status:** Approved Draft

### Required Fields

- race_context_id
- snapshot_id
- snapshot_time

### Optional Fields

- weather
- track_condition
- turf_condition
- dirt_condition
- wind
- temperature
- paddock_input
- paddock_notes
- source
- data_completeness

### Responsibility

RaceCondition holds day-of-race condition data.

It does not hold entrants, user preferences, or analysis results.

### Future Extension Note

Paddock information is included in RaceCondition v1.0 for simplicity.

In future versions, horse-level observation data may be separated into PaddockSnapshot.

Potential fields:

- horse_number
- paddock_input
- paddock_notes
- evaluator
- evaluation_time

---

## 8. UserContext v1.0

**Type:** Context  
**Owner Layer:** User Layer  
**Purpose:** Hold user decision conditions such as budget, preferred bet type, risk tolerance, and race policy.  
**Version:** 1.0  
**Immutable:** Yes  
**Status:** Approved Draft

### Required Fields

- user_context_id
- created_at

### Optional Fields

- budget
- preferred_bet_type
- risk_tolerance
- target_race_policy
- bet_unit
- max_tickets
- preferred_strategy
- avoid_strategy
- user_notes

### Responsibility

UserContext does not modify AnalysisResult.

UserContext may influence DecisionResult.

UserContext may influence Betting Review.

It is a contract for adjusting decision-making, not for changing race evaluation.

---

## 9. ARCH-0003-B Output Contracts

ARCH-0003-B will define the following Output Contracts:

- AnalysisResult
- DecisionResult
- ReviewResult
- ConfidenceResult
- FinalResponse

---

## 10. Current Completion Status

```text
ARCH-0003-A Input Contracts
RaceContext v1.0      Approved Draft
RaceData v1.0         Approved Draft
RaceCondition v1.0    Approved Draft
UserContext v1.0      Approved Draft

ARCH-0003-B Output Contracts
Pending
```

ARCH-0003-A Input Contract Design is ready for completion review.
