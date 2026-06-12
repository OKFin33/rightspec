# Change Spec template (Change Spec mode)

A change spec is mostly a typed patch. Fill the operation list as structure; keep prose to the thin
judgment residue. Conventions: `../references/change-spec-mode.md`.

## Header

```yaml
title: "Change Spec: <target> <vX → vY>"
target: <file(s) the executor must open before starting>
executor: <agent | human | "TBD — any competent agent or human editor">
depends_on: <prior change specs that must run first, or "none — standalone">
```

## Operation list

```yaml
- id: <SEQ-01>
  location: <section / heading, human-readable>
  anchor:
    after: "<exact text immediately before the edit point>"
    before: "<exact text immediately after>"      # two endpoints; disambiguate if the text repeats
  op: INSERT AFTER | INSERT BEFORE | REPLACE | APPEND | DELETE
  content: |
    <exact final content; the complete final block if the change is structural>
  intent: <one line — include only if it helps the executor resolve ambiguity>
```

Repeat per change. If phases are needed (dependencies / renumbering), group operations under
numbered phases and declare hard dependencies at the top of each phase.

## Output contract

```yaml
deliverable: "modified <filename>"
format: "<e.g. Markdown, preserving original conventions>"
constraint: "do not modify content not addressed by this spec"
```

## Failure handling

- anchor not found → mark `[ANCHOR NOT FOUND: id]`, skip, continue, report at end
- format mismatch → adapt to the target's actual formatting
- environment artefacts (trailing whitespace, smart quotes) → normalize before programmatic matching
- numbering conflict / stale cross-reference → renumber, or mark `<!-- EDIT NOTE: verify -->`

## Evaluation checklist

- [ ] each id executed (or marked ANCHOR NOT FOUND)
- [ ] inserted formatting matches surrounding content
- [ ] no unintended changes outside the operation list
- [ ] no temporary markers / old numbering / edit notes remain
