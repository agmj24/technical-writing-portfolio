# Markdown Cheatsheet

A short reference for the most common Markdown formats used in technical documentation.

---

## Headings

```markdown
# Heading 1
## Heading 2
### Heading 3
```

**Renders as:**

# Heading 1
## Heading 2
### Heading 3

**Rules**

- Use only one `#` (Heading 1) per page.
- Do not skip levels.
- Put a space after the `#`.
- Keep headings short. Do not end with a period.

---

## Emphasis

| Syntax            | Renders as    |
| ----------------- | ------------- |
| `**bold**`       | **bold**          |
| `*italic*`          | *italic*        |
| `***bold italic***` | ***bold italic***   |
| `~~strikethrough~~` | ~~strikethrough~~ |

Prefer asterisks (`*`) over underscores for consistency.

---

## Links

```markdown
[Descriptive text](https://example.com)
[Internal page](./other-page.md)
```

**Renders as:**
[Descriptive text](https://example.com)
[Internal page](./other-page.md)

**Rules**

- Use descriptive link text. Avoid “click here”.
- Prefer relative paths for files in the same repository.

---

## Lists

### Unordered

```markdown
- Item one
- Item two
- Item three
```

**Renders as:**

- Item one
- Item two
- Item three

### Ordered

```markdown
1. First step
2. Second step
3. Third step
```

**Renders as:**

1. First step
2. Second step
3. Third step

**Rules**

- Use `-` for unordered lists.
- Use numbered lists only when order matters.

---

## Code

### Inline code

```markdown
Use the `config.yaml` file.
```

**Renders as:** Use the `config.yaml` file.

### Code block

```markdown
```bash
npm install
```

**Renders as:**
```bash
npm install
```
Always specify the language after the opening backticks.

---
## Tables

```markdown
| Parameter | Type   | Description      |
|-----------|--------|------------------|
| name      | string | Name of the user |
| age       | number | Age of the user  |
```
**Renders as:**

| Parameter | Type   | Description      |
|-----------|--------|------------------|
| name      | string | Name of the user |
| age       | number | Age of the user  |

Keep tables simple. Use them only for structured data.
---

## Blockquotes / Notes

```markdown
> **Note:** Additional helpful information.

> **Important:** Something the reader must know.

> **Warning:** Risk of data loss or system issues.
```

**Renders as:**

> **Note:** Additional helpful information.

> **Important:** Something the reader must know.

> **Warning:** Risk of data loss or system issues.

---

## Images

```markdown
![Alt text](./images/diagram.png)
```

Always provide meaningful alt text.

---
