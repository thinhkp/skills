---
name: context-preservation
description: "Save durable project checkpoints during long sessions, before handoff or compaction, or when asked to save context, progress, or decisions (lưu context, lưu tiến độ, bàn giao). Use for preserving the current work; use session-continuity to restore and resume it."
---

# Context Preservation

Write a compact recovery point to project files so work can survive a shortened conversation or a new session. Preserve the reasoning needed to continue, not a transcript.

## When to checkpoint

Once active for a substantial task, save an initial checkpoint after establishing the objective and approach. Refresh it when information worth recovering changes:

- A milestone finishes or the current implementation boundary moves.
- The user changes scope, corrects a requirement, or makes a technical decision.
- A difficult failure is resolved, an approach is ruled out, or a blocker appears.
- An important check finishes, or a consequential operation is about to be attempted or has returned a result.
- The user requests a handoff, ends the session, or context pressure is explicitly signaled.

Checkpoint at meaningful boundaries; do not rewrite after every tool call or perform timed polling. Do not depend on an exact token threshold or a guaranteed notification before compaction. This skill supplies instructions, not a background process or lifecycle hook.

## Find the storage location

1. Read applicable project guidance and reuse an explicitly designated handoff file. Avoid a second competing source of current state.
2. Otherwise use `.agent-context/STATE.md` under the project root. Use the Git working tree root for a repository, including a linked worktree; otherwise use the task's workspace root. Never store project state in the installed skill folder.
3. If independent sessions or tasks share one working tree, give each its own `.agent-context/workstreams/<stable-task-slug>.md`. Reuse the same slug when resuming that task. Do not let sessions overwrite one shared snapshot. Different worktrees keep their own state.
4. Read an existing snapshot before editing it. If it belongs to unrelated work, preserve it and use a workstream file. Respect an existing schema; do not silently rewrite an unsupported version.

Use ordinary UTF-8 Markdown. The default contract is `agent-context/v1`, defined by [assets/state-template.md](assets/state-template.md). Read that template when creating a checkpoint; fill its fields with observed facts and remove its drafting comments. Existing project formats may use different headings if they retain the same information.

## Capture the recoverable state

Collect from the current conversation, existing checkpoint, and narrow inspection of relevant artifacts. Do not reload the entire project to write a checkpoint.

| Information | What must survive |
| --- | --- |
| Objective and scope | The actual requested outcome, acceptance criteria, user constraints, and later corrections. |
| Work position | Completed items with evidence, the exact partially completed step, and remaining work in order. Distinguish implementation finished from validation finished. |
| Decisions | Chosen approach, why it was chosen, and the user or technical constraint behind it. Distinguish accepted decisions from proposals. |
| Resolved failures | Symptom, cause if known, fix or rejected attempt, and conditions that would justify investigating it again. |
| Workspace evidence | Project identity, branch and HEAD when available, relevant tracked and untracked files, and the observed state of unfinished edits. Use `not available` when Git is absent. |
| Verification | Commands or observations actually performed, working directory, result, and the code/artifact state they covered. Mark checks not run or invalidated by later edits. |
| Pending operations | Last completed action; interrupted or in-flight operation; nonsecret job/receipt identifiers and any action needed to establish its outcome. |
| Next action | A concrete first step with a target file, symbol, artifact, or command and an expected result. Record blockers and the specific missing answer or prerequisite. |

Prefer project-relative paths plus stable symbols to line numbers alone. Link durable plans, design docs, test reports, and large outputs rather than copying them. Label unverified claims, assumptions, and unknowns explicitly. Do not invent events lost before this checkpoint.

For a potentially consequential operation, persist its intended target and `outcome unknown` before it begins when practical, then update with the observed receipt or result. This records a retry boundary; it does not authorize performing the operation.

## Refresh without losing useful information

- Keep one current snapshot per task. Replace obsolete status with current status while retaining still-relevant constraints, decision reasons, resolved failures, and unfinished work. Avoid an append-only conversation log.
- Aim for roughly 600–1,200 words, often less for a small task. Keep the objective, current step, blockers, and next action near the top. Move lengthy durable detail to a linked project document only when it materially helps; do not discard essential context to meet a size target.
- Record an actual ISO 8601 update time with timezone. Use `in_progress`, `blocked`, `completed`, or `paused` for task status; `paused` requires the user's request, and `completed` requires the acceptance criteria to be satisfied. This is file metadata, separate from any platform goal status.
- A test result belongs to the code state that was checked. The same HEAD does not establish freshness when there are uncommitted changes. Preserve the known revision/edit boundary and mark uncertain coverage instead of claiming current success.
- Re-read the destination immediately before replacing it. If it changed since it was read, reconcile the changes or select a separate workstream; do not blindly overwrite. Use a targeted edit or, where supported, a complete temporary sibling file followed by atomic replacement. Atomic replacement prevents partial files, not concurrent lost updates.
- Do not commit, stash, reset, switch branches, change ignore rules, or alter global instructions merely to save context. Follow existing project tracking conventions.

Exclude credentials, tokens, `.env` contents, sensitive raw logs, and unnecessary personal data. Record the relevant secret's variable name or configured location instead of its value.

## Confirm the handoff

Read back the saved file. Confirm the objective, actual partial-work boundary, retained decisions, and first next action are accurate; verify that referenced recovery artifacts exist or are marked unavailable. Check the checkpoint itself without rerunning the project's tests solely to save state.

Report the path and a short statement of the resume point in the user's language. If saving is a milestone in ongoing work, continue the authorized task. If persistence is unavailable, provide the checkpoint text and clearly say it was not saved; do not imply a future session can access it.

If asked to enable this workflow across sessions, offer or merge the small [assets/agents-snippet.md](assets/agents-snippet.md) into the project's existing `AGENTS.md` within the requested scope. Read that asset only for setup. Do not overwrite other guidance or change global files just because this skill was invoked.
