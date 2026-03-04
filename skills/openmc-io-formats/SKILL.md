---
name: openmc-io-formats
description: This skill should be used when users ask about io formats in openmc; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmc: Io Formats

## High-Signal Playbook

### Route conditions
- Use this skill for XML/HDF5 schema questions, file version mismatches, and output dataset interpretation.
- Route to `openmc-inputs-and-modeling` for how to build inputs that generate these files.
- Route to `openmc-analysis-and-output` for broader analysis/visualization workflows.

### Triage questions
- Is the issue with input XML, nuclear data files, or simulation outputs?
- Which exact file is involved (`statepoint.h5`, `summary.h5`, `track_*.h5`, etc.)?
- What OpenMC version produced the file, and what version is reading it?
- Is run mode eigenvalue or fixed source (changes available datasets)?
- Does the user need schema description or Python access pattern?

### Canonical workflow
1. Start at `docs/source/io_formats/index.rst` and pick exact format page.
2. Confirm `filetype` and `version` attributes in the HDF5 file.
3. Map required datasets/attributes from docs to the user question.
4. Use Python readers (`openmc.StatePoint`, `openmc.Summary`, restart helpers) for practical access.
5. If expected fields are missing, verify run mode and output settings.
6. If docs and observed behavior differ, inspect writer/reader implementation in `src/state_point.cpp`, `src/summary.cpp`, `src/track_output.cpp`, `openmc/statepoint.py`, and `openmc/summary.py`.

### Minimal working example
```python
import h5py
import openmc

with h5py.File('statepoint.10.h5', 'r') as f:
    print(f.attrs['filetype'], tuple(f.attrs['version']))

with openmc.StatePoint('statepoint.10.h5') as sp:
    print(sp.run_mode, sp.n_batches, sp.current_batch)
    if sp.run_mode == 'eigenvalue':
        print(sp.keff)
```

### Pitfalls and fixes
- Wrong reader for file type: verify `filetype` attribute first.
- Version mismatch errors: regenerate files with the same OpenMC major format version expected by the reader.
- Missing eigenvalue-only fields (`entropy`, `source_bank`) during fixed-source runs: expected behavior.
- Assuming tallies are always present: check `tallies_present` and tally definitions.
- Confusing `summary.h5` (model metadata) with `statepoint.h5` (results/statistics).

### Convergence and validation checks
- File `filetype`/`version` match the reader expectations.
- `current_batch` and `n_batches` are consistent with run completion.
- `n_realizations` is nonzero when tallies are expected.
- Runtime datasets in the HDF5 `runtime` group are populated and plausible.

## Primary documentation references
- `docs/source/io_formats/index.rst`
- `docs/source/io_formats/statepoint.rst`
- `docs/source/io_formats/summary.rst`
- `docs/source/io_formats/track.rst`
- `docs/source/io_formats/particle_restart.rst`
- `docs/source/io_formats/collision_track.rst`
- `docs/source/io_formats/depletion_results.rst`
- `docs/source/io_formats/weight_windows.rst`
- `docs/source/io_formats/volume.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Source entry points for unresolved issues
- `openmc/statepoint.py`
- `openmc/summary.py`
- `openmc/particle_restart.py`
- `openmc/weight_windows.py`
- `src/state_point.cpp`
- `src/summary.cpp`
- `src/track_output.cpp`
- `src/collision_track.cpp`
- `src/particle_restart.cpp`
- `src/weight_windows.cpp`
- `include/openmc/state_point.h`
- `include/openmc/summary.h`
- `include/openmc/track_output.h`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" include openmc src`).
