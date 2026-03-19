# Spec Review Checklist

Use this checklist when auditing a specification for zero‑context executability and overall quality.

## Quick Screen (start here)

Answer these five yes/no questions first. If any answer is "no", the spec is not ready — fix the failing item before proceeding to the detailed review.

1. Can the executor complete the task without reading any prior conversation?
2. Are all terms defined that a reasonable executor might interpret differently?
3. Are all required inputs listed, with handling instructions for missing ones?
4. Is every workflow step driven by what the spec says, not by unstated author intent?
5. Does the spec define what to do when something goes wrong, not just the happy path?

If all five pass, proceed to the detailed review below. For each item, mark whether the criterion is satisfied (✔️) or needs improvement (⚠️). Provide comments for any unmet criteria.

## Structure and Purpose

- **Clear Title** – Does the spec title accurately reflect its function?
- **Purpose Statement** – Does the spec clearly state why it exists and the desired outcome?
- **Executor / Audience Defined** – Is the intended executor specified with assumptions about their skills and tools?

## Scope and Boundaries

- **Scope Defined** – Are the tasks covered by the spec described concretely?
- **Non‑goals Listed** – Are adjacent tasks explicitly excluded to prevent scope creep?

## Clarity and Assumptions

- **Definitions Provided** – Are ambiguous terms defined?
- **Assumptions Explicit** – Are all inferred assumptions about context or missing data stated?
- **Zero‑Context Ready** – Could a competent executor follow the spec without any prior conversation? (Zero‑context hard test)

## Inputs and Preconditions

- **Required Inputs Listed** – Are all prerequisites, data, tools and permissions specified?
- **Missing Input Handling** – Does the spec describe what to do if an input is absent?

## Workflow

- **Structured Process** – Is there a clear sequence of stages with objectives and actions?
- **Minimum Standards** – Are quality criteria for each stage specified?
- **Adaptability** – Does the process allow for reasonable judgement where appropriate, without becoming vague?
- **Good/Bad Examples** – For stages involving subjective judgement, does the spec provide examples of good and bad output with explanations?

## Internal Consistency

- **No Contradictions** – Do non‑goals, workflow steps, assumptions and output contract tell a coherent story? Are there places where one section contradicts another?
- **Output Traceability** – Does the output contract only ask for things the workflow actually produces?

## Tool and Resource Policy

- **Tool Usage Defined** – Are tools enumerated with when/how to use them?
- **Evidence Priority** – Does the spec explain how to weigh evidence from different sources?

## Output Contract

- **Deliverables Specified** – Are the required outputs and their formats clearly defined?
- **Citation Guidance** – If external facts are involved, does the spec instruct on using up‑to‑date sources and citation formats?
- **Distinguish Fact vs Interpretation** – Does the spec require separation of factual reporting, analysis and assumptions?

## Success Criteria

- **Quality Bar Defined** – Are there clear standards for completeness, accuracy, clarity and relevance?

## Failure and Uncertainty Handling

- **Anticipated External Failures** – Does the spec anticipate common external breakdowns (e.g. missing data, conflicting sources, tool failures)?
- **Anticipated Judgement Dilemmas** – Does the spec anticipate situations where the executor must make a subjective decision and provide guidance on how to decide?
- **Anticipated Structural Failures** – Does the spec consider the possibility that all steps are completed but the overall result is incoherent or unusable?
- **Recovery Instructions** – For each failure mode, does the spec provide guidance on how to proceed?

## Escalation and Handoff

- **Escalation Triggers** – Are there conditions under which the executor should request clarification or assistance?
- **Handoff Rules** – Are there guidelines for handing the task to another specialist or returning partial results?

## Evaluability

- **Evaluation Checklist Included** – Does the spec include or link to a review checklist like this one?
- **Testability** – Can a reviewer verify whether the spec has been followed without guessing the author’s intent?


## Change Spec–Specific Checks (apply only when reviewing a Change Spec)

- **Anchor Precision** – Does every change item specify its location with enough precision to find the exact insertion/replacement point? Best practice: two-sided anchors (before X, after Y).
- **Anchor Uniqueness** – If the anchor text appears multiple times in the target document, does the spec disambiguate which occurrence is intended?
- **Operation Clarity** – Is each change explicitly labelled with a directional operation (INSERT BEFORE, INSERT AFTER, REPLACE, APPEND, or DELETE)?
- **Content Completeness** – For REPLACE operations, is the full replacement content provided (not just a diff description)?
- **Structural Replacement** – When a change modifies the structure of a list, table, or multi-line block (not just individual elements), does the spec provide the complete final version rather than incremental patching instructions?
- **Dependency Chain** – If the Change Spec is part of a series, are dependencies between specs clearly stated? Is the execution order explicit?
- **Temporary Numbering** – If temporary IDs are used, is the scheme documented and is there a designated phase for final renumbering?
- **Cross-Reference Integrity** – Do references to section numbers point to the correct (post-change) numbering? If the Change Spec is written before a renumbering phase, is this noted?
- **Format Awareness** – Does the spec warn about potential format differences in the target document (e.g., trailing whitespace, inconsistent list markers)?
- **Residue Check** – Does the evaluation checklist include a step to verify that no temporary markers, old numbering, or edit notes remain in the final output?

## Overall Assessment

Provide an overall verdict on whether the specification is ready for use. Suggest concrete improvements for any unmet criteria.
