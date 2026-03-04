# openmc source map: Inputs and Modeling

Use this map when docs are insufficient and function-level behavior checks are required.

## Source roots
- `openmc`
- `include/openmc`
- `src`
- `tests`

## Fast navigation
- `rg -n "<symbol_or_keyword>" openmc include/openmc src tests`

## Function-level entry points
- `openmc/model/model.py` | Top-level model container and export/run methods.
- `openmc/mixin.py` | ID management behavior (`IDManagerMixin`).
- `openmc/checkvalue.py` | Input type/value validation helpers.
- `openmc/material.py` | Material API and XML serialization.
- `openmc/geometry.py` | Geometry API and XML serialization.
- `openmc/cell.py` | Cell region/fill behaviors.
- `openmc/universe.py` | Universe composition and traversal mapping.
- `openmc/lattice.py` | Rect/hex lattice construction and indexing.
- `openmc/settings.py` | Settings constraints affecting model validity.
- `openmc/tallies.py` | Tally/filter composition behavior.
- `include/openmc/geometry.h` | Core geometry interfaces.
- `include/openmc/cell.h` | Cell runtime interfaces.
- `include/openmc/universe.h` | Universe runtime interfaces.
- `include/openmc/lattice.h` | Lattice runtime interfaces.
- `include/openmc/tallies/tally.h` | Tally runtime interfaces.
- `src/geometry.cpp` | Geometry search and particle location behavior.
- `src/cell.cpp` | Cell-level transport interactions.
- `src/universe.cpp` | Universe-level traversal behavior.
- `src/lattice.cpp` | Lattice traversal/index mapping.
- `src/material.cpp` | Material loading and runtime properties.
- `src/tallies/tally.cpp` | Tally accumulation and management.

## Behavior/regression anchors
- `tests/unit_tests/test_material.py`
- `tests/unit_tests/test_geometry.py`
- `tests/unit_tests/test_lattice.py`
- `tests/unit_tests/test_tallies.py`
- `tests/regression_tests/model_xml/test.py`
