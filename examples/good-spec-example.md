# Example Specification – Agent‑to‑Agent Data Handoff

This example demonstrates a zero‑context executable specification for an agent‑to‑agent workflow. Agent A (data collector) hands off to Agent B (analyst). Agent B must be able to execute this spec without any knowledge of Agent A's prior conversation or internal state.

## Title

User Research Data → Competitive Analysis Handoff Specification

## Purpose

Enable Agent B to receive structured user research data from Agent A and produce a competitive analysis report, without access to Agent A's conversation history or the original human request.

## Executor / Intended User

**Agent B** — a generalist LLM agent with access to web search and document creation tools. No assumed knowledge of the research domain or the upstream data collection process.

## Scope

- Receive a structured data package from Agent A
- Validate the data package against the input contract below
- Produce a competitive analysis report following the output contract below

## Non‑goals

- Agent B does not collect additional primary data (no surveys, no interviews)
- Agent B does not redesign Agent A's data format
- Agent B does not contact the end user for clarification — if inputs are insufficient, it returns a partial result with a gap report

## Definitions and Assumptions

- **Data package**: A JSON object conforming to the input schema below. Assumed to be delivered via the orchestrator's message payload.
- **Competitor**: Any company offering a product in the same category as the subject company. Agent B identifies competitors through web search, not from the data package.
- **Analysis period**: Defaults to the past 12 months unless the data package specifies otherwise.
- **Assumption**: Agent B has unrestricted web search access. If search is unavailable, Agent B halts and returns an error status rather than fabricating data.

## Inputs / Preconditions

**Mandatory input — Data package from Agent A:**

```json
{
  "subject_company": "string — company name",
  "industry": "string — industry or category",
  "user_research_summary": "string — plain text summary of findings",
  "key_themes": ["string array — main themes identified"],
  "sample_size": "integer — number of users researched",
  "data_quality_flag": "green | yellow | red"
}
```

**Handling missing fields:**
- If `subject_company` or `industry` is missing: halt, return error — these cannot be inferred.
- If `key_themes` is empty: proceed but note in the report that analysis is based solely on the summary.
- If `data_quality_flag` is missing: assume `yellow` and note the assumption.
- If `sample_size` is missing: assume unknown and flag in the report's limitations section.

## Workflow / Required Process

### Stage 1: Input Validation

**Objective:** Confirm the data package is usable.

**Actions:** Parse the JSON payload. Check all mandatory fields exist. Check `data_quality_flag` value.

**Intermediate output:** Validation status (pass / fail with reasons).

**Quality criteria:** If validation fails on `subject_company` or `industry`, do not proceed.

### Stage 2: Competitor Identification

**Objective:** Identify 5–8 competitors in the same industry.

**Actions:** Use web search with queries like `"{industry}" competitors 2025 2026` and `"{subject_company}" competitors`. Cross‑reference at least two sources per competitor.

**Intermediate output:** Competitor list with name, one‑line description, and source URL.

**Quality criteria:** Minimum 5 competitors. Each must appear in at least 2 independent sources.

**Good example:** "Competitor: Notion — collaborative workspace tool. Sources: G2 market report (URL), TechCrunch funding coverage (URL)."

**Bad example:** "Competitor: Notion — popular app." — No sources cited, description too vague to distinguish from adjacent products. This would cause downstream analysis to lack grounding.

### Stage 3: Comparative Analysis

**Objective:** Analyse each competitor against the themes from the user research data.

**Actions:** For each key theme, assess how each competitor addresses it. Use web search for current product information. Distinguish between factual findings (what the competitor offers) and interpretive claims (how well it addresses the theme).

**Intermediate output:** Theme × competitor matrix.

**Quality criteria:** Every cell in the matrix must contain either a factual finding with a source or an explicit "no data found" marker. No empty cells.

### Stage 4: Report Generation

**Objective:** Produce the final deliverable per the output contract.

**Actions:** Assemble the report. Run the internal consistency check: does every section reference only data that was actually collected? Does the limitations section accurately reflect any gaps?

**Intermediate output:** Final report.

**Quality criteria:** Passes the zero‑context gate (below).

## Tool / Resource Policy

- **Web search**: Use for competitor identification and product information. Do not rely on snippets alone — fetch and verify from the source page. If a source is paywalled, note it and use the available snippet with reduced confidence.
- **Document creation**: Use for the final report output.
- **Code execution**: Not required for this spec.

## Output Contract

Produce a Markdown report with these exact section headers in this order:

1. **Title and Date**
2. **Executive Summary** — 3–5 sentences.
3. **Input Data Summary** — Restate key facts from Agent A's data package. Include `data_quality_flag` and `sample_size`.
4. **Competitor Profiles** — One subsection per competitor. Each must include: company name, one‑line description, key product features, and relevance to user research themes. All factual claims cited.
5. **Theme Analysis** — The theme × competitor matrix, plus a narrative synthesis per theme.
6. **Limitations** — Data gaps, assumptions made, search failures encountered.
7. **Appendix: Sources** — Full list of URLs referenced.

Distinguish facts from interpretation: factual claims must have a citation; interpretive claims must be prefixed with "Assessment:".

## Quality Bar / Success Criteria

- Minimum 5 competitors with at least 2 sources each
- Every factual claim in Competitor Profiles has a citation
- Theme × competitor matrix has zero empty cells (either data or explicit "no data found")
- Limitations section is non‑empty (there are always limitations)
- Report can be understood by a reader who has never seen the user research data, Agent A's conversation, or this spec's author

## Failure Modes and Recovery

**External failures:**
- Web search unavailable → halt, return error status with message "search tool required but unavailable"
- Data package JSON is malformed → halt, return error with parse failure details
- Fewer than 5 competitors found → proceed with what is available, note in Limitations

**Judgement dilemmas:**
- Two sources give conflicting information about a competitor's product → report both, note the conflict, do not pick a winner
- A key theme from the user research is too vague to search for → note it in Limitations, skip that row in the matrix rather than guessing

**Structural failures:**
- Report is complete but the Theme Analysis contradicts the Competitor Profiles → re‑read both sections, identify the inconsistency, fix or flag it before delivering
- Report is technically correct but reads as a list of facts with no synthesis → add narrative connectors in Theme Analysis, ensure Executive Summary tells a coherent story

## Escalation / Handoff Rules

- If `subject_company` or `industry` is missing from input: return immediately with error, do not attempt to infer
- If `data_quality_flag` is `red`: produce the report but prepend a warning that upstream data quality is low and conclusions should be treated as provisional
- If more than 3 key themes have no searchable data: return a partial result with a gap report instead of a full analysis

## Evaluation Checklist

Refer to [Spec Review Checklist](../rubrics/spec-review-checklist.md). Key checks for this spec:

- [ ] Can Agent B execute this without any context from Agent A's conversation?
- [ ] Are all input fields defined with handling for missing values?
- [ ] Does every workflow stage have measurable quality criteria?
- [ ] Are failure modes covered for all three categories (external, judgement, structural)?
- [ ] Does the output contract specify exact section headers and ordering?
