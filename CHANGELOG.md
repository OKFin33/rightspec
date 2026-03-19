# Changelog

## v2.0 (2026-03-19)

**New capability: Change Spec mode**

Added a fourth output mode for specifications that modify existing documents rather than creating new ones. This was the primary capability gap — v1.0 only handled new-document specs.

### SKILL.md
- Added Change Spec to Output Modes
- Added `## Task Decomposition` section (when and how to split large change sets into phases)
- Added `## Change Spec Conventions` section (anchor points, operation types, complete replacement rule, cross-file reference timing, execution environment warnings)
- Process steps reference these sections (scheme 3: inline core judgment, detail in independent sections)
- Added Executor TBD handling (step 1 + step 2)
- Added execution environment note (step 10)
- Updated YAML description with Change Spec trigger phrases
- Added meta-recursion note in Maintaining the Skill
- Standard Spec Structure §3 (Executor) now includes TBD guidance

### New files
- `templates/change-spec-template.md` — Complete template for document modification specs
- `examples/good-change-spec-example.md` — Minimal worked example (2 changes, domain-neutral)

### Modified files
- `templates/full-spec-template.md` — Added TBD option to Executor field
- `rubrics/spec-review-checklist.md` — Added 10-item Change Spec–Specific Checks section
- `references/spec-principles.md` — Added Change Spec Principles paragraph

### Unchanged files
- `templates/spec-skeleton-template.md`
- `examples/good-spec-example.md`

---

## v1.0 (2026-03-18)

Initial release. Four output modes planned, three implemented: Full Spec, Skeleton, Audit.
