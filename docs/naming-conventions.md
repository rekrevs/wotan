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

Implementation stages are **small, incremental development steps** within a publon, organized into a two-level hierarchy:

- **Major stages** (identified by the numeric part `<k>`)
- **Minor stages** (identified by the full ID `S<k><suffix>`)

### Stage ID Format

Each stage has an ID: `S<k><suffix>`:

- `<k>`: an integer for the **major implementation theme** within the publon (`1`, `2`, `3`, …)
- `<suffix>`: a lowercase letter (`a`, `b`, `c`, …) for **atomic development steps** within that theme

### Major vs. Minor Stages

**Major stages** represent significant implementation themes or milestones:

- They group related functionality or architectural components
- They correspond to coherent phases of system development
- They are **not** separate commits; they are organizational concepts

Examples of major stage themes:

- Major stage 1: Minimal system scaffold
- Major stage 2: Add realism (network simulation, edge infrastructure)
- Major stage 3: Add intelligence (ML models, placement algorithms)
- Major stage 4: Optimization and scalability

**Minor stages** are the **actual units of work** and correspond to individual commits:

- Each is small enough to implement, test, and review in one sitting
- Each should be completable in hours to at most a day
- Each produces one clean commit (or small set of related commits)
- Each has its own stage report and review checklist

### Examples

**Scenario: Implementing a distributed simulation system**

- `S1a` – Create event queue and coordinator scaffold
- `S1b` – Add basic node abstraction
- `S1c` – Implement deterministic time advancement
- *(Major stage 1 = minimal working system)*

- `S2a` – Integrate network simulator interface
- `S2b` – Bridge nodes to network simulation
- `S2c` – Add realistic latency and topology
- *(Major stage 2 = add network realism)*

- `S3a` – Add Docker-based edge container support
- `S3b` – Implement resource monitoring
- *(Major stage 3 = add edge infrastructure)*

### Stage Files

Stage files are stored under:

```text
research/publons/P1/impl-stages/S1a-report.md
research/publons/P1/impl-stages/S1a-review-checklist.md
research/publons/P1/impl-stages/S1b-report.md
research/publons/P1/impl-stages/S1b-review-checklist.md
...
```

### Planning Major Stages

The numeric part `<k>` should be decided when planning the publon's implementation:

1. Identify 2–5 major themes or milestones for the publon
2. Assign each theme a number (`1`, `2`, `3`, …)
3. Sketch initial minor stages (`a`, `b`, `c`, …) for the first 1–2 major stages
4. Refine the list of minor stages iteratively as implementation progresses

The staging plan lives in `research/publons/{PUBLON_ID}/{PUBLON_ID}-design.md` section 7 and should be updated after each minor stage is completed.

### Flexibility

Projects have flexibility in how they define major stage boundaries:

- **Architectural layers:** S1 = data model, S2 = logic, S3 = API
- **Feature sets:** S1 = basic simulation, S2 = monitoring, S3 = placement
- **Capability levels:** S1 = deterministic, S2 = realistic, S3 = optimized
- **Milestones:** S1 = M0 POC, S2 = M1 with network, S3 = M2 with edge

The key is to keep major stages **conceptually coherent** and minor stages **small and atomic**.

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
