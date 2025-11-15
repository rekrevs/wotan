# Prompt: Run an Implementation Stage for a Publon

You are working in a **project repository** with the research methodology structure in place.

I will provide:

- The publon ID (e.g. `P1`).
- The stage ID (e.g. `S1a`).
- A short description of the objective for this stage.

Your task is to:

1. Review and update the implementation staging plan.
2. Define a precise objective and acceptance criteria for the stage.
3. Create or update stage-specific documents.
4. Design tests for this stage before implementing.
5. Implement the code changes and tests for this stage, keeping changes minimal and well-scoped.
6. Run tests (stage-specific and cumulative) and perform a code-quality review using a checklist.
7. Update relevant publon docs, refine the staging plan, and commit.

---

## Step 0 – Review implementation staging plan

Before starting this stage:

1. Open `research/publons/{{PUBLON_ID}}/{{PUBLON_ID}}-design.md`

2. Review section 7 "Implementation staging plan (sketch)"

3. Check:
   - Does this stage (`{{STAGE_ID}}`) appear in the plan?
   - Is its objective still relevant given what you learned from previous stages?
   - Are there stages listed after this one that need to be added, removed, split, or merged?

4. If the plan needs refinement:
   - Update section 7 with current understanding
   - Adjust stage sequence, scope, or objectives as needed
   - Document why changes were made (e.g., "Split S2a into S2a and S2b after discovering X complexity")

**Planning is iterative:** The staging plan is a living document that evolves as implementation progresses.

---

## Step 1 – Locate publon and context

1. Identify the publon directory:

   - `research/publons/{{PUBLON_ID}}/`

2. Inspect:
   - `{{PUBLON_ID}}-spec.md`
   - `{{PUBLON_ID}}-design.md` (including updated staging plan from Step 0)
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

Before significant code changes, plan tests following `docs/test-conventions.md`:

1. **Identify test locations:**
   - Stage-specific tests: `tests/stages/{{STAGE_ID}}/`
   - Integration tests to update: `tests/integration/`
   - Shared fixtures/helpers: `tests/fixtures/`

2. **Plan three categories of tests:**
   - **Unit tests:** For individual functions/classes changed in this stage
   - **Integration tests:** End-to-end scenarios exercising new behavior
   - **Runtime assertions:** Invariants to add in production code

3. **Decide on determinism expectations:**
   - Will tests be deterministic (exact equality) or statistical (distributions/ranges)?
   - Document this in the stage report

4. **Update the stage report** sections:
   - "Tests added / updated" – list planned test files
   - "Test execution" – note intended commands (refine after implementation)

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

## Step 5 – Run tests (two tiers)

Follow the two-tier testing strategy from `docs/test-conventions.md`:

### Tier 1: Stage-Specific Tests (Fast Feedback)

Run only tests for the current stage to get fast feedback:

```bash
# Example (adjust for your test framework)
pytest tests/stages/{{STAGE_ID}}/ -v
```

Fix failures before proceeding.

### Tier 2: Cumulative Regression Tests (Quality Gate)

Before marking the stage complete, run **all tests up to and including this stage**:

```bash
# Example: run all stages up to {{STAGE_ID}} plus integration tests
pytest tests/stages/S1a/ tests/stages/S1b/ ... tests/stages/{{STAGE_ID}}/ tests/integration/ -v
```

**Stage completion requirement:** All Tier 2 tests must pass.

### Document in Stage Report

Record in section 4 "Test execution":

- Exact commands used for both tiers
- Test results (all passed, or reasons for skipped tests)
- Any tests from earlier stages that required updating (explain why in section 3.2)

If tests fail, either fix the code or adjust tests with clear justification documented in the stage report.

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

## Step 8 – Refine the staging plan for future stages

After completing this stage, you have learned something about the system. Use that knowledge to refine the plan:

1. Open `research/publons/{{PUBLON_ID}}/{{PUBLON_ID}}-design.md` section 7 "Implementation staging plan"

2. Update the plan:
   - Mark `{{STAGE_ID}}` as completed
   - Adjust remaining stages based on what you learned:
     - **Split** stages that turned out more complex than expected
     - **Merge** stages if scope was smaller than anticipated
     - **Add** new stages if you discovered unforeseen work
     - **Remove** stages that are no longer needed
     - **Reorder** stages if dependencies changed

3. Keep the plan lightweight:
   - 1-line objective per future stage
   - No need to plan every detail; plan 2-5 stages ahead at most
   - The plan will be refined again after the next stage

4. Document major changes:
   - If you significantly revised the plan, note why in the current stage report under "Known limitations and technical debt" or as a separate note

**Iterative planning is key:** The staging plan evolves as you implement. This is expected and healthy.

---

## Step 9 – Commit

1. Ensure there are no remaining `{{…}}` placeholders in the new / modified docs.
2. Stage:
   - Code changes.
   - Test changes (including new test directories under `tests/stages/{{STAGE_ID}}/`).
   - Stage report and checklist.
   - Any publon spec/design updates (including refined staging plan).

3. Commit with a message like:

   - `{{PUBLON_ID}} {{STAGE_ID}}: <short description>`

4. Do not push unless I explicitly instruct you to.

---

## Step 10 – Summary

Print a short summary including:

- Publon ID and stage ID.
- One-sentence summary of what changed.
- Tests run and their outcome.
- Any important limitations or follow-ups noted.
