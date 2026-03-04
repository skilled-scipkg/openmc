# openmc source map: Simulation Workflows

Use this map when docs are insufficient and function-level behavior checks are required.

## Source roots
- `openmc`
- `include/openmc`
- `src`
- `tests`

## Fast navigation
- `rg -n "<symbol_or_keyword>" openmc include/openmc src tests`

## Function-level entry points
- `openmc/model/model.py` | High-level run and XML export orchestration.
- `openmc/executor.py` | Process execution wrapper behavior.
- `openmc/settings.py` | Run-mode/sourcepoint/output settings.
- `openmc/source.py` | Source definitions and serialization.
- `openmc/deplete/coupled_operator.py` | Transport-coupled depletion flow.
- `openmc/deplete/integrators.py` | Depletion step progression behavior.
- `openmc/particle_restart.py` | Restart particle handling.
- `openmc/statepoint.py` | Run metadata and results continuity checks.
- `src/simulation.cpp` | Core simulation loop and batch progression.
- `src/settings.cpp` | Settings ingestion into runtime.
- `src/source.cpp` | Source bank generation and usage.
- `src/state_point.cpp` | Statepoint write lifecycle.
- `include/openmc/simulation.h`
- `include/openmc/settings.h`
- `include/openmc/source.h`

## Behavior/regression anchors
- `tests/regression_tests/statepoint_restart/test.py`
- `tests/regression_tests/sourcepoint_restart/test.py`
- `tests/regression_tests/particle_restart_fixed/test.py`
- `tests/regression_tests/deplete_with_transport/test.py`
