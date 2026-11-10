# Standlo — separate customer storefront and admin portal

## Included
- `index.html` — customer-facing shopping storefront (no admin controls)
- `admin.html` — separate password-protected admin portal
- `firestore.rules` — Firestore security rules
- `firebase.json` — Hosting configuration

Both pages use Firebase project `bingo-a206a`. Customer checkout is COD only. Supplier details are stored in the admin-only `supplierSources` collection. Supplier ordering and tracking are manual; there is no unofficial Meesho API, scraping, or automatic order forwarding.

## Firebase setup
1. Enable Email/Password in Firebase Authentication.
2. Create Cloud Firestore.
3. In Authentication → Users, create the admin account and copy its UID.
4. Create `users/{ADMIN_UID}` in Firestore with `role` (string) = `admin`.
5. Publish the included `firestore.rules`.
6. Admin portal is `/admin.html`.

## Deploy with Firebase Hosting
1. Install Firebase CLI: `npm install -g firebase-tools`
2. Run `firebase login`
3. Run `firebase use bingo-a206a`
4. Run `firebase deploy --only hosting`
5. Customer site: `https://bingo-a206a.web.app/`
6. Admin portal: `https://bingo-a206a.web.app/admin.html`

## Before accepting real orders
- Confirm supplier permission and process for shipping to third-party customers.
- Confirm COD availability, delivery charges, returns/refunds and delivery timelines with the supplier.
- Add privacy, terms, shipping/return policies, contact details and applicable business/tax disclosures.
- Add Firebase App Check, stronger validation, abuse protection and server-side order validation before public launch.
- Public order creation is required for guest checkout; harden it against spam before launch.
