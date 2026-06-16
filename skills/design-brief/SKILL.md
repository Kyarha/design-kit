---
name: design-brief
description: Write a structured design brief for Claude design (CD) and record it per version under docs/design/<page>/ that the user copies into CD. Use when the user wants to brief Claude design, start designing a page/screen/component/asset, or get a prompt to paste into CD. The brief is sectioned and as detailed as the deliverable needs (intro, audience/tone, structure, content, style, rules, and a "Done when" success list) but every line is phrased as what to create — never what to avoid — and it leaves the visual design for CD to invent. Every brief is a new design version: it opens with a preamble telling CD to build all its files (a JS file + the HTML pages) into a design_vX.Y folder and stamp a version header in each file — from scratch (major bump) or based on a previous version (minor bump). Pairs with the design-tweaks skill for iterating on the result.
---

# design-brief — write a brief for Claude design (CD)

Writes a structured brief the user pastes into Claude design, recorded per version in the project so
every version's intent is preserved. (Iterating on a version is the separate `design-tweaks` skill.)

## The one hard rule

**Positive direction only.** Every line says what TO create. Never tell CD what to avoid — no
"don't / avoid / no / not / never", no anti-examples, no "good vs bad" comparisons. CD follows
"do X" well and handles "don't do Y" badly. Rephrase any avoid-X as the positive alternative
("use real colour swatches as the imagery", not "don't use stock photos").

## Versioning — each version is a folder of files

CD doesn't make one file — it makes a JavaScript file plus one or more HTML pages (a landing page,
a time picker, a glyph set…). One **version** is all of those files together, in a folder named
`design_vX.Y/`, and CD writes a version header at the top of every file so any file traces back to
its version.

**Every brief is a new version** — that's the model. The only question is where it starts from:

- **From scratch** (the first design, or a fresh direction) → **major** bump. The first design is
  `design_v1.0`; later from-scratch versions are `design_v2.0`, `design_v3.0`… CD builds the folder
  new.
- **Based on a previous version** (reuse its files as a base, then evolve) → **minor** bump:
  `design_v1.0` → `design_v1.1`. CD copies the prior folder as the starting point, then applies the
  brief. The earlier version stays intact, so you can always go back.

Quick refinements that don't need the before-state kept are **tweaks**, not briefs — the
`design-tweaks` skill edits the current version's files in place (no new folder).

Each version's brief is recorded at `docs/design/<slug>/vX.Y.md`, mirroring CD's folders.

## How detailed

A brief is a **structured document with sections** — as detailed as the deliverable needs. A
specific component or asset set can be very precise (list the exact elements/inventory); an
early page exploration is lighter. Be concrete about **requirements and content**; leave the
**visual design for CD to invent**. Always ask for a few directions (usually 2–3). Mobile-first
by default. Start shallow and go deeper later.

## Sections (use the ones that fit the deliverable; all phrased positively)

- **Intro (1–2 lines):** what to produce + the core interaction/purpose + a line of product context.
- **Audience & tone:** who it's for; the feeling (a few adjectives).
- **Layout / structure:** the key regions / sections / screens to include — what the deliverable
  contains and what the user can do. Leave the styling to CD.
- **Content:** the real elements, copy, data, or inventory that must appear (the actual list of
  items, sample data, etc.). Specificity here is what makes the output good.
- **Style:** palette / tokens / typography / imagery direction when they exist and you want them
  honoured. For an early exploration keep this light (a few adjectives) and invite range —
  introduce exact tokens later as change requests once a direction is chosen.
- **Rules:** constraints as positive statements (mobile-first, metric units, crisp at small
  sizes, accessible contrast…).
- **Done when:** a short bullet list of success criteria — what "good" looks like, stated
  positively. Always include this.
- Close with: "Show me N distinct directions."

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

1. Gather/infer inputs from the user and the repo (`CLAUDE.md`, `docs/product-vision.md`,
   `docs/brand-guidelines.md`). Ask at most one short question, only if something essential is
   missing.
2. Pick the version. Look in `docs/design/<slug>/` for existing versions:
   - none yet → `v1.0`, from scratch;
   - a fresh direction → next **major** (`v2.0`), from scratch;
   - evolving the current version → next **minor** (`v1.1`), based on it.
   Confirm which case it is if it isn't obvious.
3. Write the brief into `docs/design/<slug>/vX.Y.md`: frontmatter (`version`, `base`) + the build &
   version preamble + the sections + "Show me N distinct directions." + an empty `## Revisions`.
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

<the structured brief: intro + the sections that fit + "Show me N distinct directions.">

## Revisions

_(none yet — design-tweaks adds change rounds here, editing the design_v1.0 files in place)_
```

The user copies from the build & version preamble through the brief (everything above
`## Revisions`) into CD. Create `docs/design/<slug>/` if needed; use a short kebab-case `<slug>`
(`landing`, `yarn-card`, …).

## Gotchas

- Catch any "avoid / don't / no / not" or anti-example → rewrite it positively or cut it.
- Specific about requirements and content; open about the visual look — give CD room to design.
- Hold exact brand tokens for early explorations (add them later via change requests once a
  direction is picked). For a tightly-specified component or asset set, include them up front.
- Always include a "Done when" list — it's the positive acceptance checklist.
- One coherent design per brief — it can span several related files/pages (landing page, time
  picker, glyph set), all in the one version folder.
- Open every copy-paste block with the build & version preamble, so CD builds into the version
  folder and headers each file. From scratch bumps the major number; based on a previous version
  bumps the minor; quick changes that stay in the current version are tweaks, not a new brief.
