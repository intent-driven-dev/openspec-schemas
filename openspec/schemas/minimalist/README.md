# Minimalist OpenSpec Schema

`minimalist` is for getting to build quickly with a direct `specs -> tasks` flow.

- Good fit: landing pages and simple apps with too many technical design decisions.
- Not a good fit: complete apps with multiple layers, database work, and broader architecture concerns.

## Install (copy/paste)

Use the root `README.md` single-line install command with:
- `SCHEMA="minimalist"`

## Activate

Set this in `openspec/config.yaml`:

```yaml
schema: minimalist
```

## Spec Format

When authoring `specs` artifacts in this schema:
- Write each requirement as a user story:
  `As a <role>, I want <capability>, so that <benefit>.`
- Write acceptance criteria using Gherkin structure:
  `Given ...`, `When ...`, `Then ...`

For more schemas, refer to https://github.com/intent-driven-dev/openspec-schemas.
