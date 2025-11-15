# Prompt: Ideation and Publon Discovery

You are working in a **project repository** that already uses the research methodology and has a `research/` directory.

Your task is to:

1. Capture current research ideas and questions in a structured way.
2. Propose and refine **candidate publons**.
3. Record candidates under `research/ideation/`.
4. Suggest which candidates should be promoted to real publons (`P2`, `P3`, …).

You will **not** create publon directories in this prompt. Actual publon creation is done via `prompts/new-publon.md` after candidates are selected.

---

## Step 1 – Ensure ideation structure exists

1. Check for `research/ideation/` in the project repo.
2. If it does not exist, create:
   - `research/ideation/`
3. Ensure the following files exist (create them if they do not):

   - `research/ideation/ideation-log.md`
   - `research/ideation/candidate-publons.md`

If you create them, initialise with a short header and today's date.

---

## Step 2 – Read project context

1. Open `research/meta/meta-plan.md` to understand:
   - Overall project questions and context.
   - Existing publons (`P1`, `P2`, …) and their status.

2. Optionally, skim existing publon specs:
   - `research/publons/P1/P1-spec.md`, etc.
   - So you don't propose candidates that duplicate existing publons.

Use this context to avoid re-inventing existing publons.

---

## Step 3 – Update `ideation-log.md`

1. Append a new dated section to `research/ideation/ideation-log.md`, for example:

   ```markdown
   ## YYYY-MM-DD

   - Short bullets summarising new ideas, questions, and observations.
   - References to any papers, systems, or datasets that motivated them.
   ```

2. Summarise:

   * New ideas or questions given by me in this chat.
   * Any emergent ideas suggested by reading `meta-plan.md` or existing publon specs.

Keep this section concise but concrete. Use bullets, not long prose.

---

## Step 4 – Update `candidate-publons.md`

1. Open `research/ideation/candidate-publons.md`.

2. If the file is empty or minimal, initialise a table with header:

   ```markdown
   | ID   | Working title                         | Status     | Short claim sketch                           | Notes                |
   |------|---------------------------------------|------------|----------------------------------------------|----------------------|
   ```

3. Propose **2–7 candidate publons** based on:

   * Ideas in `ideation-log.md`
   * Project context from `meta-plan.md`
   * Gaps relative to existing publons

4. For each candidate row, fill:

   * `ID`:

     * Use `C1`, `C2`, … for new candidates.
     * Reuse existing IDs if already present (update them rather than duplicating).
   * `Working title`:

     * Short and descriptive (1 line).
   * `Status`:

     * One of: `candidate`, `selected`, `discarded`, `merged`.
   * `Short claim sketch`:

     * 1–2 sentences describing the potential contribution.
   * `Notes`:

     * Dependencies, risks, or relationships to existing publons.

5. For existing candidate rows:

   * Update status or notes if the situation has clearly changed.
   * Do not delete rows; keep history unless explicitly instructed.

---

## Step 5 – Suggest candidates to promote

Based on:

* Project goals and risks in `meta-plan.md`.
* Existing publons and their state.
* The new candidate table.

1. Identify **1–3 candidates** that look most promising to promote to real publons.

2. In `candidate-publons.md`:

   * Mark them as `selected` in the `Status` column.
   * Add a short note in `Notes` indicating why they were selected.

3. In a short summary at the end of the file (or in a comment block), explain:

   * Why these candidates are preferred.
   * How they relate to or depend on existing publons.

---

## Step 6 – Update project meta-plan if appropriate

If a candidate is **very likely** to become a publon soon:

1. Optionally update `research/meta/meta-plan.md`:

   * Under the publon table, add a short note such as:

     * "Candidate `C2` is likely to become `P2` once scaffolding from P1 is in place."

2. Keep `meta-plan.md` focused and concise; detailed brainstorm belongs in `ideation/`.

---

## Step 7 – Summary (for the user)

After edits, print a short summary including:

* New or updated candidate IDs with working titles.
* Which candidates you marked as `selected`, with one-sentence justifications.
* Any dependencies or ordering suggestions (e.g., "C2 should come after P1 is stable").

Do **not** create or modify `research/publons/Pk/` directories in this prompt. We will use `prompts/new-publon.md` for that.
