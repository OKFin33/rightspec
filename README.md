# rightspec

Every time you open a new chat window, switch agents, or hand work to a collaborator, information falls through the cracks. Context that was obvious five minutes ago becomes invisible. Decisions that were carefully reasoned get flattened into "do X." The next person — or the next agent — has to guess what you meant.

You've felt this. The new chat window that doesn't know what you spent two hours figuring out. The agent handoff where half the context vanished. The collaborator who read your doc and came back with ten questions you thought you'd already answered.

The cost isn't the ten questions. It's the times nobody asks — and the work quietly goes sideways.

**rightspec** is a method for writing handoff documents, specs, and instructions that survive the transfer. When the next reader has zero access to your head, your chat history, or your "obvious" context, a rightspec still works.

## What it actually is

A set of files — principles, templates, checklists, examples — that you can load into an AI agent as a skill, or use as a human reference. It covers:

- How to write a spec that a stranger (human or agent) can execute without asking you what you meant
- How to write modification instructions for existing documents that hit the right spot every time
- How to check whether a spec is actually executable before you send it off
- When and how to split large handoffs into phases that can each be verified independently

It works for any domain. Code, research, operations, content, analysis, document editing. The underlying discipline is the same: say what you mean, define your terms, specify what to do when things go wrong, make the output measurable.

## Who this is for

- **You use AI agents in your daily work** and you've noticed that the quality of what they produce depends almost entirely on the quality of what you give them
- **You work across multiple chat windows or agent sessions** and you're tired of re-explaining context that should have carried over
- **You hand off work to other people or agents** and you want the handoff to actually work the first time
- **You use tools like GitHub Spec Kit or Kiro** and you want the specs you feed them to be better — rightspec is about spec quality, not spec-to-code automation

## Quick start

**For AI agents**: Copy the `rightspec/` directory into your agent's skill or tool directory. The agent reads `SKILL.md` as the entry point and follows links to templates and rubrics as needed.

**For humans**: Read `SKILL.md` for the core process. Use the templates in `templates/` when writing specs. Use the checklist in `rubrics/` to review them before sending.

**The 30-second version**: Before you hand anything off, ask yourself five questions:

1. Can the reader do this without access to our conversation?
2. Did I define every term they might read differently?
3. Did I list what they need before starting — and what to do if it's missing?
4. Did I say what to do when things go wrong, not just when things go right?
5. Can someone check whether this was followed, without asking me?

If any answer is no, the handoff will leak. The templates help you fix that systematically instead of guessing.

## Installation

rightspec follows the open [Agent Skills standard](https://agentskills.io) and works across platforms that support SKILL.md.

**Claude Code**
```bash
# Clone into your personal skills directory
git clone https://github.com/OKFin33/rightspec.git ~/.claude/skills/rightspec

# Or for a specific project
git clone https://github.com/OKFin33/rightspec.git .claude/skills/rightspec
```

**OpenClaw**
```bash
# Clone into your workspace skills directory
git clone https://github.com/OKFin33/rightspec.git skills/rightspec
```

**VS Code / GitHub Copilot**
```bash
# Clone into your workspace skills directory
git clone https://github.com/OKFin33/rightspec.git .github/skills/rightspec
```

**Any other Agent Skills–compatible platform**: Copy the `rightspec/` folder into wherever your platform loads skills from. The agent reads `SKILL.md` as the entry point.

Once installed, the agent will automatically activate rightspec when you ask it to write a spec, create a handoff document, or draft modification instructions for an existing file.

## File structure

```
rightspec/
├── SKILL.md                              # Entry point — principles, process, conventions
├── CHANGELOG.md                          # What changed between versions
├── DECISIONS.md                          # Why each design choice was made
├── templates/
│   ├── full-spec-template.md             # Template for new specs and handoff docs
│   ├── change-spec-template.md           # Template for document modification instructions
│   └── spec-skeleton-template.md         # Minimal skeleton with section prompts
├── examples/
│   ├── good-spec-example.md              # Worked example: agent-to-agent data handoff
│   └── good-change-spec-example.md       # Worked example: document modification
├── rubrics/
│   └── spec-review-checklist.md          # Audit checklist — catches leaks before they happen
└── references/
    └── spec-principles.md                # Core principles reference
```

## How this was tested

The v2.0 release was built through a specific process: one agent instance wrote seven document modification specs. A separate, independent agent instance — with no shared context — executed all of them. 35+ modifications across four documents. Every single anchor point was found on the first try. Zero cases where the executor had to guess intent. The execution feedback directly shaped the templates, conventions, and checklist you see here.

The method was tested by the method. If the specs had leaked context, we'd have found out immediately.

## The core idea

Most handoff failures aren't caused by carelessness. They're caused by the author knowing things the reader doesn't — and not realizing it. You wrote the spec right after a two-hour discussion, so "the approach we discussed" felt specific. To the reader, it's meaningless.

rightspec's discipline is simple: **write as if the reader has never met you.** Every term defined. Every assumption stated. Every edge case handled. Every deliverable specified precisely enough that two different people (or agents) would produce the same thing.

This costs almost nothing when an agent does the writing. One extra pass to check the five questions above. Thirty seconds of agent time that saves hours of downstream confusion.

## License

MIT
