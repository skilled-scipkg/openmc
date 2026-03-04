# openmc source map: Tests

Use this map when docs are insufficient and function-level behavior checks are required.

## Source roots
- `tests`
- `openmc`
- `include/openmc`
- `src`

## Fast navigation
- `rg -n "<symbol_or_keyword>" tests openmc include/openmc src`

## Function-level entry points
- `tests/testing_harness.py` | Regression harness lifecycle and result comparison.
- `tests/regression_tests/conftest.py` | Regression CLI flags/fixtures (`--update`, `--mpi`, etc.).
- `tests/unit_tests/conftest.py` | Unit-test fixtures and data setup.
- `tests/regression_tests/statepoint_restart/test.py` | Restart regression scenario.
- `tests/regression_tests/tallies/test.py` | Tally regression scenario.
- `tests/regression_tests/deplete_with_transport/test.py` | Depletion transport regression.
- `tests/unit_tests/test_lib.py` | `openmc.lib` init/finalize behavior.
- `tests/unit_tests/test_model.py` | Model object behavior and XML export checks.
- `tests/unit_tests/test_statepoint.py` | Statepoint reader unit checks.
- `tests/cpp_unit_tests/test_tally.cpp` | C++ tally unit behavior.
- `src/tallies/tally.cpp` | Core tally runtime implementation linked to many tests.
- `openmc/model/model.py` | Python API behavior exercised by tests.

## Behavior/regression anchors
- `tests/regression_tests/track_output/test.py`
- `tests/regression_tests/random_ray_k_eff/test.py`
- `tests/regression_tests/weightwindows/test.py`
