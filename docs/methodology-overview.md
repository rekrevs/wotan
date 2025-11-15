# Methodology Overview

This methodology is designed for **AI-assisted research projects** where tools like Claude Code help manage the entire lifecycle:

- Ideation and framing
- Design and architecture
- Implementation and testing
- Experiments and analysis
- Paper / report writing

It assumes a clear separation between:

- A **methodology repository** (this repo)
- Multiple **project repositories** that implement concrete systems and studies

The methodology repo is read-only and acts as a **pattern library**. Each project repo instantiates templates from here and maintains its own evolving **research state** under a `research/` directory.

---

## Core concepts

### Publon (least publishable unit)

A **publon** is a small but coherent research contribution. It typically has:

- A focused **claim**: e.g. "We show that X improves Y in setting Z."
- A minimal **system + experiment** needed to support the claim.
- A target **venue style** (conference, workshop, tech report, internal report).

Each publon is identified by an ID: `P1`, `P2`, `P3`, …

A project can have multiple publons over time, and publons may depend on each other (e.g. P2 requires system scaffolding implemented in P1).

---

### Phases for each publon

Each publon goes through some or all of the following phases:

1. **Ideation & framing**
   - Clarify research questions and motivation.
   - Map the publon to related work at a high level.

2. **Design & architecture**
   - Identify system components and data/algorithmic pieces.
   - Make explicit design choices and open questions.

3. **Implementation**
   - Make scoped changes to the codebase in small implementation stages.
   - Maintain high test coverage and clean architecture.
   - Follow iterative staging plan that evolves as implementation progresses.

4. **Experiments & analysis**
   - Define experiment plans, metrics, baselines.
   - Run experiments, collect logs, summarise and interpret results.

5. **Paper / report write-up**
   - Maintain an up-to-date paper skeleton for the publon.
   - Iterate through drafts in passes (structure, content, polish).

The phases are **iterative**, not strictly linear. For example, experiment results may trigger a return to design and implementation.

---

## Three nested loops

This methodology is built around three nested levels of iteration:

1. **Project level loop**
   - Maintained under `research/meta/` in each project.
   - Captures:
     - Overall research questions and context.
     - List of publons (`P1`, `P2`, …) with status and dependencies.
   - Evolves as new publons are added, split, merged, or abandoned.

2. **Publon level loop**

   Each publon is treated as a first-class unit of work with its own lifecycle:

   - Spec and framing (`P1-spec.md`)
   - Design and architecture (`P1-design.md`)
   - Implementation stages (`impl-stages/`)
   - Experiments (`experiments/`)
   - Paper skeleton and manuscript (`P1-paper-skeleton.md`, `research/papers/P1-paper.*`)

   The publon loop continues until the contribution is either published or consciously retired.

3. **Inner loops**

   For each publon, there are several inner loops:

   - **Implementation stages** (S1a, S1b, …)
   - **Experiment batches** (E1a, E1b, …)
   - **Paper passes** (structure, results integration, polish)

   These loops are short and focused, often completable in hours to a day.

The templates and prompts in this repo are designed to keep these three loops in sync and well-documented.

---

## Publon-first and paper-driven development

The methodology encourages **publon-first, paper-driven development**:

- Start from a **publon spec** (`P1-spec.md`):
  - A focused claim and motivation.
  - A minimal system + experiment needed to support the claim.
  - A target venue style (conference, workshop, internal report, etc.).

- Maintain a **paper skeleton** (`P1-paper-skeleton.md`):
  - Section headings and bullet points describing intended content.
  - Mapping from sections → required experiments → required system features.

- Drive implementation and experiments from the publon's needs:
  - Implementation stages are defined to enable specific figures/tables or analyses.
  - Experiment batches are designed to answer the questions posed in the publon spec.

This makes it easier to:

- Stop when a least publishable unit is ready.
- Avoid over-building systems without clear publication value.
- Keep papers, code, and experiments aligned.

See `docs/ideation-and-publons.md` for more on turning ideas into publons.

---

## Automation boundaries

AI tools like Claude Code can automate large parts of the workflow, but not all of it.

Roughly:

- **Highly automatable**
  - Maintaining meta-plans and publon specs.
  - Implementing well-scoped stages with tests.
  - Generating experiment plans/logs and plots from logs.
  - Drafting and refactoring paper sections.

- **Partially automatable**
  - Suggesting good publon candidates and staging plans.
  - Proposing design alternatives and trade-offs.
  - Interpreting experimental results and suggesting follow-ups.

- **Human-dominated**
  - Judging which ideas are worth pursuing or publishing.
  - High-level research direction and ethics.
  - Final interpretation and positioning of contributions.

The prompts in this repo are written so that:

- Claude can be **authoritative** for mechanical steps (code edits, tests, diffs).
- Claude is **advisory** for conceptual steps (idea selection, contribution framing).

Projects can adjust this balance based on their risk tolerance and domain.

---

## Roles

The methodology is designed so that AI tools (e.g. Claude) can act in three conceptual roles:

- **Planner**
  - Maintains meta-plans and publon definitions.
  - Proposes new publons and next steps.

- **Implementer**
  - Edits code, tests, and scripts according to templates and instructions.
  - Runs and interprets tests.

- **Reporter**
  - Updates logs and research notes.
  - Drafts text for design docs, experiment logs, and papers.

In practice, the same AI agent can switch roles depending on the instruction prompts used.

### Multiple agents and environments

For projects that require different development environments (e.g., Docker testing, GPU access, different operating systems), the methodology supports a **multi-agent delegation pattern** where multiple Claude Code instances coordinate via git.

See `docs/multi-agent-delegation.md` for details on task delegation between agents.

---

## Levels of iteration

There are three nested levels of iteration:

1. **Project level**
   - Maintained in `research/meta/` in each project repo.
   - Tracks overall research questions, context, and the list of publons.

2. **Publon level**
   - Each publon has its own directory under `research/publons/`.
   - Contains spec, design, implementation stage reports, experiment folders, and a paper skeleton.

3. **Inner loops**
   - Implementation stages: small, test-driven increments organized into major and minor stages.
   - Experiment batches: planned runs with logs and analyses.
   - Paper passes: structured passes over the manuscript.

The templates and prompts in this repo are organised around these levels.

### Implementation stages in detail

Implementation stages use a two-level hierarchy:

- **Major stages** group related functionality (e.g., S1 = basic system, S2 = add realism, S3 = optimization)
- **Minor stages** are atomic units of work (e.g., S1a, S1b, S1c)

Each minor stage:

- Has a clear, small objective (completable in hours to a day)
- Adds tests in three categories: unit, integration, and runtime assertions
- Is tested using a two-tier strategy (stage-specific + cumulative regression)
- Updates the staging plan based on what was learned

See `docs/naming-conventions.md` and `docs/test-conventions.md` for details.

---

## How to use this repository

1. **Keep this repo read-only.**
   - Clone it once and update it occasionally.
   - Do not write project-specific content here.

2. **In each project repo:**
   - Use the `prompts/` files here as **instruction blocks** for Claude Code.
   - Use the `templates/` files as the basis for project-level files under `research/`.
   - See also `docs/lifecycle-cheatsheet.md` for a high-level map from tasks to prompts.

3. **Extend locally as needed.**
   - If a project needs extra templates or prompts, add them **in the project repo**, not here.
   - If the methodology itself evolves, update this repo in a deliberate, versioned way.
