# Prompt: Paper Polish Pass for a Publon

You are working on the manuscript for a specific publon in a **project repository** using the research methodology.

I will provide:

- Publon ID (e.g. `P1`).
- Manuscript path (e.g. `research/papers/P1-paper.md` or `.tex`).

Assume that:

- The overall structure is already reasonable.
- Core content and results are present, though may be rough.

Your task is to perform a **polish pass** focusing on:

1. Clarity and concision of language.
2. Consistency of terminology and notation.
3. Alignment between claims and evidence.
4. Removal of obvious redundancies and tangents.

---

## Step 1 – Gather context

1. Open:
   - Manuscript at `{{MANUSCRIPT_PATH}}`
   - `research/publons/{{PUBLON_ID}}/{{PUBLON_ID}}-spec.md`
   - `research/publons/{{PUBLON_ID}}/{{PUBLON_ID}}-paper-skeleton.md`
   - Optional: paper pass notes `{{PUBLON_ID}}-paper-passes.md`

2. Use these to understand:

   - The central claim and contributions.
   - Any known limitations or design decisions that must be accurately reflected.

---

## Step 2 – Language and clarity pass

Go through the manuscript and:

1. Simplify overly complex sentences while preserving technical accuracy.
2. Remove filler phrases and redundancies.
3. Ensure each paragraph has a clear topic sentence and coherent flow.
4. Fix obvious grammar, spelling, and punctuation issues.

Avoid introducing new technical content in this pass.

---

## Step 3 – Terminology and notation

1. Identify key terms and symbols.
2. Ensure they are introduced clearly and used consistently.
3. Align terminology with:
   - The publon spec and design doc.
   - Common usage in the relevant research community.

Adjust text where necessary to keep terms consistent.

---

## Step 4 – Claims vs evidence check

1. For each major claim in the abstract, introduction, and conclusion:
   - Check that corresponding evidence is clearly presented in the results section.
   - If evidence is missing or weak, annotate the text (comments or TODO markers) rather than fabricating results.

2. Adjust wording of claims to match the strength of evidence currently available.

If substantial evidence is missing, propose follow-up experiments in a separate note rather than implying results exist.

---

## Step 5 – Record the pass

If `research/publons/{{PUBLON_ID}}/{{PUBLON_ID}}-paper-passes.md` exists:

1. Add a new section:

   - `## Pass: polish-<N>` (e.g. `polish-1`)

2. Document:

   - Date
   - Scope: "polish pass"
   - Main types of changes made
   - Remaining issues (e.g. sections still too weak, missing citations)

If the file does not exist, you may create it via the corresponding template if you judge this useful.

---

## Step 6 – Commit

1. Stage:
   - Manuscript changes.
   - Paper pass notes if updated.

2. Commit with a message like:

   - `{{PUBLON_ID}}: polish pass on paper`

3. Do not push unless I explicitly instruct you to.

---

## Step 7 – Summary

Print a short summary including:

- Main improvements in clarity and consistency.
- Any notable sections that still require more substantial content revisions.
- Any suggested follow-up actions (e.g. experiment batches or design clarifications).
