# PRD Lifecycle Management

**Scope:** How to maintain a Product Requirements Document over a multi-milestone project
**Applies to:** Any project where milestone planning decisions need to be anchored to explicit
product goals

---

## Core Principle: One Living PRD

A project has one PRD. It is updated as the product vision evolves. It is not versioned per
milestone or release.

**Why not per-version PRDs?**
Per-version PRDs fragment context. When making a feature decision in v0.3, you want a single
document that tells you who the product is for and why — not a chain of versioned documents
to reconcile. ADRs handle version-specific architectural decisions; the PRD handles the stable
question of *who this is for and what they need*.

---

## What a PRD Contains

A lightweight PRD covers four things and nothing more:

1. **User personas** — who uses this and why. Include the context that makes their needs
   non-obvious. Two or three personas is usually enough; more suggests scope creep.

2. **Jobs to be done** — the outcomes users are trying to achieve, expressed as user goals
   rather than features. "Know what weight to use next session" is a job. "Show a weight
   recommendation screen" is a feature. The PRD contains jobs.

3. **Non-goals** — what this product explicitly will not do, for now. Non-goals are as
   important as goals: they are the primary tool for preventing scope creep at milestone
   planning time. Distinguish between *never* and *not yet* — label deferred features clearly.

4. **Success metrics** — how you will know v1.0 (or the relevant version) is working. Metrics
   should be legible to a non-technical stakeholder. "Training max updated correctly after each
   session" is a good metric. "Progression accuracy" is not — it requires additional context.

---

## Two-Tier Update Process

All PRD changes are made via pull request. Changes are classified before the PR is opened.

### Minor

Clarification, added detail, or typo fix with no impact on milestone scope or stakeholder
expectations.

**Process:** Branch → PR → merge. No special justification required beyond a clear PR
description. No changelog entry required (though one is welcome for significant clarifications).

**Examples:**
- Rewording a job description for clarity with no change in meaning
- Adding a measurement method to an existing success metric
- Fixing a factual error that does not affect scope

### Material

Any change to a persona, job, non-goal, or success metric. These changes affect what the
team is building and for whom.

**Process:**
1. Branch → PR
2. PR description must explicitly state:
   - **What changed** — which section, what the old version said, what the new version says
   - **Why** — what new information or decision prompted the change
   - **Which milestone is affected** — if a milestone is in flight, flag it
3. A changelog entry must be added to the PRD (see Changelog section below)
4. **Material changes must land before the affected milestone's planning begins, not after.**
   A PRD change made after sprint planning is a scope negotiation, not a document update.

**Examples:**
- Adding a new user persona
- Adding or removing a job to be done
- Moving an item from non-goals into scope (or vice versa)
- Changing a success metric's target or definition

---

## Changelog

The PRD itself carries a changelog table at the bottom:

```markdown
## Changelog

| Date | Classification | Summary |
|------|---------------|---------|
| YYYY-MM-DD | Initial | Document created |
| YYYY-MM-DD | Material | Added J4: weight tracking for bodyweight-component exercises |
```

This makes the history auditable without reading git blame.

---

## Relationship to Other Documents

| Document | Purpose | Update cadence |
|----------|---------|----------------|
| PRD | Who the product is for and why | Infrequent; only when product vision changes |
| ADRs | Why specific technical decisions were made | Per decision; never amended, only superseded |
| Milestone plan / issues | What will be built in a given cycle | Per milestone |

The PRD anchors the milestone plan. When a feature is proposed for a milestone, the first
question is: which job does this serve? If the answer is not in the PRD, the feature either
needs a PRD update (Material change process) or it does not belong in scope.

---

## Signals That the PRD Needs a Material Update

- A feature is being debated in milestone planning with no clear anchor in the existing jobs
- A new user type is being discussed that does not map to any existing persona
- A non-goal is being revisited because circumstances changed
- A success metric is no longer meaningful given what was actually built

If any of these come up during planning, pause and update the PRD before finalizing the
milestone scope. The PRD exists precisely to make these conversations shorter.
