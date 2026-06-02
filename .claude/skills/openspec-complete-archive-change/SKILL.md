---
name: openspec-complete-archive-change
description: Complete verification, delta spec sync, and archive for one or more finished OpenSpec changes in one step — no prompts, no manual checkbox work. Use this whenever the user has deployed changes to production and wants to close them out, or says things like "驗證打勾", "幫我打勾", "archive 完成的 change", "close out", "openspec complete", "finalize change", "complete and archive", or wants to archive multiple changes at once. Also use when the user mentions deploying to production and wanting to clean up their openspec changes. This skill is the right choice any time the user would otherwise need to manually mark tasks, agree to spec sync, and run archive — do not make them ask for each step separately.
license: MIT
compatibility: Requires openspec CLI.
metadata:
  author: openspec
  version: "1.0"
---

# openspec-complete-archive-change

Finalize one or more deployed OpenSpec changes in a single step: mark all remaining tasks as complete, sync delta specs to main specs, and archive each change. No confirmation prompts for tasks or sync — this skill is designed for production-deployed changes where all work is done.

## When to use

After deploying to production and wanting to close out changes cleanly. The user has already validated the work in production; this skill just catches up the paper trail.

## Steps

### 1. Identify active changes

Run:
```
openspec list --json
```

Parse the output to get the list of active (non-archived) changes.

**If the user named specific changes in their prompt**, use those directly (validate they exist in the list; warn if any are not found).

**If no specific changes were named**, use **AskUserQuestion** to let the user select which changes to process. Enable `multiSelect: true` so they can pick several at once. Include an option like "All of the above" if there are multiple changes, or just list them individually. Show each change name clearly.

**If only one active change exists**, skip the prompt and use it directly — no need to make the user confirm the obvious.

### 2. Process each selected change

Work through the selected changes one at a time. For each change `<name>`:

#### 2a. Mark all tasks complete

Read `openspec/changes/<name>/tasks.md`.

Find all lines matching `- [ ]` (unchecked tasks) and change them to `- [x]`.

This is safe to do unconditionally: the change has been deployed to production, so all tasks are considered verified. Count how many were already done vs. how many were just marked — you'll need this for the summary.

Save the file.

If `tasks.md` doesn't exist, skip this step silently.

#### 2b. Sync delta specs automatically

Check if `openspec/changes/<name>/specs/` exists and has any spec files.

If delta specs exist, sync each one to its corresponding main spec:
- Delta spec: `openspec/changes/<name>/specs/<capability>/spec.md`
- Main spec: `openspec/specs/<capability>/spec.md`

For each delta spec:
1. Read the delta spec content
2. If the main spec directory doesn't exist yet, create it
3. Copy the delta spec to the main spec path (overwrite if exists)

Do this automatically — the user always wants to sync. No prompt needed.

Track which capabilities were synced for the summary.

If no delta specs exist, skip this step silently.

#### 2c. Archive the change

Create the archive directory if it doesn't exist:
```bash
mkdir -p openspec/changes/archive
```

Generate the archive target name using today's date: `YYYY-MM-DD-<change-name>`

Check if the target already exists. If it does, report an error for this change and skip it (don't block other changes in the batch).

Move the change directory:
```bash
mv openspec/changes/<name> openspec/changes/archive/YYYY-MM-DD-<name>
```

The `.openspec.yaml` moves with the directory automatically.

### 3. Display summary

After all changes are processed, show a combined summary:

```
## Complete & Archive Done

| Change | Tasks | Specs Synced | Archived To |
|--------|-------|--------------|-------------|
| my-feature | 3 already done, 2 marked ✓ | quiz-progress-bar | archive/2026-05-13-my-feature/ |
| another-change | 5 already done, 0 marked | (none) | archive/2026-05-13-another-change/ |
```

If any changes were skipped due to errors (e.g., archive target already existed), list them separately with the reason.

## Guardrails

- Never prompt "are you sure?" for task completion or spec sync — the user chose this skill because they don't want those prompts
- If a change name was specified but doesn't exist in the active list, warn and skip it rather than failing entirely
- Handle missing files gracefully (no tasks.md, no delta specs) — just skip those sub-steps
- Process changes sequentially so partial failures don't block the rest of the batch
- The `.openspec.yaml` file is preserved automatically when the directory is moved — no special handling needed
