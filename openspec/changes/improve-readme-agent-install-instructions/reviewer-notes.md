## Summary

- Reworked the root `Install a Schema` section so it starts with raw-README agent prompt blocks, including an exact `event-driven` example, followed by manual self-install guidance.
- Kept the pasted user-facing prompt simple, with the detailed clone-and-copy behavior described inside the README itself.
- Kept `openspec --version` with `openspec >= 1.0.0` as the first prerequisite check inside the AI-agent flow.
- Documented the early-exit path: stop, ask for install or upgrade, require `openspec init`, and do not continue when `openspec/config.yaml` is missing.
- Kept the surrounding guidance generic to all schemas while using `event-driven` only as the concrete example for prompt, clone, copy, activation, and validation.
