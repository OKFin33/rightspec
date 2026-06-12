---
name: rightspec
description: >-
  Use when an agent writes a spec/handoff that another agent will execute — agent-writes,
  agent-reads (human readability is an optional bonus, not the premise). Reach for it to: write
  an executable spec/SOP/handoff a fresh agent can run with zero prior context; write precise
  change-instructions ("change spec") an agent will apply to an existing document; audit whether
  a spec is zero-context executable; or decide which part of an agent task should be
  deterministic code/tool/RPC versus left to the LLM. It partitions the task — structurable
  parts become schema/typed contracts/tool policy, prose only for the irreducible judgment core
  (methodology in references/partition.md). NOT for product PRDs, user stories, or business
  requirements (human-facing PM spec-writing — a different lane), nor general prose like READMEs
  or reports.
---

# rightspec

rightspec is a **methodology, not a template library**. Its core act is a *judgment*, not a
fill-in form: partition what an agent handoff needs into what can be structured and what genuinely
needs an LLM, then deliver **one spec that combines both** — structure where structurable, natural
language where not. The templates downstream are scaffolding — this partition is the point.

## What an agent spec actually is

This applies to the **agent-writes, agent-reads** case: an agent authors the handoff and another
agent executes it. A human being able to read it is an optional bonus, not the premise — which is
exactly what separates this from a PRD (human author, human / organization audience).

An agent spec is **one artifact with two parts**: a **structured envelope** — the data and
contract the task can pin down (inputs, output contract, tool policy, enums, thresholds), written
*as structure* — and a **natural-language judgment core**, the irreducible part that needs an
LLM's understanding. Write schema where it can be schema, prose where it genuinely needs judgment;
the deliverable is the two combined. (If a task has *no* judgment core at all, see the gate below
— then it should not be a spec, or an LLM, at all.)

The sharpest edge of the methodology:

> **If you can fully specify a task — fixed inputs, fixed rules, fixed outputs — it is a
> function. Write code and call it (RPC). Do not write a spec, and do not use an LLM.**

You reach for an LLM only for the part that resists being structured: open-ended judgment. That
part is the spec's **judgment core**, carried in natural language because language is the only
interface to an LLM's understanding. The spec still carries the structured envelope alongside it —
the executor needs both the fixed contract and the judgment. The LLM's *surface* is only the prose
part; keep it small.

Reliability follows directly: **the smaller the natural-language surface you hand an LLM, the
more reliable, testable, and cheap the system.** A spec that is mostly prose is usually a spec
that failed to structure what it could have.

The spec's **container is situational**: a structured container (JSON / YAML — the envelope as
fields, the judgment as string fields) is natural for agent-to-agent; Markdown when a human also
reads it. The format is not the point — the **partition (schema + NL)** and the **agent-to-agent
handoff** are the first principles.

## Always partition first

Before writing anything, split the task three ways. This partition *is* the skill; everything
below is mechanics.

**1. Structurable → emit as structure, never as prose.**
Inputs, typed output contract, tool / resource policy, enumerations, thresholds, control flow,
validation rules. Write these as JSON / YAML / tables. If a "requirement" can be a schema
field, an enum, or a checkable constraint, it does not belong in prose. Catalog of structurable
patterns: `references/partition.md`.

**2. Irreducibly natural-language → the judgment core.** The *only* place prose earns its keep:
goals and intent; quality / taste criteria ("what counts as good"); how to act in situations you
could not enumerate; judgement dilemmas (two valid options, no clear winner); when to halt or
escalate.

**3. The minimize-LLM-surface gate.** Look at the residue after partitioning:
- **No NL residue** → this is a function. Tell the user to write code / an RPC / a tool, not a
  spec — and not to use an LLM. Stop here. Saying this is a *success*, not a failure of the skill.
- **A specific NL residue** → write the spec as the **structured envelope (Catalog A, as structure)
  plus that NL residue (Catalog B)** — both combined are the spec.

## Pick a mode (only after partitioning)

- **Spec mode** — author a fresh handoff a fresh agent (or human) can run with zero prior
  context. → `references/spec-mode.md`, `templates/spec.md`
- **Change Spec mode** — instruct an executor to modify an existing document precisely.
  → `references/change-spec-mode.md`, `templates/change-spec.md`

If the executor is not yet known, write **Executor: TBD** and spec for the most constrained
plausible executor (a generalist agent with no context). A human can skip detail an agent needs;
an agent cannot recover context a spec silently assumed.

## Spec mode — assemble the spec (envelope + judgment core)

Ship the structured envelope as structure, then write the NL core so a context-less executor can
act on it: zero-context complete, the three failure categories handled (external / judgement-
dilemma / structural), and a definition of done that is actually checkable. The template is a
scaffold to fill *after* you partition — not a substitute for partitioning. Full guidance:
`references/spec-mode.md`.

## Change Spec mode — a typed patch

Modifying a document sits near the structured end of the spectrum; it is almost a diff. Emit the
modifications as a **structured operation list**, machine-applicable:

```yaml
- anchor: { after: "<text immediately before>", before: "<text immediately after>" }  # two endpoints
  op: INSERT AFTER | INSERT BEFORE | REPLACE | APPEND | DELETE                         # direction always explicit
  content: |
    <exact final content; for a structural change give the complete final block, not incremental edits>
```

Prose is reserved for the thin judgment residue: deciding whether a change is structural (→
complete replacement vs incremental), cross-file numbering timing, and the intent behind a change
so the executor can resolve ambiguity. The conventions (precise two-endpoint anchors, phasing for
dependent changes, temporary numbering, the trailing-whitespace warning) are evidence-backed —
see `references/change-spec-mode.md`.

## A spec is a design-time contract

What you write is the contract *while the handoff is still being defined*. When an interaction
stabilizes and repeats, compile the structured half into a fixed schema / protocol and let the
prose core shrink further. rightspec is for the design-time and evolving cases — not the hot path
of a settled, high-frequency loop, where structure wins outright.

## Validate before handing off

- **Zero-context gate** — could the executor finish with no access to this conversation? Are all
  terms, inputs, and missing-input behaviors defined? Is every step driven by the spec rather than
  unstated intent? Is the unhappy path handled?
- **Change-spec gate** — can every anchor be located without guessing? Is every REPLACE's full
  content present?

Pointing rightspec at an *existing* spec to grade it (the audit use) runs the same checklist:
`references/review-checklist.md`.

## References

- `references/partition.md` — the partition discipline, the structurable-pattern catalog, and the
  gate, in depth. **The heart; read this first when applying the skill.**
- `references/spec-mode.md` — Spec mode full guidance (NL-core sections, zero-context gate).
- `references/change-spec-mode.md` — Change Spec conventions and the evidence behind them.
- `references/review-checklist.md` — validation / audit checklist for both modes.
- `references/examples.md` — a partitioned spec and a structured change spec, worked end to end.
- `references/decisions.md` — design rationale (why the partition spine, why two modes).
- `templates/spec.md`, `templates/change-spec.md` — fill-in scaffolds, used *after* partitioning.
