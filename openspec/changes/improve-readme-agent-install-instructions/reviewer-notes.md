## Summary

- Added an `AI Agent Install Instructions` section near the top of the root `README.md`.
- Made `openspec --version` with `openspec >= 1.0.0` the first prerequisite check before any schema copy step.
- Documented the early-exit path: stop, ask for install or upgrade, require `openspec init`, and do not continue when `openspec/config.yaml` is missing.
- Kept the surrounding guidance generic to all schemas while using `event-driven` only as the concrete example for copy, activation, and validation.
