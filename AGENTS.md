# Gold Events Directory

## Overview
A single static HTML file (`gold-events-directory (1).html`) — an event professionals directory with search, category/country filters, business detail dialogs, and a listing-submission form with **real PayPal checkout** (PayPal Smart Buttons via the JS SDK). No backend, no build step.

## Running in Base44
- Served by `nginx:alpine` (bind-mounted from the repo root) on host port 3000.
- The compose startup runs `envsubst` on `nginx.conf.template` to inject `PAYPAL_CLIENT_ID` into the nginx `sub_filter` directive, which replaces the `__PAYPAL_CLIENT_ID__` placeholder in the served HTML at runtime.
- A symlink `index.html -> gold-events-directory (1).html` is created so nginx serves it as the default page.
- No live-reload dev server; edits to the HTML are reflected on page refresh (or call `reload_preview`).
- **Secret:** `PAYPAL_CLIENT_ID` — PayPal REST app client ID from developer.paypal.com. Defaults to `test` (PayPal sandbox) via `.env.base44-defaults`; user provides the real live client ID via the dashboard.

## Verify
- `curl http://localhost:3000/` returns the HTML page with the PayPal SDK loaded (`client-id=...`).
- Open a plan dialog ("Choose Featured") — PayPal Smart Buttons should render inside the modal.
- The page renders the directory: hero search, category chips, business cards, and pricing plans.

## Going Live
1. Create a PayPal REST app at developer.paypal.com → My Apps & Credentials → Live tab → Create App.
2. Copy the Client ID and set it as the `PAYPAL_CLIENT_ID` secret in the Base44 dashboard.
3. Deploy the docker-compose stack to any server that runs Docker (e.g., a VPS, AWS, DigitalOcean).
4. Ensure port 3000 (or your chosen port) is publicly accessible and HTTPS is configured (e.g., via a reverse proxy like Caddy or nginx with Let's Encrypt).
