# Prompt: Initialise a Project with the Research Methodology

You are working in a **project repository** that will use an external methodology repository as a pattern library.

The methodology repository is available at:

- `../research-methodology/`

Treat the methodology repo as **read-only**. All evolving state must be created in the current project repo.

Your task is to:

1. Create the `research/` directory structure in this project.
2. Instantiate the core templates for:
   - Project meta-plan
   - First publon `P1`
   - Project dev log
3. Make minimal, concrete initial content based on the project's existing `README` or a short description I provide.
4. Commit the changes with a clean message.

---

## Step 1 – Inspect the methodology repo

1. List the contents of `../research-methodology/templates/`.
2. List the contents of `../research-methodology/docs/`.
3. Do not modify anything in `../research-methodology`.

---

## Step 2 – Create the `research/` directory structure

In the current project repo, create:

- `research/`
- `research/meta/`
- `research/publons/`
- `research/dev-log/`
- `research/papers/`

Under `research/publons/`, create:

- `research/publons/P1/`
- `research/publons/P1/impl-stages/`
- `research/publons/P1/experiments/`

---

## Step 3 – Instantiate core templates

Use the templates from `../research-methodology/templates/` as follows.

Where you see `{{PLACEHOLDER_NAME}}`, replace it by a reasonable value inferred from:

- The project's `README`, if it exists.
- Otherwise, the short description I gave you.

### 3.1 Meta plan

1. Copy `../research-methodology/templates/meta-plan.md.tmpl` to:
   - `research/meta/meta-plan.md`
2. Replace at least:
   - `{{PROJECT_NAME}}` → the name of this repository.
   - `{{DATE}}` → today's date.
   - `{{PROJECT_SHORT_DESCRIPTION}}` → 1–3 sentences about the project.
   - Other placeholders with simple, concrete initial guesses.
3. For `{{INITIAL_PUBLON_LIST}}`, create a row for `P1` with:
   - A working title.
   - Status `planned` or `in-progress`.
   - One-line description.
   - Empty or `-` for dependencies.

### 3.2 Publon P1 spec

1. Copy `../research-methodology/templates/publon-spec.md.tmpl` to:
   - `research/publons/P1/P1-spec.md`
2. Replace placeholders:
   - `{{PUBLON_ID}}` → `P1`
   - `{{PUBLON_WORKING_TITLE}}` → a reasonable working title.
   - `{{DATE}}` → today's date.
   - Fill in claim, motivation, and scope sketch in a minimal but concrete way.

### 3.3 Publon P1 design doc

1. Copy `../research-methodology/templates/publon-design.md.tmpl` to:
   - `research/publons/P1/P1-design.md`
2. Replace placeholders:
   - `{{PUBLON_ID}}` → `P1`
   - `{{PUBLON_WORKING_TITLE}}` → same title as in P1 spec.
   - `{{PROJECT_NAME}}` → this repo's name.
   - Add brief context, goals, and an initial implementation staging sketch.

### 3.4 Publon P1 paper skeleton

1. Copy `../research-methodology/templates/publon-paper-skeleton.md.tmpl` to:
   - `research/publons/P1/P1-paper-skeleton.md`
2. Replace placeholders:
   - `{{PUBLON_ID}}` → `P1`
   - `{{PAPER_TITLE}}` → a working title.
   - Fill in short bullets for introduction, method, and results.

### 3.5 Dev log

1. Create `research/dev-log/project-log.md` with initial content:

   - Today's date.
   - Note that the research methodology structure has been initialised.
   - Very short summary of P1's working title and purpose.

---

## Step 4 – Optional README fragment

If the project `README` exists:

1. Copy `../research-methodology/templates/project-readme-fragment.md.tmpl` content.
2. Append it to `README` under a suitable heading, adapting wording minimally if needed.

If `README` does not exist, you may skip this step or create a minimal one.

---

## Step 5 – Consistency check

Before committing:

1. Ensure there are no remaining `{{…}}` placeholders in the new files.
2. Check that `P1`'s working title and description are consistent across:
   - `research/meta/meta-plan.md`
   - `research/publons/P1/P1-spec.md`
   - `research/publons/P1/P1-design.md`
   - `research/publons/P1/P1-paper-skeleton.md`

Fix any inconsistencies.

---

## Step 6 – Commit (no push)

1. Stage all files under `research/` and the `README` change if any.
2. Commit with message:

   - `init: add research methodology structure`

3. Do not push; I will decide when to push.

---

## Step 7 – Brief summary

After performing all steps, print a short summary including:

- The `research/` directory tree.
- The working title and one-line description for `P1`.
- Any assumptions or guesses you made that I should confirm or adjust.
