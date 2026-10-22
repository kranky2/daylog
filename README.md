# Daylog

A single-file web app that logs your day as timeblocks, with tags you create yourself. Data is saved as JSON to this GitHub repo, one file per day per person.

## Setup

1. Create a repo called `daylog` (private is fine) and upload these files, keeping the folder structure.
2. Turn on GitHub Pages (Settings → Pages → Deploy from branch → `main` / root) so `index.html` is served at `https://kranky2.github.io/daylog/`.
   - Pages on a private repo needs a paid plan. If you're on the free plan, make the repo public, or host the page elsewhere and only keep the data private. The data is only readable through the API with a token anyway, so keep anything sensitive out of it.
3. Create a fine-grained personal access token:
   - GitHub → Settings → Developer settings → Fine-grained tokens
   - Repository access: **Only select repositories** → `daylog`
   - Permissions: **Contents: Read and write**. Nothing else.
   - Set an expiry date.
4. Open the page on your phone or laptop. The setup screen appears on first load. Enter owner, repo, token, and "Tom", then save.

## Daughter's device

1. Create a second token the same way, or use a separate private repo for her data. A separate repo is the cleaner option. It keeps her token from touching your data at all.
2. Open the same page on her device, or open `…/daylog/?who=child`, and in setup choose **Child**.
3. Her blank tag list lives in `data/child/tags.json`. She creates her own tags with the "New tag" box.

## Using it

- **Add block:** set start and end (it pre-fills from your last block), give it a title, set focus 1–5, tap tags, and press Add block. Each save is a git commit.
- **New tag:** type it in "New tag" and press Enter or "+ Tag". It is created and selected in one step.
- **Edit tags:** tap "Edit tags", then tap a chip to remove it from the list. Existing blocks keep the text.
- **By tag:** the summary at the bottom totals hours per tag for the day.

## Data layout

```
data/tom/tags.json
data/tom/2026/10/2026-10-22.json
data/child/tags.json
data/child/2026/10/2026-10-22.json
```

Day file:

```json
{ "date": "2026-10-22", "who": "tom", "blocks": [
  { "start": "09:00", "end": "10:30", "title": "Backtest UnR filter", "tags": ["trading","build"], "focus": 4 }
]}
```

## Notes

- The token lives in each device's browser storage. Use "Remove" on a shared device, or clear site data when you're done with it.
- Saves use the GitHub Contents API. If two devices save the same day at once you'll get a conflict message. Press ← and → to reload the day, then add the block again.
- Analytics script (`stats.py`) isn't in this version yet. The JSON layout is designed so it can be added next.
