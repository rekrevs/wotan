# Multi-Agent Delegation Pattern

When working with AI-assisted research using Claude Code, you may encounter situations where **different development environments** are needed for different tasks. For example:

- Development machine (lightweight, no heavy dependencies)
- Testing machine (Docker, GPU access, specialized hardware)
- Cluster access (for large-scale experiments)
- Different OS environments (macOS dev, Linux testing)

This document describes a **multi-agent delegation pattern** for coordinating work across multiple Claude Code instances running on different machines.

---

## Core Concept

The pattern uses **git as the coordination mechanism** between multiple Claude Code instances (agents), each running in different environments. Agents communicate via:

1. **Task files** – explicit instructions for what needs to be done
2. **Result files** – documentation of what was accomplished
3. **Git commits** – handoff points between agents

This keeps all coordination **explicit, versioned, and auditable**.

---

## When to Use This Pattern

Consider this pattern when:

- You need capabilities unavailable on your main development machine (Docker, GPU, specific OS)
- Long-running tasks (experiments, builds) would block interactive development
- You want to parallelize work (agent A continues design while agent B runs tests)
- Different security/access contexts are required for different tasks
- You're working with resource-constrained environments (e.g., laptop + cloud VM)

---

## Directory Structure

Create a `claude/` directory in your project repository:

```text
claude/
├── tasks/          # Pending tasks (written by delegating agent)
│   └── TASK-*.md   # Individual task files
├── results/        # Completed results (written by executing agent)
│   └── TASK-*.md   # Task outcomes and documentation
└── README.md       # Project-specific delegation protocol notes
```

This directory lives **in the project repository**, not in the methodology repo.

---

## Workflow

### Step 1: Delegating Agent Creates Task

When the current agent needs work done in a different environment:

1. **Create a task file** under `claude/tasks/TASK-{ID}.md` with:
   - Clear objective
   - Context and background
   - Specific instructions
   - Success criteria
   - Debugging guidance if things fail

2. **Commit and push:**
   ```bash
   git add claude/tasks/TASK-{ID}.md
   git commit -m "task: Delegate TASK-{ID} to {environment} agent"
   git push
   ```

3. **Stop and handoff** – notify the user that a context switch is needed.

### Step 2: User Switches Environment

User:
- Switches to the machine/environment with the required capabilities
- Opens Claude Code in that environment
- Tells Claude: "Do the task in `claude/tasks/TASK-{ID}.md`"

### Step 3: Executing Agent Processes Task

The executing agent:

1. **Reads task file:** `claude/tasks/TASK-{ID}.md`
2. **Executes the task** (run tests, experiments, builds, etc.)
3. **Debugs and fixes issues** if needed
4. **Documents results** in `claude/results/TASK-{ID}.md` including:
   - Status (✅ SUCCESS / ❌ FAILED / ⚠️ PARTIAL)
   - Full output/logs
   - Issues found
   - Fixes applied
   - Next steps for the delegating agent

5. **Commits and pushes:**
   ```bash
   git add [any code fixes] claude/results/TASK-{ID}.md
   git commit -m "fix: [description]"  # if code was fixed
   git commit -m "test: Complete TASK-{ID}"
   git push
   ```

### Step 4: User Switches Back

User:
- Returns to original development environment
- Tells Claude: "Pull and continue" or "Check results for TASK-{ID}"

### Step 5: Delegating Agent Resumes

The delegating agent:

1. **Pulls changes:** `git pull`
2. **Reads results:** `claude/results/TASK-{ID}.md`
3. **Reviews status and next steps**
4. **Continues work** based on results

---

## Task File Format

Recommended structure for `claude/tasks/TASK-{ID}.md`:

```markdown
# Task: {Short Description}

**Status:** PENDING

**Created by:** {Delegating agent context}

**Target environment:** {Required capabilities}

## Context

Why this task is needed. Reference to publon, stage, or experiment if applicable.

## Your Task

Clear, step-by-step instructions for the executing agent.

## Expected Results

Success criteria. What should work? What metrics should pass?

## If Things Fail

Guidance on debugging. Where to look, common issues, acceptable workarounds.

## Document Results

Create `claude/results/TASK-{ID}.md` with:
- Status
- Test output
- Issues found
- Fixes applied
- Next steps

## Deliverables

- [ ] Task completed (success/failure/partial)
- [ ] Results documented
- [ ] Code fixes committed (if any)
- [ ] Changes pushed
```

---

## Results File Format

Recommended structure for `claude/results/TASK-{ID}.md`:

```markdown
# Results: {Task Short Description}

**Status:** ✅ SUCCESS / ❌ FAILED / ⚠️ PARTIAL

**Completed by:** {Executing agent context}

**Date:** {Date}

## Test Results

Full output, logs, or summary of what was run.

## Issues Found

Problems discovered during task execution.

## Fixes Applied

Code changes made by the executing agent, with rationale.

## Commits Made

```
git log --oneline {relevant commits}
```

## Next Steps

Guidance for the delegating agent on how to proceed.
```

---

## Integration with Publons and Stages

This pattern can be integrated with the core methodology:

### During Implementation Stages

If stage `S1a` requires Docker tests:

1. Delegating agent creates `claude/tasks/TASK-P1-S1a-docker-tests.md`
2. Testing agent runs tests, fixes issues, documents in `claude/results/`
3. Delegating agent incorporates results into `P1/impl-stages/S1a-report.md`

### During Experiment Batches

If experiment `E1a` needs GPU resources:

1. Delegating agent creates experiment plan: `research/publons/P1/experiments/E1a-plan.md`
2. Delegating agent creates delegation task: `claude/tasks/TASK-P1-E1a-run.md`
3. Executing agent runs experiments, logs results
4. Delegating agent incorporates into `research/publons/P1/experiments/E1a-log.md`

---

## Benefits

- **Explicit handoffs:** No ambiguity about what needs to be done
- **Automatic documentation:** Task and result files create a paper trail
- **Git-based:** Uses existing version control, no special tools
- **Parallel work:** Delegating agent can continue on other tasks
- **Debugging context:** Executing agent has full instructions and can fix issues

---

## Variations and Extensions

### Multiple Executing Agents

For projects with >2 environments, use descriptive task IDs:

- `TASK-docker-{ID}.md` → for Docker testing agent
- `TASK-gpu-{ID}.md` → for GPU cluster agent
- `TASK-windows-{ID}.md` → for Windows compatibility agent

### Task Queues

If multiple tasks are pending:

- Use `PENDING`, `IN_PROGRESS`, `COMPLETED` status in task files
- Executing agent picks tasks in order or by priority

### Integration with CI/CD

Task files can trigger automated CI/CD pipelines:

- Push to `claude/tasks/` triggers a GitHub Action
- Results posted back to `claude/results/` by automation
- Hybrid human-AI + automated workflow

---

## Example: xedgesim Project

The xedgesim project uses this pattern for Docker-based testing. See `xedgesim/claude/README.md` for a concrete implementation with task and result templates.

---

## Notes

- This pattern is **optional**. Many projects work fine with a single Claude Code instance.
- Keep `claude/` in the project repo, **not** in the methodology repo.
- If a project-specific variation works better, document it in that project's `claude/README.md`.
- This pattern can coexist with the core publon/stage/experiment workflow seamlessly.
