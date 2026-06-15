---
name: design-brief
description: Write a structured design brief for Claude design (CD) and record it as a per-page md file under docs/design/ that the user copies into CD. Use when the user wants to brief Claude design, start designing a page/screen/component/asset, or get a prompt to paste into CD. The brief is sectioned and as detailed as the deliverable needs (intro, audience/tone, structure, content, style, rules, and a "Done when" success list) but every line is phrased as what to create — never what to avoid — and it leaves the visual design for CD to invent. Pairs with the design-tweaks skill for iterating on the result.
---

# design-brief — write a brief for Claude design (CD)

Writes a structured brief the user pastes into Claude design, recorded in the project so the
intent is versioned. (Iterating on the result is the separate `design-tweaks` skill.)

## The one hard rule

**Positive direction only.** Every line says what TO create. Never tell CD what to avoid — no
"don't / avoid / no / not / never", no anti-examples, no "good vs bad" comparisons. CD follows
"do X" well and handles "don't do Y" badly. Rephrase any avoid-X as the positive alternative
("use real colour swatches as the imagery", not "don't use stock photos").

## How detailed

A brief is a **structured document with sections** — as detailed as the deliverable needs. A
specific component or asset set can be very precise (list the exact elements/inventory); an
early page exploration is lighter. Be concrete about **requirements and content**; leave the
**visual design for CD to invent**. Always ask for a few directions (usually 2–3). Mobile-first
by default. One deliverable per brief; start shallow and go deeper later.

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

## Steps

1. Gather/infer inputs from the user and the repo (`CLAUDE.md`, `docs/product-vision.md`,
   `docs/brand-guidelines.md`). Ask at most one short question, only if something essential is
   missing.
2. Write the brief into `docs/design/<slug>.md` as the body (sections above), with light
   frontmatter and a trailing `## Revisions` section left empty for `design-tweaks`.
3. Output the brief in chat as a fenced copy-paste block (the title down to before `## Revisions`).

## Record — `docs/design/<slug>.md`

```markdown
---
page: <name>
product: <one line>
tool: Claude design
status: briefed   # briefed | iterating | chosen
---

# <Name> — design brief

<the structured brief: intro + the sections that fit + "Show me N distinct directions.">

## Revisions

_(none yet — the design-tweaks skill adds change rounds here)_
```

The user copies the title through the brief (everything above `## Revisions`) into CD. Create
`docs/design/` if needed; use a short kebab-case `<slug>` (`landing`, `yarn-card`, …).

## Gotchas

- Catch any "avoid / don't / no / not" or anti-example → rewrite it positively or cut it.
- Specific about requirements and content; open about the visual look — give CD room to design.
- Hold exact brand tokens for early explorations (add them later via change requests once a
  direction is picked). For a tightly-specified component or asset set, include them up front.
- Always include a "Done when" list — it's the positive acceptance checklist.
- One deliverable per brief.
