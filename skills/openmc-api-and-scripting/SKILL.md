---
name: openmc-api-and-scripting
description: This skill should be used when users ask about api and scripting in openmc; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmc: API and Scripting

## High-Signal Playbook

### Route conditions
- Use this skill for Python API usage, `openmc.lib` in-memory control, C/C++ API mapping, and scripting automation.
- Route to `openmc-inputs-and-modeling` for geometry/material/tally definition details.
- Route to `openmc-analysis-and-output` for deep interpretation/visualization of results.

### Triage questions
- Is the user using high-level Python API (`openmc.Model`, `openmc.run`) or in-memory coupling (`openmc.lib`)?
- Do they need transport only, depletion (`openmc.deplete`), or MGXS/data tooling?
- Are they modifying the C API and expecting Python ctypes bindings to expose new symbols?
- Is the workflow file-based (XML/statepoint) or library-driven in one process?
- Are they running under MPI and expecting `openmc.lib`/depletion parallel behavior?

### Canonical workflow
1. Build model with Python API objects (`openmc.Model` and sub-objects) and set runtime data paths.
2. Run via high-level interface (`model.run()` / `openmc.run()`) for standard workflows.
3. For in-memory workflows, use `openmc.lib.init() -> ... -> openmc.lib.run() -> openmc.lib.finalize()`.
4. Use `openmc.StatePoint`, `openmc.Summary`, and tally objects for post-processing.
5. For depletion, compose `CoupledOperator` or `IndependentOperator` and an integrator.
6. If C API changes are involved, update `include/openmc/capi.h` and corresponding ctypes signatures in `openmc/lib/core.py` plus related wrapper modules (for example, `openmc/lib/settings.py`).

### Minimal working examples
```python
import openmc

model = openmc.examples.pwr_pin_cell()
sp_path = model.run()
with openmc.StatePoint(sp_path) as sp:
    print(sp.run_mode, sp.keff)
```

```python
import openmc.lib

openmc.lib.init()
try:
    openmc.lib.run()
    print(openmc.lib.keff())
finally:
    openmc.lib.finalize()
```

### Pitfalls and fixes
- `openmc.lib` session leaks: always finalize in `finally`.
- C API drift: when adding/changing symbols in `capi.h`, update ctypes `argtypes` and `restype` in `openmc/lib`.
- Depletion setup errors: `chain_file` must be provided or set in `openmc.config['chain_file']`.
- Shared library load issues: ensure `libopenmc.so`/`dylib` is present in `openmc/lib` package.
- Incorrect type/value inputs: setters enforce `openmc.checkvalue` checks and will raise early.

### Convergence and validation checks
- High-level run creates statepoint file and `openmc.StatePoint(...).keff` is readable for eigenvalue runs.
- In-memory flow toggles `openmc.lib.is_initialized` correctly across init/finalize.
- Depletion run writes results and advances expected step count.
- Any new C API symbol is callable from both C docs and Python bindings.

## Primary documentation references
- `docs/source/pythonapi/index.rst`
- `docs/source/pythonapi/capi.rst`
- `docs/source/capi/index.rst`
- `docs/source/pythonapi/deplete.rst`
- `docs/source/pythonapi/data.rst`
- `docs/source/pythonapi/mgxs.rst`
- `docs/source/pythonapi/stats.rst`
- `docs/source/pythonapi/openmoc.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Source entry points for unresolved issues
- `include/openmc/capi.h`
- `openmc/lib/__init__.py`
- `openmc/lib/core.py`
- `openmc/model/model.py`
- `openmc/deplete/openmc_operator.py`
- `openmc/deplete/integrators.py`
- `openmc/statepoint.py`
- `openmc/data/library.py`
- `src/mgxs_interface.cpp`
- `src/cross_sections.cpp`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" include openmc src`).
