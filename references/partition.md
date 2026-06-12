# Partition — the heart of rightspec

The partition *is* the skill. Before writing a single line of a spec, split the task into what
can be structured, what genuinely needs an LLM, and what should not be an LLM task at all. This
document is how to make that split well.

## The decisive test

For each piece of the task, ask one question:

> **Can this be pinned down in advance — as a fixed rule, a typed field, an enum, a checkable
> constraint — so that a deterministic process (or a context-free reader) gets it right every
> time?**

- **Yes →** it is *structurable*. Emit it as structure (schema / table / enum / typed contract),
  not prose. Prose here only adds tokens and ambiguity.
- **No — it needs open-ended understanding of intent in context →** it is *irreducibly natural
  language*. This is the judgment core, the only place prose earns its keep.

The mistake rightspec exists to prevent is writing *prose* for things that were structurable —
"the output should usually have about five sections" instead of `min_sections: 5`. Vague prose
where a constraint would do is how delegated work drifts.

## Catalog A — structurable (emit as structure)

If a requirement matches any of these, it is not prose:

| Piece | Emit as | Prose smell (don't) |
|---|---|---|
| What inputs exist, their types | input schema | "you'll get some files and a config" |
| The deliverable's shape | typed output contract (fields, types, format) | "return a nice summary" |
| Allowed options / categories | enum | "pick high, medium, or low-ish" |
| Limits, counts, sizes | numeric threshold | "don't make it too long" |
| Which tools, when | tool / resource policy table | "use search if you need to" |
| Order / branching of steps | control flow (numbered steps, or a state list) | "generally do A then B" |
| What makes output valid | validation rule (checkable) | "make sure it's good quality" |

**Conversion example** (prose → structure):

> Prose: "Extract the key risks. Give back maybe up to ten, each with a severity and where you
> found it. Skip anything trivial."

becomes structure:

```yaml
output:
  type: list
  max_items: 10
  item: { risk: string, severity: enum[high, medium, low], evidence_ref: string }
filter: drop anything below the "real risk" bar   # the only judgment left — see Catalog B
```

Everything except *what counts as a real vs trivial risk* just became a schema.

## Catalog B — irreducibly natural language (the judgment core)

What survives the test — the part that genuinely needs an LLM:

- **Goal / intent** — what the work is *for*, so the executor can resolve cases the rules do not cover.
- **Quality / taste criteria** — "what counts as a *good* risk, a *trivial* one." Cannot be
  enumerated; needs understanding. Anchor it with one good + one bad example — examples calibrate
  far better than adjectives do.
- **Un-enumerated situations** — what to do when reality matches none of the fields you defined.
- **Judgement dilemmas** — two valid options, no clear winner; say how to weigh them, or that the
  executor may choose and must note which it chose and why.
- **Escalation / halt** — when to stop and ask rather than guess.

If you catch yourself writing a *rule* here ("if severity == high and count > 3, then…"), it
belongs in Catalog A — move it to structure.

## The gate — is there a residue at all?

After partitioning, look at Catalog B for this task:

- **Empty** — every piece was structurable. **This is a function, not an agent task.** Tell the
  user: write the code / tool / RPC, call it deterministically, and keep the LLM out of the loop.
  Writing no spec is the correct output. *Reaching this conclusion is a success of the method, not
  a failure to produce a spec.*
- **Non-empty** — that residue is your spec's core. Write it (Spec mode or Change Spec mode);
  everything in Catalog A ships as structure beside it.

**Worked example — "this should not be an LLM":**

> Request: "Write a spec for an agent to rename every `.jpeg` to `.jpg` in a folder and update
> the references in `index.md`."

Partition: inputs (folder, file pattern) → structure; operation (rename, find-and-replace) →
deterministic; output (renamed files, patched references) → checkable. Catalog B is **empty** —
there is no open-ended judgment anywhere. → **Do not write a spec. Write a ten-line script.**
rightspec's job here is to say exactly that.

## Design-time, not run-time

The structure you emit is a *design-time* contract — the shape of the handoff while it is still
being defined. When an interaction settles and repeats, compile Catalog A into a fixed schema /
typed protocol, and let the Catalog B core shrink as you learn which judgments recur (some will
harden into rules). rightspec is for the design-time and evolving cases; a settled,
high-frequency loop should be pure structure with no spec at all.
