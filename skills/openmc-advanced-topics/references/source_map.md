# openmc source map: Advanced Topics

Use this map when docs are insufficient and implementation-level checks are required.

## Source roots
- `openmc`
- `include/openmc`
- `src`
- `tests`

## Fast navigation
- `rg -n "<symbol_or_keyword>" openmc include/openmc src tests`

## Function-level entry points
- `src/eigenvalue.cpp` | Eigenvalue generation loop and convergence behavior.
- `include/openmc/eigenvalue.h` | Eigenvalue solver interfaces/state.
- `src/error.cpp` | Core error-reporting and fatal-path behavior.
- `include/openmc/error.h` | Error API used across C++ modules.
- `openmc/lib/error.py` | Python exception translation for C API errors.
- `src/main.cpp` | Executable startup, argument handling, top-level dispatch.
- `src/simulation.cpp` | High-level simulation orchestration.
- `src/xml_interface.cpp` | XML input parsing and validation handoff.

## Behavior/regression anchors
- `tests/regression_tests/entropy/test.py` | Source convergence behavior checks.
- `tests/unit_tests/test_lost_particles.py` | Troubleshooting geometry/lost-particle scenarios.
