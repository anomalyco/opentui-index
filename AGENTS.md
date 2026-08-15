# Package entry guide

This guide is for agents and contributors who import packages into this index.
Each entry is one MDX file in `packages/` and becomes a page at
`opentui.com/packages/<id>`. [README.md](README.md) documents the file format
and the fields. This guide gives the content rules.
[packages/opentui-tex.mdx](packages/opentui-tex.mdx) is a live entry that
applies them.

## How the website shows each field

Write for the render target. The website shows each field in one place:

| Field                              | Where it appears                                     |
| ---------------------------------- | ---------------------------------------------------- |
| `name`                             | List-page link and the package-page title            |
| `summary`                          | List-page text and the HTML meta description         |
| `categories`                       | Bracket labels on the list page                      |
| MDX body                           | Main text on the package page                        |
| `surfaces`                         | "APIs" table in the sidebar: name, import, docs link |
| `distributions[].install`          | Copyable install block in the sidebar                |
| `distributions[].identifier` (npm) | The npm link on the package page                     |
| `links`                            | The links row on the package page                    |
| `maintainers`                      | "Maintained by" line on the package page             |
| Generated version, license, stars  | The facts line on the package page                   |
| `kind`, `surfaces[].language`      | Not shown. Validation only                           |

This table has two consequences. The sidebar already shows the install command and the
import paths, so the body must not repeat them. The list page shows only the
name, summary, `id`, and categories, and its text filter matches only those
fields, so the summary must identify the package by itself.

## Collect the facts first

Read the source repository README, the package manifest, and the registry
page. Then obey these rules:

- Use only facts from those sources. If a fact is not there, omit it.
- Do not guess a URL, an npm identifier, or a GitHub handle. Open each one.
- If the owner archived the source repository, set `status: archived`.

## Frontmatter rules

- Set `name` to the display name, not to the npm identifier.
- Write the summary as one noun phrase of at most 14 words, with a period at
  the end. Name what the package is and the domain words a user would search.
- Quote YAML strings that start with `@`.
- List one surface for each import path that users write in code.
- Make each `install` command complete, so that it works when a user copies it.
- Select one to three free-text `categories` that a user would search. Keep
  each category at 32 characters or fewer.
- Add a `links` URL only when you opened the target.
- Set `maintainers` to the GitHub handles of the people who maintain the
  package.

## Body rules

Shape:

- Write two to five short paragraphs. No headings, no bullet lists, no tables.
- Prefer at most two code fences.
- Keep each sentence under 25 words.

Content:

Write the body from the collected facts. Do not paste the source README.
Projects differ, so include the points that apply, roughly in this order:

1. Start with the package name and what the package does, in concrete terms.
   Expand the summary. Do not repeat it.
2. Show one small example when it makes the behavior clear, for example a
   code fence with source code or terminal output, but this is not required if
   it doesn't make sense for the package.
3. Give the facts a user needs before adoption, such as runtimes, platforms,
   native dependencies, or limits.
4. End with a link to the best documentation the project has.

Style:

- Use the active voice and simple tenses. State facts.
- Do not copy marketing text from the source README. Replace each claim with
  the fact behind it. Do not write: `seamless`, `powerful`, `robust`,
  `blazing`, `easy`, `simple`, `beautiful`, or `lightweight`.
- Do not add badge images.
- Link other index packages with a relative path, for example
  `/packages/opentui-core`.
- MDX parses JSX. Keep `<`, `>`, `{`, and `}` inside inline code or code
  fences.
- Use the writing-ste skill to make the text easy to read.

## Checklist

Before you open a pull request, make sure that:

1. The filename equals the frontmatter `id`.
2. The `id` does not collide with an entry in this repository or with a
   first-party package.
3. Each URL and npm identifier resolves.
4. The body does not contain an install command or an import list.
5. The entry does not contain versions, licenses, stars, or the other excluded
   fields from [README.md](README.md). Do not edit `packages/facts.json`.
6. The body contains no unquoted `<` or `{` characters.

## Validate

Continuous integration runs the schema and network checks on each pull
request. To run the schema check from an OpenTUI checkout:

```sh
cd packages/web
bun scripts/validate-packages.ts <path-to-this-repository>/packages
```
