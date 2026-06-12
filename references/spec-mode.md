# Spec mode — assembling the spec (envelope + judgment core)

Use this after you have partitioned (`partition.md`). By now you know which pieces are structure
(Catalog A) and which are the irreducible judgment core (Catalog B). Spec mode assembles both
into a handoff a fresh agent can run with zero prior context.

A spec is two layers: a **structured envelope** (Catalog A, emitted as structure) and a **prose
judgment core** (Catalog B). Do not blur them — the spec's value is that the reader can tell a
fixed contract from a place that needs their judgment. The template (`../templates/spec.md`) is
the fill-in scaffold; this is the reasoning behind each part.

## Structured envelope (Catalog A — as structure, never prose)

- **Executor / tools** — who runs this. If an agent, list available tools explicitly (an agent
  cannot infer tool access). If unknown, `Executor: TBD` → write for a generalist agent with no
  context: a human can skip detail an agent needs, but an agent cannot recover assumed context.
- **Inputs / preconditions** — typed: what must exist before starting, mandatory vs optional, and
  the behavior when a required input is missing.
- **Output contract** — the deliverable's exact shape: fields, types, format, ordering, stable
  section headers (no creative renaming between runs), numeric thresholds ("at least 5 sources",
  not "thorough").
- **Tool / resource policy** — when to use each tool, when not to, how to weigh results.
- **Scope / non-goals** — what is in, and (just as important) what is explicitly out, to stop drift.

## Judgment core (Catalog B — the only prose that earns its place)

- **Goal / intent** — what the work is *for*, so the executor resolves cases the contract did not cover.
- **Quality bar** — what "good" means, anchored with one good + one bad example and *why* the bad
  one fails. Examples calibrate far better than adjectives.
- **Failure handling** — three categories: external (missing data, tool failure, conflicts);
  judgement dilemma (two valid options, no clear winner); structural (all steps done but the whole
  is incoherent). For each: assume-and-note, ask, or halt.
- **Escalation / handoff** — when to stop and ask rather than guess; when to return a partial result.

## Zero-context gate (run before handing off)

Any "no" means revise:

1. Can the executor finish with no access to this conversation?
2. Are all terms a reasonable executor might read differently defined?
3. Are all required inputs listed, with missing-input behavior?
4. Is every step driven by the spec, not unstated author intent?
5. Is the unhappy path handled, not just the happy path?

## Splitting large specs into phases

If the task has more than ~10 discrete operations, or dependency chains (a later step needs an
earlier step's result), split into numbered phases (A → B → C) — each a self-contained spec with
its own output contract, failure handling, and checklist, verifiable independently rather than
only at the end. For phases that insert into a numbered sequence, use the temporary-numbering
pattern in `change-spec-mode.md`.
