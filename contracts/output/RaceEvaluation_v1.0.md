# RaceEvaluation v1.0 Schema

**Document:** MKS-HAI-ARCH-0003-B  
**Parent Contract:** AnalysisResult v1.0  
**Status:** Approved Draft  
**Category:** Evaluation Record  
**Owner Layer:** Analysis Layer

---

## 1. Purpose

RaceEvaluation holds analytical evaluation of the target race as a whole.

It is not an aggregation of individual HorseEvaluation records. It represents race-level emergent properties.

---

## 2. Responsibility

RaceEvaluation is responsible for:

- Race-level evaluation
- Race-level pace assessment
- Race difficulty assessment
- Race volatility assessment
- Tactical tendency assessment

RaceEvaluation does not contain:

- Horse-level evaluation
- Decision information
- Confidence information
- Review information

---

## 3. Required Fields

| Field | Type | Responsibility |
| --- | --- | --- |
| race_evaluation_id | UUID | Uniquely identifies RaceEvaluation. |
| pace_prediction | Enum | Represents expected race pace. |
| race_difficulty | Enum | Represents race difficulty. |
| race_volatility | Enum | Represents race volatility. |
| tactical_profile | Enum | Represents race-level tactical tendency. |
| evaluation_summary | String | Summarizes race-level evaluation. |

---

## 4. Optional Fields

| Field | Type | Responsibility |
| --- | --- | --- |
| pace_reason | String | Explains pace evaluation. |
| difficulty_reason | String | Explains difficulty evaluation. |
| volatility_reason | String | Explains volatility evaluation. |
| tactical_notes | String | Adds tactical context notes. |
| remarks | String | Holds supplementary notes. |

---

## 5. Enum Definitions v1.0

### pace_prediction

- Slow
- Medium
- Fast

### race_difficulty

- Low
- Medium
- High

### race_volatility

- Stable
- Moderate
- Volatile

### tactical_profile

- Front Runner Advantage
- Balanced
- Closer Advantage

---

## 6. Notes

RaceEvaluation is not the sum of HorseEvaluation.

RaceEvaluation represents race-level properties that cannot be represented only by horse-level evaluations.

RaceEvaluation is immutable. If the evaluation changes, a new AnalysisResult must be generated.

Future versions may extend optional fields or enum values while preserving required field compatibility.

---

## 7. Approval Record

| Criterion | Result |
| --- | --- |
| Semantic Correctness | Approved |
| Responsibility | Approved |
| Consistency | Approved |
| Implementability | Approved |

**Final Status:** Approved Draft
