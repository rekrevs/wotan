# Research Methodology Templates and Prompts

This repository defines a reusable structure for **AI-assisted, Claude-driven research projects**.

It contains:

- **File templates** under `templates/` to be instantiated in each project repository:
  - Project-level meta-plan
  - Publon (least publishable unit) specifications
  - Design documents
  - Implementation stage reports and checklists
  - Experiment plans and logs
  - Paper skeleton and pass notes

- **Prompt blocks** under `prompts/`:
  - Ready-to-use instruction files that can be given to Claude Code
  - They describe how to:
    - Initialise a project with this methodology
    - Create new publons
    - Run implementation stages
    - Plan and run experiment batches
    - Perform structured paper-writing passes

The methodology is based on three nested levels of iteration:

1. **Project level** – the overall research programme.
2. **Publon level** – least publishable units (small, coherent contributions).
3. **Inner loops** – design, implementation, experiments, and paper-writing for each publon.

Projects using this methodology treat this repository as **read-only**. Each project repository creates its own `research/` directory structure where all evolving state (plans, logs, design decisions, experiments, papers) lives.

See:

- `docs/methodology-overview.md` for a conceptual overview.
- `docs/directory-conventions.md` for per-project directory layout.
- `docs/naming-conventions.md` for publon / stage / experiment naming.
