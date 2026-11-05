# Gold Events – repository notes

Static, single-file site: all markup, CSS and JavaScript live in `index.html`
(listings and the "pay" step are simulated in the browser — no backend, no
database, no build step).

## Running it

`docker compose -f docker-compose.base44.yml up -d`

- One `python:3.12-alpine` service runs `python -m http.server 3000` over the
  checkout on host port 3000.
- Python's `http.server` is used on purpose: the sandbox checkout is mode 0700
  root, so a server that drops privileges (nginx's `nginx` user) returns 403.
- No build step: edits to `index.html` appear on a browser reload.
- Verify with `curl -s http://localhost:3000/ | grep -q 'Gold Events'`.

## Notes

- The page was originally `gold-events-directory (1).html`; it was renamed to
  `index.html` so `/` resolves (also required by GitHub Pages, which the `CNAME`
  history suggests is the deploy target).
- No test or lint tooling in the repo.
