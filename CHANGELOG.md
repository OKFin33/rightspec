# Changelog

## v3.0 (2026-06-12)

**Rebuilt around partition — minimize the LLM surface.**

rightspec is now a methodology, not a template library. Its core is a *judgment*: partition every
task into what is structurable (→ schema / typed contracts / tool policy) and the irreducible
natural-language judgment core (the only place prose belongs). New first-class behavior — **the
gate**: if a task can be fully structured, it is a function; the skill says "write code, don't use
an LLM," and producing *no spec* is a correct outcome.

### Changed
- New spine: `references/partition.md` (the heart) replaces the old principles-first framing.
- Four modes → two: cut the generic Full Spec; folded Skeleton into the templates and Audit into
  the review checklist. Spec mode (author an execution handoff) and Change Spec mode (modify a
  document) remain — they genuinely need different precision.
- Change Spec realigned to the partition view: modifications are a **structured operation list** (a
  typed patch); prose is reserved for the thin judgment residue. The evidence-backed conventions
  (two-endpoint anchors, directional operations, complete-replacement on structural change,
  phasing, temporary numbering, execution-environment warnings) are preserved.
- Scope sharpened to **agent-writes / agent-reads**; PRD / product-requirement use cases removed
  (that is a different lane).

### File structure
- `references/`: `partition.md`, `spec-mode.md`, `change-spec-mode.md`, `review-checklist.md`,
  `examples.md`, `decisions.md`.
- `templates/`: `spec.md`, `change-spec.md`.
- Removed: top-level `DECISIONS.md` (→ `references/decisions.md`), `rubrics/`
  (→ `references/review-checklist.md`), `references/spec-principles.md` (→ `references/partition.md`),
  the old `templates/*-template.md`, and `examples/` (→ `references/examples.md`).

---

## v2.0 (2026-03-19)

**New capability: Change Spec mode**

Added a fourth output mode for specifications that modify existing documents rather than creating
new ones. This was the primary capability gap — v1.0 only handled new-document specs.

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
