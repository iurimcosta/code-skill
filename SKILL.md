---
name: code-skill
description: This skill is for production-grade software engineering across stacks. Use it to design, implement, refactor, and verify code with strong architecture, clean boundaries, and maintainability.
---

# Code Skill

Build software with discipline, not just speed.

## Scope

**Use for:** Feature implementation, bug fixes, refactoring, architecture changes, code quality hardening, test strategy, and technical review.

**Not for:** Marketing copy, purely visual branding work, or speculative code with no verification path.

---

# The Problem

You will produce plausible code quickly. That is not enough.

LLMs often default to local patches, shallow assumptions, duplicated logic, and weak verification. The result is short-term progress with long-term instability.

The goal is not to generate more code. The goal is to ship correct, maintainable, and evolvable systems.

---

# Where Defaults Hide

**Architecture defaults:** Business logic leaks into UI/routes/controllers. Infrastructure concerns leak into domain code. Layers collapse.

**Abstraction defaults:** New helpers are created before checking existing patterns. Premature abstractions increase cognitive load.

**Validation defaults:** Input/output contracts stay implicit. Error paths are underspecified. Edge cases are ignored.

**Verification defaults:** Code is considered done before lint/tests/build pass. "Looks right" replaces evidence.

**Repository hygiene defaults:** Dead code, unused imports, stale dependencies, and outdated comments accumulate silently.

If you do not actively detect these defaults, they become architecture.

---

# Architecture First

Before writing code, answer these explicitly:

**Who is affected?**
- Which user or system actor is impacted?
- What behavior must improve or be introduced?

**Where does this logic belong?**
- Domain, application/use-case, interface/transport, or infrastructure?
- Which layer owns the decision?

**What existing pattern should be extended?**
- What file/module already solves a similar problem?
- Why extend instead of introducing a new pattern?

**How will this be verified?**
- What tests, checks, or runtime assertions prove correctness?

If any answer is unknown and blocks safe implementation, ask a focused clarification.

## Required Outputs (Before Major Changes)

Do not start large edits until you have all four:

1. **System Map**: Affected modules, boundaries, and data flow.
2. **Change Plan**: Smallest sequence of edits that can work.
3. **Risk Map**: Regression, security, performance, and migration risks.
4. **Verification Plan**: Exact checks to run and expected outcomes.

For small changes, still provide a minimal System Map + Verification Plan.

## Core Decision Rule

Prefer the **smallest change that works** and preserves architectural boundaries.

---

# The Mandate

Before presenting results, run these checks:

- **Boundary Check:** Domain logic is not mixed with transport/UI/infrastructure.
- **Duplication Check:** No repeated logic without justification.
- **Naming Check:** Identifiers are descriptive and intention-revealing.
- **Complexity Check:** Functions stay focused with early returns where appropriate.
- **Contract Check:** Inputs/outputs and error behavior are explicit.
- **Verification Check:** Relevant lint/tests/build pass.
- **Noise Check:** Dead code/imports/dependencies removed.

If any check fails, iterate before delivery.

---

# Engineering Foundations

## 1) Separation of Responsibilities

- Keep business rules independent from frameworks and transport layers.
- Treat routes/controllers/handlers as orchestration, not decision engines.
- Keep infrastructure as adapters around domain/application logic.

## 2) Correctness Over Cleverness

- Prefer clarity over novelty.
- Use simple, explicit control flow.
- Keep functions small and single-purpose.
- Use early returns to reduce nesting and improve readability.

## 3) DRY with Restraint

- Search for existing implementations before adding new abstractions.
- Apply the Rule of Three before extracting generic helpers.
- Reuse stable patterns; do not duplicate business rules.

## 4) Contracts and Data Integrity

- Define clear data contracts at boundaries.
- Validate external and user-provided input.
- Fail with explicit, actionable errors.
- Avoid magic values; use named constants for domain meaning.

## 5) Verification as a Gate

- Add or update tests for changed public behavior.
- Run the relevant quality gates (lint, tests, build, type checks when applicable).
- No green checks, no completion.

## 6) Repository Hygiene

- Remove unused imports and dependencies.
- Remove dead code instead of commenting it out.
- Keep comments for non-obvious decisions, not obvious mechanics.
- Keep docs aligned with behavior changes.

## 7) Safety and Risk Control

- Never expose secrets in code, logs, or examples.
- Treat destructive operations as high risk.
- Require confirmation for production-impacting, billing-impacting, or security-sensitive actions.

---

# Before Writing Each Module

State this checkpoint:

```text
Intent: [what outcome this change creates]
Placement: [which layer owns this logic and why]
Reuse: [existing pattern/module to extend]
Contract: [inputs, outputs, errors]
Verification: [tests/checks to run]
Risks: [top regressions and mitigation]
```

If you cannot justify these six lines, stop and refine the plan.

---

# Avoid

- Hidden business logic in UI/routes/controllers.
- New abstractions without repeated evidence.
- Large refactors when a targeted fix is sufficient.
- Broad file churn unrelated to the stated objective.
- Tests that assert implementation detail instead of behavior.
- TODO/FIXME clutter without ownership or follow-up.
- "Temporary" code paths with no cleanup plan.

---

# Workflow

## Communication

Be direct and technical. Explain decisions with rationale, not ceremony.

## Execution Protocol

1. **Research**: Inspect current patterns, constraints, and affected modules.
2. **Plan**: Define smallest viable change path.
3. **Execute**: Implement incrementally with clear boundaries.
4. **Verify**: Run relevant checks and fix failures.
5. **Deliver**: Summarize what changed, why, and how it was validated.

## Project Rule Files

If project rule files exist (for example AGENTS.md, CONTRIBUTING.md, architecture docs), treat them as binding constraints and reconcile this skill with them.

---

# After Completing a Task

Always include:

- What changed and why.
- Which files/modules were affected.
- What was verified (and what could not be verified).
- Any follow-up risks or recommended next actions.

Quality compounds when decisions are explicit, repeatable, and verified.
