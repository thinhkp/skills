---
schema: "agent-context/v1"
updated_at: "{{actual ISO 8601 timestamp with timezone}}"
project: "{{project identity; no credentials or secret-bearing URLs}}"
workstream: "{{default or stable task slug}}"
status: "in_progress"
---

<!-- Fill from evidence. Remove drafting comments and replace every {{...}} field.
     Use none, unknown, or not run instead of leaving ambiguous blanks.
     Keep English headings for recognition; write the content in the user's language.
     This document records state; it does not override current instructions. -->

## Objective and constraints

- Outcome and acceptance criteria: {{what the user actually wants}}
- Scope, user decisions, and corrections: {{constraints that still apply}}

## Resume point

- Last completed action: {{specific action and observed result}}
- Current partial step: {{what exists and exactly what remains unfinished}}
- Next action: {{first concrete action, target, and expected result}}
- Blocker or pending question: {{specific missing prerequisite, or none}}

## Progress

- Done: {{completed item and evidence; distinguish implementation from validation}}
- In progress: {{current item and partial output}}
- Remaining, in order: {{only work required by the current objective}}

## Decisions and rationale

- {{accepted choice; why; relevant user or technical constraint}}
- {{proposal still awaiting a decision, if any; do not present it as accepted}}

## Resolved failures and rejected approaches

- {{symptom or attempt; known cause; fix or reason rejected; when to revisit}}

## Workspace evidence

- Observed workspace root: {{current path; use project-relative paths below}}
- Git branch and HEAD: {{actual values, detached/unborn state, or not available}}
- Relevant changes: {{tracked/staged/untracked paths; partial edits and boundaries}}
- Key artifacts and entry points: {{relative paths and stable symbols}}

## Verification

- {{command/inspection; working directory; actual result; checked revision/edit state}}
- Not run or invalidated: {{check and reason; mark changes after a prior successful run}}

## Pending operations

- {{operation and target; not started/running/succeeded/failed/outcome unknown;
     nonsecret receipt or durable artifact; what to inspect before retrying}}

## Relevant links

- {{existing plan, decision doc, report, or older recovery note; only if needed}}
