# Full Specification Template

Use this template when drafting a complete, deployable specification. Replace bracketed placeholders (`{{ like this }}`) with task‑specific content. Remove sections that are clearly irrelevant, but be careful not to omit necessary context.

## Title

{{ Describe the function of the specification concisely, e.g., “Market Research Execution Specification” or “Data Processing SOP”. }}

## Purpose

{{ Explain why this specification exists and the outcome it should enable in one to three sentences. }}

## Executor / Intended User

{{ Specify who will follow this spec (e.g., “LLM agent with web search access”, “Data Analyst”, “Software Engineer”). State whether the executor is a human, an agent, or either. Describe assumed skills, tool access or prerequisite knowledge. If the executor is an agent, list available tools explicitly — agents cannot infer tool access from context. If the executor is not yet known, state “TBD — written for generalist executor with no assumed background” and write accordingly. }}

## Scope

{{ Describe the tasks included within this specification. List the activities or deliverables that are in scope. Be concrete. }}

## Non‑goals

{{ List adjacent tasks, responsibilities or outcomes that are explicitly excluded from this specification. }}

## Definitions and Assumptions

{{ Define any terms that could be interpreted differently. List any assumptions you made (e.g., assumed date ranges, geographic scope, technologies used). Note how to revisit these assumptions if new information arises. }}

## Inputs / Preconditions

{{ Enumerate the required inputs, data, tools or permissions needed to begin execution. For each input, specify whether it is mandatory or optional and what to do if it is missing. }}

## Workflow / Required Process

{{ Describe the overall process, divided into stages. For each stage, specify:

1. **Objective** – What this stage accomplishes.
2. **Actions** – The steps or techniques to perform. Be as specific as necessary but avoid rigidity when adaptive reasoning is needed.
3. **Intermediate Outputs** – Artifacts or information produced.
4. **Quality Criteria** – Minimum standards for this stage.
5. **Good/Bad Examples** (when applicable) – If the stage involves subjective judgement, show one good example and one bad example. For the bad example, explain briefly what makes it bad and what failure it would cause downstream.

Use numbered lists or subheadings if it improves clarity. }}

## Tool / Resource Policy

{{ For each relevant tool or resource, define: when to use it, when not to use it, and how to treat its results. For example:

* **Web search** – Use to gather current facts; do not rely solely on snippets; cross‑check across sources.
* **Database connector** – Use for internal data queries; respect access permissions.
* **Python execution** – Use for calculations or data transformations; include code in the deliverable when needed. }}

## Output Contract

{{ Describe the deliverable(s) required. Specify:

* Section structure and order.
* Formats (e.g., Markdown, PDF, spreadsheet).
* Required fields and level of detail.
* Citation requirements, including citation format.
* How to distinguish facts from interpretation and assumptions.

If the executor is an agent: use stable, predictable section headers (no creative renaming between runs). Prefer structured formats (tables, key-value pairs, JSON) over free prose where possible. Specify thresholds numerically (e.g., "at least 5 sources" not "a thorough selection").

Provide a link to any supporting template or file needed to produce the output. }}

## Quality Bar / Success Criteria

{{ Define what makes the work acceptable. Mention completeness, accuracy, clarity, relevance to the purpose, adherence to the output contract, and proper handling of assumptions and uncertainty. }}

## Failure Modes and Recovery

{{ Anticipate breakdowns in three categories:

**External failures** — missing data, conflicting sources, tool failures, time constraints.
**Judgement dilemmas** — the executor faces a subjective decision the spec does not resolve (e.g., two valid approaches, output feels wrong despite being technically correct, a trade-off with no clear winner).
**Structural failures** — all steps are completed but the overall result is incoherent or unusable.

For each, describe:

* How the executor should proceed (e.g., make a provisional assumption, request clarification, select the most reliable source).
* When to stop execution and report uncertainty.

Encourage transparent reporting of unresolved issues. }}

## Escalation / Handoff Rules

{{ Specify when the executor should:

* Ask for additional information or clarification.
* Hand off the task to a different specialist.
* Return a partial result with documented uncertainties.

Define triggers for escalation such as unresolved blocking assumptions or ethical concerns. }}

## Evaluation Checklist

Refer to [Spec Review Checklist](../rubrics/spec-review-checklist.md) and include a summary here if necessary.
