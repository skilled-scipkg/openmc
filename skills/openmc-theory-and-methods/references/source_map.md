# openmc source map: Theory and Methods

Use this map when docs are insufficient and function-level behavior checks are required.

## Source roots
- `openmc`
- `include/openmc`
- `src`
- `tests`

## Fast navigation
- `rg -n "<symbol_or_keyword>" openmc include/openmc src tests`

## Function-level entry points
- `src/eigenvalue.cpp` | Eigenvalue source iteration and convergence behavior.
- `include/openmc/eigenvalue.h` | Eigenvalue solver interfaces.
- `src/physics.cpp` | Continuous-energy transport physics behavior.
- `src/physics_mg.cpp` | Multigroup transport physics behavior.
- `src/photon.cpp` | Photon interaction/sampling behavior.
- `src/ifp.cpp` | Kinetics/IFP implementation.
- `src/cmfd_solver.cpp` | CMFD acceleration implementation.
- `src/random_lcg.cpp` | Random number generator implementation.
- `src/random_dist.cpp` | Distribution sampling helpers.
- `src/tallies/tally_scoring.cpp` | Scoring estimators and accumulation logic.
- `src/tallies/filter_energy.cpp` | Energy-filter behavior used in theory docs.
- `src/random_ray/random_ray.cpp` | Random-ray method implementation.
- `src/random_ray/random_ray_simulation.cpp` | Random-ray simulation loop.
- `include/openmc/tallies/tally_scoring.h`
- `include/openmc/random_ray/random_ray.h`
- `include/openmc/random_ray/random_ray_simulation.h`

## Behavior/regression anchors
- `tests/regression_tests/entropy/test.py`
- `tests/regression_tests/cmfd_nofeed/test.py`
- `tests/regression_tests/random_ray_k_eff/test.py`
- `tests/regression_tests/random_ray_fixed_source_linear/test.py`
