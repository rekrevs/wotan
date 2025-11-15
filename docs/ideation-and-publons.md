# Ideation and Publons

This document explains how to:

- Capture early-stage ideation in a lightweight but structured way.
- Turn raw ideas into **publons** (least publishable units).
- Keep ideation, publons, and project meta-plans in sync.

It complements:

- `docs/methodology-overview.md` (core concepts and roles)
- `docs/directory-conventions.md` (where files live)
- `templates/publon-spec.md.tmpl` (publon spec template)

---

## 1. Ideation goals

Ideation should answer questions like:

- What are we curious about in this project?
- What systems or datasets do we have access to?
- Where are the promising gaps in existing work?
- What "publon-sized" contributions might be feasible?

The goal is **not** polished text, but a **trail of decisions**:

- What ideas were considered and why selected/rejected.
- How publons emerged from those ideas.
- How publons relate to each other and to the overall project.

---

## 2. Where ideation lives in a project

All ideation state for a project lives under:

```text
research/ideation/
  ideation-log.md
  candidate-publons.md
  (optionally more files)
```

### 2.1 `ideation-log.md`

A chronological log of:

* Questions, hunches, and "what if?" scenarios.
* Links to papers, systems, datasets that triggered ideas.
* Short sketches of possible directions.

Format is flexible; a simple structure is:

```markdown
## 2025-03-12

- Noticed that system X fails when ...
- Idea: try technique Y as a plugin.
- Papers to check: [A], [B].

## 2025-03-15

- After reading [A], the idea splits into:
  - P1: behaviour analysis
  - P2: extension with Y
```

### 2.2 `candidate-publons.md`

A structured view of candidates that might become publons.

A simple table format:

```markdown
| ID   | Working title                             | Status     | Short claim sketch                            | Notes                |
|------|-------------------------------------------|------------|-----------------------------------------------|----------------------|
| C1   | Robustness of X under Y                   | candidate  | X degrades non-linearly when Y crosses Z      | based on experiment1 |
| C2   | Fast approximation of Z for large graphs  | selected   | new approx yields 2x speed for <5% loss       | good venue fit       |
| C3   | Visual debugging tool for W               | discarded  | too similar to existing tool V                |                      |
```

Possible status values:

* `candidate`
* `selected`
* `discarded`
* `merged` (merged into another candidate)

Once a candidate is **selected** and becomes a real publon (e.g. `P2`), you should:

* Create `research/publons/P2/` via `prompts/new-publon.md`.
* Update `candidate-publons.md` to record which candidate became which publon.

---

## 3. From idea to publon

A recommended loop for turning ideas into publons:

1. **Dump ideas into `ideation-log.md`**

   * Don't worry about structure at first.
   * Capture questions, hunches, and context.

2. **Cluster ideas into candidate publons**

   * Group related ideas into a few coherent potential contributions.
   * For each, add a row to `candidate-publons.md`.

3. **Stress-test candidates**

   * For each candidate:

     * Is there a clear *claim* we might be able to support?
     * Is there a minimal system + experiment we can realistically build?
     * Is there a plausible venue and audience?

4. **Select 1–3 publons**

   * Mark them as `selected` in `candidate-publons.md`.
   * Give each a clear working title and one-sentence claim sketch.

5. **Create publons**

   * For each selected candidate:

     * Use `prompts/new-publon.md` to create `P1`, `P2`, … under `research/publons/`.
   * Fill in the publon spec (`P1-spec.md`) using the candidate's information.

6. **Keep iterating**

   * As you learn from implementation and experiments:

     * Update `ideation-log.md` with new questions.
     * Split or merge publons if needed.
     * Add new candidates as they arise.

---

## 4. Publon spec as a contract

The publon spec (`P1-spec.md`) plays the role of a **contract** between:

* Ideation (what we hope might be true).
* System design (what we will build).
* Experiments (what we will measure).
* Paper writing (what we will eventually claim).

When instantiating a publon spec from a candidate:

1. Make the **claim** explicit:

   * Even if provisional or hedged ("we hypothesize that…").
2. Specify **success criteria**:

   * What would make this worth publishing?
3. List **in-scope** and **out-of-scope** aspects:

   * To avoid scope creep in implementation.
4. Record **risks and fallbacks**:

   * How this publon might fail, and what can still be salvaged.

The publon spec can and should evolve over time, but changes should be **intentional** and **documented**.

---

## 5. Interaction with project meta-plan

The project meta-plan (`research/meta/meta-plan.md`) is the **bird's-eye view**:

* It lists publons (`P1`, `P2`, …), their status, and dependencies.
* It summarizes high-level questions and risks.

When you promote a candidate to a publon:

1. Add or update a row in the publon table in `meta-plan.md`.
2. Keep the short description consistent with `P1-spec.md`.
3. Update risks/opportunities if this publon significantly changes them.

This keeps ideation (`research/ideation/`), publon-level work (`research/publons/`), and project-level planning (`research/meta/`) linked but not muddled.
