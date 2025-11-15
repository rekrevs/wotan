# Naming Conventions

Consistent naming makes it easier for AI tools and humans to coordinate work across planning, implementation, experiments, and writing.

---

## Publons

- Publons are identified by IDs: `P1`, `P2`, `P3`, …
- Each publon has a directory under `research/publons/`, named exactly by its ID:
  - `research/publons/P1/`
  - `research/publons/P2/`
- Within each publon directory, principal files are prefixed with the publon ID:
  - `P1-spec.md`
  - `P1-design.md`
  - `P1-paper-skeleton.md`
  - `P1-experiments-index.md` (optional)

---

## Implementation stages

Implementation stages are **small, incremental development steps** within a publon.

- Each stage has an ID: `S<k><suffix>`:
  - `<k>`: an integer for the broad implementation milestone within the publon (`1`, `2`, `3`, …).
  - `<suffix>`: a lowercase letter (`a`, `b`, `c`, …) identifying minor steps within that milestone.

Examples:

- `S1a`, `S1b`, `S1c` – three small implementation stages for the first milestone.
- `S2a`, `S2b` – stages for the second milestone.

Stage files are stored under:

```text
research/publons/P1/impl-stages/S1a-report.md
research/publons/P1/impl-stages/S1a-review-checklist.md
```

The exact semantics of the numeric part (`1`, `2`, …) are project-dependent, but typically:

* The number groups a set of related code changes or features.
* The letter distinguishes atomic commits or work units.

---

## Experiment batches

Experiment batches are grouped runs with a shared plan and analysis.

* Each experiment batch has an ID: `E<k><suffix>`:

  * `<k>`: an integer grouping related experiments within the publon.
  * `<suffix>`: a lowercase letter for variants or sub-batches.

Examples:

* `E1a`, `E1b` – two batches of experiments under the first experimental theme.
* `E2a` – first batch for a second theme.

Files:

```text
research/publons/P1/experiments/E1a-plan.md
research/publons/P1/experiments/E1a-log.md
```

---

## Paper passes

Paper passes capture structured editing passes over a manuscript.

* Passes can be referred to informally (e.g. "structure pass", "results integration pass") or with IDs such as `pass-structure-1`, `pass-polish-2`.
* Notes for passes are typically stored in a file per publon manuscript, e.g.:

```text
research/publons/P1/P1-paper-passes.md
```

and use headings like:

* `## Pass: structure-1`
* `## Pass: results-integration-1`
* `## Pass: polish-1`

The template `templates/paper-pass-notes.md.tmpl` provides a basic structure.

---

## Commit messages (optional convention)

Commit messages can refer to publon and stage IDs, for example:

* `P1 S1a: add basic simulation scaffold`
* `P2 S2b: refine evaluation metrics`

This is optional but helpful for tracing changes back to publons and stages.
