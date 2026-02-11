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
