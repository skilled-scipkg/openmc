---
name: openmc-theory-and-methods
description: This skill should be used when users ask about theory and methods in openmc; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmc: Theory and Methods

## High-Signal Playbook

### Route conditions
- Use this skill for estimator theory, physics method choices, random-ray/CMFD questions, and convergence interpretation.
- Route to `openmc-inputs-and-modeling` for concrete model definition changes.
- Route to `openmc-io-formats` when the question is file schema rather than method behavior.

### Triage questions
- Is this about eigenvalue source convergence, tally estimator choice, or physics model assumptions?
- Continuous-energy or multigroup mode?
- Is random-ray solver involved?
- Which observable matters most: `keff`, reaction-rate uncertainty, runtime/FOM?
- Are discrepancies statistical (noise) or deterministic (setup/algorithm mismatch)?

### Canonical workflow
1. Anchor in the corresponding method doc section (`eigenvalue`, `tallies`, neutron and photon physics, `random numbers`, `random ray`, `cmfd`).
2. Translate method assumptions into concrete settings/tally choices.
3. Run a small pilot and examine `keff`, entropy, and tally uncertainties.
4. Increase inactive/active batches and particles until convergence diagnostics stabilize.
5. Choose estimator/filter combinations consistent with method constraints.
6. Validate with repeated runs or independent checks before drawing conclusions.

### Minimal working example
```python
import openmc

model = openmc.examples.pwr_pin_cell()
model.settings.batches = 80
model.settings.inactive = 20
model.settings.particles = 5000
sp_path = model.run()

with openmc.StatePoint(sp_path) as sp:
    print('keff:', sp.keff)
    if sp.entropy is not None:
        print('entropy tail:', sp.entropy[-5:])
```

### Pitfalls and fixes
- Starting active tallies before source convergence: increase inactive batches and inspect entropy trend.
- Using track-length estimator where post-collision info is needed (e.g., outgoing-energy dependent quantities): use compatible estimator.
- Overinterpreting single noisy runs: repeat with different seeds and compare uncertainty overlap.
- Confusing faster runtime with better physics: compare figure of merit and uncertainty targets.
- Ignoring random-number reproducibility settings when debugging differences.

### Convergence and validation checks
- Entropy trend plateaus before active tallying (eigenvalue).
- `keff` batch trend is stable within uncertainty.
- Key tally relative errors meet target thresholds.
- Repeated runs produce statistically consistent central values.

## Primary documentation references
- `docs/source/methods/index.rst`
- `docs/source/methods/eigenvalue.rst`
- `docs/source/methods/tallies.rst`
- `docs/source/methods/neutron_physics.rst`
- `docs/source/methods/photon_physics.rst`
- `docs/source/methods/random_numbers.rst`
- `docs/source/methods/random_ray.rst`
- `docs/source/methods/cmfd.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Source entry points for unresolved issues
- `src/eigenvalue.cpp`
- `src/random_lcg.cpp`
- `src/physics.cpp`
- `src/physics_mg.cpp`
- `src/cmfd_solver.cpp`
- `src/tallies/tally_scoring.cpp`
- `src/random_ray/random_ray.cpp`
- `src/random_ray/random_ray_simulation.cpp`
- `include/openmc/eigenvalue.h`
- `include/openmc/random_ray/random_ray.h`
- `include/openmc/random_ray/random_ray_simulation.h`
- `include/openmc/tallies/tally_scoring.h`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" include openmc src`).
