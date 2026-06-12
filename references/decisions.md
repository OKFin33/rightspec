# Design decisions

Why the skill is shaped this way. New decisions (partition era) first, then the Change Spec craft
carried from the original, evidence-backed version.

## DN1 — Partition is the spine, not a step

rightspec's core is a *judgment* — partition the task, push everything structurable into
structure, keep prose only for the irreducible judgment core — not a template to fill. This
reframes it from "a spec writer" (which overlaps Anthropic's PM-facing `/write-spec`) to "the tool
for the natural-language core of an agent handoff, after minimizing the LLM surface." Templates are
scaffolding; the partition is the value.

## DN2 — The minimize-LLM-surface gate as a first-class output

If partition leaves no judgment residue, the task is a function: the skill tells the user to write
code / RPC and not use an LLM. Producing *no spec* is a valid, correct outcome — it prevents the
most expensive failure (an LLM doing a job a function should do). This behavior is what makes
rightspec a methodology rather than a document generator.

## DN3 — Two modes, not four

Cut the generic "Full Spec" (it overlapped `/write-spec`'s territory and was the least
differentiated part). Folded Skeleton into the templates and Audit into the review checklist. What
remains is purpose-distinct: Spec mode (author an execution handoff) and Change Spec mode (modify a
document) — they genuinely need different precision (output-contract precision vs anchor precision).

## DN4 — Scope is agent-writes, agent-reads

The premise is agent-to-agent: an agent authors the handoff, an agent executes it; human
readability is an optional bonus, not the point. This is the clean boundary against PRDs / PM
spec-writing (human author, human / org audience) — a different lane, served by `/write-spec`.

---

## Carried from the original (Change Spec craft, evidence-backed)

Seven change specs were executed against four real documents (35+ modifications); anchor quality
was the single biggest factor in execution speed and accuracy. Each convention below came from
observed execution friction, not taste:

- **D01 — Change Spec is a first-class mode**, not a Full-Spec variant. New-document precision
  depends on the output contract; change precision depends on anchor precision. Different focus.
- **D03 — Directional operations only** (INSERT BEFORE / AFTER). Bare INSERT forced the executor to
  guess direction; resolving it at write time removes the error class.
- **D04 — Complete replacement when structure changes** (not a line-count threshold). The failure
  mode is "can't see the final shape", which is cognitive: a nested-list rewrite needs the whole
  block; an appended row does not.
- **D05 — Temporary numbering + a dedicated renumbering phase**. Guessing final numbers couples
  phases; temporary IDs keep each phase independently verifiable.
- **D07 — Execution-environment warning in both the process and the template**. Trailing whitespace
  was the single largest source of debugging friction; one sentence of warning saved ~30% of
  debugging time.

> Method note: the original v2.0 was iterated by two independent instances (design side and
> execution side) working from the same feedback, then merged — convergent conclusions taken as
> high-confidence, divergent ones flagged as genuine design trade-offs. That discipline (independent
> iteration → structured merge) is itself the spec discipline applied to its own evolution.
