# SinghaniaB2B Firebase starter

Responsive wholesale computer-products storefront plus a separate admin page. Uses Firebase Authentication and Cloud Firestore. Product photos are external image URLs, not Firebase Storage uploads.

## Setup
1. In Firebase Console, create/select your project and register a Web app.
2. Enable Authentication → Sign-in method → Email/Password.
3. Create a Cloud Firestore database.
4. Copy your web config into `firebase-config.js`.
5. Create an admin user in Authentication, copy its UID, and replace `PASTE_ADMIN_AUTH_UID_HERE` in both `firebase-config.js` and `firestore.rules`.
6. Paste `firestore.rules` into Firestore → Rules and Publish.
7. Deploy this folder with Firebase Hosting or another web server. Don't open `index.html` directly as a `file://` URL because the app uses JavaScript modules.
8. Visit `admin.html`, sign in with the configured admin user, add products and paste direct public image URLs. Admin can edit hero/banner, promo strip and popup content.

## Features
- Attractive responsive storefront, category filters and search
- Registration collects name, phone, shop/business name, address, email and password
- User-specific cart saved in that browser, account profile, order history and return requests
- Separate admin dashboard for products, orders, return requests and editable banner/popup content
- Firestore rules restrict customers to their own profile/orders/return requests; products carry an owner UID

## Notes
- Demo products appear until Firebase is configured or if the catalog is empty. They are not real inventory.
- Image links must be direct, publicly accessible, and allowed to be embedded by their host. URLs can expire or stop working.
- This is a starter, not an audited production commerce system. Order totals and prices are calculated in the browser; before accepting real money, add server-side price verification, stock validation, payment verification and other trusted backend functions. Don't store card data in Firestore.
- Order submission is a request only; payment is not integrated. Add delivery, tax, privacy, terms and return policies before public launch.


ACCOUNT APPROVAL WORKFLOW
1. Publish the included firestore.rules in Firebase Console → Firestore Database → Rules.
2. New registrations create a users/{uid} profile with status pending and are signed out immediately.
3. In admin.html → Account approvals, approve/reject requests. Approved customers can then sign in and see prices.
4. Rules require status=approved for order and return creation. Price hiding is also implemented in app.js; do not rely on hiding alone for security.
