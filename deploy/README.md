# El Centro Leasing Proposal

Static site. Deploy with:

    npx wrangler deploy

## Structure

    wrangler.toml                     assets config — wrangler needs this to find the site
    public/index.html                 the proposal
    public/support.js                 runtime
    public/image-slot.js              image runtime
    public/image-slots.state.json     the dropped photos (19)
    public/assets/                    logos and brand marks

## Notes

- Keep `public/` intact. `index.html` loads the two scripts and fetches
  `image-slots.state.json` by relative path; move or rename either and the
  photos stop loading.
- The state file deliberately has no leading dot. As `.image-slots.state.json`
  it is treated as a hidden file and several static hosts refuse to serve it.
- Must be served over HTTP. Opening `index.html` from the filesystem blocks
  the state-file fetch and the photos will not appear.
