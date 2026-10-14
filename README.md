# MarSan GCC Intelligence

The assessment frontend is a single self-contained HTML file: [index.html](index.html). It includes the page layout, CSS, and browser JavaScript. [privacy.html](privacy.html) is self-contained too. Download [MarSan-GCC-Single-HTML-Source.zip](MarSan-GCC-Single-HTML-Source.zip) for the complete frontend, server-side calculation, lead capture, database migration, and deployment configuration. The older Portable-Source ZIP is superseded.

HTML alone cannot securely save leads or keep the savings calculation on the server. The included JavaScript server accepts a valid company email, stores the lead, then returns results. It has no OTP or automatic email delivery. The source is public, so MarSan should review the provisional savings assumptions before launching a campaign.

## Test locally

Install Node.js 22 or newer. Unzip the current source package, run npm install, initialize the local database using the migration in migrations/0001_init.sql, then run npm run dev.

## Publish a test link

Use a Cloudflare account with Workers and D1 enabled. Create a D1 database named marsan-gcc-leads, replace the placeholder database_id in wrangler.jsonc with the ID returned by Cloudflare, and apply migrations/0001_init.sql to the remote database. Run npm run deploy. Cloudflare will provide a public workers.dev test URL. The web team can later connect gcc.marsanglobal.com.

The frontend and API must stay on the same origin. Leads are stored in D1 for authenticated export; there is no public export endpoint. For LinkedIn campaigns, append UTM parameters to the published assessment URL. Before a broad campaign, replace the brief privacy notice with MarSan's approved policy.
