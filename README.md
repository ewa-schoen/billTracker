# Bill Tracker

A simple monthly checklist for the payments you have to make: electric bill, mortgage, swimming, and so on.

Add each payment once. Tick it when you've paid. The app records the date, and the list starts fresh every month so you can always see whether everything has been paid.

It runs as an installable app on Android, works offline, and keeps all your data on your own phone. No account, no ads, no tracking.

## Features

- **Monthly checklist** that renews itself automatically, so there is nothing to reset
- **Paid date recorded** when you tick a payment (you can correct it if you paid on another day)
- **Add, edit and remove** payments, or skip one for a single month
- **One-time payments** as well as recurring ones
- **History** of previous months, so you can check that everything was paid
- **Optional amounts and due days**, with overdue and due-soon hints and a running total of what's left
- **Backup and restore** to a file
- **Works offline** and follows your phone's light or dark mode

## Install on Android

1. On your phone, open **https://ewa-schoen.github.io/billTracker/** in **Chrome**.
2. Tap the **⋮** menu (top right) and choose **Install app**. On some versions this is **Add to home screen**, then **Install**.
3. Open Bill Tracker from your home screen like any other app.

After the first visit it works without internet.

## Your data

Everything you enter is stored only on your phone, inside the app. Nothing is uploaded, and the website only delivers the app itself.

Because of that, uninstalling the app or clearing Chrome's site data erases your payments. Use **Settings → Save backup file** now and then, and **Restore from backup file** to bring your data back, for example on a new phone.

## Publishing on GitHub Pages

The install link above only works once GitHub Pages is switched on for this repository. You only need to do this once:

1. Open the repository's **Settings → Pages** (<https://github.com/ewa-schoen/billTracker/settings/pages>).
2. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
3. Choose the **main** branch and the **/ (root)** folder, then **Save**.
4. Wait a minute or two. GitHub then shows the live address at the top of that page: `https://ewa-schoen.github.io/billTracker/`.

The app files (`index.html`, `manifest.webmanifest`, `sw.js` and the `icons` folder) must stay in the root of the repository, as they are now.

### Updating

Change the files in the repository, and edit `sw.js` so the `CACHE` version name changes (for example `bill-tracker-v1` to `bill-tracker-v2`). Phones then pick up the new version the next time the app is opened. Saved data is not affected.

## Troubleshooting

- **No "Install app" option:** make sure you opened the `https://ewa-schoen.github.io/billTracker/` address in Chrome, and that Chrome is up to date. If the app is already installed, the menu shows **Open** instead.
- **The page shows 404:** GitHub Pages isn't switched on yet, or it was switched on a moment ago. Check the steps above and give it a few minutes.
- **The app doesn't show my latest changes:** bump the version name in `sw.js` as described above, then close and reopen the app.
- **My data disappeared:** clearing Chrome data or uninstalling removes it. Restore from a backup file. If the app ever moves to a different web address, it starts empty, so restore your backup there.

## Built with

Plain HTML, CSS and JavaScript in a single file. No frameworks, no dependencies, no network requests. It is a Progressive Web App (web manifest plus service worker), and data is saved in the browser's `localStorage`.
