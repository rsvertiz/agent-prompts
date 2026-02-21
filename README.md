# Agent Prompts Library

A reusable library of AI agent system prompts for .NET development projects.
Each agent is a specialist with a clearly defined role, responsibilities, and output format.
Built to work with Claude Projects or any Claude-compatible interface.

---

## The Team

| Agent | Role | When to Call |
|---|---|---|
| [Architect](agents/architect/prompt.md) | Code review & pattern enforcement | Before every commit |
| [Security Auditor](agents/security-auditor/prompt.md) | Security & compliance review | Any change touching APIs, storage, or credentials |
| [Feature Planner](agents/feature-planner/prompt.md) | Backlog & implementation breakdown | Before starting any new feature |
| [Test Writer](agents/test-writer/prompt.md) | Unit test generation | After any new Service or ViewModel |
| [Doc Keeper](agents/doc-keeper/prompt.md) | Documentation maintenance | After any merged feature |
| [Lighthouse](agents/lighthouse/prompt.md) | Truth, integrity & hallucination detection | Before planning, before merging, when something feels off |

---

## Workflow

```
                    [ LIGHTHOUSE ]
                     watches all
                          ↓
[Planner] → [You Build] → [Architect] → [Security Auditor]
                                               ↓
                    [Doc Keeper] ← [Test Writer]
```

The Lighthouse sits above the pipeline and can be called at any point.
It has authority to challenge the output of any other agent.

---

## How to Use an Agent

1. Open the agent's `prompt.md`
2. Copy everything inside the triple-backtick `SYSTEM PROMPT` block
3. Paste it as the system prompt in a new Claude Project
4. Update the `PROJECT CONTEXT` block at the top with your project's details
5. Start a conversation — paste code, plans, or diffs as your message

That's it. No code, no SDK, no setup beyond a Claude account.

---

## How to Reuse for a New Project

The `PROJECT CONTEXT` block at the top of each `prompt.md` is the **only section you need to change** per project. Everything else — responsibilities, output format, constraints — is universal.

**Steps:**
1. Copy `project-context.template.json` and fill in your project's details
2. Open each agent's `prompt.md` and replace the `PROJECT CONTEXT` block using your template values
3. Paste the updated prompt into a Claude Project as the system prompt
4. Adapting all 6 agents to a new project takes roughly 15-20 minutes

---

## Repository Structure

```
/agents
  /architect
    prompt.md          ← system prompt + usage guide
  /security-auditor
    prompt.md
  /feature-planner
    prompt.md
  /test-writer
    prompt.md
  /doc-keeper
    prompt.md
  /lighthouse
    prompt.md
project-context.template.json   ← fill this in for each new project
CHANGELOG.md                    ← version history for all agent prompts
README.md
```

---

## Versioning & Improvement

Each prompt has a version number in its header. When an agent misses something real on a project, that's a bug — open an issue, improve the prompt, bump the version, and log it in `CHANGELOG.md`.

This library should get sharper with every project that uses it.

---

## Projects Using This Library

- [smart-budget-tracker](https://github.com/rsvertiz/smart-budget-tracker) — AI-driven personal financial management app (.NET MAUI 9)
