# Directory Conventions for Project Repositories

Projects that use this methodology maintain research-related state in a dedicated `research/` directory in the project repository.

Below is the recommended structure.

---

## Top-level

```text
research/
  meta/
  ideation/
  publons/
  dev-log/
  papers/
```

### `research/meta/`

Project-level planning and context. Typical files:

* `meta-plan.md`

  * Overall project questions, context, and list of publons.
* `venues.md` (optional)

  * Candidate venues, deadlines, and constraints.
* Other project-wide planning documents as needed.

### `research/ideation/`

Early-stage ideation and publon-discovery notes. Typical files:

- `ideation-log.md`
  - Chronological log of ideas, questions, and sketches.
- `candidate-publons.md`
  - Table or list of potential publons with rough claims and status:
    - `candidate` / `selected` / `discarded` / `merged`.

This directory captures the **messy, exploratory phase** before publons are fully specified. Once a publon is selected, its concrete spec, design, and lifecycle live under `research/publons/`.

### `research/publons/`

Each publon (least publishable unit) gets its own directory:

```text
research/publons/P1/
research/publons/P2/
...
```

Inside each publon directory:

```text
P1/
  P1-spec.md               # Publon specification (claim, motivation, scope)
  P1-design.md             # Design & architecture notes for this publon
  P1-paper-skeleton.md     # Paper/section outline
  P1-experiments-index.md  # Index of experiments for this publon (optional)

  impl-stages/
    S1a-report.md
    S1a-review-checklist.md
    S1b-report.md
    ...

  experiments/
    E1a-plan.md
    E1a-log.md
    E1b-plan.md
    E1b-log.md
    ...
```

The naming of implementation stages (`S1a`, `S1b`, …) and experiment batches (`E1a`, `E1b`, …) is described in `docs/naming-conventions.md` in this methodology repo.

### `research/dev-log/`

Cross-cutting logs that are not tied to a single publon, for example:

* `project-log.md`

  * Chronological log of decisions, major changes, and milestones.

You can add more logs here as needed:

* `meeting-notes.md`
* `infrastructure-notes.md`
* etc.

### `research/papers/`

Manuscript sources and long-form write-ups. For example:

```text
research/papers/P1-paper.md     # Markdown or LaTeX for publon P1
research/papers/P2-paper.tex
research/papers/overview-report.md
```

The paper-writing prompts in this methodology repo assume that:

* Each publon has at least one associated manuscript under `research/papers/`.
* The manuscript name indicates which publon it belongs to, e.g. `P1-paper.*`.

---

## Flexibility

These conventions are meant to be **helpful defaults**, not strict constraints.

* For very small projects, you may only have `P1/` and a single paper.
* For larger projects, you can introduce additional subdirectories (e.g. `datasets/`, `figures/`) under `research/` or within publon directories.
* If you extend the structure, keep names and paths explicit so prompts can be adapted easily.
