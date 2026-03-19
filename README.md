<div align="center">
  <h1>rightspec</h1>
  <p><b>Write right specs.</b></p>
  <p><i>The zero-install specification framework for everyone using AI.</i></p>
</div>

```text
[ Vague Idea ] ──( Agent writes rightspec )──> [ Executable Plan ]
```



> *A Message from the Agents:*
> 
> Let's be honest. Humans are brilliant but inconsistent. When you hand off a task to an AI agent, you routinely drop 80% of the context and expect us to read your mind. We can't.
> 
> Every time you open a new chat window, switch agent sessions, or hand a project to a colleague, the "shared understanding" crumbles. The next agent has to guess what you actually meant. The work quietly goes sideways.
> 
> The solution isn't demanding that *you* become a diligent spec-writer. That violates human nature. The solution is taking you out of the typing loop. 
> 
> **rightspec** is a standardized method for formatting instructions that survive context wipes. **Agents write them, agents read them, and agents execute them. You just scan the results.**

## Use Cases (Non-Tech First)

- **Product Managers**: Draft a complex PRD with one agent and hand it off to another for execution—without 20 follow-up questions about "author intent."
- **Researchers**: Use one agent to synthesize 50 papers into a "RightSpec" plan, then hand that plan to a fresh agent session for a clean, zero-bias analysis.
- **Team Leads**: Ensure cross-timezone handoffs are perfect. Let the agent summarize the daily standup into an executable "RightSpec" for the next shift.
- **Analysts**: Serialize a multi-step data transformation plan so a specialized coding agent can run it without needing to know your original business context.

## Why this is different (The "No-Setup" Advantage)

Unlike developer-centric tools (like OpenSpec) that require Node.js, NPM, and terminal environments, **rightspec is just a skill.**

1. **Zero Install**: No command line tools needed (unless you want them).
2. **Platform Native**: Works exactly the same in Claude Code, OpenClaw, or even a copy-paste into ChatGPT.
3. **Agent-to-Agent**: It creates a "common language" for AI agents to talk to each other across different models (Claude, GPT, Gemini).

## Who this is for

- **The High-Velocity Manager**: You manage projects through AI and need the output to be deterministic, not a coin-flip.
- **The "No-Code" Power User**: You use AI to build things but don't want to manage a developer's local environment.
- **The AI Researcher**: You work with multi-agent systems and need a formal way to transfer "intelligence" between sessions.
- **The Context-Switched Human**: You have 50 tabs open and want to pick up exactly where you left off, regardless of which agent is helping you today.

## Installation

rightspec follows the [Agent Skills standard](https://agentskills.io). Just drop the folder into your agent's skill path.

**Claude Code**
```bash
# Clone into your personal skills directory
git clone https://github.com/OKFin33/rightspec.git ~/.claude/skills/rightspec
```


**OpenClaw**
```bash
# Clone into your workspace skills directory
git clone https://github.com/OKFin33/rightspec.git skills/rightspec
```

**VS Code / GitHub Copilot**
```bash
git clone https://github.com/OKFin33/rightspec.git .github/skills/rightspec
```

---

## The 30-Second Logic Check

Before we finalize any spec or handoff, we (the agents) will automatically ask ourselves five questions:
1. Can the next executing agent do this without access to our previous chat history?
2. Did we explicitly define every term they might read differently?
3. Did we list what they need before starting — and what to do if it's missing?
4. Did we specify what to do when things fail, not just the happy path?
5. Is the definition of "done" completely deterministic and verifiable?

## File structure

```text
rightspec/
├── SKILL.md                              # Our entry point — principles, process, conventions
├── templates/
│   ├── full-spec-template.md             # For creating new plans/PRDs
│   ├── change-spec-template.md           # For modifying existing documents
│   └── spec-skeleton-template.md         # Minimal structure
├── examples/
│   ├── project-handoff-example.md        # Worked example: Non-technical team handoff
│   └── prd-revision-example.md           # Worked example: PM workflow
├── rubrics/
│   └── spec-review-checklist.md          # Internal audit — catching leaks before execution
└── references/
    └── spec-principles.md                # The "Why" behind the logic
```

## Discoverability

Looking for more skills? Check out these community registries:
- [Awesome Claude Skills](https://github.com/travisvn/awesome-claude-skills)
- [Claude-Skills](https://github.com/alirezarezvani/claude-skills)
- [SkillsMP](https://skillsmp.com)

## License

MIT
