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

## Use

- **Automatically** — Claude invokes the skill on its own when a request matches the description (coordinating multi-step development work).
- **Explicitly** — type `/dev-fable` in Claude Code to invoke it directly.

## Subagents

The routing table in `SKILL.md` refers to subagent types (`deep-reasoner`, `fast-worker`, `explorer`). If your Claude Code setup uses different agent names, map each row to the closest equivalent you have available — the workflow itself is agent-name agnostic.

## License

[MIT](./LICENSE)
