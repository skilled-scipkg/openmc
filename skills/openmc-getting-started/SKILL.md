---
name: openmc-getting-started
description: This skill should be used when users ask about getting started in openmc; it prioritizes practical first-run workflow guidance and escalates to source only as needed.
---

# openmc: Getting Started

## High-Signal Playbook

### Route conditions
- Use this skill for first installation checks, first model creation, first run execution, and first output interpretation.
- Route to `openmc-build-and-install` for detailed compiler/toolchain failures.
- Route to `openmc-inputs-and-modeling` for deep geometry/material/tally authoring questions.

### Triage questions
- Is OpenMC already importable (`python -c "import openmc"`) and runnable (`openmc --version`)?
- Is cross section data configured (`OPENMC_CROSS_SECTIONS`)?
- Does the user want a Python API quickstart or XML-driven run?
- Is the first issue setup-related, modeling-related, or interpretation-related?

### Canonical workflow
1. Verify install and data environment.
2. Start from a known-good example model.
3. Run a short eigenvalue simulation.
4. Read `keff` from the generated statepoint.
5. Expand model complexity incrementally.

### Minimal first-run example
```python
import openmc

model = openmc.examples.pwr_pin_cell()
model.settings.batches = 20
model.settings.inactive = 5
model.settings.particles = 1000
sp_path = model.run()

with openmc.StatePoint(sp_path) as sp:
    print('keff:', sp.keff)
```

### Command-line starter check
```bash
python -c "import openmc; print(openmc.__version__)"
openmc --version
```

### Validation checkpoints
- `openmc` imports and executable responds.
- Run writes `statepoint.*.h5` and `summary.h5`.
- `keff` can be read from `openmc.StatePoint`.
- No missing-cross-sections or lost-particle fatal errors.

## Primary documentation references
- `docs/source/quickinstall.rst`
- `docs/source/usersguide/install.rst`
- `docs/source/usersguide/basics.rst`
- `docs/source/usersguide/materials.rst`
- `docs/source/usersguide/geometry.rst`
- `docs/source/usersguide/settings.rst`
- `docs/source/usersguide/processing.rst`
- `docs/source/pythonapi/examples.rst`
- `docs/source/methods/introduction.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Source entry points for unresolved issues
- `openmc/examples.py`
- `openmc/model/model.py`
- `openmc/material.py`
- `openmc/geometry.py`
- `openmc/settings.py`
- `openmc/executor.py`
- `openmc/statepoint.py`
- `src/main.cpp`
- `src/simulation.cpp`
- `src/settings.cpp`
- `src/source.cpp`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" include openmc src openmc tests`).
