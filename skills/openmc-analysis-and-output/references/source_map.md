# openmc source map: Analysis and Output

Use this map when docs are insufficient and function-level behavior checks are required.

## Source roots
- `openmc`
- `include/openmc`
- `src`
- `tests`

## Fast navigation
- `rg -n "<symbol_or_keyword>" openmc include/openmc src tests`

## Function-level entry points
- `openmc/statepoint.py` | Statepoint reader properties and tally accessors.
- `openmc/summary.py` | Geometry/material reconstruction from summary files.
- `openmc/tallies.py` | Tally data structures, slicing, arithmetic helpers.
- `openmc/tracks.py` | Track file parsing and iteration behavior.
- `openmc/plots.py` | Plot object definitions for XML export.
- `openmc/plotter.py` | Plotting helper behavior from Python side.
- `src/state_point.cpp` | Statepoint writing internals.
- `src/summary.cpp` | Summary-file writing internals.
- `src/track_output.cpp` | Track output generation.
- `src/output.cpp` | Runtime/output logging control.
- `src/plot.cpp` | Plot generation backend.

## Behavior/regression anchors
- `tests/unit_tests/test_statepoint.py`
- `tests/unit_tests/test_summary.py`
- `tests/unit_tests/test_tracks.py`
- `tests/regression_tests/track_output/test.py`
- `tests/regression_tests/plot/test.py`
