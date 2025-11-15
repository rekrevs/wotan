# Prompt: Create a New Publon in an Existing Project

You are working in a **project repository** that already uses the research methodology and has a `research/` directory.

Your task is to:

1. Create a new publon directory `Pk` (e.g. `P2`).
2. Instantiate:
   - Publon spec
   - Publon design doc
   - Publon paper skeleton
   - Optional paper pass notes
3. Link the new publon into the project meta-plan.

I will provide:

- The new publon ID (e.g. `P2`).
- A short working title and synopsis.
- Optionally, a short note on how it relates to existing publons.

---

## Step 1 – Confirm current structure

1. Inspect the existing `research/` directory.
2. Identify:
   - `research/meta/meta-plan.md`
   - Existing publon directories (e.g. `research/publons/P1/`).

Do not modify existing publon directories unless necessary for consistency.

---

## Step 2 – Create publon directory

Given publon ID `{{NEW_PUBLON_ID}}` (e.g. `P2`), create:

- `research/publons/{{NEW_PUBLON_ID}}/`
- `research/publons/{{NEW_PUBLON_ID}}/impl-stages/`
- `research/publons/{{NEW_PUBLON_ID}}/experiments/`

---

## Step 3 – Instantiate publon documents from templates

Use the templates from `../research-methodology/templates/`.

### 3.1 Publon spec

1. Copy `../research-methodology/templates/publon-spec.md.tmpl` to:

   - `research/publons/{{NEW_PUBLON_ID}}/{{NEW_PUBLON_ID}}-spec.md`

2. Replace placeholders:

   - `{{PUBLON_ID}}` → `{{NEW_PUBLON_ID}}`
   - `{{PUBLON_WORKING_TITLE}}` → the working title I gave you.
   - `{{DATE}}` → today's date.
   - Fill in synopsis, claim, motivation, scope, and risks based on:
     - The working title and synopsis.
     - Existing project context from `research/meta/meta-plan.md`.

### 3.2 Publon design doc

1. Copy `../research-methodology/templates/publon-design.md.tmpl` to:

   - `research/publons/{{NEW_PUBLON_ID}}/{{NEW_PUBLON_ID}}-design.md`

2. Replace placeholders:

   - `{{PUBLON_ID}}` → `{{NEW_PUBLON_ID}}`
   - `{{PUBLON_WORKING_TITLE}}` → the working title.
   - `{{PROJECT_NAME}}` → this repo's name.
   - Provide:
     - A short context paragraph.
     - 2–4 functional goals.
     - Any non-functional considerations.
     - Initial architecture impact notes.
     - A rough implementation staging sketch.

### 3.3 Publon paper skeleton

1. Copy `../research-methodology/templates/publon-paper-skeleton.md.tmpl` to:

   - `research/publons/{{NEW_PUBLON_ID}}/{{NEW_PUBLON_ID}}-paper-skeleton.md`

2. Replace placeholders:

   - `{{PUBLON_ID}}` → `{{NEW_PUBLON_ID}}`
   - `{{PAPER_TITLE}}` → a working paper title (can match publon working title).
   - Add minimal but concrete bullets for introduction, method, and results.

### 3.4 Optional: paper pass notes

1. Copy `../research-methodology/templates/paper-pass-notes.md.tmpl` to:

   - `research/publons/{{NEW_PUBLON_ID}}/{{NEW_PUBLON_ID}}-paper-passes.md`

2. Replace placeholders:

   - `{{PUBLON_ID}}` → `{{NEW_PUBLON_ID}}`
   - You may leave the example pass section as a template for later.

---

## Step 4 – Update meta-plan

Open `research/meta/meta-plan.md` and update:

1. The publon table under "Publons" with a new row for `{{NEW_PUBLON_ID}}` including:
   - ID
   - Working title
   - Status (`planned` or `in-progress`)
   - Short description
   - Dependencies (list any existing publons that this one builds on)

2. If relevant, update high-level questions or system context sections to reflect the new publon.

---

## Step 5 – Consistency check

1. Ensure there are no remaining `{{…}}` placeholders in:

   - `{{NEW_PUBLON_ID}}-spec.md`
   - `{{NEW_PUBLON_ID}}-design.md`
   - `{{NEW_PUBLON_ID}}-paper-skeleton.md`
   - `{{NEW_PUBLON_ID}}-paper-passes.md` (if created)

2. Confirm that publon ID and working title are consistent across all new files and the meta-plan.

---

## Step 6 – Commit

1. Stage the new files under `research/publons/{{NEW_PUBLON_ID}}/` and the edited `research/meta/meta-plan.md`.
2. Commit with a message like:

   - `{{NEW_PUBLON_ID}}: add publon spec, design, and paper skeleton`

3. Do not push unless I explicitly asked you to.

---

## Step 7 – Summary

Print a short summary including:

- The publon ID and working title.
- A one-sentence description of the publon.
- Any assumptions you made that I should confirm or revise.
