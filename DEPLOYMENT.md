# Online setup plan

The app supports hosted Postgres and shared product-photo storage while keeping its current local SQLite mode for development.

## Services

- **Render** runs the Python website/API and provides HTTPS.
- **Supabase Postgres** stores shared user, product, session, and order data.
- **Supabase Storage** stores public product listing photos in a `karigar-products` bucket.

## Prepare accounts and hosted data

1. Create a Supabase project and choose a region appropriate for the project. Save its database connection string from **Connect**; for a hosted service, use the Session Pooler connection option if direct IPv6 connectivity is unavailable. Keep the password private.
2. In Supabase **SQL Editor**, run `supabase-schema.sql`.
3. In **Storage**, create a bucket named `karigar-products`, mark it public for product photos, and set allowed content types to JPEG, PNG, and WebP with a 5 MB limit. Public read access is intentional for marketplace listing photos; uploads are made only by the backend with a server-only key.
4. From the Supabase project settings, copy the project URL and server-side service-role key. Never put the service-role key in `index.html`, `app.js`, GitHub, or a message. It bypasses Storage access policies and must stay in the hosting provider's secret environment settings.
5. Put this folder in a private GitHub repository. Do not add `.env`, API keys, database URLs, personal customer exports, or the local `data/` and `uploads/` folders.
6. In Render, create a Web Service from that repository. `render.yaml` supplies the build/start commands and health check. Set `DATABASE_URL`, `SUPABASE_URL`, and `SUPABASE_SERVICE_ROLE_KEY` in Render's Environment settings. Render sets `PORT`; leave it alone. Keep `KARIGAR_SECURE_COOKIE=true`.
7. Deploy and check `/healthz`. Confirm signup, sign-in, product listing/photo upload, and order history using accounts you control.

The cloud database starts empty. Local demo accounts, passwords, listings, photos, and orders are not copied automatically. Review records and intentionally migrate only what you want to keep.

## Direct UPI checkout

- An artisan saves a UPI ID in **My shop**. At checkout, the buyer can hand off to an installed UPI app such as Google Pay, PhonePe, Paytm, or another compatible app. The payment goes directly to the artisan's UPI ID; Karigar does not receive or split the money.
- This is a live UPI handoff, not a sandbox. When a buyer approves a payment in their UPI app, real money may move. Do not use it for a test payment unless the buyer and artisan agree to the amount and destination.
- The website cannot securely verify a direct UPI transfer by itself. A buyer's “I have paid” action is only a report. The artisan must independently check their UPI app or bank statement before confirming the order. Karigar reduces stock only after the artisan confirms receipt.
- The current direct-payment flow does not provide automatic payment confirmation, payment refunds, dispute handling, delivery/shipping tools, or platform commission collection. Do not describe an order as paid until the artisan confirms it. Decide how cancellations, returns, failed transfers, fees, and any platform income will work before accepting real customers.

## Security and privacy

- Use HTTPS and secure session cookies in the hosted environment. Login/signup attempts are rate-limited; state-changing JSON requests check same-origin; responses include basic browser security headers.
- Keep hosting credentials private and rotate any key accidentally committed or shared.
- Product photos in the public bucket are visible to anyone with their URL. Do not upload private documents or people's sensitive images there.
- Finish `PRIVACY-NOTICE-DRAFT.md`, add a monitored contact, choose data-retention periods, and add account deletion/data-request handling before collecting real customers' data.
- Back up the hosted database and decide what recovery plan and operating costs apply to the selected service tiers.

## Local use

Use `run.bat` for local development. It continues to use the local SQLite file and `uploads/` directory unless cloud environment variables are configured. After changing server-side code, restart the server so it loads the latest changes.