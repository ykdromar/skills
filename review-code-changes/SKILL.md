---
name: review-code-changes
description: "Review a code diff for defects and report evidence-based findings, with developer review routing for critical, architectural, and design changes. Use for local or pull request reviews."
---

# Review Code Changes

Review the requested change and report findings to the developer. This is a review skill: do not edit or repair the code unless the developer separately asks for fixes.

## Review workflow

1. Establish the exact change set from the requested diff, pull request, commit range, or working tree. State the base and scope when they are available; do not silently review a different range.
2. If the `classify-code-changes` skill is available, use it to classify the same change set and include its criticality result. If it is unavailable or the classification cannot be established, say so and request developer review when material risk cannot be ruled out. Never silently treat unknown as non-critical.
3. Read enough surrounding code and relevant project guidance to understand the behavior. Check for correctness defects, regressions, edge cases, contract or data issues, security problems, and missing or inadequate tests. Focus on actionable issues introduced by the change.
4. For every finding, provide severity, concise explanation of impact, and file/line evidence where possible. Do not report speculative concerns as confirmed defects; label uncertainty.
5. If there are no findings, say so explicitly and mention important review limits, such as unavailable context or checks not performed.
6. Give the developer a clear handoff. Require manual developer review when the change is critical, affects architecture/design, or its criticality is unknown due to missing evidence. Agent findings and automated checks do not constitute human approval.

## Architecture and design changes

When the review starts before implementation and the planned change affects architecture or design, first present a concise proposed design before code is implemented. Describe the intended boundaries, responsibilities, important tradeoffs, and affected contracts or data. Keep it as review context; do not implement the change.

When the implementation is available, compare it with the proposal and review both the design outcome and the code. Explicitly ask the developer to review the architectural or design result. If no pre-implementation proposal is available, say that the design assessment is retrospective; do not invent an earlier proposal.

## Report format

Put findings first, ordered by severity. Then provide:

- **Change classification:** critical/non-critical, or unknown, with the reason and any criteria triggered.
- **Developer review:** whether manual review is required and what specifically needs the developer's judgment.
- **Verification and limits:** checks observed or performed, plus material gaps. Do not imply a check was run when it was not.
- **Summary:** brief scope description, only after findings and review status.

For critical changes, identify the affected critical area (for example, contract, persisted data, main flow, security, operations, or concurrency). For architectural/design changes, call out the proposal and implementation comparison. Do not approve, merge, or accept risk on the developer's behalf.
