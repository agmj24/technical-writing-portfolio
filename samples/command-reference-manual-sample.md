# Verification Toolkit — Command Reference Manual (Sanitized Sample)

> The tool name, commands, and examples here are fictional. This is built to show how I organize and write a full command reference manual, not to document a real product.

## About This Manual

This covers the command-line interface for a made-up EDA verification tool I'm calling `vtk` for this sample. In a real manual, this section would also list the tool version it applies to and link back to the installation guide — I've left that out here since there's no real product behind it.

A quick note on how I actually build these: every command in a manual like this gets validated by running it against the real tool first. I don't write from a spec document alone, because specs and actual command behavior drift apart more often than you'd think, especially flags that were added late in a release. So the steps below are more of a template for structure than a claim that this exact syntax was tested — this is a fictional tool, after all.

## Document Conventions

| Convention | Meaning |
|---|---|
| `monospace` | A literal command, flag, or file name — type it exactly as shown |
| `<placeholder>` | A value you provide, like a file name |
| `[optional]` | Optional argument or flag |
| `{choice1 \| choice2}` | Pick one of the listed options |

## Global Options

These flags work with any `vtk` command:

| Flag | Description |
|---|---|
| `-v`, `--verbose` | Prints detailed progress output. Useful when a run is taking longer than expected and you want to see where it's stuck. |
| `-q`, `--quiet` | Suppresses everything but errors. |
| `--config <file>` | Points to a config file instead of the default `.vtkrc`. |

## Commands

### `vtk check`

Runs a rule-based structural check against a design file.

**Syntax**
```
vtk check -file <design_file> [-rules <ruleset>] [-severity <level>] [-report <output_file>]
```

**Parameters**

| Parameter | Required | Description |
|---|---|---|
| `-file <design_file>` | Yes | Path to the design file being checked. |
| `-rules <ruleset>` | No | Rule set to apply. Defaults to `standard`. |
| `-severity <level>` | No | Minimum severity to report — `info`, `warning`, or `error`. Defaults to `warning`. |
| `-report <output_file>` | No | Writes results to a file instead of printing to the terminal. |

**Example**
```
vtk check -file top_module.def -rules strict -severity error -report results.log
```

This runs a strict check on `top_module.def`, but only reports errors (warnings and info-level items are dropped), and saves everything to `results.log` instead of printing it.

**Related:** `vtk explain`, `vtk rules list`

---

### `vtk rules list`

Lists the rule sets currently available, along with a short description of what each one checks for.

**Syntax**
```
vtk rules list [-verbose]
```

Without `-verbose`, you just get rule set names. With it, you get a one-line description under each one — handy when you're not sure which rule set is the right fit for what you're checking.

**Example**
```
vtk rules list -verbose
```

**Related:** `vtk check`

---

### `vtk explain`

Looks up a specific violation code and prints an explanation, along with (where available) a suggested fix.

**Syntax**
```
vtk explain <violation_code>
```

**Example**
```
vtk explain DRC-0142
```

This is one people ask about a lot in support tickets — a check fails, they get a code, and they don't know what it actually means or where to start fixing it. `vtk explain` exists specifically to answer that without having to dig through the full rule set documentation.

**Related:** `vtk check`

---

## Exit Codes

| Code | Meaning |
|---|---|
| 0 | Command completed with no violations found |
| 1 | Command completed but found one or more violations |
| 2 | Command failed to run (bad input, missing file, etc.) |

Worth knowing if you're wiring `vtk check` into a CI pipeline and deciding what should count as a build failure — exit code 1 isn't necessarily a broken build, depending on your team's policy on warnings vs. errors.

## A Note on Why This Is Structured This Way

Each command gets its own short, self-contained topic — syntax, parameters, one example, related commands. That's deliberate: in the DITA source this would come from, each command is its own reusable topic, which means it can be pulled into the full manual, the quick-reference card, and the in-tool help without being rewritten three times. If I documented commands as one long flowing narrative instead, none of that reuse would be possible, and every place the command shows up would need separate edits when something changes.
