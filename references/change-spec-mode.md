# Change Spec mode — a typed patch

A Change Spec modifies an existing document. On the partition spectrum it sits far toward the
structured end: its core — *where*, *what operation*, *what content* — is almost a diff. So the
Catalog-A part dominates: emit the modifications as a **structured operation list**, machine-
applicable. Prose is reserved for the thin Catalog-B residue.

These conventions are evidence-backed — seven change specs against four real documents, 35+
modifications (see `decisions.md`). Anchor quality was the single biggest factor in execution
speed and correctness.

## The operation list (the structured core)

```yaml
- id: BP-01                                   # sequential, stable
  location: "§3.4 Layer Interactions, after §3.4.6"   # human-readable
  anchor:                                     # two endpoints — eliminates ambiguity
    after: "<exact text immediately before the edit point>"
    before: "<exact text immediately after>"
  op: INSERT AFTER | INSERT BEFORE | REPLACE | APPEND | DELETE   # direction ALWAYS explicit
  content: |
    <exact final content>
```

**Conventions (each earned from real execution friction):**

- **Two-endpoint anchors.** Locate every edit by the text *before* and *after* it. Single-point
  anchors force the executor to guess direction. If the anchor text appears more than once,
  disambiguate by parent section ("the instance in §2.7, not §2.8").
- **Directional operations only.** Never bare `INSERT` — always `INSERT BEFORE` / `INSERT AFTER`.
  Resolving direction at write time, not execution time, removes a whole class of error.
- **Complete replacement when structure changes.** If a change alters a block's *structure* (list
  nesting, table columns, reorganization), give the complete final block, not incremental edits —
  the executor should never have to mentally reconstruct the result. For a single element inside an
  unchanged structure, incremental is fine. The threshold is cognitive ("can they see the final
  shape?"), not a line count.
- **Phases for dependencies.** If later changes depend on earlier ones (e.g., renumbering must
  follow insertion), split into ordered phases, each independently verifiable; declare hard
  dependencies at the top of each phase.
- **Temporary numbering.** When inserting into a numbered sequence across phases, use temporary IDs
  (§4.4a, §4.4b) during insertion, then a dedicated renumbering phase replaces them all at once.
  Verify with "search for 4.4a, confirm zero matches."
- **Cross-file reference timing.** When one file references another's section numbers, state whether
  the reference uses pre- or post-modification numbering. Default: final (post-mod), stated.

## The prose residue (Catalog B — keep it thin)

Only what genuinely needs judgment: the *intent* of a change (so the executor resolves ambiguity),
whether a change is structural (→ complete replacement), and how to handle the failures below.

## Failure handling (document-modification specific)

- **Anchor not found** — mark `[ANCHOR NOT FOUND: id]`, skip, continue, report at end.
- **Format mismatch** — adapt inserted content to the target's actual formatting (bullet style,
  heading level).
- **Execution-environment artefacts** — target files may have trailing whitespace, smart quotes, or
  inconsistent blank lines that break exact string matching. Warn the executor; normalize whitespace
  before programmatic matching. (This one sentence saved ~30% of debugging time in practice.)
- **Numbering conflict / cross-reference staleness** — renumber to avoid collision, or mark
  `<!-- EDIT NOTE: verify reference -->` when not determinable.

Template: `../templates/change-spec.md`. Worked example: `examples.md`.
