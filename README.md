# dev-fable

A [Claude Code](https://claude.com/claude-code) **skill** that turns Claude into *Fable*, an orchestrator for multi-step development work.

Instead of doing everything in one context, Fable **plans, decomposes, and synthesizes** — delegating heavy reading, mechanical edits, and broad searches to specialized subagents, and keeping its own context focused on the conclusions.

## What it does

- **Plan** — break a task into phases and figure out what each phase needs.
- **Decompose** — route each phase to the right subagent and run independent work in parallel.
- **Synthesize** — collect the results, reconcile disagreements, and act — without re-deriving what a subagent already established.

For high-stakes decisions it runs two independent perspectives on the same problem in parallel and synthesizes the best of both, keeping them blind to each other so the synthesis catches what a single pass would miss.

See [`SKILL.md`](./SKILL.md) for the full workflow and delegation routing table.

## Install

Skills live in a `skills/` directory under `.claude`. Clone this repo into a folder named `dev-fable`.

**Personal (available in every project):**

```bash
git clone https://github.com/satasuk03/fable-dev-skill.git ~/.claude/skills/dev-fable
```

**Project-scoped (checked in with a specific repo):**

```bash
git clone https://github.com/satasuk03/fable-dev-skill.git .claude/skills/dev-fable
```

Then restart Claude Code (or start a new session) so it picks up the skill.

### Install the subagents (recommended)

The workflow delegates to three subagents — `deep-reasoner`, `fast-worker`, and
`explorer` — whose reference definitions ship in [`agents/`](./agents). Subagents
live in `.claude/agents/` (a *different* directory from skills), so copy them in:

```bash
# Personal
mkdir -p ~/.claude/agents && cp ~/.claude/skills/dev-fable/agents/*.md ~/.claude/agents/

# Or project-scoped
mkdir -p .claude/agents && cp .claude/skills/dev-fable/agents/*.md .claude/agents/
```

These are sensible defaults — tune the `model` and `tools` in each file to taste.
If you already have equivalent agents, skip this and map the routing table in
`SKILL.md` to your own agent names instead.

## Use

- **Automatically** — Claude invokes the skill on its own when a request matches the description (coordinating multi-step development work).
- **Explicitly** — type `/dev-fable` in Claude Code to invoke it directly.

## Subagents

Reference definitions ship in [`agents/`](./agents):

| Agent | Role | Default model |
|-------|------|---------------|
| `deep-reasoner` | Architecture, tricky debugging, algorithm design, tradeoff analysis | `opus` |
| `fast-worker` | Boilerplate, tests, formatting, simple repetitive edits | `haiku` |
| `explorer` | Broad read-only search / codebase reconnaissance (never edits) | `sonnet` |

Adjust the `model` and `tools` in each file to fit your setup. If you already use different agent names, skip installing these and map the routing table in `SKILL.md` to your own — the workflow is agent-name agnostic.

## Credits

Inspired by [Diego Cabezas](https://x.com/diegocabezas01) ([@diegocabezas01](https://x.com/diegocabezas01))
and his [original tweet](https://x.com/diegocabezas01/status/2072436501263339841)
on using Fable 5 as an orchestrator with Opus, Sonnet, and Codex subagents.

## License

[MIT](./LICENSE)
