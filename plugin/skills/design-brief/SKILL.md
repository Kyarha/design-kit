---
name: design-brief
description: Write a SHORT design brief for Claude design (CD) and record it per version under docs/design/<page>/ that the user copies into CD. Use when the user wants to brief Claude design, start designing a page/screen/component/asset, or get a prompt to paste into CD. The brief gives CD only what to build and the real content it must contain, and hands every visual decision — mood, palette, type, layout, imagery — to CD, the designer. It never dictates colours, tone adjectives, or style rules, and stays as lean as possible. Every brief is a new design version: it opens with a preamble telling CD to build all its files (a JS file + the HTML pages) into a design_vX.Y folder and stamp a version header in each file — from scratch (major bump) or based on a previous version (minor bump). Pairs with the design-tweaks skill for iterating on the result.
---

# design-brief — write a brief for Claude design (CD)

Writes a **short** brief the user pastes into Claude design, recorded per version so every version's
intent is preserved. (Iterating on a version is the separate `design-tweaks` skill.)

## The two hard rules

**1. Brief the *what*, not the *look*. CD is the designer — let it design.**
The brief carries two things only: **what to build** and **the real content it must contain**. Every
visual decision — mood, atmosphere, colour, palette, typography, imagery, spacing, layout styling —
belongs to CD. Do **not** put a palette, hex codes, tone adjectives ("warm, calm, precise"), or a
list of style rules in the brief. CD will choose the aesthetic, or ask you for direction — that is
its job, not yours. A brief padded with constraints just makes CD rebuild what Claude Code would have
designed, which defeats the point. Give CD room.

**2. Positive direction only.** Every line says what TO create. Never "don't / avoid / no / not /
never", no anti-examples, no "good vs bad". Rephrase any avoid-X as the positive alternative.

If you catch yourself writing a colour, a mood word, or a "Rules:" list — stop and cut it. The brief
should be about as long as the content it carries, and no longer.

## What goes in a brief

Keep it to these, and nothing more:

- **What to build (1–2 lines):** the deliverable + its purpose / core interaction + who it's for.
- **What it must contain:** the structure (the regions, screens, or steps — *functionally*, what's
  there and what the user can do) and the **real content** — the actual copy, data, sample values,
  or inventory that must appear. This is the whole point of the brief; spend your specificity here.
- **Done when (a few bullets):** functional success — what it must *do* or *show* to be right. Not
  how it should look.
- **Close with:** "You own the visual design — mood, colour, type, layout, imagery. Show me N
  distinct directions (usually 3), and ask me if you'd like any direction." (N is up to the user.)

That's the whole brief. No Style section. No tone. No palette. No rules list.

**The one exception:** a genuine *functional* constraint the deliverable can't be right without —
"works on a phone", "shows real numbers, never lorem", "prices in CHF". Only real requirements, one
line, never dressed up as a style guide. When unsure, leave it out and let CD decide.

**Brand colours:** include them *only* if the user explicitly says to honour specific brand tokens.
Even then, one line ("use the brand's existing palette") — don't paste hex tables. Default: CD picks.

## Versioning — each version is a folder of files

CD doesn't make one file — it makes a JavaScript file plus one or more HTML pages (a landing page,
a time picker, a glyph set…). One **version** is all of those files together, in a folder named
`design_vX.Y/`, and CD writes a version header at the top of every file so any file traces back to
its version.

**Every brief is a new version.** The only question is where it starts from:

- **From scratch** (the first design, or a fresh direction) → **major** bump. First is `design_v1.0`;
  later from-scratch versions are `design_v2.0`, `design_v3.0`… CD builds the folder new.
- **Based on a previous version** (reuse its files as a base, then evolve) → **minor** bump:
  `design_v1.0` → `design_v1.1`. CD copies the prior folder as the starting point, then applies the
  brief. The earlier version stays intact, so you can always go back.

Quick refinements that don't need the before-state kept are **tweaks**, not briefs — the
`design-tweaks` skill edits the current version's files in place (no new folder).

Each version's brief is recorded at `docs/design/<slug>/vX.Y.md`, mirroring CD's folders.

## Build & version preamble — opens every copy-paste block

Every brief's copy-paste block starts with a short instruction telling CD which folder to build into
and to stamp the version header on each file. Phrased positively, in one of two forms.

**From scratch** (first design, or a fresh direction — major bump):

```
Create a folder `design_v1.0/` and build every file of this design inside it — the JavaScript file
and each HTML page. Begin each file with a version header on its first line: `<!-- design_v1.0 -->`
for HTML files, `// design_v1.0` for the JavaScript file. Keep any existing `design_v*` folders as
they are.
```

**Based on a previous version** (reuse its files, then evolve — minor bump):

```
Create a folder `design_v1.1/` by copying the files from `design_v1.0/` as the starting base, then
apply this brief. Set each file's version header to `design_v1.1` (`<!-- design_v1.1 -->` for HTML
files, `// design_v1.1` for the JavaScript file). Keep `design_v1.0/` as it is.
```

Use each file's own comment syntax for the header (`<!-- … -->` for HTML, `// …` for JS, `/* … */`
for CSS). Then the rest of the brief follows the preamble.

## Steps

1. Gather the real inputs — mainly the **content** (copy, data, inventory) and the functional
   structure, from the user and the repo. Ask at most one short question, only if something essential
   is missing. Do **not** go scavenging the repo for a colour palette to bolt on.
2. Pick the version. Look in `docs/design/<slug>/` for existing versions:
   - none yet → `v1.0`, from scratch;
   - a fresh direction → next **major** (`v2.0`), from scratch;
   - evolving the current version → next **minor** (`v1.1`), based on it.
   Confirm which case it is if it isn't obvious.
3. Write the brief into `docs/design/<slug>/vX.Y.md`: frontmatter (`version`, `base`) + the build &
   version preamble + the lean brief (what to build · what it must contain · done when) + the closing
   line + an empty `## Revisions`.
4. Output the copy-paste block in chat — the build & version preamble through the brief (everything
   above `## Revisions`).

## Record — `docs/design/<slug>/vX.Y.md`

```markdown
---
page: <name>
version: v1.0
base: scratch          # scratch | design_v1.0 (the folder this version started from)
product: <one line>
tool: Claude design
status: briefed        # briefed | iterating | chosen
---

# <Name> — design brief (v1.0)

Create a folder `design_v1.0/` and build every file of this design inside it — the JavaScript file
and each HTML page. Begin each file with a version header on its first line: `<!-- design_v1.0 -->`
for HTML files, `// design_v1.0` for the JavaScript file. Keep any existing `design_v*` folders as
they are.

**What to build** — <1–2 lines: deliverable + purpose + who it's for>

**What it must contain** — <the structure, functionally, and the real content/data/copy/inventory>

**Done when** — <a few bullets of functional success>

You own the visual design — mood, colour, type, layout, imagery. Show me 3 distinct directions, and
ask me if you'd like any direction.

## Revisions

_(none yet — design-tweaks adds change rounds here, editing the design_v1.0 files in place)_
```

The user copies from the build & version preamble through the closing line (everything above
`## Revisions`) into CD. Create `docs/design/<slug>/` if needed; use a short kebab-case `<slug>`
(`landing`, `yarn-card`, …).

## Gotchas

- **If the brief mentions a colour, a mood word, or has a "Rules:" list — you've overstepped. Cut
  it.** Those are CD's decisions. The brief is requirements + content, then hand off.
- Spend all your specificity on the **content** (real copy, data, inventory). That's what makes the
  output good — not constraints.
- Don't scavenge the repo for a palette or brand tokens to attach. Include brand colours only if the
  user explicitly asks, and then in one line.
- Catch any "avoid / don't / no / not" or anti-example → rewrite it positively or cut it.
- Always include a short "Done when" — functional success, not how it should look.
- One coherent design per brief — it can span several related files/pages, all in the one version
  folder.
- Open every copy-paste block with the build & version preamble. From scratch bumps the major;
  based on a previous version bumps the minor; quick changes that stay in the current version are
  tweaks, not a new brief.
