# Karigar — artisan marketplace website

This is the multi-file, server-backed version of Karigar. The frontend is split across `index.html`, `styles.css`, and `app.js`. `server.py` serves those files and provides accounts, product listings, photos, stock, and orders. Local development uses Python/SQLite; hosted configuration can use Supabase Postgres and Supabase Storage.

## Run on Windows

1. Double-click `run.bat`.
2. Keep the server window open while using the site.
3. Open <http://127.0.0.1:8000> on this computer.

The first run creates `data/karigar.sqlite3`. Product photos are stored in `uploads/`.

## Share on the same Wi-Fi

Use the computer's local IPv4 address (for example, `http://192.168.1.3:8000`) from another phone or laptop connected to the same Wi-Fi. Keep `run.bat` running, and allow Python through the computer's firewall if prompted. Accounts and products are shared because both devices connect to this server.

## Demo the buy flow

1. Create an account as an Artisan and publish a product.
2. Sign out and create a separate Buyer account.
3. In My shop, save the artisan UPI ID. Then sign in as a Buyer, open the product, and choose Pay with UPI apps. The phone should offer installed UPI apps such as Google Pay, PhonePe, or Paytm.
4. Sign back in as the Artisan and open Orders/My shop to view it.

A UPI order stays pending until the artisan checks their UPI app and confirms receipt. Tapping the UPI app link can transfer real money; this is not sandbox checkout. Stock is reduced only after the artisan confirms receipt. Catalog photo scanning and listing text suggestions run in the browser as guided prototype features; semantic object recognition by a live AI model is not connected.

## Online hosting

See `DEPLOYMENT.md` for cloud setup steps and `PRIVACY-NOTICE-DRAFT.md` for the incomplete notice that must be reviewed before launch. Direct UPI handoff is available when an artisan has saved a UPI ID. It does not automatically verify payments or provide refunds, disputes, or marketplace payouts. Read DEPLOYMENT.md before using it with customers.
