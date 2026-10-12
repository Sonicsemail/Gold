# Gold Events Directory

## Overview
A single static HTML file (`gold-events-directory (1).html`) — an event professionals directory with search, category/country filters, business detail dialogs, and a listing-submission form with simulated payment. No backend, no build step, no dependencies.

## Running in Base44
- Served by `nginx:alpine` (bind-mounted from the repo root) on host port 3000.
- The compose startup creates a symlink `index.html -> gold-events-directory (1).html` so nginx serves it as the default page.
- No live-reload dev server; edits to the HTML are reflected on page refresh (or call `reload_preview`).
- No secrets or external services required.

## Verify
- `curl http://localhost:3000/` returns the HTML page.
- The page renders the directory: hero search, category chips, business cards, and pricing plans.
