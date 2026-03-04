---
name: openmc-usersguide
description: This skill should be used when users ask user-facing advanced OpenMC workflow questions covered by the User's Guide.
---

# openmc: Usersguide

## High-Signal Playbook

### Route conditions
- Use this skill for advanced user workflows from the User's Guide: tallies, variance reduction, decay sources, kinetics, stochastic volumes, and CLI scripts.
- Route to `openmc-getting-started` for first-run basics.
- Route to `openmc-io-formats` for strict file schema questions.

### Triage questions
- Which user-guide feature is involved (tallies, variance reduction, decay/R2S, kinetics, volume, scripts)?
- Is the user blocked on setup, configuration semantics, or result interpretation?
- Does the request need API examples, CLI usage, or both?

### Canonical workflow
1. Anchor in the relevant users-guide chapter.
2. Build or adapt a minimal model that exercises only the target feature.
3. Run a small case and validate one key observable.
4. Scale up while monitoring convergence/uncertainty.

### Minimal feature validation sketch
```python
import openmc

model = openmc.examples.pwr_pin_cell()
t = openmc.Tally(name='flux')
t.scores = ['flux']
model.tallies = [t]
sp_path = model.run()

with openmc.StatePoint(sp_path) as sp:
    flux = sp.get_tally(name='flux').mean
    print('flux shape:', flux.shape)
```

### Validation checkpoints
- Feature-specific outputs are present (e.g., tally data, weight windows, volume results).
- Settings and run mode are consistent with requested workflow.
- Results are physically plausible and statistically converged for pilot thresholds.

## Primary documentation references
- `docs/source/usersguide/index.rst`
- `docs/source/usersguide/beginners.rst`
- `docs/source/usersguide/tallies.rst`
- `docs/source/usersguide/variance_reduction.rst`
- `docs/source/usersguide/decay_sources.rst`
- `docs/source/usersguide/kinetics.rst`
- `docs/source/usersguide/volume.rst`
- `docs/source/usersguide/scripts.rst`
- `docs/source/usersguide/random_ray.rst`
- `docs/source/usersguide/processing.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Source entry points for unresolved issues
- `openmc/tallies.py`
- `openmc/weight_windows.py`
- `openmc/volume.py`
- `openmc/deplete/r2s.py`
- `openmc/settings.py`
- `src/tallies/tally.cpp`
- `src/tallies/trigger.cpp`
- `src/weight_windows.cpp`
- `src/volume_calc.cpp`
- `src/ifp.cpp`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" include openmc src openmc tests`).
