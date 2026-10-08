# Lèle Essentials — Final Sakura & Matcha Mask Store

## What is included

- `index.html` — **fully self-contained** premium website: all CSS, JavaScript and both authentic supplied product photographs are embedded. Upload this ONE file to preview the complete store without broken CSS/JS/image paths.
- `api/order.js` — private serverless Cash on Delivery order endpoint; validates order information and emails the store owner. It never exposes the destination inbox to shoppers.
- `api/health.js` — private API deployment status endpoint (only returns whether required variables are configured, never their values).
- `vercel.json` — Vercel project configuration.
- `.env.example` — **placeholders only**, never store secrets here.
- `assets/` — original user-supplied photographs retained separately for future editing.

## IMPORTANT: Prices and product information

The supplied photos show LAIKOU Japan Sakura Mud Mask and LAIKOU Matcha Mud Mask, both 5 g / 0.18 oz. They do not show reliable retail prices, shipping fees, full ingredients, manufacturing country, or application times. Therefore the site truthfully says **price on request** and requires the shop to confirm the final amount and delivery fee before dispatch. Product claims are attributed to the packaging, not asserted as independently verified facts. Set real prices and policies before taking fully priced orders.

## Recommended: full store with private orders on Vercel

1. Extract the ZIP. Upload `index.html`, `api/`, `vercel.json` and `.gitignore` to a **new GitHub repository** or a branch, or import the folder into Vercel. (Do not overwrite your original site without a backup.)
2. Go to [Vercel](https://vercel.com) → Add New Project → import that repository → deploy as a simple static site with serverless functions. The root `index.html` is served as the homepage and `api/order.js` is served at `/api/order`.
3. Create a [Resend](https://resend.com) account, verify a domain you control for sending, and create a private API key.
4. In **Vercel Project → Settings → Environment Variables**, set:
   - `RESEND_API_KEY`: your private Resend key.
   - `ORDER_TO_EMAIL`: **your actual private inbox** (do not put it in HTML or public GitHub files).
   - `ORDER_FROM_EMAIL`: a verified sender on your domain, e.g. `Lèle Essentials <orders@yourdomain.com>`.
   - `SEND_CUSTOMER_RECEIPT`: `true` to email the customer a confirmation acknowledgment as well.
   - `ALLOWED_ORIGINS`: optional for same-origin Vercel storefront. Set to `https://genzahnaf2009-hub.github.io` if your public storefront stays on GitHub Pages.
5. **Redeploy** after setting environment variables. Check `https://YOUR-VERCEL-SITE.vercel.app/api/health` — `configured` must be `true`.
6. Submit a test order with your own email and phone; verify the private inbox receives the request and the customer acknowledgment arrives. Do not accept real orders until this test passes.

## Alternative: keep the website on GitHub Pages

1. Upload **only `index.html`** to your existing GitHub Pages repository root. It contains its own CSS, JavaScript, and product photos, so there are no missing assets.
2. Deploy the `api/` folder as a separate Vercel project (with `vercel.json` and an `index.html` if needed for the project), and configure the environment variables above.
3. In `index.html`, find `window.LELE_ORDER_API_URL = "";` and change it to your exact Vercel endpoint, e.g. `window.LELE_ORDER_API_URL = "https://your-order-api.vercel.app/api/order";`.
4. In Vercel, set `ALLOWED_ORIGINS=https://genzahnaf2009-hub.github.io` and redeploy.
5. Commit the edited `index.html` to GitHub Pages and test a real submission.

**GitHub Pages alone cannot send secure order emails.** If you don't deploy the API, the catalog, cart, and checkout form work as a demonstration, but submitting an order clearly reports that private ordering is not activated. It will **not** show a false success message.

## Customer-facing experience

- Exactly two masks, actual supplied product photographs, responsive editorial design, product details and image enlargement.
- Cart quantities saved locally on the customer's device.
- Checkout requires customer name, email, Bangladesh phone, division, district, area, full address, optional note, and explicit COD acknowledgment.
- No online payment option and no card data collected.
- Private order reference and optional customer email acknowledgment after the merchant email is accepted.
- Contact: +880 1970-155970 and +880 1729-228117. The public site displays **Veeneria · Order support** but never exposes the recipient inbox.

## Production readiness

The backend performs server-side validation, input escaping, request-size limits, allowed-origin checks, and a hidden spam-trap field. For a higher-volume live store, add bot protection (e.g., Turnstile), durable order storage, proper rate limiting, and a clear privacy/returns/delivery policy. Email is not a durable order database. Confirm rights to use the supplied product photographs commercially and verify all packaging claims.
