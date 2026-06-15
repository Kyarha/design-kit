# design-kit

A Claude Code plugin for working with **Claude design (CD)**. Two skills:

- **`design-brief`** — write a structured, positive design brief (intro · audience & tone ·
  structure · content · style · rules · "Done when"), record it to `docs/design/<page>.md`, and
  give a copy-paste block for CD.
- **`design-tweaks`** — turn your feedback on a CD result into copy-paste change requests and
  log them under that page's `## Revisions`, so design decisions are tracked.

Both keep briefs **positive** (what to create, never what to avoid), since that's what CD
follows well.

## Install (any machine, any project)

```
/plugin marketplace add Kyarha/design-kit
/plugin install design-kit@design-kit
```

Then the `design-brief` and `design-tweaks` skills are available in every project on that
machine. (If you previously kept these as personal skills in `~/.claude/skills/`, delete those
copies after installing so they don't duplicate the plugin's.)

## Layout

```
.claude-plugin/plugin.json        plugin manifest
.claude-plugin/marketplace.json   one-plugin marketplace (git-subdir → this repo)
skills/design-brief/SKILL.md
skills/design-tweaks/SKILL.md
```
