# openmc source map: Usersguide

Use this map when docs are insufficient and function-level behavior checks are required.

## Source roots
- `openmc`
- `include/openmc`
- `src`
- `tests`

## Fast navigation
- `rg -n "<symbol_or_keyword>" openmc include/openmc src tests`

## Function-level entry points
- `openmc/tallies.py` | User-facing tally/filter API behavior.
- `openmc/weight_windows.py` | User-side weight-window objects.
- `openmc/volume.py` | Stochastic volume API behavior.
- `openmc/deplete/r2s.py` | R2S-related user workflow helper behavior.
- `openmc/settings.py` | User-facing run controls.
- `src/tallies/tally.cpp` | Tally runtime behavior.
- `src/tallies/trigger.cpp` | Tally trigger behavior.
- `src/weight_windows.cpp` | Weight-window generation/IO behavior.
- `src/volume_calc.cpp` | Stochastic volume calculation behavior.
- `src/ifp.cpp` | Kinetics/IFP internals.

## Behavior/regression anchors
- `tests/regression_tests/weightwindows/test.py`
- `tests/regression_tests/trigger_tallies/test.py`
- `tests/regression_tests/volume_calc/test.py`
- `tests/unit_tests/test_tallies.py`
- `tests/unit_tests/test_volume.py`
