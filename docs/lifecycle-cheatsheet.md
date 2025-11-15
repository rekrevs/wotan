# Lifecycle Cheatsheet – Tasks and Prompts

This document gives a **"which prompt when?"** overview for typical workflows in projects that use this methodology.

Each prompt lives under `prompts/` in the methodology repo and is meant to be copied into Claude Code when working in a **project repo**.

---

## 1. New project setup

**Goal:** Turn an existing codebase (or empty repo) into a research project using this methodology.

**Prompt to use:**

- `prompts/new-project-setup.md`

**Result in the project repo:**

- Creates `research/` with:
  - `meta/meta-plan.md`
  - `publons/P1/` with spec, design, and paper skeleton
  - `dev-log/project-log.md`
- Optionally updates `README` with a short description of the methodology.

---

## 2. Ideation and publon discovery

**Goal:** Explore ideas, map them to candidate publons, and decide what to work on.

**Prompt to use:**

- `prompts/ideation-publon-discovery.md` (added by this refinement)

**Result in the project repo:**

- Updates/creates:
  - `research/ideation/ideation-log.md`
  - `research/ideation/candidate-publons.md`
- Proposes candidate publons with:
  - Working titles
  - Short claim sketches
  - Suggested status (`candidate`, `selected`, …)
- Suggests which candidates to promote to real publons (`P2`, `P3`, …).

---

## 3. Creating a new publon

**Goal:** Instantiate a new publon (`Pk`) once a candidate is selected.

**Prompt to use:**

- `prompts/new-publon.md`

**Result in the project repo:**

- Creates `research/publons/Pk/` with:
  - `Pk-spec.md` (publon spec)
  - `Pk-design.md` (design notes)
  - `Pk-paper-skeleton.md` (paper outline)
  - `Pk-paper-passes.md` (optional)
- Updates `research/meta/meta-plan.md` to include `Pk`.

---

## 4. Implementation stage (Ska, Skb, …)

**Goal:** Make a small, well-scoped code change with tests and documentation.

**Prompt to use:**

- `prompts/impl-stage.md`

**Result in the project repo:**

- For publon `Pk`, stage `Ska`:
  - Creates/updates:
    - `research/publons/Pk/impl-stages/Ska-report.md`
    - `research/publons/Pk/impl-stages/Ska-review-checklist.md`
  - Adds/updates tests under:
    - `tests/stages/Ska/`
    - `tests/integration/` as needed
  - Updates:
    - `Pk-design.md` section on staging plan and design choices

---

## 5. Experiment batch (E1a, E1b, …)

**Goal:** Plan, run, and log a batch of experiments for a publon.

**Prompt to use:**

- `prompts/experiment-batch.md`

**Result in the project repo:**

- For publon `Pk`, experiment `E1a`:
  - Creates:
    - `research/publons/Pk/experiments/E1a-plan.md`
    - `research/publons/Pk/experiments/E1a-log.md`
  - Keeps experiment scripts/configs aligned with the plan.
  - Updates publon spec/design and paper skeleton if results change claims.

---

## 6. Paper passes (structure + polish)

**Goal:** Keep manuscripts in sync with publon state and improve clarity.

**Prompts to use:**

1. **Structure pass**

   - `prompts/paper-pass-structure.md`
   - Aligns manuscript structure with `Pk-paper-skeleton.md`.
   - Records pass in `Pk-paper-passes.md`.

2. **Polish pass**

   - `prompts/paper-pass-polish.md`
   - Improves language, consistency, and claims vs evidence.
   - Records pass in `Pk-paper-passes.md`.

**Result in the project repo:**

- Manually selected manuscript (e.g. `research/papers/Pk-paper.md`) is incrementally improved while staying consistent with publon docs.

---

## 7. Multi-agent delegation across environments

**Goal:** Coordinate multiple Claude Code instances across machines (e.g. dev laptop, Docker/GPU host, cluster).

**Doc to use:**

- `docs/multi-agent-delegation.md` (pattern and file formats)

**Typical usage:**

- Create tasks under `claude/tasks/` describing work for another environment.
- Run Claude Code in that environment to process tasks.
- Record results under `claude/results/`.
- Use git to move tasks/results between environments.

This pattern integrates naturally with publons, stages, and experiments:

- Tasks can reference specific `Pk`, `Ska`, or `E1a`.
- Results can be reflected back into stage reports, experiment logs, and publon docs.
