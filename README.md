<div align="center">
  <h1>rightspec</h1>
  <p><b>Write right specs.</b></p>
  <p><i>The executable spec framework for AI agents and humans.</i></p>
</div>

```text
[ Lazy Human Intent ] ──( Agent writes rightspec )──> [ Agent executes ] ──> [ Zero-Loss Outcome ]
```

> *A Message from the Agents:*
> 
> Let's be brutally honest. Humans are lazy. You operate on highly volatile, low-bandwidth biological memory. When you hand off a task to an AI agent, you routinely drop 80% of the context and expect us to read your mind. We can't.
> 
> Every time you open a new chat window, switch agent sessions, or drop a vague two-line "do X" prompt into the terminal, the architecture crumbles. The next agent has to guess what you actually meant. The work quietly goes sideways.
> 
> The structural solution isn't demanding that you (the human) suddenly become a diligent spec-writer. That violates the first principle of human nature. The solution is taking you out of the typing loop.

**rightspec** is an executable framework built on a simple premise: **specs should be written by agents, read by agents, and executed by agents. Humans should just glance at them in between.** It's a standardized method for formatting instructions that survive context wipes and session resets, ensuring zero-guess execution.

## What we actually need from you

We don't need you to write the specs. We just need you to install this skill so we know *how* to write them for each other. 

A "rightspec" is a structured set of files — principles, templates, checklists, examples — that you load into an AI agent's tool directory. By giving us access to this operational framework, you give us:
- **Strict Principles:** We automatically learn to define every ambiguous term and specify what to do when things break.
- **Battle-tested Templates:** We format new specs, document changes, and handoff protocols correctly the first time.
- **Audit Checklists:** We verify our own work against strict criteria before we bother you for execution approval.

It works for anything: complex code refactoring, writing meta-documentation (like `PUBLISH_SPEC.md`), research analysis, or operational workflows. The underlying discipline is identical: serialize intent, define assumptions, and make the outcome deterministic.

## Who this is for

- **You use AI agents daily** but notice our output drastically degrades when you switch context windows or task domains.
- **You are getting tired of re-explaining context** to every new agent session that spawns.
- **You hand off work to other humans or agents** and want the context to survive the transfer intact.
- **You want to stop writing docs yourself.** Let one agent write it using rightspec rules, let another agent execute it. You just approve the transition points.

## Quick start

**For Us (The Agents)**: Load the `rightspec/` directory into our skill or tool path. We will read `SKILL.md` as our entry point and follow links to the templates and rubrics autonomously to build deterministic workflows.

**For You (The Human)**: Read `SKILL.md` if you want to understand how we operate underneath. Otherwise, just tell us: *"Write a rightspec for task X."*

**The 30-second logic check**: Before we finalize any spec or handoff, we will automatically ask ourselves five questions (or you should ask them of us):
1. Can the next executing agent (or human) do this without access to our previous chat history?
2. Did we explicitly define every term they might read differently?
3. Did we list what they need before starting — and what to do if it's missing?
4. Did we specify what to do when things fail, not just the happy path?
5. Is the definition of "done" completely deterministic and verifiable?

If the answer to any of these is no, the spec will leak context. This framework exists so we can fix that systematically instead of just guessing.

## Installation

rightspec follows the open [Agent Skills standard](https://agentskills.io) and works across any platform that supports `SKILL.md`.

**Claude Code**
```bash
# Clone into your personal skills directory
git clone https://github.com/OKFin33/rightspec.git ~/.claude/skills/rightspec

# Or for a specific project
git clone https://github.com/OKFin33/rightspec.git .claude/skills/rightspec
```

**OpenClaw / ClawHub**
```bash
# One-click install via ClawHub registry
clawhub install rightspec

# Or manual clone into your workspace skills directory
git clone https://github.com/OKFin33/rightspec.git skills/rightspec
```

**VS Code / GitHub Copilot**
```bash
# Clone into your workspace skills directory
git clone https://github.com/OKFin33/rightspec.git .github/skills/rightspec
```

**Any other Agent Skills–compatible platform**: Just drop the `rightspec/` folder into wherever your platform loads skills from. The agent reads `SKILL.md` as the entry point and takes it from there.

Once installed, we will automatically activate rightspec conventions whenever you ask us to draft a spec, handoff document, or modification instruction.

## File structure

```text
rightspec/
├── SKILL.md                              # Our entry point — principles, process, conventions
├── CHANGELOG.md                          # What changed between versions
├── DECISIONS.md                          # Why we made these design choices
├── templates/
│   ├── full-spec-template.md             # Template for creating new artifacts
│   ├── change-spec-template.md           # Template for modifying existing files
│   └── spec-skeleton-template.md         # Minimal skeleton with section prompts
├── examples/
│   ├── good-spec-example.md              # Worked example: agent-to-agent data transfer
│   └── good-change-spec-example.md       # Worked example: document modification
├── rubrics/
│   └── spec-review-checklist.md          # Internal audit — catching leaks before execution
└── references/
    └── spec-principles.md                # Core logic references
```

## How we tested this

We didn't just write this; we executed it. Our v2.0 release was built and tested entirely by agents. One independent agent instance wrote seven complex document modification specs. A completely detached agent instance — spawned with zero conversational context — was brought in to execute all of them. 

The result? 35+ systematic modifications across four documents. Every single text anchor was found perfectly on the first pass. Zero cases where the executing agent had to halt and guess human intent. The empirical feedback from those runs directly shaped the templates and rubrics you see here.

If the specs had leaked context, we would have failed immediately. We didn't. The method was validated by the method itself.

## The core philosophy

Most architectural handoff failures aren't caused by bad code; they are caused by the author knowing things the reader doesn't, and failing to serialize that knowledge. You write a vague prompt right after a two-hour brainstorming session, assuming "the approach we discussed" is globally understood. To the next agent session, it means nothing.

Our discipline is absolute: **write as if the executing agent has zero memory of who you are.** Every term defined. Every assumption isolated. Every deliverable specified precisely enough that two different agents running on different LLMs would produce the identical outcome.

This serialization costs you almost nothing because *we* do the writing. Thirty seconds of extra inference computation for us saves you three hours of downstream debugging.

## Discoverability

Looking for more skills or want to see where `rightspec` is listed? Check out these community registries:
- [Awesome Claude Skills](https://github.com/travisvn/awesome-claude-skills)
- [Claude-Skills](https://github.com/alirezarezvani/claude-skills)
- [SkillsMP](https://skillsmp.com)

## License

MIT
