---
name: openmc-build-and-install
description: This skill should be used when users ask about build and install in openmc; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmc: Build and Install

## High-Signal Playbook

### Route conditions
- Use this skill for install method selection, CMake/toolchain setup, Python package install, and test prerequisites.
- Route to `openmc-parallel-hpc` for cluster launcher/scheduler behavior and MPI scaling studies.
- Route to `openmc-inputs-and-modeling` once build questions are resolved and the user is defining materials/geometry/tallies.

### Triage questions
- Are they using conda/docker/spack binaries or building from source?
- Do they need MPI, DAGMC, libMesh, or strict reproducibility for tests?
- Which compiler/CMake/HDF5 stack is available on this machine?
- Is `OPENMC_CROSS_SECTIONS` already set, and is NNDC data required for regression tests?
- Do they need editable Python install (`pip -e`) for development?
- Are failures during configure, link, runtime startup, or pytest/ctest?

### Canonical workflow
1. Pick install path from docs: conda/docker for fastest onboarding, source build for feature flags.
2. Install source-build prerequisites (C++ compiler, CMake, HDF5, libpng).
3. Configure CMake with explicit options for OpenMP/MPI/optional features and `OPENMC_ENABLE_STRICT_FP` for test reproducibility.
4. Build the C++ executable/library.
5. Install Python API (typically editable mode in development).
6. Install NNDC/ENDF test data and set `OPENMC_CROSS_SECTIONS` / `OPENMC_ENDF_DATA`.
7. Run `ctest` and `pytest` with `OMP_NUM_THREADS=2` when validating changes.

### Minimal working example
```bash
cmake -S . -B build \
  -DCMAKE_BUILD_TYPE=RelWithDebInfo \
  -DOPENMC_USE_OPENMP=ON \
  -DOPENMC_USE_MPI=OFF \
  -DOPENMC_USE_DAGMC=OFF \
  -DOPENMC_USE_LIBMESH=OFF \
  -DOPENMC_ENABLE_STRICT_FP=ON
cmake --build build -j
python -m pip install -e .[test]
bash tools/ci/download-xs.sh
export OPENMC_CROSS_SECTIONS="$HOME/nndc_hdf5/cross_sections.xml"
export OPENMC_ENDF_DATA="$HOME/endf-b-vii.1"
export OMP_NUM_THREADS=2
ctest --test-dir build --output-on-failure
pytest tests/unit_tests
```

### Pitfalls and fixes
- Missing HDF5 or wrong HDF5 variant: ensure `find_package(HDF5 REQUIRED COMPONENTS C HL)` succeeds; if parallel HDF5 is detected, also enable `OPENMC_USE_MPI`.
- OpenMP failure on macOS/Xcode clang: use LLVM clang/libomp as documented in install guide.
- Regression drift across platforms: build with `-DOPENMC_ENABLE_STRICT_FP=on` and cap thread count.
- Tests fail immediately with missing data: set `OPENMC_CROSS_SECTIONS` (and `OPENMC_ENDF_DATA` where needed) to unpacked CI dataset paths.
- Py API import works but executable missing: verify build/install path and that `openmc` is on `PATH`.

### Convergence and validation checks
- `openmc --version` runs and `python -c "import openmc"` succeeds.
- `ctest --output-on-failure` passes for the configured build.
- `pytest tests/unit_tests` passes with `OMP_NUM_THREADS=2`.
- If running regression tests, confirm NNDC data is configured and `OPENMC_ENABLE_STRICT_FP` was enabled at configure time.

## Primary documentation references
- `docs/source/quickinstall.rst`
- `docs/source/usersguide/install.rst`
- `docs/source/devguide/tests.rst`
- `docs/source/pythonapi/base.rst`
- `docs/source/pythonapi/model.rst`
- `docs/source/devguide/docbuild.rst`
- `docs/source/devguide/policies.rst`
- `examples/custom_source/README.md`
- `examples/parameterized_custom_source/README.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Source entry points for unresolved issues
- `CMakeLists.txt`
- `pyproject.toml`
- `tools/ci/download-xs.sh`
- `src/main.cpp`
- `src/xml_interface.cpp`
- `include/openmc/version.h.in`
- `openmc/lib/__init__.py`
- `openmc/lib/core.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" include openmc src`).
