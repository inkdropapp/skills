# Inkdrop Skills

[![skills.sh](https://www.skills.sh/b/inkdropapp/skills)](https://www.skills.sh/inkdropapp/skills)

Agent Skills that make your AI coding agent fluent in [Inkdrop](https://www.inkdrop.app),
the Markdown note-taking app. They teach the agent Inkdrop's Markdown dialect and how to run
note-driven workflows — so plans, research, and documentation land in your notebooks looking
the way you'd write them by hand.

These skills pair with the [Inkdrop MCP server](https://github.com/inkdropapp/mcp-server),
which gives the agent the tools to actually create, read, and update notes. The MCP server is
the _hands_; these skills are the _know-how_.

## Quickstart

### Install with skills.sh

Install with the [skills.sh](https://skills.sh) CLI — it works with Claude Code, Codex,
Cursor, and 70+ other agents:

```bash
npx skills@latest add inkdropapp/skills
```

Pick the skills and agents you want, and it copies them into place. That's it — the agent
picks up each skill automatically when a task matches its description.

### Install with APM

If you manage agent dependencies with [APM](https://github.com/microsoft/apm), add the skills
to your project's `apm.yml` and deploy them to every agent it targets:

```bash
# All skills
apm install inkdropapp/skills

# or a single skill
apm install inkdropapp/skills --skill note-taking
```

### Manual install

A skill is just a folder with a `SKILL.md`. Copy (or symlink) one into your agent's skills
directory:

```bash
git clone https://github.com/inkdropapp/skills.git

# User-level (Claude Code) — available across all projects
cp -r skills/skills/note-taking ~/.claude/skills/

# or Project-level — scoped to one repo
cp -r skills/skills/note-taking .claude/skills/
```

## Requirements

- An [Inkdrop](https://www.inkdrop.app) account with notes to work with.
- The [Inkdrop MCP server](https://github.com/inkdropapp/mcp-server) configured in your
  agent, so it can call `create-note`, `read-note`, `update-note`, `patch-note`, and the
  other note tools these skills reference.

## Skills

Skills split on one axis — who invokes them. **User-invoked** skills run only when you type
them (e.g. `/fill-out-template`); they orchestrate a task. **Model-invoked** skills are
reached for automatically by the agent when the work fits; they hold reusable know-how.

### User-invoked

- **[fill-out-template](skills/fill-out-template/SKILL.md)** `[note-link]` — Fill out an
  Inkdrop note created from a template, in place, following the template's own instructions.
  A planning step: fill the plan, then wait for your go-ahead before writing code. For example:

  ```
  > Read [Support XXX](inkdrop://note/xxxxxx) and fill out the template
  ```

### Model-invoked

- **[note-taking](skills/note-taking/SKILL.md)** — The Markdown reference for Inkdrop note
  bodies: code-block attributes (`filename`, `line`, `title`), Mermaid diagrams, KaTeX math,
  and `inkdrop://note/<id>` links. The agent reaches for it whenever it writes a note.
- **[mermaid](skills/mermaid/SKILL.md)** — Layout rules for readable Mermaid diagrams in a
  narrow preview pane: choosing the diagram type and direction, subgraph `direction` and
  `~~~` placement, label wrapping, and syntax pitfalls.

## Contributing

To add a skill, create `skills/<skill-name>/SKILL.md` with frontmatter and instructions:

```markdown
---
name: my-skill
description: One line telling the agent when to reach for this skill.
argument-hint: [optional-arg] # include to make it a user-invoked slash command
---

# My skill

Instructions the agent should follow…
```

Keep the `description` specific — it's what the agent matches against to decide whether the
skill is relevant. Then add an entry to the list above under the right invocation type.

## License

No license file is present yet — add one to declare how these skills may be used.
