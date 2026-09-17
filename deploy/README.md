# El Centro Leasing Proposal

Static site, flat at the root. Deploy with:

    npx wrangler deploy

## Structure

    wrangler.toml            assets config
    index.html               the proposal
    support.js               runtime
    image-slot.js            image runtime
    image-slots.state.json   crop/framing only (small)
    assets/photos/           the 20 building & team photos
    assets/                  logos and brand marks

## Notes

- Photos are real files in `assets/photos/`, referenced directly by the page.
  The state file carries only crop positions, so it stays a few hundred bytes.
  Earlier it inlined every photo as base64 and grew past a 2 MB write ceiling,
  which silently dropped newly added photos.
- The state file deliberately has no leading dot. As `.image-slots.state.json`
  it is treated as a hidden file and several static hosts refuse to serve it.
- Must be served over HTTP. Opening `index.html` from the filesystem blocks
  the state-file fetch and the crops fall back to centered.
- When replacing a deployed copy, delete the old files first so nothing stale
  is left behind.
