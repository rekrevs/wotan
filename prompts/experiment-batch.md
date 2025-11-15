# Prompt: Plan and Log an Experiment Batch for a Publon

You are working in a **project repository** with the research methodology structure.

I will provide:

- Publon ID (e.g. `P1`).
- Experiment batch ID (e.g. `E1a`).
- A short description of what we want to test.

Your task is to:

1. Create an experiment plan document.
2. (Optionally) update or create experiment scripts/configurations.
3. After runs are done, create or update the experiment log.

---

## Step 1 – Locate publon and context

1. Identify:

   - `research/publons/{{PUBLON_ID}}/{{PUBLON_ID}}-spec.md`
   - `research/publons/{{PUBLON_ID}}/{{PUBLON_ID}}-design.md`
   - Any relevant implementation stage reports.

2. Use these to understand:

   - The current state of the system for this publon.
   - The hypotheses or questions relevant to this experiment batch.

---

## Step 2 – Create experiment plan from template

Use `../research-methodology/templates/experiment-plan.md.tmpl`.

1. Path for the plan:

   - `research/publons/{{PUBLON_ID}}/experiments/{{EXPERIMENT_ID}}-plan.md`

2. Instantiate the template:

   - Replace `{{PUBLON_ID}}` and `{{PUBLON_WORKING_TITLE}}`.
   - Set `{{EXPERIMENT_ID}}` to the provided ID.
   - Set `{{DATE}}` to today's date.
   - Fill in purpose, hypotheses, setup, metrics, protocol, and analysis plan based on:
     - The short description I gave you.
     - The publon's spec & design.

Keep the plan concrete but concise.

---

## Step 3 – Update or create experiment code/config

If experiment scripts or configs do not exist yet:

1. Create a minimal structure under the project's preferred location (e.g. `experiments/`, `scripts/`), following project conventions.
2. Ensure that:

   - Commands in the plan (`{{COMMAND_1}}`, `{{COMMAND_2}}`, etc.) map to actual scripts or invocations.
   - There is a small-scale "smoke test" configuration that can run quickly.

If experiment code already exists:

1. Review it for compatibility with the new plan.
2. Adjust configurations or scripts if needed, keeping changes minimal and well-documented.

---

## Step 4 – (Manual) Run experiments

You or an external system will run the experiments, not this prompt.

However, you should:

1. Provide clear commands and instructions in the plan so they can be run reproducibly.
2. After runs are completed and logs/results are available, proceed to the next step.

---

## Step 5 – Create or update experiment log

Use `../research-methodology/templates/experiment-log.md.tmpl`.

1. Path for the log:

   - `research/publons/{{PUBLON_ID}}/experiments/{{EXPERIMENT_ID}}-log.md`

2. Instantiate the template if the log does not exist:

   - Set `{{PUBLON_ID}}`, `{{EXPERIMENT_ID}}`, `{{DATE}}`.
   - Set `{{PLAN_FILE_PATH}}` to the relative path of the plan.
   - Fill in initial run metadata as available (code version, dates, responsible agent).

3. After experiment runs:

   - Fill in executed commands, configurations, run IDs, and output locations.
   - Summarise key results and analysis.
   - Note issues, deviations from the plan, and follow-up actions.

---

## Step 6 – Update publon documents if needed

If the experiment results affect the publon's:

- Claim
- Scope
- Design decisions

then update:

- `{{PUBLON_ID}}-spec.md`
- `{{PUBLON_ID}}-design.md`
- `{{PUBLON_ID}}-paper-skeleton.md` (e.g. adjust expected results sections)

to keep them aligned with reality.

---

## Step 7 – Commit

1. Stage:

   - Experiment plan and log.
   - Any experiment scripts/config changes.
   - Any publon document updates.

2. Commit with a message like:

   - `{{PUBLON_ID}} {{EXPERIMENT_ID}}: add experiment plan and log`

3. Do not push unless I explicitly instruct you to.

---

## Step 8 – Summary

Print a summary including:

- Publon ID and experiment ID.
- Main hypotheses tested.
- High-level outcome (supported / not supported / unclear).
- Key follow-up actions you propose.
