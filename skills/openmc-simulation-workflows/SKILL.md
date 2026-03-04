---
name: openmc-simulation-workflows
description: This skill should be used when users ask about simulation workflows in openmc; it prioritizes practical run/restart/depletion flow and then source inspection for unresolved details.
---

# openmc: Simulation Workflows

## High-Signal Playbook

### Route conditions
- Use this skill for execution settings, run mode selection, restart/statepoint/sourcepoint workflows, and depletion pipelines.
- Route to `openmc-parallel-hpc` for MPI/OpenMP scaling or launcher issues.
- Route to `openmc-inputs-and-modeling` for geometry/material definition problems.

### Triage questions
- Is the workflow eigenvalue, fixed source, random ray, or depletion?
- Is this a fresh run, continuation run, or restart from `statepoint`/`sourcepoint`/particle restart?
- Are required output artifacts enabled in settings?
- Is the user running file-based (`openmc`) or Python-driven (`model.run()`) execution?

### Canonical workflow
1. Build/validate model and settings for the target run mode.
2. Run a short pilot to verify output artifacts and convergence trend.
3. Configure restart/sourcepoint/depletion specifics.
4. Run production settings and validate output continuity.
5. Use regression tests for restart/depletion behavior checks.

### Minimal run and restart-friendly setup
```python
import openmc

model = openmc.examples.pwr_pin_cell()
model.settings.batches = 30
model.settings.inactive = 10
model.settings.particles = 2000
model.settings.sourcepoint = {'write': True}
sp_path = model.run()
print('statepoint:', sp_path)
```

### Validation checkpoints
- Run writes expected artifacts (`statepoint`, `summary`, optional sourcepoint/track files).
- Restart/continuation run advances batches without input/schema errors.
- Depletion run produces `depletion_results.h5` and expected step count.
- Reported `run_mode` in statepoint matches intended workflow.

## Primary documentation references
- `docs/source/usersguide/settings.rst`
- `docs/source/usersguide/data.rst`
- `docs/source/usersguide/parallel.rst`
- `docs/source/usersguide/depletion.rst`
- `docs/source/pythonapi/model.rst`
- `docs/source/pythonapi/deplete.rst`
- `docs/source/io_formats/statepoint.rst`
- `docs/source/io_formats/source.rst`
- `docs/source/io_formats/particle_restart.rst`
- `docs/source/io_formats/track.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Source entry points for unresolved issues
- `openmc/model/model.py`
- `openmc/executor.py`
- `openmc/settings.py`
- `openmc/source.py`
- `openmc/deplete/coupled_operator.py`
- `openmc/deplete/integrators.py`
- `openmc/particle_restart.py`
- `openmc/statepoint.py`
- `src/simulation.cpp`
- `src/settings.cpp`
- `src/source.cpp`
- `src/state_point.cpp`
- `include/openmc/simulation.h`
- `include/openmc/settings.h`
- `include/openmc/source.h`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" include openmc src openmc tests`).
