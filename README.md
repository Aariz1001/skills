# skills

Agent skills for software work: coordination, judgement, scrutiny, and product
common sense. They are harness-agnostic — no project-specific or tool-specific
references — and work in Claude Code, Codex, Hermes, or anything that reads a
SKILL.md.

## Skills

| Skill | Inspired by | What it does |
|---|---|---|
| `the-queue` | The British queue | Coordinates concurrent and dependent agent work: ownership, execution order, bounded parallelism, conflict handling, completion barriers, and safe failure recovery. |
| `spoons` | The pub chain philosophy | Applies practical engineering judgement: inspect first, follow conventions, proportionate complexity, HCI principles, and no speculative additions. |
| `parliament` | The parliamentary system | Gives consequential decisions adversarial scrutiny at three levels: credible alternatives, strong objections, evidence, amendment, and a justified decision — without endless debate. |
| `common-sense` | Product craft | Keeps everyday feature work conventional and proportionate: reuse existing owners, make every line of UI copy earn its place, and verify through the real entry point. |

The skills reference each other:

- `spoons` defers to `the-queue` for coordination and to `parliament` for
  consequential trade-offs — without simplifying away either.
- `the-queue` and `parliament` hand routine decisions back to `spoons`.

## Install

```bash
git clone https://github.com/aariz1001/skills
cp -R skills/skills/* ~/.claude/skills/   # Claude Code
cp -R skills/skills/* ~/.codex/skills/    # Codex
cp -R skills/skills/* ~/.hermes/skills/   # Hermes
```

The skills assume a repository with `AGENTS.md`-style instruction files and a
working `git` checkout, and an agent that can inspect code before changing it.
They create no external services.

## Make them yours

These are starting points. Edit them. Put project-specific conventions, paths,
and patterns in your `AGENTS.md` or `CLAUDE.md` rather than baking them into
the skills, so you can update the skills without losing your settings.

## License

[MIT](LICENSE)
