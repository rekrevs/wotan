# Test Organization and Conventions

This document defines **test organization, execution strategies, and quality expectations** for projects using this methodology.

Tests are essential for maintaining quality and enabling iterative development. The conventions below ensure that:

- Tests are easy to locate and understand
- Stage-specific changes can be validated quickly
- Cumulative regression testing protects earlier work
- Deterministic and statistical behaviors are handled appropriately

---

## Test Directory Structure

Projects must organize tests to support both **stage-specific validation** and **cumulative regression testing**.

### Recommended Structure

```text
tests/
  stages/
    S1a/
      test_*.py     # Tests specific to stage S1a
    S1b/
      test_*.py     # Tests specific to stage S1b
    S2a/
      test_*.py     # Tests specific to stage S2a
    ...
  integration/
    test_*.py       # End-to-end integration tests
  unit/
    test_*.py       # Publon-agnostic unit tests (optional)
  fixtures/
    ...             # Shared test data, configs, helpers
  conftest.py       # Pytest configuration (if using pytest)
```

### Directory Purposes

**`tests/stages/{STAGE_ID}/`**

- Contains tests **introduced or significantly modified** during stage `{STAGE_ID}`
- Focus: validate the specific functionality added in that stage
- Naming: use the exact stage ID from `research/publons/{PUBLON_ID}/impl-stages/`
- These tests should be **fast and focused** (seconds to run)

**`tests/integration/`**

- Contains **cumulative end-to-end tests** that exercise the full system
- Updated as major capabilities are added
- These tests may be **slower** (minutes acceptable for complex scenarios)
- Should cover realistic workflows relevant to the publon's experiments

**`tests/unit/` (optional)**

- For unit tests not tied to a specific stage
- Useful for utility functions, data structures, or algorithms used across stages
- Projects may omit this and put everything under `stages/` if preferred

**`tests/fixtures/`**

- Shared test data (input files, expected outputs, configuration files)
- Test helper functions and utilities
- Mock objects or stubs

---

## Test Execution Strategy

For each implementation stage, tests must be run in **two tiers**:

### Tier 1: Stage-Specific Tests (Fast Feedback)

Run only the tests for the **current stage** to get fast feedback during development.

**Example:**

```bash
# Working on stage S2b
pytest tests/stages/S2b/ -v
```

**Purpose:**

- Validate that the stage objective is met
- Quick iteration during development
- Should complete in seconds

### Tier 2: Cumulative Regression Tests (Quality Gate)

Before completing a stage, run **all tests up to and including the current stage**.

**Example:**

```bash
# Before marking S2b complete, run all tests through S2b
pytest tests/stages/S1a/ tests/stages/S1b/ tests/stages/S2a/ tests/stages/S2b/ tests/integration/ -v
```

**Purpose:**

- Ensure no regressions were introduced
- Validate that earlier functionality still works
- Confirm integration tests pass with new changes

**Stage completion requirement:**

- All Tier 2 tests must pass before a stage is marked `completed` in its report
- Document the exact command(s) used in the stage report

---

## Test Coverage Requirements

Each implementation stage should add or update tests in **three categories**:

### 1. Unit Tests

**What:** Tests for individual functions, classes, or modules changed in the stage.

**Characteristics:**

- Fast (milliseconds to seconds per test)
- Isolated (no external dependencies, file I/O, or network)
- Deterministic (same inputs → same outputs every time)

**Location:** `tests/stages/{STAGE_ID}/test_{module}_unit.py` or `tests/unit/`

**Example:**

```python
def test_event_queue_ordering():
    """S1a: Verify events are dequeued in time-priority order."""
    queue = EventQueue()
    queue.enqueue(Event(t=10, type='A'))
    queue.enqueue(Event(t=5, type='B'))
    queue.enqueue(Event(t=8, type='C'))

    assert queue.dequeue().type == 'B'  # t=5
    assert queue.dequeue().type == 'C'  # t=8
    assert queue.dequeue().type == 'A'  # t=10
```

### 2. Integration / System Tests

**What:** Tests that exercise multiple components or the full system end-to-end.

**Characteristics:**

- May be slower (seconds to minutes)
- Realistic scenarios relevant to publon goals
- May involve files, processes, or external tools (Docker, simulators)

**Location:** `tests/stages/{STAGE_ID}/test_{feature}_integration.py` or `tests/integration/`

**Example:**

```python
def test_full_simulation_run():
    """S2a: Run a minimal 3-node simulation for 100 virtual seconds."""
    scenario = Scenario.from_file('fixtures/minimal_3node.yaml')
    coordinator = Coordinator(scenario)
    coordinator.run(max_time=100.0)

    # Check that all nodes advanced to t=100
    for node in coordinator.nodes:
        assert node.current_time == 100.0

    # Check expected message count
    assert coordinator.message_count >= 10
```

### 3. Runtime Assertions / Invariants

**What:** Assertions embedded in production code that fail loudly if assumptions are violated.

**Characteristics:**

- Not separate test files; part of the main codebase
- Enforce invariants (e.g., time monotonicity, non-empty queues, expected ranges)
- Should be cheap enough to leave enabled in research runs

**Location:** Within implementation code

**Example:**

```python
def advance_time(self, delta_t: float):
    """Advance virtual time by delta_t seconds."""
    assert delta_t >= 0, "Time cannot go backwards"
    assert self.event_queue, "Event queue must not be empty when advancing time"
    self.current_time += delta_t
```

**Documentation:** List key invariants added in the stage report under section 3.2 "Tests added / updated"

---

## Deterministic vs. Statistical Tests

Research systems often mix **deterministic components** (simulators, models) and **statistical components** (real-world systems, stochastic models).

### Deterministic Tests

**When:** Testing components expected to be reproducible with fixed inputs/seeds.

**Strategy:**

- Use exact equality checks (`==`, `assert x == expected`)
- Fix random seeds if RNG is involved
- Avoid wall-clock time; use virtual time or counters

**Example:**

```python
def test_deterministic_routing():
    """S3a: Routing decisions must be reproducible with same seed."""
    rng = Random(seed=42)
    router = Router(rng=rng)

    path1 = router.compute_path(src='A', dst='B')

    # Reset and re-run with same seed
    rng = Random(seed=42)
    router = Router(rng=rng)
    path2 = router.compute_path(src='A', dst='B')

    assert path1 == path2
```

### Statistical Tests

**When:** Testing components with inherent randomness or real-world variability (network latency, Docker containers, ML training).

**Strategy:**

- Check distributions, ranges, or statistical properties
- Run multiple trials and check aggregate behavior
- Use tolerance bounds rather than exact equality

**Example:**

```python
def test_network_latency_distribution():
    """S4b: Latency should be roughly uniform between 10-50ms over 100 trials."""
    latencies = [measure_network_latency() for _ in range(100)]

    # Check range
    assert all(10 <= lat <= 50 for lat in latencies), "Latency out of expected range"

    # Check mean is reasonable (statistical, not exact)
    mean_latency = sum(latencies) / len(latencies)
    assert 25 <= mean_latency <= 35, f"Mean latency {mean_latency} outside expected range"
```

**Documentation:** Clearly mark statistical tests in the stage report and review checklist (section 4 of the checklist template already prompts for this).

---

## Test Maintenance and Evolution

### When Tests from Earlier Stages Must Change

Sometimes stage `Sk` requires modifying tests written in stage `Si` (where `i < k`).

**Legitimate reasons:**

- Refined understanding of system invariants
- Intentional behavior change documented in stage `Sk` design
- Improved test coverage or clarity

**Process:**

1. Update the test in `tests/stages/Si/`
2. In stage `Sk` report, document the change under "Changes made → Tests added / updated"
3. Explain why the change was necessary and how it preserves or extends the original intent

**Anti-pattern to avoid:**

- Weakening tests to make them pass without justification
- Deleting failing tests rather than fixing bugs

### Refactoring Test Code

As test suites grow, refactor common patterns into `tests/fixtures/` or helper modules.

**Example:** If multiple stage tests need to set up a 3-node scenario:

```python
# tests/fixtures/scenarios.py
def minimal_3node_scenario():
    """Fixture: minimal 3-node scenario used across stages."""
    return Scenario(
        nodes=['A', 'B', 'C'],
        links=[('A', 'B'), ('B', 'C')],
        duration=100.0
    )
```

Use this in stage tests:

```python
from tests.fixtures.scenarios import minimal_3node_scenario

def test_message_passing():
    """S2b: Nodes can pass messages."""
    scenario = minimal_3node_scenario()
    # ... test logic
```

---

## Test Frameworks and Tools

Projects are free to choose test frameworks, but should document the choice in `research/meta/meta-plan.md` under "Workflow conventions".

### Recommended for Python Projects

- **pytest** – powerful, widely used, good fixture support
- **unittest** – standard library, works everywhere
- **doctest** – for simple example-driven tests in docstrings

### Recommended for Other Languages

- **Go:** `go test` (standard library)
- **Rust:** `cargo test` (standard tooling)
- **C++:** Google Test, Catch2
- **JavaScript/TypeScript:** Jest, Mocha

### CI/CD Integration

If the project uses continuous integration:

- Run Tier 2 (cumulative) tests on every push to main branches
- Optionally run Tier 1 (stage-specific) tests on feature branches for fast feedback
- Document CI setup in `research/dev-log/` or project README

---

## Test Quality Checklist

When reviewing tests during a stage, check:

- [ ] Tests are **focused**: each test validates one specific behavior
- [ ] Tests are **readable**: clear setup, action, assertion structure
- [ ] Tests are **fast enough**: unit tests < 1s, integration tests < 1min per test
- [ ] Tests are **independent**: order of execution doesn't matter
- [ ] **Deterministic tests** use fixed seeds/inputs and exact assertions
- [ ] **Statistical tests** clearly document expected distributions/ranges
- [ ] Test names and docstrings explain **what** is being tested and **why**
- [ ] Failing tests provide **clear diagnostic messages**

This checklist complements section 4 of the `impl-stage-review-checklist.md.tmpl`.

---

## Examples: Stage-Specific Test Evolution

### Example 1: Pure Deterministic System

**Stage S1a:** Add event queue

```
tests/stages/S1a/test_event_queue.py
  - test_enqueue_dequeue_ordering
  - test_empty_queue_behavior
  - test_time_priority
```

**Stage S1b:** Add coordinator loop

```
tests/stages/S1b/test_coordinator.py
  - test_coordinator_advances_time
  - test_coordinator_dispatches_events
tests/integration/test_full_run.py  # NEW: first end-to-end test
```

**Tier 2 before completing S1b:**

```bash
pytest tests/stages/S1a/ tests/stages/S1b/ tests/integration/ -v
```

### Example 2: System with Statistical Components

**Stage S3a:** Add deterministic routing

```
tests/stages/S3a/test_routing_deterministic.py
  - test_shortest_path_deterministic
  - test_routing_reproducible_with_seed
```

**Stage S3b:** Add network latency simulation (statistical)

```
tests/stages/S3b/test_network_latency.py
  - test_latency_within_bounds
  - test_latency_distribution_shape  # statistical
tests/integration/test_end_to_end_with_latency.py
  - test_message_delivery_with_realistic_latency  # statistical
```

**Stage report for S3b** documents:

- Deterministic tests in S3a still pass (routing unchanged)
- New statistical tests in S3b check latency distributions
- Integration test verifies latency doesn't break message delivery

---

## Summary

**Key principles:**

1. **Organize tests by stage** to support iterative development
2. **Run two tiers** of tests: fast (stage-specific) and comprehensive (cumulative)
3. **Cover three categories**: unit, integration, runtime assertions
4. **Handle both deterministic and statistical** behaviors appropriately
5. **Maintain test quality** as the suite evolves

These conventions enable rapid, confident iteration while maintaining quality and reproducibility throughout the research process.
