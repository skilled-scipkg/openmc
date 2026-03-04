# openmc source map: Io Formats

Use this map when docs are insufficient and function-level behavior checks are required.

## Source roots
- `openmc`
- `include/openmc`
- `src`
- `tests`

## Fast navigation
- `rg -n "<symbol_or_keyword>" openmc include/openmc src tests`

## Function-level entry points
- `openmc/statepoint.py` | Statepoint reader and dataset access.
- `openmc/summary.py` | Summary reader behavior.
- `openmc/particle_restart.py` | Particle restart file reader.
- `openmc/weight_windows.py` | Weight-window IO and conversions.
- `openmc/volume.py` | Stochastic volume result reading.
- `openmc/tracks.py` | Track output reader behavior.
- `src/state_point.cpp` | Statepoint writer implementation.
- `src/summary.cpp` | Summary writer implementation.
- `src/track_output.cpp` | Track file writing implementation.
- `src/collision_track.cpp` | Collision-track file writing behavior.
- `src/particle_restart.cpp` | Particle restart write/read path.
- `src/weight_windows.cpp` | Weight window serialization behavior.
- `src/volume_calc.cpp` | Volume file output behavior.
- `src/chain.cpp` | Depletion chain XML parsing.
- `include/openmc/state_point.h`
- `include/openmc/summary.h`
- `include/openmc/track_output.h`
- `include/openmc/collision_track.h`
- `include/openmc/particle_restart.h`
- `include/openmc/weight_windows.h`

## Behavior/regression anchors
- `tests/unit_tests/test_statepoint.py`
- `tests/unit_tests/test_summary.py`
- `tests/unit_tests/test_collision_track.py`
- `tests/unit_tests/test_volume.py`
- `tests/regression_tests/statepoint_restart/test.py`
- `tests/regression_tests/track_output/test.py`
- `tests/regression_tests/collision_track/test.py`
