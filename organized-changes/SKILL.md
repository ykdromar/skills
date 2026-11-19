---
name: organized-changes
description: Guide AI agents to make project changes in organized, reviewable steps. Use when implementing one or more features in a repository.
---

# Organized Changes for Human Review

Use this skill to make requested project changes organized and easy for a human to review, regardless of which AI agent or coding environment is being used. Follow any more specific branch, planning, or delivery instructions the user gives in the request.

## 1. Classify the requested work

Before editing, inspect the repository guidance and current Git state, then parse the request into user-visible features. Treat work as multiple features when it contains independently reviewable outcomes that could reasonably be implemented and delivered separately. Treat implementation details that together deliver one outcome as one feature.

Summarize the feature count and scope to the user. If the request is ambiguous in a way that changes the branch structure or review gates, ask one focused question before changing files. Do not ask questions already answered by the user or repository instructions.

Check the working tree before switching or creating branches. Preserve existing user changes: do not reset, discard, stash, or silently carry unrelated changes onto another branch. If existing changes make a requested branch operation unsafe, explain the concrete conflict and ask how to proceed.

## 2. Choose the branch strategy

For one feature:

- If the user specified a branch or explicitly authorized the current branch, follow that instruction.
- Otherwise, ask whether to work on the current branch or create a feature branch. Wait for the answer before modifying files.
- For a new feature branch, create and switch to it before implementation. Use the repository's naming convention; if none exists, use `feat/<short-feature-name>`.

For multiple features:

- Use the environment's planning capability, if available, to make a plan that identifies the features, their dependencies, and the reviewable implementation units within each feature. Otherwise, write that plan directly and share it with the user.
- Work on one feature branch at a time, in dependency order. Use a separate feature branch for each feature.
- Start the first feature from the appropriate base branch. After completing that feature, stop for the user's review and commit as described below. Only after the user approves the result should you create the next feature branch from the reviewed current branch. This carries forward prerequisite work when later features depend on it.
- If a later feature is independent and should not include earlier feature changes, make that branch from the original base instead, and explain the dependency choice in the plan.

Do not create all feature branches upfront from the same base when later features may depend on earlier work. Do not merge, rebase, or push branches unless the user asks.

## 3. Plan one feature into reviewable units

For every feature, use the environment's planning capability to break implementation into small, logically ordered units that are easy to understand and review. If no planning capability is available, create the plan directly. A unit should deliver a coherent slice, keep the project in a buildable state where practical, and avoid mixing unrelated concerns. Identify the relevant validation for each unit, including the project's applicable build, type-check, lint, or focused test commands.

Show the user the feature plan before implementation. Keep the plan focused on outcomes, files or areas likely to change, dependencies, and how each unit will be checked. Revise it when repository discoveries materially change the scope.

## 4. Implement and hand off one unit at a time

Implement units in plan order. Keep each unit's changes limited to its stated scope. After each unit:

1. Run the relevant checks needed to confirm the unit is coherent and the project builds or compiles without errors where applicable. Report checks that cannot be run and why.
2. Summarize the changes and validation results, and show the user the diff or the relevant files so the work is reviewable.
3. Ask the user to review and commit the unit. Stop implementation and wait. Continue to the next unit only after the user confirms review and commit, or gives a clear instruction to continue without that gate.

Do not make the commit on the user's behalf unless they ask you to commit. Do not begin the next unit while review is pending. At the end of a feature, give a concise feature summary and wait for approval before starting a dependent feature branch.

If review feedback requests changes, update the current unit, rerun relevant checks, and return it for review. Keep new or unrelated requests out of the unit unless the user agrees to revise the plan.

## 5. Keep the user informed

Keep branch transitions and review gates explicit. Before each feature, state the branch and its base. Before each unit, state its goal. At each handoff, report changed areas, validation, and the specific action needed from the user. Do not imply that a feature or unit is complete until its checks and review gate are complete.
