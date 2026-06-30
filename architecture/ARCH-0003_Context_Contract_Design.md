# MKS-HAI-ARCH-0003 Context Contract Design

**Status:** In Progress  
**Scope:** Context Contract Design  
**Depends on:** ARCH-0001 / ARCH-0002

---

## 1. Purpose

This document defines the Context Contracts used by MKS Decision Support Platform and MKS Horse AI.

The purpose is to separate race identity, race participant data, day-of-race conditions, and user decision conditions.

---

## 2. Common Principles

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

## 3. Contract Overview

| Contract | Type | Status |
| --- | --- | --- |
| RaceContext v1.0 | Identity / Context | Approved Draft |
| RaceData v1.0 | Snapshot | Approved Draft |
| RaceCondition v1.0 | Snapshot | Approved Draft |
| UserContext v1.0 | Context | Approved Draft |

---

## 4. RaceContext v1.0

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

## 5. RaceData v1.0

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
