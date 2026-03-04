---
name: openmc-analysis-and-output
description: This skill should be used when users ask about analysis and output in openmc; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmc: Analysis and Output

## High-Signal Playbook

### Route conditions
- Use this skill for statepoint/summary/tally interpretation, plotting outputs, track output, and post-processing workflows.
- Route to `openmc-io-formats` for strict schema/version questions.
- Route to `openmc-inputs-and-modeling` if the output issue is caused by input model definition.

### Triage questions
- Which output file is involved (`statepoint`, `summary`, `track`, `collision_track`, `voxel`)?
- Is the user validating run correctness, extracting metrics, or plotting geometry/results?
- Are expected tallies/scores missing, zero, or unexpectedly noisy?

### Canonical workflow
1. Confirm the simulation completed and output files exist.
2. Inspect run metadata (`run_mode`, batches, realizations) before interpreting results.
3. Extract only required tallies and validate dimensions/filters.
4. For plotting artifacts, check plot settings and compare with known-good regression cases.
5. Use test anchors for behavior confirmation when results look suspicious.

### Minimal analysis snippet
```python
import openmc

with openmc.StatePoint('statepoint.10.h5') as sp:
    print('run_mode:', sp.run_mode)
    print('batches:', sp.current_batch, '/', sp.n_batches)
    if sp.run_mode == 'eigenvalue':
        print('keff:', sp.keff)
    print('tallies_present:', sp.tallies_present)
```

### Validation checkpoints
- Output file loads without version/type errors.
- `current_batch` and `n_batches` are consistent.
- Expected tallies are present and have nonzero realizations.
- Derived metrics match manual spot checks for at least one tally bin.

## Primary documentation references
- `docs/source/usersguide/processing.rst`
- `docs/source/usersguide/plots.rst`
- `docs/source/io_formats/statepoint.rst`
- `docs/source/io_formats/summary.rst`
- `docs/source/io_formats/track.rst`
- `docs/source/io_formats/collision_track.rst`
- `docs/source/io_formats/voxel.rst`
- `docs/source/io_formats/tallies.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Source entry points for unresolved issues
- `openmc/statepoint.py`
- `openmc/summary.py`
- `openmc/tallies.py`
- `openmc/tracks.py`
- `openmc/plots.py`
- `openmc/plotter.py`
- `src/state_point.cpp`
- `src/summary.cpp`
- `src/track_output.cpp`
- `src/output.cpp`
- `src/plot.cpp`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" include openmc src openmc tests`).
