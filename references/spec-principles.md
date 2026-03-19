# Specification Writing Principles

This reference document summarises core principles for writing executable specifications. It can be consulted by agents or humans for deeper understanding. The main SKILL.md file should link to this reference only when needed.

## Executability

A specification must enable an executor to perform the task without guessing the author’s intent or relying on hidden context. Use clear, direct language and avoid rhetorical flourishes.

## Zero‑Context Tolerance

Assume the executor has no access to prior conversations or documents. Define all required terms, inputs and assumptions within the specification.

## Explicit Boundaries

Define both what is in scope and what is not. Listing non‑goals prevents the executor from drifting into tasks the spec does not cover.

## Structured Information

Break the specification into predictable sections: purpose, scope, inputs, workflow, outputs, etc. This improves readability and makes it easier to identify missing pieces.

## Output Contracts

Define the deliverable(s) precisely. Specify required formats, sections, fields, citation requirements and how to distinguish facts from analysis or assumptions.

## Failure Handling

Anticipate three categories of failure: (a) external failures such as missing data, tool errors or conflicting sources; (b) judgement dilemmas where the executor faces a subjective decision the spec does not resolve; (c) structural failures where all steps complete but the overall result is incoherent. For each, provide guidance on whether to assume, pause for clarification, or halt execution.

## Evaluability

Include success criteria and a review checklist so that another party can judge whether the specification has been followed. A specification that cannot be evaluated is incomplete.

## Change Spec Principles

Modifying existing documents requires a different precision focus than creating new ones. In a new spec, execution precision depends primarily on the output contract — how clearly the deliverable is defined. In a change spec, execution precision depends primarily on anchor quality — how precisely each modification point is located in the target document.

Key differences from new-document specs: (a) Every modification needs an unambiguous location anchor, ideally with two reference points (before and after the target). (b) When modifications change the structure of content (list nesting, table columns, paragraph organisation), the complete final version should be provided rather than incremental patching instructions — the executor should not need to mentally reconstruct the result. (c) When multiple modifications have dependencies (later changes depend on earlier ones), the spec should be split into sequential phases, each independently verifiable. (d) Cross-file references must specify whether they use pre-modification or post-modification numbering.
