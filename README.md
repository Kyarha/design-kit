# design-kit

> A Claude Code plugin for briefing and iterating on **Claude design (CD)**. Write structured,
> positive design briefs, turn your feedback into copy-paste change requests, and keep every
> design decision recorded per version under `docs/design/`.

design-kit gives you two skills that bracket the design loop:

| Skill | Use it when | It produces |
|---|---|---|
| **`design-brief`** | Starting — or re-versioning — a page, screen, component, or asset | A structured brief that tells CD to build all its files into a fresh `design_vX.Y/` folder + a new `docs/design/<page>/vX.Y.md` |
| **`design-tweaks`** | Reacting to something CD made | Concise change requests targeting the current version's files + a new round in that version's `## Revisions` |

Records live in the repo next to your code — one Markdown file per version — so your design intent
and the full history of changes are reviewable and never lost in a chat scroll-back.

## The core principle: positive direction only

CD — like image and design models generally — follows **"do X"** far better than **"don't do Y."**
So design-kit has one hard rule: **every line says what to _create_, or what something should
_become_ — never what to avoid.** The skills actively catch any "don't / avoid / no / not" or
anti-example and rewrite it into its positive form ("use real colour swatches as the imagery"
instead of "don't use stock photos").

It also keeps a clean division of labour:

- **You** specify requirements and content — the concrete stuff: sections, real copy, data, the
  actual inventory. Specificity here is what makes the output good.
- **CD** invents the visual design. Briefs stay specific about _what must be there_ and open about
  _how it looks_.

## Versioning, so you can always go back

A CD design isn't one file — it's a **folder of files** (the JavaScript file plus the HTML pages:
landing page, time picker, glyph set…). design-kit treats that whole folder as one **version**,
`design_vX.Y/`, and has CD write a version header at the top of every file so any file traces back
to its version.

**Every brief is a new version.** The only question is where it starts:

- **From scratch** — the first design, or a fresh direction — bumps the **major** number:
  `design_v1.0`, then `design_v2.0`, `design_v3.0`. CD builds the folder new.
- **Based on a previous version** — reuse its files as a base, then evolve — bumps the **minor**
  number: `design_v1.0` → `design_v1.1`. CD copies the prior folder as the starting point; the
  earlier version stays intact, so you can always go back.
- **Tweaks edit the current version in place** — quick changes where you don't need the before-state
  kept. Every change request names the current folder (`Update the files in design_v1.0/: …`), so CD
  refines the right version and never an old one.

The current version and what it's based on live in each version file's `version:` / `base:`
frontmatter, and every file CD generates carries its `design_vX.Y` header on line one.

## Install

```
/plugin marketplace add Kyarha/design-kit
/plugin install design-kit@design-kit
```

Both skills are then available in every project on that machine. (If you previously kept these as
personal skills in `~/.claude/skills/`, delete those copies after installing so they don't
duplicate the plugin's.)

**Requirements:** Claude Code with plugin support, plus access to Claude design (CD) — the tool you
paste the briefs and change requests into.

## How it works — a worked example

You don't invoke anything special: just tell Claude Code what you want (or run
`/design-kit:design-brief` directly).

**1. Brief it.** _"Brief a mobile landing page for Lanora, my hand-dyed yarn shop."_ The
`design-brief` skill writes `docs/design/landing/v1.0.md` and hands you a copy-paste block:

```
# Landing — design brief (v1.0)

Create a folder `design_v1.0/` and build every file of this design inside it — the JavaScript file
and each HTML page. Begin each file with a version header on its first line: `<!-- design_v1.0 -->`
for HTML files, `// design_v1.0` for the JavaScript file. Keep any existing `design_v*` folders as
they are.

A mobile-first landing page for Lanora, a small-batch hand-dyed yarn shop. Its job: greet a
first-time visitor and lead them into the collection. Lanora sells limited seasonal colourways to
knitters and crocheters who care about craft.

Audience & tone: hobbyist makers who value craft and colour; warm, tactile, calm.

Layout: a hero with the shop name, one line of positioning, and a primary call to action; a strip
of three featured colourways with name + price; a short "how it's dyed" trust note; a footer with
newsletter sign-up.

Content:
- Hero line: "Small-batch yarn, dyed by hand in Geneva."
- Featured colourways: Mistral (CHF 28), Lavande (CHF 26), Ardoise (CHF 30)
- Trust note: "Every skein dyed in batches of twelve."

Style: warm, tactile, calm — earthy palette, generous whitespace, real product photography.

Rules: mobile-first; Swiss-franc prices; accessible contrast; crisp at small sizes.

Done when:
- The hero communicates what Lanora sells in one glance
- The three colourways read as the heart of the page
- It feels handcrafted and calm, not mass-market

Show me 3 distinct directions.
```

**2. Paste into CD.** Copy everything from the build-and-version preamble down to (but not
including) `## Revisions`, paste it into Claude design, and let it generate the directions —
all built into `design_v1.0/`, each file headed `design_v1.0`.

**3. Tweak it.** _"The hero feels cramped and the green buttons are too cold."_ The
`design-tweaks` skill turns that into a positive change request aimed at the current folder:

```
Update the files in `design_v1.0/`:
- Make the hero headline larger and give it more breathing room
- Use a warmer, earthier green for the primary buttons
- Move the "Shop the collection" button directly under the headline
```

CD edits the files in `design_v1.0/` in place, and the round is appended to that version's file.

**4. Repeat — or re-version.** Quick changes stay tweaks. When you want a fresh direction or a safe
checkpoint, brief again: `design-brief` makes `design_v1.1/` (based on v1.0) or `design_v2.0/` (from
scratch), leaving v1.0 intact.

## What gets recorded

After the tweak above, `docs/design/landing/v1.0.md` looks like this — brief at the top as the
version's intent, revisions accumulating below:

```markdown
---
page: landing
version: v1.0
base: scratch            # scratch | design_v1.0 (the folder this version started from)
product: Lanora — an online shop for hand-dyed yarn
tool: Claude design
status: iterating        # briefed | iterating | chosen
---

# Landing — design brief (v1.0)

Create a folder `design_v1.0/` and build every file of this design inside it — the JavaScript file
and each HTML page. Begin each file with a version header on its first line: `<!-- design_v1.0 -->`
for HTML files, `// design_v1.0` for the JavaScript file. Keep any existing `design_v*` folders as
they are.

… the full brief from step 1 …

Show me 3 distinct directions.

## Revisions

### R1 — warmer, roomier hero · design_v1.0
- Make the hero headline larger and give it more breathing room
- Use a warmer, earthier green for the primary buttons
- Move the "Shop the collection" button directly under the headline
```

Each version gets its own file under `docs/design/landing/`, so `v1.0.md`, `v1.1.md`, `v2.0.md` sit
side by side — mirroring CD's `design_v*/` folders.

## Repository layout

```
.claude-plugin/plugin.json        plugin manifest (name, version, author)
.claude-plugin/marketplace.json   one-plugin marketplace (git-subdir → this repo)
skills/design-brief/SKILL.md      the briefing skill
skills/design-tweaks/SKILL.md     the change-request skill
.github/workflows/release-please.yml   automated changelog + version bump + tagged release
```

## Releases

Versioning is automated with [release-please](https://github.com/googleapis/release-please).
Conventional-commit messages on `main` (`feat:`, `fix:`, …) drive the changelog, bump the version
in `plugin.json`, and cut a `vX.Y.Z` tag. You generally don't touch the version by hand.

## License

No license is declared yet. Until one is added, all rights are reserved by the author — add a
`LICENSE` file if you intend others to reuse this.
