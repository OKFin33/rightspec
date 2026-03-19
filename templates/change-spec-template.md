# Change Specification Template

Use this template when drafting a specification that modifies one or more existing documents. A Change Spec is not a new document — it is a set of instructions for an executor to apply changes to files that already exist.

Replace bracketed placeholders (`{{ like this }}`) with task-specific content. Remove sections that are clearly irrelevant, but be careful not to omit necessary context.

## Title

{{ Name the change spec by function, e.g., "Change Spec: Core Spec — §4 New Content" or "Change Spec: Blueprint v1.0 → v1.1". Include the target document name and version transition. }}

## Purpose

{{ Explain what changes this spec introduces and why. One to three sentences. }}

## Executor / Preconditions

{{ Specify who will execute the changes (e.g., "LLM Agent", "Human editor") and what capability level is assumed. If the executor is TBD at time of writing, state "TBD — spec must be executable by any competent LLM agent or human editor". }}

**Must read before executing**: {{ List the files the executor must have open — typically the target document(s) and any referenced files. }}

## Execution Order and Dependencies

{{ If this Change Spec is part of a series (e.g., A → B → C → D), state:
- Where this spec falls in the sequence
- Which prior specs must be completed first (hard dependencies)
- Which can be done in any order (no dependency)

If this is a standalone change spec, state "No dependencies — can be executed independently." }}

## Definitions

{{ Define terms used in the change instructions that the executor might not know or might interpret differently. Only include terms that actually appear in the change content. Do not pad with unused definitions.

Rule of thumb: if a term appears in the "Insert Content" of any change item and is not self-explanatory, define it here. }}

## Change List

{{ For each change, use the following structure. Number changes sequentially (e.g., BP-01, A-03, AR-04).

### {{ CHANGE-ID }}: {{ Brief description }}

**Location**: {{ Where in the target document this change applies. Be specific — section number, heading text, or both. }}

**Anchor**: {{ How to find the exact insertion/replacement point. Best practice: give TWO reference points (before-anchor and after-anchor) to eliminate ambiguity. If the target text appears multiple times in the document, specify which occurrence (e.g., "the instance within §2.7, not the one in §2.8"). }}

**Operation**: {{ One of: INSERT BEFORE (add content before anchor), INSERT AFTER (add content after anchor), REPLACE (swap old content for new), APPEND (add to end of existing section or list), DELETE (remove content). Always specify direction for insertions — do not use bare "INSERT". }}

**Content**: {{ The exact content to insert or replace with. Use fenced code blocks for content that must be preserved verbatim. When a modification changes the structure of a list, table, or multi-line block (e.g., adding nesting levels, changing column count, reorganizing items), provide the complete final version of that block rather than incremental patching instructions. If the modification only adds or changes individual elements within an unchanged structure, incremental instructions are acceptable. }}

**Rationale** *(optional)*: {{ One sentence explaining why this change is being made. Mark as "Design note" to distinguish from operational instructions. Useful for reviewers but not required for execution. }}

---

Repeat for each change. }}

## Temporary Numbering (if applicable)

{{ When inserting new sections into a numbered sequence, temporary IDs can prevent conflicts with existing numbering. If used:
- State the temporary numbering scheme (e.g., "§4.4a, §4.4b")
- State that a later phase will renumber to final IDs
- List the mapping from temporary to final numbers if known

If not applicable, omit this section. }}

## Output Contract

**Deliverable**: {{ Description of what the executor produces — typically "Modified version of [filename]". }}
**Format**: {{ File format and any style requirements (e.g., "Markdown, preserving original formatting conventions"). }}
**Requirements**: {{ Key constraints — e.g., "Do not modify content not addressed by this spec." }}

## Failure Handling

{{ Anticipate problems specific to document modification:

- **Anchor not found**: The specified text does not exist in the target document (possibly due to version mismatch or prior modifications). Recommended default: mark `[ANCHOR NOT FOUND: CHANGE-ID]`, skip the change, continue with remaining changes, report at end.
- **Format mismatch**: The target document uses different formatting than expected (e.g., different table column count, trailing whitespace, inconsistent heading levels). Recommended: adapt inserted content to match the target's actual format.
- **Numbering conflict**: A section number or item number already exists. Recommended: renumber the new content to avoid collision and note the deviation.
- **Cross-reference staleness**: A reference to another section points to a number that has changed. Recommended: update to the correct number if determinable; otherwise mark with `<!-- EDIT NOTE: verify reference -->`.
- **Execution environment artefacts**: Target documents may contain trailing whitespace, inconsistent blank lines, smart quotes, or other formatting artefacts that interfere with exact string matching. If the executor uses programmatic tools (e.g., str_replace, sed), whitespace should be normalized before matching.

Add any task-specific failure modes. }}

## Evaluation Checklist

{{ Provide a checklist specific to this change spec. Each change should have at least one verification item. Include:

- [ ] Each CHANGE-ID has been executed (or marked as ANCHOR NOT FOUND)
- [ ] New content formatting matches surrounding content
- [ ] No unintended modifications to content outside the change list
- [ ] {{ Task-specific checks }}
}}
