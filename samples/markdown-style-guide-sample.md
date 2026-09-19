# Markdown Style Guide for Docs-as-Code (Sample)

> This is a style guide I put together as a sample of how I'd set writing conventions for a team moving to a docs-as-code workflow — Markdown files, version control, pull requests instead of a shared authoring tool. It's written the way I'd actually hand it to a team, not as a formal specification.

## Why This Exists

Once documentation lives in Git instead of a CMS or authoring tool, you lose some of the built-in consistency that tools like Oxygen or a CCMS enforce for you. Two people writing the same type of page can end up with different heading levels, different code block styles, different ways of formatting a note — and it shows once you publish. This guide is meant to close that gap before it becomes a cleanup job six months in.

## Headings

Use `#` for the page title only — one per file. Use `##` for major sections, `###` for subsections. Don't skip a level (going from `##` straight to `####`) just because a section feels like it needs to be smaller; restructure the content instead.

```markdown
# Page Title
## Major Section
### Subsection
```

Write headings as short phrases, not full sentences, and don't end them with a period. "Configuring the Retry Policy," not "How you can configure the retry policy."

## Code Blocks

Always specify a language after the triple backtick, even for plain output — it affects syntax highlighting and it's one extra keystroke.

````markdown
```bash
npm install
```
````

For inline code — file names, flag names, single commands — use single backticks: `` `config.yaml` ``. Don't bold text that's already in code formatting; it's redundant and looks cluttered.

## Notes and Warnings

We use three levels, and they're not interchangeable:

```markdown
> **Note:** Additional context that's helpful but not critical.

> **Important:** Something the reader needs to know to avoid a mistake.

> **Warning:** Risk of data loss, security issue, or breaking change.
```

Don't overuse "Important" and "Warning" — if every third paragraph has one, readers stop reading them. Save them for things that are actually consequential.

## Links

Use descriptive link text, not "click here" or a bare URL:

- Good: `See the [authentication guide](./auth.md) for setup steps.`
- Avoid: `Click [here](./auth.md) for more info.`

For links to other pages in the same repo, use relative paths (`./auth.md`), not absolute URLs — relative links keep working if the docs move to a different domain or hosting setup.

## Lists

Use `-` for unordered lists, not `*` or `+` — pick one and stay consistent across the whole repo so diffs in pull requests don't show noisy changes from someone's editor auto-converting bullet styles.

Use numbered lists only for sequences where order actually matters (steps in a procedure). If the order doesn't matter, it's a bulleted list, not a numbered one — numbering implies sequence even when you don't mean it to.

## Tables

Keep tables to what's actually tabular — parameters, options, comparison data. Don't force prose into a table just because it has two columns; a table with one sentence per cell is usually better as plain paragraphs.

## File and Folder Naming

- Lowercase, hyphen-separated: `getting-started.md`, not `GettingStarted.md` or `getting_started.md`.
- Name files for what they contain, not for where they sit in the nav — `configuring-retries.md`, not `page-12.md`. Nav structure changes; file names shouldn't have to.

## Pull Request Expectations

- One logical change per PR. A typo fix and a new section rewrite shouldn't be in the same PR — it makes review harder and makes it impossible to revert one without the other.
- PR descriptions should say what changed and why, not just "updated docs." Future you, six months from now trying to find when something changed, will thank you.
- Run the linter (see below) before requesting review — don't make a reviewer flag formatting issues that a tool could've caught.

## Linting

We use `markdownlint` with a shared config file (`.markdownlint.json`) checked into the repo root, so everyone's editor and CI pipeline enforce the same rules. If a rule genuinely doesn't fit a specific file, disable it inline for that one instance rather than turning it off repo-wide:

```markdown
<!-- markdownlint-disable MD013 -->
This line is intentionally long because it's a full CLI example that shouldn't wrap awkwardly.
<!-- markdownlint-enable MD013 -->
```

## The Short Version

If you only remember three things: be consistent with heading levels, don't skip specifying a language on code blocks, and don't reach for "Warning" unless something's actually at risk. Everything else in this guide exists to catch the smaller inconsistencies that pile up once more than one person is writing in the same repo.
