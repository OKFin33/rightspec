# Example Change Specification – Document Modification

This example demonstrates a zero-context executable Change Spec. It modifies an existing design document by inserting new sections and updating cross-references. An executor agent should be able to apply all changes without access to any prior conversation.

## Title

Change Spec: Design Guidelines v1.0 → v1.1 — Add Governance Section and Update Mapping

## Purpose

Add a document governance section (§3.4.7) and expand the file mapping list (§3.6) in the Design Guidelines to reflect the expanded file set introduced in the companion Implementation Spec v2.0.

## Executor / Preconditions

**Executor**: LLM Agent or human editor.
**Must read before executing**: Design_Guidelines.md (the target file).

## Execution Order and Dependencies

No hard dependencies. The companion Implementation Spec should ideally be updated first (so cross-references can be verified), but this Change Spec is self-contained and can be executed independently.

## Definitions

- **Governance file**: A document that records update rules for all other documents in the system. Each core document has a short "update anchor" at its end pointing to the governance file.
- **Update anchor**: A 3–5 line paragraph at the end of a document that points to the governance file's relevant section. Acts as a reminder when the document is being modified.

## Change List

### DG-01: Insert §3.4.7

**Location**: §3.4 "Layer Interactions", after §3.4.6.

**Anchor**: Find `#### 3.4.6 System roles can override runtime logic but must not absorb identity`. The new section inserts after this section's content, before the `---` separator that precedes §3.5.

**Operation**: INSERT AFTER

**Content**:

```markdown
#### 3.4.7 Document governance constrains all layers' self-modification

When an agent modifies its own documents at runtime, it must follow the update rules in GOVERNANCE.md. This prevents the experience layer's daily changes from overwriting constitutional content without validation. The cascade direction is always: constitutional layer constrains runtime layer, runtime layer calls experience layer, experience layer may update the constitutional layer only at a high threshold. GOVERNANCE.md itself belongs to the runtime layer; structural changes to it (such as modifying the constitutional layer's update threshold) require user confirmation.
```

---

### DG-02: Replace §3.6 file mapping list

**Location**: §3.6 "How layers map to files".

**Anchor**: Find the bullet list that starts with `- **Constitutional layer**` and ends with `- **System role layer**`. Replace the entire list (5 items).

**Operation**: REPLACE

**Old content** (5-item list starting with "Constitutional layer" and ending with "System role layer").

**New content**:

```markdown
- **Constitutional layer** maps to `SOUL.md`
- **Runtime layer** maps to multiple files:
  - `AGENTS.md`: launcher — identity summary, startup behavior, activation paths
  - `METHODS.md`: method discipline — analysis methods, quality standards
  - `KNOWLEDGE.md + learning/`: knowledge anchors — index of key concepts and sources
  - `TOOLS.md + skill/`: tool configuration
  - `GOVERNANCE.md`: document update governance — update rules and cascade rules (not injected at startup; read on demand)
- **Experience layer** maps to `MEMORY.md + memory/`
- **Shared environment layer** maps to:
  - `USER.md`: shared user context
  - `ORG_RULES.md`: organization-level shared rules
- **System role layer** maps to runtime supplements or standalone role descriptions
```

## Output Contract

**Deliverable**: Modified Design_Guidelines.md file.
**Format**: Markdown, preserving original heading levels and formatting conventions.
**Requirements**: Do not modify any content not addressed by this spec. Inserted content must match the heading level and list style of surrounding sections.

## Failure Handling

- **Anchor not found**: Mark `[ANCHOR NOT FOUND: DG-XX]`, skip the change, continue with remaining changes, list skipped items at end of file.
- **Format mismatch**: If the original list uses different bullet style (e.g., `*` instead of `-`), adapt the new content to match.
- **Internal contradiction**: If inserted content contradicts an existing paragraph not covered by this spec, add `<!-- EDIT NOTE: potential tension with §X.X, needs review -->` without modifying the existing paragraph.

## Evaluation Checklist

- [ ] DG-01: §3.4.7 exists with correct heading level (####)
- [ ] DG-02: §3.6 mapping list has been replaced (old 5-item list gone, new expanded list present)
- [ ] §3.4 sub-section numbering is continuous (3.4.1 through 3.4.7)
- [ ] No content outside §3.4.7 and §3.6 has been modified
- [ ] File reads coherently from start to finish with no formatting breaks
