# openmc source map: API and Scripting

Use this map when docs are insufficient and function-level behavior checks are required.

## Source roots
- `openmc`
- `include/openmc`
- `src`
- `tests`

## Fast navigation
- `rg -n "<symbol_or_keyword>" openmc include/openmc src tests`

## Function-level entry points
- `include/openmc/capi.h` | C API declarations (`openmc_init`, `openmc_run`, etc.).
- `openmc/lib/core.py` | ctypes symbol binding and lifecycle control.
- `openmc/lib/__init__.py` | Python C API namespace exports.
- `openmc/model/model.py` | High-level model run/export API.
- `openmc/executor.py` | Python-side run invocation helpers.
- `openmc/deplete/openmc_operator.py` | Transport-coupled depletion operator.
- `openmc/deplete/coupled_operator.py` | Coupled depletion setup.
- `openmc/deplete/integrators.py` | Depletion time integration algorithms.
- `openmc/statepoint.py` | Result access from Python API.
- `openmc/data/library.py` | Nuclear data library indexing.
- `openmc/mgxs/library.py` | MGXS library object behavior.
- `src/mgxs_interface.cpp` | C++/Python MGXS bridge behavior.
- `src/cross_sections.cpp` | Cross section loading/index resolution.

## Behavior/regression anchors
- `tests/unit_tests/test_lib.py` | `openmc.lib` lifecycle behavior.
- `tests/unit_tests/test_deplete_integrator.py` | Integrator correctness checks.
- `tests/unit_tests/test_model.py` | `openmc.Model` run/export behavior.
- `tests/regression_tests/deplete_with_transport/test.py` | End-to-end depletion coupling.
