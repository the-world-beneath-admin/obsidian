# Website Admin Support Live Deploy Report

## Scope

Shared website/platform production deploy for:

```text
C:\Users\yrred\Desktop\Marketing\Websites\the-world-beneath-site
```

## What Changed

- Applied pending remote D1 migrations `0015` through `0020` to `twb-core`.
- Deployed the Worker and static assets to the live custom domains.
- Admin-support foundation is now live:
  - admin member stats
  - manual email-prep/export
  - support-ticket schema/API
  - admin ticket queue UI
  - support-ticket API contract notes

## Deployment Details

Remote D1 database:

```text
twb-core
f03dc009-7e57-4c9d-89a9-113fd847fd23
```

Live Worker version:

```text
3f30b86b-f992-4b49-8787-bfe5110d5900
```

Routes:

- `the-world-beneath.com`
- `www.the-world-beneath.com`

## Checks Run

Before deploy:

```powershell
powershell -ExecutionPolicy Bypass -File .\scripts\verify-local.ps1
npx wrangler d1 migrations list twb-core --remote
npx wrangler deploy --dry-run
```

Deploy:

```powershell
npx wrangler d1 migrations apply twb-core --remote
npx wrangler deploy
```

After deploy:

```powershell
curl.exe -I https://the-world-beneath.com/
curl.exe -I https://the-world-beneath.com/admin/
curl.exe -s -o NUL -w "%{http_code} %{content_type}\n" https://the-world-beneath.com/api/admin/users
curl.exe -s -o NUL -w "%{http_code} %{content_type}\n" https://the-world-beneath.com/api/admin/support/tickets
curl.exe -s -o NUL -w "%{http_code} %{content_type}\n" -X POST https://the-world-beneath.com/api/support/tickets -H "Content-Type: application/json" --data "{}"
npx wrangler d1 migrations list twb-core --remote
```

## Results

- Local verification passed.
- Wrangler dry-run passed.
- Remote migrations applied cleanly.
- Live deploy succeeded.
- `/` returned `200`.
- `/admin/` returned `200`.
- Anonymous `/api/admin/users` returned `401`.
- Anonymous `/api/admin/support/tickets` returned `401`.
- Empty public ticket submission returned validation `400` and did not create a ticket.
- Remote D1 migration list reported no migrations to apply.

## Risks

- Manual admin-session browser smoke has not yet been performed.
- Game-side Report Bug buttons are not wired yet.
- Public support-ticket submission should receive rate limiting / abuse controls before broad public exposure.
- Email remains manual-prep/export only; no live email sending is implemented.
- The website repository still has a broad pre-existing dirty working tree, so avoid broad staging, reverting, or cleanup without a separate review.

## Next Gate

Run an authenticated admin browser smoke test with seeded users and a real test ticket, then wire the first game-side Report Bug button/client helper.
