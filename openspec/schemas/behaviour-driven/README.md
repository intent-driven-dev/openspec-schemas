# Behaviour-Driven OpenSpec Schema

`behaviour-driven` is a strict BDD workflow for changes whose implementation
must be driven by observable Gherkin acceptance tests.

The schema keeps OpenSpec delta specs mergeable while requiring downstream
projects to extract root-level `features/*.feature` files, test them with a
root-level `acceptance-tests/` Node project, and pass Cucumber.js before the
implementation gate is complete.

## Activate

Set this in `openspec/config.yaml`:

```yaml
schema: behaviour-driven
```

## Canonical Flow

Artifact order:

```text
proposal -> specs -> design -> tasks
```

Apply-time order:

```text
OpenSpec specs -> feature files -> failing Cucumber.js acceptance tests -> implementation -> passing Cucumber.js acceptance tests
```

## Strict BDD Gates

- Extract or update root `features/*.feature` files before writing acceptance
  test code.
- Run `gherkin-lint` from `acceptance-tests/` and require zero errors before
  the feature extraction commit.
- Use a root `acceptance-tests/` Node project with Cucumber.js, JavaScript lint
  scripts, ignored `node_modules/`, and HTML acceptance reports.
- Commit the failing acceptance setup before implementation starts; the failure
  must be the intended unimplemented application behaviour, not test plumbing.
- Run acceptance fixes as a bounded retry loop using the attempt limit recorded
  in `tasks.md`, defaulting to 3 when none is chosen.
- Commit after feature extraction, after failing acceptance setup, and after the
  passing implementation. Stop before crossing a gate if its commit cannot be
  made.
- Never weaken committed feature files or acceptance tests to make the
  implementation pass.

## Validate

```bash
openspec schema validate behaviour-driven
```
