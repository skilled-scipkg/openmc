---
name: openmc-tests
description: This skill should be used when users ask about tests in openmc; it prioritizes practical test execution and harness usage before source inspection.
---

# openmc: Tests

## High-Signal Playbook

### Route conditions
- Use this skill for running unit/regression/C++ tests, interpreting harness failures, and updating references.
- Route to `openmc-build-and-install` if failures are due to missing build/data prerequisites.
- Route to feature skills after identifying the failing subsystem.

### Triage questions
- Is the target Python unit tests, regression tests, or C++ unit tests?
- Are NNDC cross sections configured and is `OMP_NUM_THREADS` constrained?
- Is MPI enabled and should tests run with `--mpi`?
- Is the request verification-only or reference-update (`pytest --update`)?

### Canonical workflow
1. Confirm environment prerequisites and data paths.
2. Run the smallest relevant test slice first.
3. Expand to broader suite only after local failures are understood.
4. For deterministic reference updates, regenerate with explicit intent.
5. Re-run without update mode to confirm clean pass.

### Minimal test commands
```bash
export OMP_NUM_THREADS=2
pytest tests/unit_tests/test_model.py
pytest tests/regression_tests/statepoint_restart/test.py
ctest --test-dir build --output-on-failure
```

### Validation checkpoints
- Unit/regression/C++ tests selected for the task pass locally.
- Failing cases are reproducible and isolated to a subsystem.
- Updated regression references (`inputs_true.dat`/`results_true.dat`) are regenerated only when intended.
- MPI/event-mode test invocations use the correct flags when required.

## Primary documentation references
- `docs/source/devguide/tests.rst`
- `tests/readme.rst`
- `tests/testing_harness.py`
- `tests/regression_tests/conftest.py`
- `tests/unit_tests/conftest.py`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Source entry points for unresolved issues
- `tests/testing_harness.py`
- `tests/regression_tests/conftest.py`
- `tests/unit_tests/conftest.py`
- `tests/regression_tests/statepoint_restart/test.py`
- `tests/regression_tests/deplete_with_transport/test.py`
- `tests/regression_tests/tallies/test.py`
- `tests/unit_tests/test_lib.py`
- `tests/unit_tests/test_model.py`
- `tests/unit_tests/test_statepoint.py`
- `tests/unit_tests/test_deplete_integrator.py`
- `src/tallies/tally.cpp`
- `openmc/model/model.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" include openmc src openmc tests`).
