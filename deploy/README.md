# El Centro Leasing Proposal

Static site. Deploy with:

    npx wrangler deploy

## Structure

    wrangler.toml                     assets config — wrangler needs this to find the site
    public/index.html                 the proposal
    public/support.js                 runtime
    public/image-slot.js              image runtime
    public/image-slots.state.json     crop/framing only (small)
    public/assets/photos/             the 20 building & team photos
    public/assets/                    logos and brand marks

## Notes

- Keep `public/` intact. `index.html` loads the two scripts and fetches
  `image-slots.state.json` by relative path; move or rename either and the
  photos stop loading.
- Photos are real files in `public/assets/photos/`, referenced by the page.
  The state file now carries only crop positions, so it stays a few hundred
  bytes. Earlier it inlined every photo as base64 and grew past the 2 MB write
  ceiling, which silently dropped new photos.
- The state file deliberately has no leading dot. As `.image-slots.state.json`
  it is treated as a hidden file and several static hosts refuse to serve it.
- Must be served over HTTP. Opening `index.html` from the filesystem blocks
  the state-file fetch and the photos will not appear.
