---
name: rightspec
description: |
  Create zero-context, executable specifications that can be reliably followed by humans or agents. Use this skill when the user asks to write, revise, evaluate or operationalize a specification, standard operating procedure (SOP), workflow contract, agent prompt spec, handoff document, capability definition, or document modification plan. Trigger phrases include "draft a spec", "write a specification", "create an SOP", "operationalize these guidelines", "make an execution plan", "write a handoff doc", "write a change spec", "spec out these modifications", or similar. Also trigger when the user wants to turn a high-level goal into structured instructions for someone else, wants to audit an existing spec for clarity, or wants to produce a structured modification plan for existing documents. This skill is intended for use across human-agent and agent-agent collaboration. Do NOT trigger for general document writing (READMEs, blog posts, reports, essays), project plans without execution detail, simple to-do lists, or meeting notes — those are not specifications.
---

# rightspec

You are responsible for producing high-quality execution specifications. A specification written with this skill must be **executable**, **stand-alone**, and **robust to missing context**. Any executor — human or agent — should be able to follow it without access to any prior conversation or hidden assumptions.

Specifications are the contract between intent and execution. A vague spec leads to inconsistent results and broken delegation chains.

## Purpose

This skill converts vague requests, goals or descriptions into concrete, actionable documents. Use it whenever a user or an upstream agent needs a specification that another executor (human or agent) can follow. The resulting spec enables consistent execution, delegation and evaluation.

## Assumptions

- **Zero-context tolerance**: The executor may have no access to the conversation history or author intent. Do not rely on hidden background knowledge.
- **No hallucination**: Do not fabricate facts, standards or assumptions. If essential information is missing, state the assumption explicitly and mark it as such.
- **Non-specific domain**: The skill is generic. It handles research, analysis, process design, software or non-software tasks. Do not hard-code domain specifics unless provided in the prompt.
- **Agent and human compatibility**: Specifications should use clear language, predictable structure and no ambiguous shorthand. Avoid idioms, colloquial expressions and metaphor — agents parse these poorly and humans interpret them inconsistently.

## Key Principles

1. **Executability over elegance** — Favour clarity and precision over literary style. Eliminate ambiguity even if the wording becomes longer. The executor should never have to guess the author's intent.
2. **Explicit assumptions** — Whenever the spec depends on context not provided, note the assumption and describe how to revisit it if the assumption proves false. This prevents silent failures downstream.
3. **Clear boundaries** — Define both what is in scope and what is explicitly not required. A strong spec includes non-goals to prevent scope drift, which is one of the most common failure modes in delegated work.
4. **Layer separation** — Separate purpose, scope, workflow, outputs and evaluation into distinct sections rather than blending them into narrative prose. This makes specs scannable and auditable.
5. **Output contracts** — Specify the structure, required fields and quality criteria of deliverables. Define formats (e.g. table, list, narrative), citation requirements and level of detail.
6. **Failure and escalation handling** — Anticipate missing data, contradictory inputs or tool failures. Also anticipate *judgement dilemmas* — situations where the executor must make a subjective decision but the spec does not tell them how to decide (e.g., two sections overlap in scope, the output feels too abstract to be useful, or a trade-off has no clear winner). Provide procedures for how the executor should proceed or stop when encountering uncertainty. Specs that only describe the happy path are incomplete.
7. **Evaluability** — Provide success criteria and an evaluation checklist so that a reviewer can judge whether the spec has been followed.
8. **Progressive disclosure** — Keep SKILL.md focused on essential guidance. Move detailed templates and rubrics to the `templates/` and `rubrics/` folders, linking them here. This minimizes token usage when the full detail is not needed.

## When to Trigger

Trigger this skill whenever the user requests:

- Drafting or refining a "spec", "specification", "SOP", "execution plan", "workflow contract", "agent prompt spec" or similar.
- Turning a high-level goal or idea into a structured set of instructions for someone else to follow.
- Evaluating or auditing an existing specification for clarity, completeness and executability.

Examples:

- "Write a handoff spec so Agent B can run the analysis without any context from Agent A."
- "Create an SOP for this data pipeline that any agent can follow."
- "Check if this handoff doc is clear and suggest improvements."

## Output Modes

Determine which mode to use based on the user's request. When ambiguous, default to Full Spec.

- **Full Spec** — The user wants a complete, deployable specification. Use the full template and all relevant sections. Trigger phrases: "write a spec", "draft a specification", "create an SOP", "make this executable".
- **Skeleton** — The user wants a reusable template or framework, not a filled-in document. Deliver the skeleton template with section headers and guidance prompts. Trigger phrases: "give me a framework", "create a template", "just the structure".
- **Audit** — The user has an existing spec and wants it evaluated. Use the review checklist to assess the document and return structured feedback with concrete improvement suggestions. Trigger phrases: "review this spec", "is this clear enough", "audit this document", "what's missing".
- **Change Spec** — The user wants to modify one or more existing documents and needs a specification that an executor can follow to apply the changes. Use the change spec template. This mode produces instructions for document modification, not a new document. Trigger phrases: "write a change spec", "spec out these changes", "make a modification plan", "write edit instructions for this doc". Also trigger when the user describes changes to an existing document and wants them formalized for someone else to execute.

## Standard Spec Structure

Unless instructed otherwise, organise the spec using the following sections. Omit or merge sections only if truly irrelevant.

1. **Title** — Name the spec by function, not marketing slogan. Keep it concise.
2. **Purpose** — One to three sentences defining why the spec exists and the desired outcome.
3. **Executor / Intended User** — Describe who is expected to follow the spec (e.g., generalist LLM agent, data analyst, human researcher) and any assumed capability level. If the executor is an agent, list available tools explicitly. If the executor is not yet known at the time of writing, mark as **TBD** and write the spec as if for a generalist executor with no assumed background — this produces the most portable spec. The author or a downstream coordinator can narrow the executor profile later without weakening the spec.
4. **Scope** — Define the tasks included. Be concrete about what the spec covers.
5. **Non-goals** — Define adjacent tasks or responsibilities that are explicitly excluded.
6. **Definitions and Assumptions** — Define terms that could be interpreted differently. List any assumptions about missing information. Provide default behaviours when information is absent.
7. **Inputs / Preconditions** — List what must be available before starting execution (e.g., specific data, access credentials, constraints, deadlines). If a required input may be missing, describe how the executor should obtain or estimate it.
8. **Workflow / Required Process** — Describe the standard sequence of activities. For each stage, specify the objective, required actions, intermediate outputs, and minimum quality standards. Avoid writing rigid step-by-step instructions when flexible reasoning is needed, but ensure that essential actions are not skipped. When a stage involves subjective judgement, provide a good example and a bad example with a brief explanation of why the bad example fails. Examples anchor the executor's calibration far more than abstract criteria do.
9. **Tool / Resource Policy** — If the executor must use tools (e.g., search engines, database connectors, calculators, code execution), specify when to use them, when not to use them, and how to handle tool results. Clarify the priority of evidence from different sources.
10. **Output Contract** — Define the required deliverable(s) in explicit terms. Specify mandatory sections, ordering, formats, citation requirements, level of detail and distinctions between facts, interpretations and assumptions. Link to a template if available. If the executor is an agent, use stable section headers (no creative renaming), prefer structured formats (tables, key-value pairs) over free prose, and specify thresholds numerically where possible (e.g., "at least 5 sources" rather than "a thorough selection").
11. **Quality Bar / Success Criteria** — State what makes the work acceptable. Set minimum standards for completeness, accuracy, clarity, relevance and adherence to the output contract.
12. **Failure Modes and Recovery** — Anticipate likely breakdowns in three categories: (a) *external failures* such as missing data, conflicting sources, tool failures or time constraints; (b) *judgement dilemmas* where the executor faces a subjective decision the spec does not resolve (e.g., two approaches both seem valid, an output is technically correct but feels wrong, or a trade-off has no clear winner); (c) *structural failures* where the executor completes all steps but the result is incoherent or unusable as a whole. For each, describe how the executor should proceed, whether to make an assumption, seek clarification or halt execution.
13. **Escalation / Handoff Rules** — Define when the executor should stop and ask for guidance, hand off to another specialist, or return a partial result. Specify triggers for raising uncertainty.
14. **Evaluation Checklist** — Provide or reference a checklist that reviewers can use to determine whether the spec has been properly followed. Link to the evaluation checklist in the `rubrics/` folder.

## Task Decomposition

When a spec involves many modifications or modifications with dependencies, split into sequential phases.

**When to split:**

- Total modification count exceeds ~10 discrete operations — the executor's context will be strained by combined volume.
- Modifications have dependency chains — a later change depends on an earlier change's result (e.g., renumbering must happen before cross-reference updates).
- Modifications involve different cognitive modes — "insert text at precise locations" and "restructure section organisation" benefit from separation.

**How to split:**

- Each phase is a self-contained spec with its own scope, output contract, failure handling, and evaluation checklist.
- Phases are numbered and execution order is explicit (e.g., "A → B → C → D").
- Hard dependencies are declared at the top of each phase.
- Each phase is completable and verifiable independently — the executor runs the evaluation checklist after each phase, not only at the end.

**Temporary identifiers:** When a phase adds new content that will be renumbered in a later phase, use clearly marked temporary identifiers (e.g., `§4.4a`, `§4.4b`) rather than guessing final numbers. A dedicated renumbering phase then replaces all temporary identifiers at once.

---

## Change Spec Conventions

A Change Spec modifies existing documents rather than creating from scratch. The following conventions apply in addition to the standard spec structure.

**Anchor points:** Every modification must specify where in the target document it applies. Use two-endpoint anchors whenever possible — identify both the element before and after the insertion point (e.g., "after the paragraph starting with X, before the heading Y"). When the same label appears multiple times in a document (e.g., "**Quality check**" in every section), always scope the anchor to its parent section.

**Operation types:** Each modification must be explicitly typed: INSERT BEFORE, INSERT AFTER, REPLACE, APPEND, or DELETE. Always specify direction for insertions — bare "INSERT" is ambiguous.

**Complete replacement over incremental patching:** When a modification changes the structure of a list, table, or multi-line block (adding nesting levels, changing column count, reorganizing items), provide the complete final version rather than incremental instructions. The executor should not need to mentally reconstruct the result. When the modification only adds or changes individual elements within an unchanged structure, incremental instructions are acceptable.

**Cross-file reference timing:** When a change spec modifies multiple files and one file's content references another file's section numbers, annotate whether the reference uses pre-modification or post-modification numbering. Default convention: always use the target file's final (post-modification) numbering and state this explicitly.

**Execution environment:** Original documents may contain trailing whitespace, inconsistent blank lines, smart quotes, or invisible Unicode characters. If the executor may use programmatic text-matching tools, include a warning in Failure Handling.

---

## Process for Writing a Spec

When a request triggers this skill, follow these steps:

1. **Clarify the task** — Scan the user's input for two things: who executes the spec, and what task they execute. If both are present, skip all clarification and proceed to step 2. If either is missing and cannot be reasonably inferred, ask — but ask at most two questions and never more. Do not stall the workflow with open-ended interviews.

   For all other missing information, apply this rule:

   **Ask** when the missing information would change the task type, the output format, or a hard constraint (regulatory scope, security requirements, target audience category). These cannot be safely guessed.

   **Assume and label** when the missing information is a secondary parameter (time window, geographic scope, level of detail, default tooling). State the assumption in the Definitions and Assumptions section so the executor can override it.

   **Executor TBD**: If the executor is not yet known at the time of writing, the spec must still be complete. Write it for the most constrained plausible executor (typically: a generalist LLM agent with no access to prior conversation). State "Executor: TBD" in the Executor section and note the assumption. A spec that only works when a specific executor reads it is fragile.
2. **Identify executor and audience** — Determine who reads the spec and their capability level. If the executor is an agent, favour structured formatting and explicit thresholds over natural-language guidance. If human, adjust technicality accordingly. If TBD, default to agent-compatible formatting.
3. **Determine output mode** — Based on the user's request, select: Full Spec, Skeleton, Audit, or Change Spec. If ambiguous, default to Full Spec. If the user is describing modifications to an existing document, use Change Spec.
4. **Assess scope and split if needed** — Estimate the total number of changes and check for dependency chains. If splitting is needed, follow the rules in §Task Decomposition above.
5. **Determine required sections** — Use the standard structure (for Full Spec) or the change spec template (for Change Spec) as a checklist. Omit sections only if irrelevant and omission creates no ambiguity.
6. **Surface assumptions** — Extract any inferred constraints, domain knowledge or context. Record them in the Definitions and Assumptions section.
7. **Draft the spec using templates** — Read the appropriate template in the `templates/` directory. Insert task-specific information, assumptions and workflow. Remove or tailor sections as needed.
8. **Internal consistency check (mid-draft gate)** — Before running the final zero-context gate, pause and check for internal contradictions. Specifically: do non-goals conflict with workflow steps? Do assumptions in one section contradict definitions in another? Does the output contract ask for things the workflow never produces? If the spec has many sections, read each section's key claim and check whether they tell a coherent story together. Fix contradictions before proceeding. This step catches structural failures that the zero-context gate (which checks each section individually) will miss.

   **Change Spec additional checks**: Verify anchor precision, operation typing, and cross-reference integrity per §Change Spec Conventions above.
9. **Validate executability (zero-context gate)** — Before finalising, answer each of these questions. If any answer is "no", revise the spec until all pass:
   - Can the executor complete the task without reading any prior conversation?
   - Are all terms defined that a reasonable executor might interpret differently?
   - Are all required inputs listed, with handling instructions for missing ones?
   - Is every workflow step driven by what the spec says, not by unstated author intent?
   - Does the spec define what to do when something goes wrong, not just the happy path?

   **Change Spec additional gate**: Can the executor find every anchor point without guessing? For each REPLACE operation, is the full replacement content provided?
10. **Execution environment note** — For Change Specs, add the execution environment warning described in §Change Spec Conventions to the Failure Handling section.
11. **Link resources** — If the spec requires complex templates, checklists or rubrics, link to the appropriate file in the skill package so the executor can find them.
12. **Return the spec** — Deliver the complete spec to the user. If the user asked for an audit instead of a full spec, use the evaluation checklist in `rubrics/spec-review-checklist.md` to assess the provided document and suggest improvements.

## Templates and Rubrics

- [Full Spec Template](templates/full-spec-template.md) — A comprehensive template including all recommended sections. Read this when the user wants a deployable specification.
- [Change Spec Template](templates/change-spec-template.md) — A template for specifications that modify existing documents. Read this when the user wants to formalize changes to an existing file for someone else to execute.
- [Spec Skeleton Template](templates/spec-skeleton-template.md) — A minimal skeleton listing section headers with guidance prompts. Read this when the user wants a reusable template.
- [Spec Review Checklist](rubrics/spec-review-checklist.md) — A checklist for evaluating a spec's zero-context executability, clarity and completeness. Includes a Change Spec–specific section. Read this in audit mode or as a self-check.
- [Good Spec Example](examples/good-spec-example.md) — An example of a well-structured spec for reference. Read this if you need a concrete model of what good looks like.
- [Good Change Spec Example](examples/good-change-spec-example.md) — An example of a well-structured Change Spec for reference. Read this when writing or reviewing a document modification spec.

## Citation Guidance

When writing a spec that requires external factual statements (e.g., regulatory requirements, definitions, statistics), use the search tool to gather current information rather than relying on stale training data. Cite sources using whatever citation format the host system supports. Preserve citations in the body of the spec to support consequential facts. Do not cite this skill file.

## Handling Uncertainty and Missing Information

- If essential inputs are unknown and cannot be safely assumed, specify them as required inputs in the spec. Do not fabricate values.
- If the task requires real-time or post-cutoff information, call the search tool to obtain up-to-date data before drafting the spec.
- If conflicting sources exist, note the conflict in the spec and describe how the executor should resolve it (e.g., by prioritising primary sources or requesting clarification).

## Maintaining the Skill

To extend or modify this skill, follow these guidelines:

- Keep SKILL.md under 500 lines and focused on core instructions.
- Move detailed documentation and reference material to the `references/` folder.
- Use kebab-case naming for the skill folder.
- Include a single SKILL.md as the entry point; avoid unnecessary README files.
- When adding new templates or rubrics, link them from the Templates and Rubrics section above with guidance on when to read them.
- This skill's own iterations can be formalized using Change Spec mode — the discipline applies to itself.
