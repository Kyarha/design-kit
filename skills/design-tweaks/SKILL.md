---
name: design-tweaks
description: Turn the user's feedback on a Claude design (CD) result into short, copy-paste change requests, and log them in the page's version md under docs/design/<page>/ to track design decisions over time. Use when CD has produced a design and the user wants tweaks, changes, or comments to paste back into CD. Phrases every change as what to make it become (never what's wrong or what to avoid), targets the current version folder (design_vX.Y) so CD edits that version's files in place, and appends each round to the same docs/design/<page>/vX.Y.md that the design-brief skill created.
---

# design-tweaks — change requests for a Claude design (CD)

The user has a design version from CD and wants changes. Turn their notes into copy-paste change
requests for CD, and record each round in that version's md so design decisions are tracked.
(Writing the original brief — and starting a new version — is the separate `design-brief` skill.)

## Rules

1. **Positive instructions only.** Write what each element should *become*, not what's wrong —
   e.g. "make the search bar larger and centred", "use a warmer green for the primary buttons",
   "add a region selector to the header", "tighten the spacing between cards". Never
   "don't / avoid / no / not" or an anti-example. Rephrase any "stop doing X" as the positive
   change.
2. **Concise.** A short bulleted list CD can act on directly.
3. **One round = one revision entry**, so the md keeps a history of decisions.
4. **Target the current version's files in place.** Address every change request to the current
   folder (`design_vX.Y/`, from the version md's frontmatter `version`) so CD edits that version's
   files and leaves earlier versions as they are. A tweak keeps the version and its file headers
   the same. Wanting to preserve the current state before a bigger change means a *new version* —
   that's a `design-brief` based on this version, not a tweak.

## Steps

1. Identify which page and version the feedback is about → its `docs/design/<slug>/vX.Y.md` (the
   current version is the highest, or whichever the user is looking at). Read it for context,
   including the frontmatter `version` (the `design_vX.Y/` folder). If it's unclear, ask once.
2. Rewrite the user's notes as positive change requests, addressed to that version's folder.
3. Output a fenced copy-paste block for CD that names the folder.
4. **Append** a new numbered round under `## Revisions` in that same md, tagged with the version.
   Bump the frontmatter `status` to `iterating` if it isn't already.

## Change-request block (copy-paste)

```
Update the files in `design_v1.0/`:
- <change, phrased as what to do>
- <change …>
```

## Revisions log entry (append to the md)

```markdown
### R<n> — <short label / date> · design_vX.Y
- <change request sent to CD>
- <…>
```

## Gotchas

- Rephrase any "don't / avoid" into the positive change, or cut it.
- Carry only the user's own direction — don't invent colours, moods, or constraints they didn't
  give. CD still owns anything left unspecified.
- Name the current `design_vX.Y/` folder in every change request, so CD edits the right version's
  files and earlier versions stay recoverable.
- A tweak stays within the same version — leave each file's version header as it is.
- Keep the brief at the top of the version md intact; revisions accumulate below it.
- Preserving the current state before a big change is a new version — hand off to `design-brief`
  (based on this version), rather than tweaking in place.
