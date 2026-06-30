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

## About the auto-tagging

The 119 characters currently in here were extracted from a visual-dictionary PDF and
auto-tagged by keyword matching (faction, status, role tags). That's a fast first pass,
not a careful read — about a third came back as "Unaligned" and tags can be off or
generic. Worth a manual pass through `characters/data/*.json` to clean up faction and
tags as you have time; the bios and art themselves are extracted as-is.

A few characters lack the multi-paragraph bios their peers have (pages that were mostly
illustration in the source PDF) — those are flagged for a manual fill-in too.

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
