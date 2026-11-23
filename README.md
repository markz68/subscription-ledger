# Subscription Ledger

Version 1.0.1. A browser-local subscription and membership tracker. New installations always start empty. No personal starter list is included in this repository.

## Features

- Overview with monthly and annual cost equivalents, next 30 days of expected charges, category totals, and a subscription shelf.
- Search and filter subscriptions; add, edit, and delete records with confirmation for deletion.
- Monthly, quarterly, semiannual, annual, and multiyear billing; other imported month intervals are retained.
- Included services and benefits with no extra charge; record their bundle in the included-through field. Enter the paid bundle once and mark its component services as included to avoid double counting.
- Active, trial, paused, and canceled statuses. Access end dates, cancellation deadlines, trial and promotion prices.
- Management links, billing providers, payment nicknames, notes, and light/dark/system themes.
- Validated JSON backup and restore; CSV spreadsheet export. Imports replace the current list after confirmation. One prior local copy is preserved before import, restore, or deletion.
- Installable PWA with an offline asset cache after the first successful online load.

## Use and install

Open the deployed app, choose **Add subscription**, and enter the details you know. Blank prices and dates are allowed. Use the top-right gear for Settings, backups, imports, and appearance. To load a personal starter file, use **Settings → Import / restore JSON** and confirm the replacement.

On Android, use your browser's Install app or Add to Home screen command. On Windows, use the install command in a supporting browser such as Chrome or Edge. On iPad/iPhone, use Safari's Share → Add to Home Screen. Installation availability depends on the browser and hosting authentication.

## Costs and renewal forecasts

Currency is USD. Equivalents use the entered price divided by the billing interval in months. They do not represent a payment ledger. Paused and canceled items are excluded; included services add zero cost. An unknown price is excluded and flagged. Expired access dates exclude a record from active totals. The active count includes included services, trials, and bundle entries.

Upcoming charges require an active or trial status, a known price, auto-renew enabled, and a billing date. The forecast repeats from that date, preserving its day-of-month and clamping short months. The next-30-days interval includes today and excludes the day 30 days later. A passed offer date uses its recorded future price; an unknown future price is flagged for review. Rates are never obtained automatically. Trial end does not itself create a charge; enter the actual first billing date.

An item with auto-renew off still contributes its current ongoing budget equivalent while active, but no future charge is forecast. Canceled items contribute no future cost even while access remains. Missing billing dates do not mean there are no upcoming bills. Service costs, taxes, fees, renewal dates, and real charges must be checked with the provider.

## Privacy and backup

Records are saved in localStorage under `subscription-ledger:data:v1`, separately per browser and origin. No banking access, Google Drive sync, analytics, background notifications, or account credentials are implemented. Keep passwords and full card numbers out of the app. Download JSON backups regularly; browser data can be cleared or evicted. The recovery copy is on the same device and is not an external backup.

JSON files contain personal subscription data. Keep them private. CSV is for viewing and cannot be restored as an app backup. Invalid backups are rejected before mutation. If saved data is corrupt, normal saves are blocked, raw JSON can be downloaded, and a valid import can restore operation. A failed storage write does not replace the in-memory list.

## Development and release

Buildless ES modules in the repository root. Run `npm test` for schedule, cost, validation, and CSV checks. Serve through a static HTTP server for development, for example `python -m http.server 8000`. `sw.js` versions the app's offline cache; bump it with the visible version for releases. Updates wait for existing app windows to close before the new worker activates. No versioned filenames are used. GitHub Pages serves `main` from the repository root. No build step or dependencies are required.

## Initial release

1.0.1 moves hosting to GitHub Pages. The initial version adds the dashboard, management, bundles, promotional rates, local backups, recovery, CSV export, themes, and PWA assets. Google Drive sync is deferred. On-device Android/Windows install and offline behavior require verification after publication.

## GitHub Pages setup

Enable Pages in repository Settings → Pages using **Deploy from a branch**, **main**, **/ (root)**. The intended app address is `https://markz68.github.io/subscription-ledger/`; publication must be verified separately from saving code. Relative asset paths, manifest scope, and service worker registration support this project subpath.
