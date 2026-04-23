# Data-in-Use Control Model for RAG

## Overview

This pattern defines how Retrieval-Augmented Generation (RAG) systems should be governed at runtime in regulated environments.

The central idea is that AI governance is not only about how data is stored. It is also about how data is retrieved, exposed, reasoned over, and returned during live interactions.

This is a "data-in-use" problem.

## Why This Pattern Matters

Many AI governance approaches focus on:
- storage controls
- masking at rest
- access permissions at the dataset level

Those controls are necessary, but not sufficient for RAG systems.

RAG introduces runtime behavior where:
- user context influences retrieval
- retrieved content affects output generation
- responses may expose information differently than raw storage access would suggest
- tool and workflow interactions can create new control paths

Without runtime controls, a technically secured dataset can still lead to unsafe or non-compliant AI behavior.

## Pattern Objective

The objective of this pattern is to ensure that RAG systems operate within controlled and reviewable boundaries by enforcing governance during live AI interactions.

## Core Control Areas

### 1. Access-Scoped Retrieval
Retrieval should be constrained by:
- user role
- approved data scope
- domain boundaries
- sensitivity classification

The model should prevent users from retrieving content they are not authorized to access, even indirectly through AI.

### 2. Prompt Boundary Controls
The system should define clear rules for:
- what context can be passed into prompts
- how sensitive information is minimized
- what system and policy instructions remain non-overridable
- how embedded instructions in retrieved content are ignored or neutralized

### 3. Response Guardrails
Generated responses should be constrained through:
- policy-aware post-processing
- sensitive content filtering
- output validation rules
- citation or source-linking where appropriate
- escalation paths for high-risk requests

### 4. Runtime Auditability
Each AI interaction should be traceable across:
- input request
- retrieval scope
- retrieved sources
- transformation or filtering steps
- final response output

This supports both operational review and compliance needs.

### 5. Human-in-the-Loop for Higher-Risk Paths
Not all AI interactions should be fully autonomous.

Higher-risk actions may require:
- approval workflows
- reviewer checkpoints
- limited actionability
- controlled handoff to human operators

## Design Principles

- runtime governance is a first-class requirement
- retrieval access must respect the same control intent as direct data access
- deterministic policy controls should bound AI flexibility
- explainability is required for trust
- sensitive outputs should be reduced, not merely logged after the fact

## Where This Pattern Applies

This pattern is relevant for:
- internal enterprise copilots
- healthcare retrieval assistants
- governed search and Q&A systems
- workflow-guided AI experiences
- regulated knowledge access solutions

## Benefits

- reduces risk of unintended information exposure
- improves trust in AI-assisted workflows
- supports compliance and reviewability
- enables safer scaling of RAG in regulated environments
- creates clearer separation between storage security and runtime AI governance

## What Not to Do

Avoid these weak patterns:
- treating dataset-level permissions as sufficient for AI safety
- allowing unrestricted retrieval based only on embedding similarity
- exposing sensitive retrieved text directly without output controls
- relying on logging alone as a governance strategy
- mixing deterministic policy enforcement with uncontrolled AI action paths

---

This pattern helps make RAG systems production-ready by treating runtime interaction governance as an architectural requirement rather than a downstream patch.
