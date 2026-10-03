# Karigar privacy notice — draft for project review

**Do not publish this notice until the bracketed publisher/contact details and retention choices are completed.** This is a product draft, not legal advice or a claim of compliance with every applicable law.

## Information the current app handles

- Account name, email address, artisan/buyer role, and optional town or district.
- Password verifier (a salted scrypt hash; the original password is not stored).
- Product details, listing photos, available stock, and order history.
- Session token (stored as an HttpOnly cookie in the browser and as a one-way hash on the server).
- Basic server request logs, which can include the network address supplied by the hosting platform.

The current order form does not collect a delivery address or card/UPI details. The app should never store payment credentials. Payment processing, once enabled, is handled by the selected payment provider.

## Where information is stored and shared

Hosted account, product, and order records are stored in the project’s configured Supabase Postgres database. Public product photos are stored in the `karigar-products` public bucket so marketplace visitors can view them. Hosting and database providers process technical data to operate the service. Razorpay would receive checkout and payment details only after its integration is enabled and users choose to pay.

## Choices and requests

Users should be able to ask the project operator to correct or delete account information. Order, fraud-prevention, and financial records may need to be retained for a defined period; the project operator must choose and disclose that period before launch. Product photos are publicly viewable while their listings remain published.

## Publisher details to complete before launch

- Publisher / responsible organization: **[add name]**
- Contact email for privacy and account requests: **[add monitored email]**
- Data retention periods: **[set periods for accounts, orders, server logs, and backups]**
- Effective date and a link to the final privacy notice: **[add]**

