# Home Budget — iPhone offline web app (PWA)

## What this is
A **web app**, not a native iOS app. It stores financial records in the iPhone Safari/Home Screen app's **IndexedDB**, not in a remote database. The app shell is cached by a service worker so it can open offline after the first successful installation. It is **not encrypted** and has no login or family sync.

## Important iPhone limitation
Apple iOS does **not** install a PWA directly from a ZIP or a `file://` HTML file. To install the app, its static files must be served **once over HTTPS** (or locally from a development server for testing). This does **not** require Python, a database server, or a paid hosting service. A static host stores the application code; your entered financial records remain on your device. A static host operator can change served code, so use a trusted host and do not store sensitive financial credentials.

## Installation from iPhone
1. Unzip the package in the iPhone Files app.
2. Upload the **contents** of this folder (index.html, sw.js, manifest.webmanifest, icons/) to an HTTPS static website host that supports these file types, such as GitHub Pages. The exact mobile upload steps depend on the host and may require a computer.
3. In **Safari**, open the HTTPS site while connected to the internet. Wait for it to load completely. Reload once to allow the offline cache to finish installing.
4. Safari Share > **Add to Home Screen** > Add. Launch Home Budget from the new Home Screen icon.
5. Enter a harmless sample expense, close the app, turn on Airplane Mode, reopen the Home Screen app and verify the entry remains. Turn Airplane Mode off afterward.
6. In Settings inside the app, export a JSON backup to **Files**, ideally outside the browser's storage and on a regular schedule. Test restoring a backup with sample data before using the app for important records.

## Limitations and safety
- **Do not** use Safari Private Browsing for your financial records. Browser/site data can be deleted by the OS or user. Removing the Home Screen app or clearing website data may erase records.
- Backups contain **unencrypted financial information**. Store them somewhere private and protected. Do not enter bank passwords, full card numbers or other credentials.
- There is no automatic multi-device synchronization. Each family member using a separate iPhone will have separate records.
- Service-worker caching provides offline app loading only; it does not guarantee persistent data storage. Test thoroughly before relying on it.
- App updates may require opening the site online again. Always back up before updating.
- This is an early-stage application; test all financial calculations and backups with dummy data before relying on it.

## Data model
Uses the original 11 IndexedDB stores and existing receipt + optional item detail workflow. Receipt totals count once in reports. Includes income, expenses, detailed expenses, expense types, items, family members, credit cards, bills, debts, repayments and budgets.
