# MKS Decision Support Platform

MKS Decision Support Platform is the architecture and specification repository for MKS Horse AI.

MKS Horse AI is not designed merely to predict which horse will win. It is designed as a horse racing decision support system that helps the user make rational decisions under uncertainty.

## Project Definition

MKS is a Horse Racing Decision Support System.

The purpose of MKS is to support decisions such as:

- Buy
- Skip
- Select bet type
- Allocate budget
- Review results
- Improve future decisions

## Product Structure

```text
MKS Decision Support Platform
└── MKS Horse AI
    └── GPT UI / Conversation Frontend
```

MKS Horse AI is one user-facing interface of the broader Decision Support Platform.

## Core Principles

- Decision Support First
- Process Over Results
- Continuous Improvement
- Explainability
- Expected Value
- Human Centered
- Evidence Based Development
- Stable Architecture

## Repository Structure

```text
charter/
  MKS_Charter_v1.0.md

architecture/
  ARCH-0001_Architecture_Specification.md
  ARCH-0002_Data_Flow_Specification.md
  ARCH-0003_Context_Contract_Design.md

specifications/
knowledge/
reviews/
roadmap/
```

## Current Status

```text
Milestone 1: Completed
Milestone 2: Platform Architecture Freeze - In Progress
```

## Current Documents

- MKS Charter v1.0
- ARCH-0001 Architecture Specification v1.0
- ARCH-0002 Data Flow Specification v1.0 Freeze Candidate
- ARCH-0003 Context Contract Design Draft

## Development Policy

Design first. Implementation later.

The platform freezes architecture and contracts before implementing Prediction Engine, Decision Engine, Betting Strategy Engine, or external API integration.
