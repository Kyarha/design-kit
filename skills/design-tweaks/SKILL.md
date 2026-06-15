---
name: design-tweaks
description: Turn the user's feedback on a Claude design (CD) result into short, copy-paste change requests, and log them in the page's brief md under docs/design/ to track design decisions over time. Use when CD has produced a design and the user wants tweaks, changes, or comments to paste back into CD. Phrases every change as what to make it become (never what's wrong or what to avoid), and appends each round to the same docs/design/<page>.md that the design-brief skill created.
---

# design-tweaks — change requests for a Claude design (CD)

The user has a design from CD and wants changes. Turn their notes into copy-paste change
requests for CD, and record each round in the page's brief file so design decisions are tracked.
(Writing the original brief is the separate `design-brief` skill.)

## Rules

1. **Positive instructions only.** Write what each element should *become*, not what's wrong —
   e.g. "make the search bar larger and centred", "use a warmer green for the primary buttons",
   "add a region selector to the header", "tighten the spacing between cards". Never
   "don't / avoid / no / not" or an anti-example. Rephrase any "stop doing X" as the positive
   change.
2. **Concise.** A short bulleted list CD can act on directly.
3. **One round = one revision entry**, so the md keeps a history of decisions.

## Steps

1. Identify which page the feedback is about → its `docs/design/<slug>.md`. Read it for context.
   If it's unclear which page, ask once.
2. Rewrite the user's notes as positive change requests.
3. Output a fenced copy-paste block for CD.
4. **Append** a new numbered round under `## Revisions` in that same md (keep the brief at top as
   the current intent). Bump the frontmatter `status` to `iterating` if it isn't already.

## Change-request block (copy-paste)

```
Update the <page/component>:
- <change, phrased as what to do>
- <change …>
```

## Revisions log entry (append to the md)

```markdown
### R<n> — <short label / date>
- <change request sent to CD>
- <…>
```

## Gotchas

- Rephrase any "don't / avoid" into the positive change, or cut it.
- Keep the original brief at the top intact — revisions accumulate below it. Only rewrite the
  brief if the user wants to restart the page.
- A change that points to a new direction is still a revision round; log it, don't silently
  replace the brief.
