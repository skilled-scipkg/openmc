# openmc source map: Releasenotes

Use this map when release-note wording is ambiguous and implementation-level validation is needed.

## Source roots
- `openmc`
- `include/openmc`
- `src`
- `tests`

## Fast navigation
- `rg -n "<symbol_or_keyword>" openmc include/openmc src tests CMakeLists.txt`

## Function-level entry points
- `include/openmc/version.h.in` | Compile-time version macros.
- `openmc/__init__.py` | Python package version exposure.
- `CMakeLists.txt` | Build-option defaults and version wiring.
- `openmc/settings.py` | User-visible setting API changes.
- `openmc/source.py` | Source API changes across releases.
- `openmc/statepoint.py` | Output-reading compatibility adjustments.
- `src/settings.cpp` | Runtime settings behavior changes.
- `src/source.cpp` | Source sampling/runtime behavior changes.
- `src/state_point.cpp` | Statepoint layout/version changes.
- `src/xml_interface.cpp` | Input parsing/deprecation behavior.

## Behavior/regression anchors
- `tests/unit_tests/test_settings.py`
- `tests/unit_tests/test_source.py`
- `tests/unit_tests/test_statepoint.py`
- `tests/regression_tests/model_xml/test.py`
