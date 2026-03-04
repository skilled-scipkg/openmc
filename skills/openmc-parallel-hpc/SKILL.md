---
name: openmc-parallel-hpc
description: This skill should be used when users ask about parallel and hpc in openmc; it prioritizes run-ready MPI/OpenMP guidance and then source inspection for unresolved details.
---

# openmc: Parallel and HPC

## High-Signal Playbook

### Route conditions
- Use this skill for MPI/OpenMP configuration, launcher usage, scaling behavior, and parallel reproducibility issues.
- Route to `openmc-build-and-install` for generic build failures not specific to parallel modes.
- Route to `openmc-simulation-workflows` for non-HPC run logic (restart/depletion pipelines).

### Triage questions
- Is the binary built with MPI (`OPENMC_USE_MPI`) and OpenMP (`OPENMC_USE_OPENMP`)?
- What launcher is used (`mpiexec`, `srun`), and how many ranks/threads?
- Is the issue correctness divergence, performance scaling, or hangs/deadlocks?
- Are optional features (DAGMC/libMesh) enabled and compatible with the target system?

### Canonical workflow
1. Configure and build with explicit MPI/OpenMP flags.
2. Run a small known model on 1 rank/thread, then scale ranks/threads.
3. Keep `OMP_NUM_THREADS` controlled during validation.
4. Compare key outputs (`keff`, tally means/uncertainties, runtime metrics) across parallel settings.

### Minimal parallel run commands
```bash
cmake -S . -B build \
  -DCMAKE_BUILD_TYPE=RelWithDebInfo \
  -DOPENMC_USE_MPI=ON \
  -DOPENMC_USE_OPENMP=ON
cmake --build build -j

export OMP_NUM_THREADS=2
mpiexec -n 2 openmc
```

### Validation checkpoints
- Parallel launch completes and writes expected statepoint.
- Results are statistically consistent with single-rank baseline.
- Runtime decreases or remains stable as ranks/threads increase for the same workload.
- MPI-specific tests pass when invoked with `pytest --mpi`.

## Primary documentation references
- `docs/source/usersguide/parallel.rst`
- `docs/source/usersguide/settings.rst`
- `docs/source/methods/parallelization.rst`
- `docs/source/io_formats/settings.rst`
- `docs/source/devguide/tests.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Source entry points for unresolved issues
- `include/openmc/message_passing.h`
- `src/message_passing.cpp`
- `include/openmc/openmp_interface.h`
- `include/openmc/settings.h`
- `src/settings.cpp`
- `include/openmc/simulation.h`
- `src/simulation.cpp`
- `openmc/mpi.py`
- `openmc/settings.py`
- `openmc/lib/settings.py`
- `include/openmc/random_ray/parallel_map.h`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" include openmc src openmc tests`).
