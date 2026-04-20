# Engineering Standards

## Python & Linting
- All Python code must pass `ruff check` without errors or warnings.
- Use `ruff format` for code formatting to maintain consistency.
- Pipelines and ML parameters must be externalized in YAML config files, not hardcoded in Python or generated within functions.
- Module-level constants and small helper dictionaries may be defined in code.

## Architecture & Modularity
- Prefer small, composable units that do specific tasks over large all-in-one methods.
- Each module should have a clear, single responsibility.
- Core logic should be isolated in its own scope and imported/used by higher-level wrappers.
- For modules that handle multiple tasks (e.g., data loading + preprocessing), use a top-level wrapper that coordinates composable pieces, typically instantiated via Hydra config.
- Avoid deep nesting and overly complex call chains. Keep functions and classes focused.

## Dependency Injection
- Prefer passing dependencies as constructor arguments or function parameters over inheritance.
- Avoid global state and singletons. Make dependencies explicit.
- No DI framework required — simple parameter passing is preferred.

## Configuration Management
- Pipelines and ML parameters must be externalized as YAML config files (or other standard formats used in the ML/DS community).
- Configuration should drive behavior, not be generated or hardcoded in Python.
- Use Hydra or similar tools for config composition and instantiation where applicable.

## Testing
- Write tests while writing code; write tests first when possible (TDD).
- Tests should cover core logic and critical paths.
- Follow the test pyramid: more unit tests (fast, isolated), fewer functional tests, fewer integration tests (slower, more realistic).
- New code without tests will be flagged in review.

## Imports & Dependencies
- Avoid circular imports.
- Keep cross-module dependencies clear and intentional.
- Import from public APIs when available, but imports from internals are acceptable if they're not being actively modified or are undergoing refactoring.

## Documentation
- Docstrings required for public functions, classes, and modules.
- Keep docstrings concise and focused on the "why" and "what," not implementation details.

## Git Workflow
- All new code must be developed on a dedicated feature branch before merging to trunk.
- When updating your branch with changes from trunk, prefer rebase over merge to keep history clean and linear.