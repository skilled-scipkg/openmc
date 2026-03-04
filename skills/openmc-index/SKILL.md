---
name: openmc-index
description: This skill should be used when users ask how to use openmc and the correct generated documentation skill must be selected before going deeper into source code.
---

# openmc Skills Index

## Route the request
- Classify intent first:
  - User simulation workflow: getting started, build/install, inputs, run workflows, analysis/output.
  - Developer/contributor workflow: tests, release impacts, theory/method internals.
  - API/coupling workflow: Python API, `openmc.lib`, C API mapping.
- Choose exactly one primary topic skill, then only expand to adjacent skills if needed.

## Fast bootstrap (when user has no starting point)
1. Validate environment with `openmc-build-and-install`.
2. Run a known-good first model with `openmc-getting-started`.
3. Build/adjust problem inputs with `openmc-inputs-and-modeling`.
4. Execute target workflow with `openmc-simulation-workflows` (and `openmc-parallel-hpc` if needed).
5. Interpret outputs with `openmc-analysis-and-output`.

## Topic skills
- `openmc-getting-started`: first model/run path and basic outputs.
- `openmc-build-and-install`: toolchain, CMake flags, editable install, test prerequisites.
- `openmc-inputs-and-modeling`: materials/geometry/settings/tallies and XML mapping.
- `openmc-simulation-workflows`: run modes, restarts, depletion workflow framing.
- `openmc-parallel-hpc`: MPI/OpenMP and feature-gated HPC behavior.
- `openmc-api-and-scripting`: Python API, `openmc.lib`, C API boundary.
- `openmc-analysis-and-output`: result extraction and post-processing entry points.
- `openmc-io-formats`: XML/HDF5 format specs and versioned schemas.
- `openmc-theory-and-methods`: estimator theory, convergence methods, transport physics internals.
- `openmc-usersguide`: user-facing advanced usage topics.
- `openmc-tests`: regression/unit test harness usage and test file conventions.
- `openmc-releasenotes`: upgrade/deprecation impact by version.
- `openmc-advanced-topics`: consolidated singleton topics (license/devguide/docker/templates/eigenvalue troubleshooting).

## Escalation order (required)
1. Start with the selected topic skill's **Primary documentation references**.
2. If insufficient, use that skill's `references/doc_map.md`.
3. If still ambiguous, use that skill's `references/source_map.md` and inspect source entry points.

## Canonical roots
- Documentation roots: `docs/source`, `man/man1`
- Tutorials/examples root: `examples`
- Test behavior roots: `tests`
- Source roots: `include`, `openmc`, `src`

## Source search pattern
- `rg -n "<symbol_or_keyword>" include openmc src`
