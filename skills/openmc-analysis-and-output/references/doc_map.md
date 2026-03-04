# openmc documentation map: Analysis and Output

Use this map after the topic skill's primary references.
All paths below are repository-relative and verified.

## Core docs
- `docs/source/usersguide/processing.rst` | Statepoint/summary analysis workflow.
- `docs/source/usersguide/plots.rst` | Plot generation and interpretation.
- `docs/source/io_formats/statepoint.rst` | Statepoint datasets and attributes.
- `docs/source/io_formats/summary.rst` | Summary file metadata layout.
- `docs/source/io_formats/track.rst` | Track output structure.
- `docs/source/io_formats/collision_track.rst` | Collision track file layout.
- `docs/source/io_formats/voxel.rst` | Voxel plot format.
- `docs/source/io_formats/tallies.rst` | Tally result representation.

## Validation references
- `tests/unit_tests/test_statepoint.py` | Python statepoint reader behavior.
- `tests/unit_tests/test_summary.py` | Summary reader behavior.
- `tests/unit_tests/test_tracks.py` | Track reader behavior.
- `tests/regression_tests/track_output/test.py` | End-to-end track output regression.
- `tests/regression_tests/plot/test.py` | Plot output regression.
