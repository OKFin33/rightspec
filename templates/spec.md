# Spec template (Spec mode)

Use after partitioning (`../references/partition.md`). Fill the structured envelope as structure,
the judgment core as prose. Delete a section only if it is genuinely irrelevant — not merely empty
(an empty section that would mislead the executor should be filled, not dropped).

## Structured envelope

```yaml
title: <name by function, not a slogan>
executor: <who runs this; if an agent, list tools explicitly; if unknown: "TBD — generalist agent, no context">
inputs:
  <name>: <type; required | optional; what to do if missing>
output:
  <fields, types, format, ordering; stable section headers; numeric thresholds>
tools:
  <tool>: <when to use / when not / how to weigh results>
scope: <what is covered, concretely>
non_goals: <adjacent things explicitly excluded>
```

## Judgment core (prose — the only part that needs an LLM)

**Goal / intent.** <what this is for, so the executor can resolve cases the contract did not cover>

**Quality bar.** <what "good" means>
- Good: <one concrete good example>
- Bad: <one concrete bad example> — fails because <why, and what it would break downstream>.

**Failure handling.**
- External (missing data / tool failure / conflict): <assume-and-note | ask | halt>
- Judgement dilemma (two valid options): <how to weigh, or "choose and note which and why">
- Structural (steps done but result incoherent): <how to recover>

**Escalation.** <when to stop and ask, or return a partial result>

## Validate

Run the partition screen + zero-context gate in `../references/review-checklist.md` before handing off.
