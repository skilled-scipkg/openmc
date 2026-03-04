---
name: openmc-inputs-and-modeling
description: This skill should be used when users ask about inputs and modeling in openmc; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmc: Inputs and Modeling

## High-Signal Playbook

### Route conditions
- Use this skill for model construction (materials/geometry/settings/tallies), XML mapping, ID handling, and input validation behavior.
- Route to `openmc-build-and-install` if the problem is environment/build/test setup.
- Route to `openmc-api-and-scripting` for `openmc.lib` or coupling-specific API flows.

### Triage questions
- Is the user authoring Python API models or raw XML files?
- Is geometry CSG, DAGMC, lattice-heavy, or random-ray converted?
- Are IDs explicit or auto-assigned, and are duplicate-ID warnings appearing?
- What run mode and source definition are required (eigenvalue/fixed source)?
- Which tallies/filters/scores are required for outputs?
- Is the failure a validation error, lost particle error, or geometry overlap/misplacement?

### Canonical workflow
1. Start from `openmc.Model` or a known-good example (`openmc.examples.pwr_pin_cell`).
2. Define materials (`add_nuclide`/`add_element`, density, optional `add_s_alpha_beta`).
3. Define surfaces, regions, cells, universes/lattices, and boundary conditions.
4. Configure settings (batches/inactive/particles/source).
5. Define tallies with explicit filters/scores where needed.
6. Export to XML (`model.export_to_xml()`), then run.
7. If IDs/validation fail, inspect `IDManagerMixin` and `openmc.checkvalue` pathways.
8. If geometry/tally behavior is unclear, inspect C++ geometry/tally implementation files.

### Minimal working example
```python
import openmc

m_fuel = openmc.Material(name='fuel')
m_fuel.set_density('g/cm3', 10.0)
m_fuel.add_nuclide('U235', 1.0)

m_mod = openmc.Material(name='water')
m_mod.set_density('g/cm3', 1.0)
m_mod.add_nuclide('H1', 2.0)
m_mod.add_nuclide('O16', 1.0)
m_mod.add_s_alpha_beta('c_H_in_H2O')

r = openmc.ZCylinder(r=0.4)
left, right = openmc.XPlane(-0.63, boundary_type='reflective'), openmc.XPlane(0.63, boundary_type='reflective')
bot, top = openmc.YPlane(-0.63, boundary_type='reflective'), openmc.YPlane(0.63, boundary_type='reflective')

c1 = openmc.Cell(fill=m_fuel, region=-r)
c2 = openmc.Cell(fill=m_mod, region=+r & +left & -right & +bot & -top)
root = openmc.Universe(cells=[c1, c2])

model = openmc.Model(geometry=openmc.Geometry(root), materials=[m_fuel, m_mod])
model.settings.batches = 20
model.settings.inactive = 5
model.settings.particles = 1000
model.run()
```

### Pitfalls and fixes
- Duplicate ID warnings: call `openmc.reset_auto_ids()` in test setup or assign unique explicit IDs.
- Early type/value errors: check setters guarded by `openmc.checkvalue` (`check_type`, `check_value`, bounds checks).
- Missing nuclear data: set `OPENMC_CROSS_SECTIONS` or `materials.cross_sections`.
- Lost particles / cannot locate cell: check region Boolean logic, boundary conditions, and universe fills.
- Depletion volume errors: depletable materials must have volume defined.
- Overly complex first model: start from `openmc.examples` and modify incrementally.

### Convergence and validation checks
- Geometry exports cleanly and `model.run()` reaches statepoint output.
- `summary.h5` reconstructs geometry/materials without ID/path mismatches.
- Tallies are present with expected filters/scores in statepoint.
- For eigenvalue runs, `keff` and entropy stabilize after inactive batches.

## Primary documentation references
- `docs/source/usersguide/basics.rst`
- `docs/source/usersguide/materials.rst`
- `docs/source/usersguide/geometry.rst`
- `docs/source/usersguide/depletion.rst`
- `docs/source/io_formats/index.rst`
- `docs/source/io_formats/geometry.rst`
- `docs/source/methods/geometry.rst`
- `docs/source/devguide/tests.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Source entry points for unresolved issues
- `openmc/model/model.py`
- `openmc/mixin.py`
- `openmc/checkvalue.py`
- `openmc/material.py`
- `openmc/geometry.py`
- `openmc/tallies.py`
- `include/openmc/geometry.h`
- `include/openmc/cell.h`
- `include/openmc/universe.h`
- `include/openmc/lattice.h`
- `include/openmc/tallies/tally.h`
- `src/geometry.cpp`
- `src/cell.cpp`
- `src/universe.cpp`
- `src/lattice.cpp`
- `src/tallies/tally.cpp`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" include openmc src`).
