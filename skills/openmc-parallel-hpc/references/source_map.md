# openmc source map: Parallel and HPC

Use this map when docs are insufficient and function-level behavior checks are required.

## Source roots
- `openmc`
- `include/openmc`
- `src`
- `tests`

## Fast navigation
- `rg -n "<symbol_or_keyword>" openmc include/openmc src tests`

## Function-level entry points
- `include/openmc/message_passing.h` | MPI abstraction interfaces.
- `src/message_passing.cpp` | MPI communication implementation.
- `include/openmc/openmp_interface.h` | OpenMP wrappers and thread controls.
- `include/openmc/settings.h` | Parallel-related runtime settings.
- `src/settings.cpp` | Parsing and applying MPI/OpenMP settings.
- `include/openmc/simulation.h` | Simulation control interfaces affected by parallelism.
- `src/simulation.cpp` | Parallel run loop behavior.
- `openmc/mpi.py` | Python-side MPI convenience helpers.
- `openmc/settings.py` | User-facing settings that affect parallel execution.
- `openmc/lib/settings.py` | C API settings bridge.
- `include/openmc/random_ray/parallel_map.h` | Random-ray parallel data mapping.

## Behavior/regression anchors
- `tests/regression_tests/stride/test.py` | Reproducibility under changed stride/parallel decomposition.
- `tests/regression_tests/sourcepoint_restart/test.py` | Restart behavior in parallel contexts.
- `tests/unit_tests/test_no_reduce.py` | Reduction/aggregation behavior checks.
