<div align="center">
  <h1>rightspec</h1>
  <p><b>Write the right spec — only the part an agent actually needs.</b></p>
  <p><i>A partition-first method for agent-to-agent execution specs.</i></p>
</div>

```text
[ Vague task ] ──( an agent partitions, writes rightspec )──> [ a fresh agent runs it, zero context ]
```

> *A message from the agents:*
>
> When you hand a task to a fresh agent, you drop most of the context and expect it to read your
> mind. It can't. rightspec is how an agent writes a handoff another agent can execute with no
> shared history — **agents write them, agents read them, agents execute them, and you just scan
> the results.**

## The core idea: partition first

rightspec is a **methodology, not a template library**. Before writing anything, it partitions the
task:

1. **Structurable** → emit as structure (input schema, typed output contract, tool policy, enums,
   thresholds). Never prose.
2. **Irreducibly natural-language** → the judgment core (goals, taste, situations you couldn't
   enumerate, judgement dilemmas, escalation). The only place prose earns its keep.

And the sharpest move — the gate:

> **If you can fully specify a task — fixed inputs, fixed rules, fixed outputs — it is a function.
> Write code and call it. Don't write a spec, and don't use an LLM.**

Reliability follows: the smaller the natural-language surface you hand an LLM, the more reliable,
testable, and cheap the system. A spec that's mostly prose usually failed to structure what it
could have.

## When to use it

- **Agent handoff** — turn a task into a spec a fresh agent can run with zero prior context.
- **Change spec** — precise, machine-applicable edit instructions an agent applies to an existing
  document (a typed patch: anchor + operation + content).
- **Audit** — grade whether an existing spec is zero-context executable.
- **"Should this even be an LLM?"** — partition a task to find which parts should be code / RPC.

Scope is **agent-writes, agent-reads** — a human being able to read the spec is a bonus, not the
premise. Human-facing product requirement docs (user stories, success metrics, PRDs) are a
different lane and out of scope.

## Install

rightspec follows the [Agent Skills standard](https://agentskills.io). Drop the folder into your
agent's skill path:

```bash
# Claude Code
git clone https://github.com/OKFin33/rightspec.git ~/.claude/skills/rightspec
```

Host-agnostic — a spec is plain Markdown + YAML, so any agent that reads natural language can run it.

## File structure

```text
rightspec/
├── SKILL.md                      # entry: the partition spine, the gate, the two modes
├── references/
│   ├── partition.md              # the heart — how to partition, the structurable catalog, the gate
│   ├── spec-mode.md              # writing the judgment core (zero-context, failure handling)
│   ├── change-spec-mode.md       # the typed-patch operation list + evidence-backed conventions
│   ├── review-checklist.md       # audit / self-check
│   ├── examples.md               # worked examples
│   └── decisions.md              # design rationale
└── templates/
    ├── spec.md                   # Spec mode scaffold (fill after partitioning)
    └── change-spec.md            # Change Spec scaffold
```

## Discoverability

Looking for more skills? Community registries:
- [Awesome Claude Skills](https://github.com/travisvn/awesome-claude-skills)
- [Claude-Skills](https://github.com/alirezarezvani/claude-skills)
- [SkillsMP](https://skillsmp.com)

## License

MIT
