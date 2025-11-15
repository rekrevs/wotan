# Prompt: Run an Implementation Stage for a Publon

You are working in a **project repository** with the research methodology structure in place.

I will provide:

- The publon ID (e.g. `P1`).
- The stage ID (e.g. `S1a`).
- A short description of the objective for this stage.

Your task is to:

1. Define a precise objective and acceptance criteria for the stage.
2. Create or update stage-specific documents.
3. Implement the code changes and tests for this stage, keeping changes minimal and well-scoped.
4. Run tests and perform a code-quality review using a checklist.
5. Update relevant publon docs and commit.

---

## Step 1 – Locate publon and context

1. Identify the publon directory:

   - `research/publons/{{PUBLON_ID}}/`

2. Inspect:
   - `{{PUBLON_ID}}-spec.md`
   - `{{PUBLON_ID}}-design.md`
   - Any existing stage reports under `impl-stages/`.

Use this context to refine the stage objective.

---

## Step 2 – Create stage report and checklist

Use templates from `../research-methodology/templates/`.

1. **Stage report**

   - Path: `research/publons/{{PUBLON_ID}}/impl-stages/{{STAGE_ID}}-report.md`
   - Base template: `../research-methodology/templates/impl-stage-report.md.tmpl`

   Replace placeholders:

   - `{{PUBLON_ID}}` → provided publon ID.
   - `{{PUBLON_WORKING_TITLE}}` → from publon spec.
   - `{{STAGE_ID}}` → provided stage ID.
   - `{{DATE}}` → today's date.
   - `{{STAGE_OBJECTIVE}}` → precise objective for this stage (1–3 sentences).
   - Define 2–5 acceptance criteria.

2. **Stage review checklist**

   - Path: `research/publons/{{PUBLON_ID}}/impl-stages/{{STAGE_ID}}-review-checklist.md`
   - Base template: `../research-methodology/templates/impl-stage-review-checklist.md.tmpl`

   Replace placeholders:

   - `{{PUBLON_ID}}`, `{{STAGE_ID}}`, `{{DATE}}` if used.
   - `{{STAGE_CHECKLIST_PATH}}` in the stage report should point to this checklist.

---

## Step 3 – Plan tests for this stage

Before significant code changes, plan tests:

1. Identify which functions/modules will be affected.
2. Decide:
   - New unit tests needed.
   - Existing integration tests to extend or adjust.
   - Runtime assertions/invariants to add.

Update the stage report's sections for:

- Tests added / updated
- Intended test commands (you can refine later).

---

## Step 4 – Implement code and tests

Perform small, incremental changes focused on the stage objective:

1. Implement or modify code.
2. Add/update tests in the project's test suite, following project conventions.
3. Add assertions or invariants where appropriate.

Avoid:

- Introducing generic abstractions or configuration options "just in case".
- Changing unrelated parts of the system.

Keep the changes cohesive and minimal.

---

## Step 5 – Run tests

1. Run tests specific to this stage:

   - Unit tests covering the changed code.
   - Any stage-specific integration tests.

2. Run the relevant subset of project tests (at least publon-related tests and key integration tests).

3. Record in the stage report:

   - Commands used.
   - Results.
   - Any tests skipped or temporarily disabled (with reasons).

Fix test failures or adjust tests only when behaviour changes are justified and documented.

---

## Step 6 – Review using the checklist

Open `{{STAGE_ID}}-review-checklist.md` and:

1. Go through each section.
2. For each item, mark it `[x]` or `[ ]`.
3. Add short notes for any `[ ]` or any trade-offs worth recording.

Reflect key observations in the stage report under:

- Design decisions
- Known limitations and technical debt
- Checklist and review notes

---

## Step 7 – Update publon documents if needed

If this stage resolves or updates design decisions:

1. Update `{{PUBLON_ID}}-design.md`:
   - Move resolved questions from "Open design questions" to "Design choices and options".
   - Add new open questions if they emerged.

2. If the publon spec (claim/scope) is affected, update `{{PUBLON_ID}}-spec.md` accordingly.

---

## Step 8 – Commit

1. Ensure there are no remaining `{{…}}` placeholders in the new / modified docs.
2. Stage:
   - Code changes.
   - Test changes.
   - Stage report and checklist.
   - Any publon spec/design updates.

3. Commit with a message like:

   - `{{PUBLON_ID}} {{STAGE_ID}}: <short description>`

4. Do not push unless I explicitly instruct you to.

---

## Step 9 – Summary

Print a short summary including:

- Publon ID and stage ID.
- One-sentence summary of what changed.
- Tests run and their outcome.
- Any important limitations or follow-ups noted.
