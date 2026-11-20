---
name: classify-code-changes
description: "Classify a code diff or proposed change as critical or non-critical and explain whether it needs developer review. Use when assessing change risk or routing review."
---

# Classify Code Changes

Use this skill to assess the criticality of a proposed or implemented code change. Classify the change; do not implement it or review every line for defects unless separately asked.

## Workflow

1. Identify the exact proposed change or diff. If the scope is unclear, state what you assessed and what is missing.
2. Consider behavior and downstream effects, not just filenames or the author's label. Follow affected calls, data, and interfaces as far as the available context allows.
3. Apply the criticality criteria below. A change is **critical** if it affects at least one criterion, or if available evidence is insufficient to rule out a material impact. Otherwise classify it **non-critical**.
4. Report the classification, triggering criteria, rationale, scope and uncertainty. Keep the explanation tied to observable code or stated intent.
5. For a critical change, clearly state that developer review is required. Classification is a routing signal, not approval or a claim of correctness.

## Criticality criteria

Classify as critical when the change affects:

- **Architecture or design:** system boundaries, component responsibilities, dependency direction, integration patterns, or a significant design decision.
- **Contracts:** existing DTOs, API requests or responses, events, schemas, serialization formats, or interfaces relied on by another component or client.
- **Persisted data:** database entities, schemas, migrations, data transformations, or the interpretation and lifecycle of stored data.
- **Main flows:** a core user journey or business process, including entry points, decision logic, side effects, and failure handling.
- **Security or privacy:** authentication, authorization, security controls, sensitive data, or personal information handling.
- **High-impact business rules:** payments, billing, entitlements, or other rules where an error can cause material customer or business impact.
- **Production operation:** infrastructure, deployment, release, or configuration changes that can affect production behavior or availability.
- **Concurrency and shared state:** background jobs, parallel execution, synchronization, or shared state where a change can cause loss, duplication, or inconsistency.

Localized changes with limited behavioral impact that do not touch these areas may be classified non-critical. Examples can include documentation wording, formatting, or an isolated internal helper change, but only when the actual diff confirms the low impact.

## Output

Use a concise report:

```text
Classification: Critical | Non-critical
Scope assessed: ...
Why: ...
Criteria triggered: ... | None identified
Uncertainty: ... | None
Developer review: Required | Not required by this classification
```

Do not use “non-critical” as a synonym for “safe,” “correct,” or “approved.” If the change is mixed, classify the overall change as critical and identify the critical portion.
