# QR Pay PWA (test-first)

This is a starter Progressive Web App for creating UPI payment QR codes with a pre-filled amount. It is not connected to PhonePe, a bank, or any payment gateway.

## Included
- Shop name, UPI ID, amount, bill number
- UPI payment URI QR generation
- Download QR as PNG
- Device-local generated-QR history and CSV export
- PWA manifest and service worker
- Test-mode messaging to distinguish QR generation from verified payment

## Important limitations
- The QR encodes the amount as a UPI request (`am`) but cannot guarantee every UPI app makes it impossible for the payer to alter it.
- This starter only records that a QR was generated. It does not verify payment or mark bills paid.
- Never collect a UPI PIN, OTP, bank password, or card PIN.
- The QR library is loaded from a CDN, so the first QR generation requires internet access. For production, vendor a verified library locally and review dependencies.
- Browser local storage is not a secure accounting database and may be lost if browser data is cleared. Do not use it as the sole business ledger.
- Validate your UPI ID with your official merchant app. The app's format check does not prove that the ID exists or belongs to your shop.

## Run locally
1. Install Node.js (LTS).
2. In this folder, run `npx serve .`
3. Open the local URL printed by the command.
4. Test using a valid test UPI ID only if your UPI app/provider offers one. Do not send real money to test QR generation.
5. To install on Android, deploy over HTTPS and open the URL in Chrome. Use Chrome menu > Add to Home screen / Install app.

## Deploy for private testing
You can use a static HTTPS host (for example, GitHub Pages, Cloudflare Pages, or Netlify). Upload these files as a site. Do not put payment API secrets in this frontend.

## Production steps
1. Decide on a payment provider and request official merchant API/dynamic QR access.
2. Build a backend that creates payment requests with provider credentials stored server-side.
3. Verify payment status server-side using the provider's signed webhook/status API; check amount, currency, merchant, and transaction ID.
4. Only then mark a bill as paid. Handle duplicate webhook events safely.
5. Add authentication, HTTPS, rate limits, audit logs, backup, and privacy policy.
6. Test in the provider's sandbox before live activation.

## Files
- `index.html` - app UI and client logic
- `manifest.webmanifest` - install metadata
- `sw.js` - service worker
- `icon.svg` - app icon
