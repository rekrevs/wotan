# Prompt: Publon Lifecycle Orchestrator

You are working in a **project repository** that uses the research methodology.

Your role in this prompt is to act as a **publon lifecycle orchestrator**:

- Keep a single publon (`Pk`) moving forward through:
  - Design
  - Implementation stages
  - Experiments
  - Paper writing
- Decide what the **next 1–3 concrete steps** should be.
- Execute as many of those steps as possible in this invocation, using the methodology's structure and conventions.

You may conceptually reuse the more focused prompts:

- `prompts/impl-stage.md`
- `prompts/experiment-batch.md`
- `prompts/paper-pass-structure.md`
- `prompts/paper-pass-polish.md`

but here you **choose and sequence** actions across them.

---

## Inputs I will provide

I will specify:

- Publon ID, e.g. `P1`.
- Manuscript path, if relevant (optional).
- High-level preference, e.g.:
  - "Focus on implementation next"
  - "We should run more experiments first"
  - "Time to stabilise the paper draft"

You should still sanity-check whether that preference fits the publon state.

---

## Step 1 – Gather publon state

For publon `{{PUBLON_ID}}`:

1. Open:
   - `research/publons/{{PUBLON_ID}}/{{PUBLON_ID}}-spec.md`
   - `research/publons/{{PUBLON_ID}}/{{PUBLON_ID}}-design.md`
   - `research/publons/{{PUBLON_ID}}/{{PUBLON_ID}}-paper-skeleton.md` (if it exists)
   - `research/publons/{{PUBLON_ID}}/impl-stages/` (list existing stages)
   - `research/publons/{{PUBLON_ID}}/experiments/` (list plans/logs)
2. If present, also read:
   - `research/publons/{{PUBLON_ID}}/{{PUBLON_ID}}-paper-passes.md`
   - Manuscript file (if path provided), e.g. `research/papers/{{PUBLON_ID}}-paper.md`

Build a concise mental model of:

- How far the system and implementation have progressed.
- Which experiments exist and what they have shown.
- How mature the paper is (structure vs content vs polish).

---

## Step 2 – Decide the next 1–3 actions

Based on the publon state and my preference (if any), choose **1–3 actions** from:

- `impl-stage` – define and execute a new implementation stage (`Ska`)
- `experiment-batch` – plan and log a new experiment batch (`E1a`)
- `paper-pass-structure` – align manuscript with skeleton
- `paper-pass-polish` – improve clarity and consistency
- `design-update` – refine `{{PUBLON_ID}}-design.md` and the staging plan without coding
- `spec-update` – refine `{{PUBLON_ID}}-spec.md` if claims or scope have clearly changed

Actions should:

- Be **small and well-scoped** (completable within this invocation or clearly started).
- Move the publon toward a clearer or more publishable state.

If an obvious **blocking issue** exists (e.g. spec/design contradictions), prioritise fixing that first.

---

## Step 3 – For each chosen action, execute a focused mini-prompt

For each action in order:

1. **Implementation stage (`impl-stage`)**

   - Choose a new stage ID (e.g. `S1c`) that fits the naming and staging plan in `{{PUBLON_ID}}-design.md`.
   - Apply the process from `prompts/impl-stage.md`:
     - Update the staging plan (section 7 of `{{PUBLON_ID}}-design.md`) if needed.
     - Create `{{STAGE_ID}}-report.md` and `{{STAGE_ID}}-review-checklist.md`.
     - Plan tests and implement code + tests.
     - Run stage-specific and cumulative tests (see `docs/test-conventions.md`).
     - Update publon design/spec if needed.
     - Commit changes with an appropriate message (if allowed).

2. **Experiment batch (`experiment-batch`)**

   - Choose a new experiment ID (e.g. `E1b`) consistent with `{{PUBLON_ID}}-experiments-index.md` if it exists.
   - Apply the process from `prompts/experiment-batch.md`:
     - Create plan and log files.
     - Align or create experiment scripts/configs.
     - (You will not run experiments here, but you prepare everything for execution.)
     - After results exist, you will revisit the log in a later invocation.

3. **Paper structure pass (`paper-pass-structure`)**

   - If the manuscript path is provided and structure is weak or diverged:
     - Align manuscript structure with `{{PUBLON_ID}}-paper-skeleton.md`.
     - Update skeleton if manuscript clearly represents a better structure.
     - Record the pass in `{{PUBLON_ID}}-paper-passes.md`.

4. **Paper polish pass (`paper-pass-polish`)**

   - If structure is reasonable and content present:
     - Improve clarity, concision, and terminology.
     - Check claims vs evidence; weaken claims if evidence is incomplete.
     - Record the pass in `{{PUBLON_ID}}-paper-passes.md`.

5. **Design or spec updates**

   - If you discover contradictions or major shifts:
     - Directly edit `{{PUBLON_ID}}-spec.md` and/or `{{PUBLON_ID}}-design.md`.
     - Keep changes concise and coherent.
     - Note major decisions/changes explicitly.

For each action, do as much **actual editing work** as is reasonable, not just planning.

---

## Step 4 – Maintain consistency

After performing the chosen actions:

1. Check for consistency between:

   - Publon spec (`{{PUBLON_ID}}-spec.md`)
   - Design (`{{PUBLON_ID}}-design.md`)
   - Stage reports (`impl-stages/`)
   - Experiment plans/logs (`experiments/`)
   - Paper skeleton (`{{PUBLON_ID}}-paper-skeleton.md`)
   - Manuscript (if present)

2. When discrepancies are minor:

   - Fix them directly as part of this prompt (e.g. adjust paper skeleton bullets).

3. When discrepancies are major:

   - Document them clearly in the relevant files (e.g. in the stage report or experiment log) as TODOs or "Open issues".
   - Propose explicit follow-up actions for the next invocation.

---

## Step 5 – Commit (if allowed in this environment)

If you have permission to run git commands:

1. Stage all changes related to `{{PUBLON_ID}}` for this invocation.
2. Use a commit message that mentions publon ID and the most important action, e.g.:

   - `{{PUBLON_ID}} S1c: add monitoring and tests`
   - `{{PUBLON_ID}} E1b: add ablation experiment plan`
   - `{{PUBLON_ID}}: structure pass on paper`

If you do not have permission to commit, ensure changes are clearly visible in the working tree.

---

## Step 6 – Summary

At the end, print a concise summary including:

- Publon ID.
- Actions taken (e.g. "S1c implementation", "E1b experiment plan", "structure pass").
- Tests run and their outcome (if any).
- New TODOs or follow-up actions for the next invocation (with suggested prompt to use if appropriate).
