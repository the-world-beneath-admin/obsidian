# Website Public Ticket Entrypoints Report

## Scope

Shared website/platform usability pass for live support-ticket entry points.

## What Changed

- Added a public support-ticket form to `/contact/#support-ticket`.
- Added `Submit Ticket` buttons to:
  - `/community/forum/`
  - `/community/forum/board/`
  - `/community/forum/thread/`
- Added a shared footer `Submit Ticket` link pointing to `/contact/#support-ticket`.
- Added a shared `site.js` form handler that submits to `POST /api/support/tickets` with page/client context.

## Deployment

Deployed live on 2026-05-22.

Cloudflare Worker version:

```text
db0aa42d-cdd7-4c61-b7d9-ae899bf16695
```

## Checks

```powershell
node --check assets\js\site.js
powershell -ExecutionPolicy Bypass -File .\scripts\verify-local.ps1
npx wrangler deploy
curl.exe "https://the-world-beneath.com/contact/?deploy-check=20260522-ticket"
curl.exe "https://the-world-beneath.com/community/forum/?deploy-check=20260522-ticket"
curl.exe "https://the-world-beneath.com/assets/js/site.js?deploy-check=20260522-ticket"
curl.exe -X POST https://the-world-beneath.com/api/support/tickets -H "Content-Type: application/json" --data "{}"
```

## Results

- Local verification passed.
- Live deploy succeeded.
- Cache-busted live checks confirmed the contact form, forum button, footer link, and JS submit handler.
- Empty support-ticket API post returned validation `400`, confirming the route still rejects bad submissions without creating junk data.

## Remaining

- Manual browser submission with a real test ticket.
- Authenticated admin queue smoke to verify the ticket appears and can be resolved.
- Game-side Report Bug buttons/client helper.
