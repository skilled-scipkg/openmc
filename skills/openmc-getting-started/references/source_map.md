# openmc source map: Getting Started

Use this map when docs are insufficient and function-level behavior checks are required.

## Source roots
- `openmc`
- `include/openmc`
- `src`
- `tests`
- `examples`

## Fast navigation
- `rg -n "<symbol_or_keyword>" openmc include/openmc src tests examples`

## Function-level entry points
- `openmc/examples.py` | Built-in model constructors for fast startup.
- `openmc/model/model.py` | `Model.run()` and XML export flow.
- `openmc/material.py` | Material composition APIs used in first models.
- `openmc/geometry.py` | Geometry assembly behavior.
- `openmc/settings.py` | Batch/particle/run-mode controls.
- `openmc/executor.py` | Python-side execution wrapper.
- `openmc/statepoint.py` | First-results access pattern.
- `src/main.cpp` | Executable entrypoint.
- `src/simulation.cpp` | Main transport loop.
- `src/settings.cpp` | Settings parsing/runtime propagation.
- `src/source.cpp` | Source-bank setup behavior.

## Behavior/regression anchors
- `examples/pincell/build_xml.py` | Minimal XML flow.
- `tests/regression_tests/infinite_cell/test.py` | Stable baseline run behavior.
- `tests/unit_tests/test_model.py` | Model construction/execution API checks.
