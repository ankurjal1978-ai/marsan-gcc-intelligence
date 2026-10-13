# MarSan GCC Intelligence

A public-facing, single-page GCC assessment with server-side calculations and lead capture. The browser receives results only after a company-email lead is saved. The savings model stays in the server code; it is visible to anyone with access to this public repository, so MarSan should review the assumptions before a campaign.

## Test locally

Install Node.js 22 or newer, then run `npm install`. Initialize the local database with `npx wrangler d1 execute marsan-gcc-leads --local --file=migrations/0001_init.sql`, followed by `npm run dev`. Open the local address shown by Wrangler.

## Publish a test link

Use a Cloudflare account with Workers and D1 enabled. Create a D1 database named `marsan-gcc-leads`, replace the placeholder `database_id` in `wrangler.jsonc` with the ID returned by Cloudflare, and apply `migrations/0001_init.sql` to the remote database. Run `npm run deploy`. Cloudflare will provide a public `workers.dev` test URL. MarSan's web team can later connect `gcc.marsanglobal.com` through their DNS provider and Cloudflare dashboard.

The frontend and API must stay on the same origin. The API rejects cross-origin submissions. Leads are stored in D1 for authenticated export; there is no public export endpoint and no automatic email delivery.

## Website and campaigns

Link from the MarSan homepage to the published assessment URL. For campaigns, append UTM parameters, such as `?utm_source=linkedin&utm_medium=paid_social&utm_campaign=gcc_intelligence`. The assessment stores those parameters with each lead. Step 2 accepts up to three objectives.

Before a broad campaign, replace the brief privacy notice with MarSan's approved policy and have MarSan Finance approve the provisional savings assumptions in `src/gcc-model.js`. Work-email checks block common personal and disposable domains but do not verify ownership or deliverability.
