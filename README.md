# OpenSpec Schemas

Custom OpenSpec schemas packaged as copyable folders under `openspec/schemas/`.

## Agent Install (single line)

```bash
REPO_URL="<git-or-github-url>" SCHEMA="<schema-name>" && git clone --depth 1 "$REPO_URL" /tmp/openspec-schemas && mkdir -p openspec/schemas && cp -R "/tmp/openspec-schemas/openspec/schemas/$SCHEMA" "openspec/schemas/$SCHEMA" && rm -rf /tmp/openspec-schemas
```

## Minimalist

- Good fit: landing pages and simple apps with too many technical design decisions where the goal is to start building quickly.
- Not a good fit: complete apps with multiple layers, database design, and deeper architecture choices.

See `openspec/schemas/minimalist/README.md` for usage and activation.

## Event-Driven

- Good fit: event-centric and asynchronous systems that need a structured discovery-to-spec workflow before implementation planning.
- Not a good fit: very small low-risk work where a lightweight `specs -> tasks` flow is sufficient.

See `openspec/schemas/event-driven/README.md` for usage, activation, and stage gates.

## Agent Skills

- `openspec-schema-authoring-guide`: Deep guidance for understanding OpenSpec schema internals (with `spec-driven` as canonical) and drafting custom schemas in this repository.
  - Skill: `.codex/skills/openspec-schema-authoring-guide/SKILL.md`
  - Baseline comparison: `.codex/skills/openspec-schema-authoring-guide/references/schema-comparison.md`
