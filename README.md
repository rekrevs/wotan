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
- `docs/test-conventions.md` for test organization and execution strategies.
- `docs/multi-agent-delegation.md` for coordinating multiple Claude Code instances across environments.

---

## Additional methodology docs

In addition to the core docs above, this repo also provides:

- `docs/ideation-and-publons.md` – how to structure ideation and turn ideas into publons
- `docs/lifecycle-cheatsheet.md` – a "which prompt when?" overview for typical workflows

These documents make it easier to drive projects from vague ideas all the way to implemented systems and publishable results.

---

## Quick start

Here is a typical way to use this methodology in a new project:

1. **Initial setup**

   - Clone this methodology repo next to your project repo as `../research-methodology/`.
   - In the project repo, use the prompt in `prompts/new-project-setup.md`:
     - This creates `research/` with `meta/`, `publons/`, `dev-log/`, `papers/`.
     - It instantiates `meta-plan.md` and the first publon `P1`.

2. **Publon planning**

   - Use `prompts/ideation-publon-discovery.md` (once created in this repo) to:
     - Clarify research questions and candidate publons.
     - Record ideation under `research/ideation/` in the project.
   - Use `prompts/new-publon.md` to instantiate new publons (`P2`, `P3`, …) as needed.

3. **Implementation**

   - For each small implementation step (stage `Ska`, `Skb`, …) in a publon:
     - Use `prompts/impl-stage.md` to:
       - Plan the stage.
       - Create stage report and checklist.
       - Implement code + tests.
       - Run stage-specific and cumulative tests.
       - Update the publon design doc and staging plan.

4. **Experiments**

   - For each experiment batch (`E1a`, `E1b`, …) in a publon:
     - Use `prompts/experiment-batch.md` to:
       - Plan the experiment (hypotheses, metrics, protocol).
       - Align scripts/config with the plan.
       - Log results and analysis.

5. **Paper writing**

   - Use `prompts/paper-pass-structure.md` to keep manuscript structure aligned with the publon's paper skeleton.
   - Use `prompts/paper-pass-polish.md` to perform focused polishing passes on clarity, consistency, and claims vs evidence.

6. **Multi-agent setups**

   - If the project requires multiple environments (e.g. Docker host, GPU cluster, laptop dev):
     - Use the pattern in `docs/multi-agent-delegation.md` to coordinate multiple Claude Code instances via git and `claude/tasks/` + `claude/results/` files in the project repo.
