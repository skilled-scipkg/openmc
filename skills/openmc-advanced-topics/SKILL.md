---
name: openmc-advanced-topics
description: This skill should be used for low-frequency, narrow OpenMC topics after core workflow skills have been ruled out.
---

# openmc: Advanced Topics

## High-Signal Playbook

### Route conditions
- Use this skill for Docker deployment notes, licensing questions, developer-guide routing, and eigenvalue troubleshooting details.
- Route to core skills for direct build/model/run/output requests.

### Triage questions
- Is the question operational (build/run) or documentation/policy oriented?
- Is the user blocked by convergence/troubleshooting symptoms (entropy drift, unstable `keff`, lost particles)?
- Do they need developer workflow guidance (contributing, branching, PR expectations)?

### Canonical workflow
1. Start with topic docs in `Primary documentation references`.
2. For troubleshooting, reproduce with a minimal model first (`openmc.examples.pwr_pin_cell`).
3. Check convergence indicators (`keff`, Shannon entropy, particle loss warnings).
4. Escalate to source entry points only when doc guidance is ambiguous.

### Minimal troubleshooting probe
```python
import openmc

model = openmc.examples.pwr_pin_cell()
model.settings.batches = 60
model.settings.inactive = 20
model.settings.particles = 3000
sp_path = model.run()

with openmc.StatePoint(sp_path) as sp:
    print('keff:', sp.keff)
    if sp.entropy is not None:
        print('entropy_tail:', sp.entropy[-5:])
```

### Validation checkpoints
- Run completes and writes `statepoint.*.h5`.
- `keff` is readable and entropy trend is not divergent.
- Troubleshooting advice maps to concrete settings/model changes.

## Primary documentation references
- `docs/source/index.rst`
- `docs/source/devguide/index.rst`
- `docs/source/devguide/contributing.rst`
- `docs/source/devguide/workflow.rst`
- `docs/source/devguide/docker.rst`
- `docs/source/license.rst`
- `docs/source/usersguide/troubleshoot.rst`
- `docs/source/methods/eigenvalue.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md`.
- If docs remain insufficient, inspect `references/source_map.md`.
- Cite exact documentation file paths in responses.

## Source entry points for unresolved issues
- `src/eigenvalue.cpp`
- `include/openmc/eigenvalue.h`
- `src/error.cpp`
- `include/openmc/error.h`
- `openmc/lib/error.py`
- `src/main.cpp`
- `src/simulation.cpp`
- `src/xml_interface.cpp`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" include openmc src openmc tests`).
