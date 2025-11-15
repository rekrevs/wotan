# Prompt: Paper Structure Pass for a Publon

You are working on the manuscript for a specific publon in a **project repository** using the research methodology.

I will provide:

- Publon ID (e.g. `P1`).
- Manuscript path (e.g. `research/papers/P1-paper.md` or `.tex`).

Your task is to perform a **structure pass**:

1. Align the manuscript structure with the publon's paper skeleton.
2. Ensure sections and subsections are present and ordered coherently.
3. Record the pass in the publon's paper pass notes.

---

## Step 1 – Gather context

1. Identify the publon directory:

   - `research/publons/{{PUBLON_ID}}/`

2. Open:
   - `{{PUBLON_ID}}-spec.md`
   - `{{PUBLON_ID}}-design.md`
   - `{{PUBLON_ID}}-paper-skeleton.md`
   - Optional: `{{PUBLON_ID}}-paper-passes.md` if it exists.

Use these documents to understand:

- The intended claims and contributions.
- The desired paper structure.

---

## Step 2 – Compare skeleton and manuscript

1. Open the manuscript file:

   - `{{MANUSCRIPT_PATH}}`

2. Compare its current structure (sections, subsections) against `{{PUBLON_ID}}-paper-skeleton.md`.

3. Identify:

   - Missing sections or subsections.
   - Sections in the manuscript that do not appear in the skeleton.
   - Misordered content relative to the intended narrative.

---

## Step 3 – Adjust manuscript structure

Without fully rewriting content, make structural edits to align with the skeleton:

1. Reorder sections and subsections to match the logical flow from the skeleton (e.g. Introduction → Background → Method → Experiments → Results → Discussion → Related Work → Conclusion).
2. Add missing section headings where needed, inserting short placeholder paragraphs if necessary.
3. Merge or split sections if their scope does not match the skeleton.
4. Avoid large content rewrites in this pass; focus on headings and high-level organisation.

Keep changes minimal but decisive.

---

## Step 4 – Sync skeleton if necessary

If the skeleton is clearly outdated but the manuscript structure reflects a better understanding:

1. Update `{{PUBLON_ID}}-paper-skeleton.md` to match the improved structure.
2. Keep the skeleton concise, using bullets to describe intended content per section.

The skeleton and manuscript should describe the same structure after this pass.

---

## Step 5 – Record the pass

Use the paper pass notes template if it exists:

1. If `research/publons/{{PUBLON_ID}}/{{PUBLON_ID}}-paper-passes.md` does not exist:
   - Instantiate it from `../research-methodology/templates/paper-pass-notes.md.tmpl`.

2. Add a new section:

   - `## Pass: structure-<N>` (e.g. `structure-1`)
   - Include:
     - Date
     - Scope: "structure pass"
     - Goals
     - Brief checklist (e.g. all main sections present, order matches narrative)
     - Outcome summary

---

## Step 6 – Commit

1. Stage:
   - Manuscript file.
   - Updated skeleton.
   - Paper pass notes file.

2. Commit with a message like:

   - `{{PUBLON_ID}}: structure pass on paper`

3. Do not push unless I explicitly instruct you to.

---

## Step 7 – Summary

Print a summary including:

- Main structural changes made.
- Any sections still in a clearly draft or placeholder state.
- Any open structure questions you propose for future passes.
