# Contributing a package

Add one `<id>.mdx` file to the `packages/` directory. A pull request review
checks the package and its description before the entry becomes part of the
index.

## Entry format

Use lowercase words separated by hyphens for `id`. The ID is permanent and
becomes `/packages/<id>`. The filename and `id` must match.

Write the package metadata in YAML frontmatter. Write a longer description or
examples in the optional MDX body.

```mdx
---
id: example-widgets
name: Example Widgets
summary: Reusable OpenTUI widgets for forms and navigation.
kind: component
official: false
maintainers:
  - "@example"
source:
  url: https://github.com/example/opentui-widgets
surfaces:
  - name: TypeScript
    language: typescript
    import: example-widgets
distributions:
  - type: npm
    identifier: example-widgets
    install: bun add example-widgets
links:
  docs: https://github.com/example/opentui-widgets#readme
categories:
  - components
---

Example Widgets provides form controls that use OpenTUI Core renderables.
```

## Fields

- `id`, `name`, `summary`, `kind`, `official`, `source`, and `distributions` are required.
- `kind` is `native-library`, `library`, `renderer`, `component`, `application`, `tool`, `integration`, `examples`, or `documentation`.
- `official` must be `false` for community packages.
- `maintainers` lists one or more GitHub handles and is required for community packages.
- `source` has a repository `url` and an optional monorepo `directory`.
- `surfaces` lists APIs by display `name` and `language`. Each surface can include an `import` and a documentation `docs` URL.
- `distributions` lists one or more `source`, `npm`, `jsr`, or `github-release` distributions. A distribution can include an `identifier` and an `install` command.
- `links` can include `homepage`, `docs`, `issues`, and `changelog` URLs.
- `categories` can include `components`, `developer-tools`, `documentation`, `frameworks`, `input`, `integrations`, `rendering`, `testing`, and `utilities`.
- `status` is `active`, `archived`, or `deprecated`. It defaults to `active`.

Do not add versions, licenses, entrypoints, platform packages, platform targets, or Zig metadata. The website derives those fields for first-party packages. Package registries remain the source for current community versions.

## Checks

Continuous integration validates all community and first-party IDs together. It also checks that each npm package and source repository exists.

Run the same schema check from an OpenTUI checkout:

```sh
cd packages/web
bun scripts/validate-packages.ts ~/src/opentui-index/packages
```

## After the merge

The website rebuilds once each day and on each OpenTUI push. The package appears at
`opentui.com/packages/<id>` after the next build.
