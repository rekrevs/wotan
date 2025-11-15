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

4. **Experiments & analysis**
   - Define experiment plans, metrics, baselines.
   - Run experiments, collect logs, summarise and interpret results.

5. **Paper / report write-up**
   - Maintain an up-to-date paper skeleton for the publon.
   - Iterate through drafts in passes (structure, content, polish).

The phases are **iterative**, not strictly linear. For example, experiment results may trigger a return to design and implementation.

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
   - Implementation stages: small, test-driven increments.
   - Experiment batches: planned runs with logs and analyses.
   - Paper passes: structured passes over the manuscript.

The templates and prompts in this repo are organised around these levels.

---

## How to use this repository

1. **Keep this repo read-only.**
   - Clone it once and update it occasionally.
   - Do not write project-specific content here.

2. **In each project repo:**
   - Use the `prompts/` files here as **instruction blocks** for Claude Code.
   - Use the `templates/` files as the basis for project-level files under `research/`.

3. **Extend locally as needed.**
   - If a project needs extra templates or prompts, add them **in the project repo**, not here.
   - If the methodology itself evolves, update this repo in a deliberate, versioned way.
