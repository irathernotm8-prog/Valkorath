# Valkorath: Chronicles of Light and Shadow

A personal D&D-inspired worldbuilding archive — story, lore, and an interactive character catalog.

## What's in here

```
Valkorath-World/
├── catalog/
│   └── index.html          ← the interactive character browser
├── characters/
│   ├── catalog.json         ← all characters, combined (used by the catalog app)
│   ├── data/                ← one JSON file per character
│   │   └── reign-002.json
│   └── art/                 ← one portrait per character, matched by slug
│       └── reign-002.jpg
└── story/
    └── valkorath-story.md   ← the full narrative, chapter by chapter
```

## Viewing the character catalog

The catalog is a static HTML page that reads `characters/catalog.json` over `fetch()`.
Browsers block local file reads for security, so **don't just double-click `index.html`** —
run a tiny local server first:

```bash
# from the Valkorath-World folder
python3 -m http.server 8000
```

Then open **http://localhost:8000/catalog/** in your browser.

(If you'd rather not deal with a server at all, GitHub Pages will serve it correctly once
the repo is pushed — see below.)

## Adding or editing a character

1. Drop the portrait into `characters/art/` (jpg or png).
2. Add or edit the matching file in `characters/data/your-character-slug.json`:

```json
{
  "slug": "your-character-slug",
  "name": "Character Name",
  "epithet": "Their Title",
  "faction": "Last Bastion",
  "status": "Active",
  "tags": ["Warrior", "Leader"],
  "bio": [
    "First paragraph of their backstory.",
    "Second paragraph."
  ],
  "art": "art/your-character-slug.jpg",
  "source_page": null
}
```

3. Run the rebuild script to regenerate `catalog.json` from the individual files:

```bash
python3 scripts/build_catalog.py
```

## About the accuracy pass

119 characters total. **111 of them have now been corrected through an actual
read-through of `story/valkorath-story.md`** — faction, status (Active/Fallen/Corrupted),
and in most cases an added closing sentence grounding them in what actually happens to
them in the story. Two new factions came out of that read-through that weren't in the
original first-pass tagging: **Malakar's Legion** (Malakar operates independently of
Drexl -- the story is explicit that Drexl considers him "a nuisance," not an ally) and
**The Kabal** (a group of Drexl's former lieutenants who broke away and were later killed
by Drexl for the betrayal).

The remaining **9 characters genuinely don't appear in the story text at all** (checked
directly, not assumed): Calador, Dark Reign, Gothar, Kleon, Lucan, Lumbar, Nyx, Ouken, and
Vornath. They're visual-dictionary-only characters for now -- their original first-pass
tags are left as a placeholder, since there's nothing in the narrative yet to correct them
against.

One naming bug was also fixed: the character on visual-dictionary page 59 was mislabeled
"Kandor" in the page header even though the bio is entirely about a character named
**Alexis** -- corrected to Alexis. The story's actual Kandor (a displaced knight from King
Valerius II's era, original wielder of the sword Thunderstrike) is a different, separate
character on page 84, and was left as-is.

Worth knowing: an early automated attempt at this pass (matching faction/status by simple
keyword proximity to a character's name) produced confidently wrong answers -- e.g. it
nearly tagged David, a Last Bastion founder, as one of Drexl's own forces, simply because
Drexl's name appears near his often in battle scenes. That approach was discarded entirely
in favor of actually reading the relevant passages for each character.

A few characters still lack the multi-paragraph bios their peers have (pages that were
mostly illustration in the source PDF, with little to no body text) -- those are flagged
for a manual fill-in.

## Keeping this private

This repo is meant to stay **private** while the world is in progress:

- On GitHub: create the repo as **Private** (Settings → visibility, or choose Private at
  creation). Private repos are free and unlimited on GitHub's free tier.
- If you ever turn on **GitHub Pages** to host the catalog as a real website: on a free
  GitHub plan, Pages sites are public even if the repo is private. If you want the hosted
  version to stay private too, you'd need GitHub Pages' private-Pages support, which
  requires a paid plan (Pro/Team/Enterprise) — otherwise just keep using the local-server
  method above, which stays fully private with a free account.

## The story

`story/valkorath-story.md` has the full narrative, organized by chapter with Markdown
headers (`## Chapter N: Title`) so it renders cleanly on GitHub or in any Markdown viewer.
