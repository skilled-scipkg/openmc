# openmc documentation map: Tests

Use this map after the topic skill's primary references.
All paths below are repository-relative and verified.

## Core test docs
- `docs/source/devguide/tests.rst` | Test prerequisites and invocation options.
- `tests/readme.rst` | Test-suite organization summary.
- `tests/testing_harness.py` | Regression harness classes and behaviors.
- `tests/regression_tests/conftest.py` | Regression fixtures/options.
- `tests/unit_tests/conftest.py` | Unit-test fixtures/options.

## Representative test entry points
- `tests/regression_tests/statepoint_restart/test.py` | Restart workflow regression.
- `tests/regression_tests/tallies/test.py` | Core tally regression behavior.
- `tests/regression_tests/deplete_with_transport/test.py` | Depletion integration regression.
- `tests/unit_tests/test_lib.py` | `openmc.lib` bindings behavior.
- `tests/unit_tests/test_model.py` | Model API behavior.
- `tests/cpp_unit_tests/CMakeLists.txt` | C++ unit-test targets.
