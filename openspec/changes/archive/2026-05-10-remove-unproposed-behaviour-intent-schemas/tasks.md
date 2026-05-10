## 1. Remove Unproposed Schema Packages

- [x] 1.1 Delete `openspec/schemas/behaviour-driven/`.
- [x] 1.2 Delete `openspec/schemas/intent-driven/`.
- [x] 1.3 Remove the root README `Intent-Driven` catalog entry and ensure `behaviour-driven` is not advertised.

## 2. Verify Cleanup

- [x] 2.1 Confirm neither removed schema folder exists under `openspec/schemas/`.
- [x] 2.2 Confirm the repository root README lists only currently packaged schemas with canonical spec coverage.
- [x] 2.3 Run `openspec validate remove-unproposed-behaviour-intent-schemas --type change --strict`.
- [x] 2.4 Run `openspec list --json` and confirm only this active cleanup change remains before archive.
