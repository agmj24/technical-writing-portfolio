# DITA Topic Types in Practice

> This page shows how one subject, a design rule check, splits across DITA's three core topic types: concept, task, and reference. Each type does a different job. Mixing them into one long topic is the most common structural mistake I see in documentation that hasn't gone through a structured authoring pass.

## Why Split Content This Way

The short answer is reuse and maintenance. When "what is a design rule check," "how do I run one," and "here's the full flag list" all live on the same page, you can't pull the concept into a different manual without dragging the procedure and reference table along with it. Split into three topic types, and each piece assembles into different outputs, a full user guide, a quick start card, an in-tool help panel, without any rewriting.

Here's what that split looks like, in the DITA markup and in what the reader sees.

---

## Concept Topic: What Is a Design Rule Check?

A concept topic answers "what is this and why does it matter." It skips the steps and the full parameter list. It gives the reader just enough to orient before they act.

**DITA source (simplified):**

```xml
<concept id="drc-overview">
  <title>Understanding Design Rule Checks</title>
  <conbody>
    <p>A design rule check (DRC) verifies that a design meets the
       manufacturing constraints defined by a given process technology.
       Running a check early catches spacing, width, and connectivity
       issues before they become expensive to fix later in the flow.</p>
    <p>Checks are organized into rule sets. A rule set groups related
       constraints — for example, minimum spacing rules — so you can
       run a targeted check instead of validating every rule in the
       technology file every time.</p>
  </conbody>
</concept>
```

**What the reader sees:**

> A design rule check (DRC) verifies that a design meets the manufacturing constraints defined by a given process technology. Running a check early catches spacing, width, and connectivity issues before they become expensive to fix later in the flow.
>
> Checks are organized into rule sets. A rule set groups related constraints — for example, minimum spacing rules — so you can run a targeted check instead of validating every rule in the technology file every time.

Notice there's no "step 1, step 2" here, and no full parameter table. That content belongs in the other two topic types. Pulling it in here would make this topic hard to reuse cleanly wherever the concept alone is needed, like a glossary panel or a training deck.

---

## Task Topic: Running a Design Rule Check

A task topic is a numbered procedure: one goal, one sequence of steps, one result.

**DITA source (simplified):**

```xml
<task id="drc-run-check">
  <title>Running a Design Rule Check</title>
  <taskbody>
    <prereq>
      <p>Your design file must be saved and free of unresolved
         connectivity errors before running a check.</p>
    </prereq>
    <steps>
      <step><cmd>Open the design file in the verification tool.</cmd></step>
      <step><cmd>Select a rule set from the <uicontrol>Rules</uicontrol> menu.</cmd></step>
      <step><cmd>Click <uicontrol>Run Check</uicontrol>.</cmd></step>
    </steps>
    <result>
      <p>The tool displays a violation summary. Each violation links
         back to its location in the design for review.</p>
    </result>
  </taskbody>
</task>
```

**What the reader sees:**

> **Before you begin:** Your design file must be saved and free of unresolved connectivity errors before running a check.
>
> 1. Open the design file in the verification tool.
> 2. Select a rule set from the **Rules** menu.
> 3. Click **Run Check**.
>
> **Result:** The tool displays a violation summary. Each violation links back to its location in the design for review.

This topic assumes the reader already knows what a DRC is (that's the concept topic's job) and doesn't try to re-explain rule sets from scratch. It just tells them which menu to use.

---

## Reference Topic: Rule Set Parameters

A reference topic is lookup content: tables, parameter lists, syntax. Readers don't read it start to finish. They scan for the one row they need.

**DITA source (simplified):**

```xml
<reference id="drc-ruleset-params">
  <title>Rule Set Parameters</title>
  <refbody>
    <simpletable>
      <sthead>
        <stentry>Parameter</stentry>
        <stentry>Default</stentry>
        <stentry>Description</stentry>
      </sthead>
      <strow>
        <stentry>min_spacing</stentry>
        <stentry>0.15um</stentry>
        <stentry>Minimum allowed spacing between two features.</stentry>
      </strow>
      <strow>
        <stentry>min_width</stentry>
        <stentry>0.10um</stentry>
        <stentry>Minimum allowed width for a single feature.</stentry>
      </strow>
    </simpletable>
  </refbody>
</reference>
```

**What the reader sees:**

| Parameter | Default | Description |
|---|---|---|
| `min_spacing` | 0.15um | Minimum allowed spacing between two features. |
| `min_width` | 0.10um | Minimum allowed width for a single feature. |

---

## How These Three Come Back Together

None of these three topics stands alone forever. They assemble through a DITA map into whatever output needs them:

```xml
<map>
  <title>Design Verification Guide</title>
  <topicref href="drc-overview.dita"/>
  <topicref href="drc-run-check.dita"/>
  <topicref href="drc-ruleset-params.dita"/>
</map>
```
