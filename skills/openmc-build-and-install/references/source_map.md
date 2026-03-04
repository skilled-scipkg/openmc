# openmc source map: Build and Install

Use this map when docs are insufficient and function-level behavior checks are required.

## Source roots
- `openmc`
- `include/openmc`
- `src`
- `tests`
- `tools/ci`

## Fast navigation
- `rg -n "<symbol_or_keyword>" CMakeLists.txt pyproject.toml tools/ci openmc include/openmc src tests`

## Function-level entry points
- `CMakeLists.txt` | Build options/feature toggles (`OPENMC_USE_MPI`, `OPENMC_USE_OPENMP`, etc.).
- `pyproject.toml` | Python packaging, build backend, optional extras.
- `tools/ci/download-xs.sh` | Test-data download/setup script behavior.
- `src/main.cpp` | Executable startup and CLI entry.
- `src/initialize.cpp` | Runtime initialization sequence.
- `src/finalize.cpp` | Finalization/cleanup sequence.
- `include/openmc/version.h.in` | Version macro generation.
- `openmc/__init__.py` | Package-level version/config exposure.
- `openmc/config.py` | Runtime data/config path handling.
- `openmc/lib/__init__.py` | Shared library loading path assumptions.

## Behavior/regression anchors
- `tests/cpp_unit_tests/CMakeLists.txt` | C++ unit-test target wiring.
- `tests/unit_tests/test_config.py` | Config/path behavior checks.
