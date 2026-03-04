---
name: openmc-releasenotes
description: This skill should be used when users ask about releasenotes in openmc; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmc: Releasenotes

## High-Signal Playbook

### Route conditions
- Use this skill for upgrade impact, compatibility/deprecation checks, and mapping behavior changes by version.
- Route to feature-specific skills (`openmc-api-and-scripting`, `openmc-inputs-and-modeling`, `openmc-build-and-install`) after identifying affected areas.

### Triage questions
- What version is the user on, and what version are they targeting?
- Is the concern API compatibility, build behavior, IO format changes, or runtime behavior?
- Are there deprecated args/attributes in their scripts?
- Do they need a migration diff or just a feature summary?

### Canonical workflow
1. Identify current/runtime version (`openmc.__version__` and/or `openmc --version`).
2. Read `docs/source/releasenotes/index.rst` and all intervening versions between source and target.
3. Extract compatibility/deprecation notes first, then new features and bug fixes.
4. Map each relevant note to user code via targeted search.
5. Confirm behavior in source when release-note wording is ambiguous.
6. Validate migration by running unit/regression tests for affected workflows.

### Minimal working example
```bash
python - <<'PY'
import openmc
print(openmc.__version__)
PY

# Example migration checks from 0.15.0 notes
rg -n "domains=|only_fissionable|max_splits" openmc tests
```

### Pitfalls and fixes
- Skipping intermediate releases: always review each version hop, not only the target release.
- Missing deprecations in old scripts: search for renamed/removed arguments and attributes.
- Assuming release notes are exhaustive: verify edge cases against source and tests.
- Confusing deprecation warnings with hard removals: check exact version note text.

### Convergence and validation checks
- No deprecated-API warnings in representative runs.
- Affected unit/regression tests pass after migration.
- File readers/writers still match expected format versions for produced outputs.

## Primary documentation references
- `docs/source/releasenotes/index.rst`
- `docs/source/releasenotes/0.15.3.rst`
- `docs/source/releasenotes/0.15.2.rst`
- `docs/source/releasenotes/0.15.1.rst`
- `docs/source/releasenotes/0.15.0.rst`
- `docs/source/releasenotes/0.14.0.rst`
- `docs/source/releasenotes/0.13.3.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Source entry points for unresolved issues
- `include/openmc/version.h.in`
- `openmc/__init__.py`
- `openmc/source.py`
- `openmc/settings.py`
- `openmc/stats/multivariate.py`
- `src/source.cpp`
- `src/settings.cpp`
- `src/finalize.cpp`
- `CMakeLists.txt`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" include openmc src openmc`).
