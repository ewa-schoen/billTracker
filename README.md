# Bill Tracker

A monthly checklist of the payments you have to make (electric bill, mortgage, swimming, …).

- You add each payment once. It comes back **unticked at the start of every month** by itself.
- Tick a payment when you have paid it. The app **records the date and weekday** you ticked it.
- Every month keeps its own history, so you can look back and see whether you paid everything.
- You can **remove** a payment for good, or **skip** it for one month only.
- Works **offline**. Your data stays **on your phone**. Nothing is sent anywhere.

## What this is (and isn't)

This is a **Progressive Web App (PWA)**: a small web app that Chrome can install on your Android home screen. Once installed it has its own icon, opens full screen like any other app, and works without internet.

It is **not** an `.apk` file. Building an APK needs the Android SDK, which is not available where this was made. A PWA installs the same way for you and is simpler to update. If you specifically want an `.apk`, see [Option D](#option-d-turn-it-into-a-real-apk-optional).

## What's in the folder

```
bill-tracker/
├── index.html               the whole app
├── manifest.webmanifest     tells Android how to install it (name, icon, colours)
├── sw.js                    makes it work offline
├── icons/                   app icons
└── README.md                this file
```

Keep all of these files together in one folder.

---

## Installing on your Android phone

Android only lets a web app be **installed** if it is opened from a secure address (`https://…` or `localhost`). Just copying the files to the phone and tapping `index.html` is not enough for a proper install. Pick one option below.

### Option A: Put it online for free, then install (recommended)

Free hosting is the easiest route. The page itself is public, but **your payments are never uploaded**: they are stored only in your phone's own storage. Anyone who finds the address would just see an empty tracker.

**Using Netlify Drop** (no coding, about 2 minutes):

1. On a computer, unzip `bill-tracker.zip`.
2. Go to <https://app.netlify.com/drop> and sign in or create a free account (a site dropped without an account is only temporary).
3. Drag the whole `bill-tracker` folder onto the page.
4. Netlify gives you an address like `https://something-random.netlify.app`. Open it once to check it works.

**Or using GitHub Pages:**

1. Create a free GitHub account and a new **public** repository.
2. Upload all the files (keep the `icons` folder).
3. In the repository go to **Settings → Pages**, choose your main branch and the root folder, and save.
4. After a minute your app is at `https://YOUR-USERNAME.github.io/REPOSITORY-NAME/`.

**Then, on your phone:**

1. Open the address in **Chrome**.
2. Tap the **⋮** menu (top right) → **Install app** (on some versions: **Add to home screen**, then **Install**).
3. Confirm. The Bill Tracker icon appears on your home screen. Open it from there from now on.

After the first visit it works completely offline.

### Option B: No hosting, no computer: run it on the phone with Termux

The address `http://localhost` counts as secure, so you can serve the app from the phone itself.

1. Install **Termux** from **F-Droid** (<https://f-droid.org/packages/com.termux/>). The Google Play version is outdated.
2. Copy `bill-tracker.zip` to the phone (USB cable, Google Drive, WhatsApp to yourself, etc.) and extract it. In the Files app: long-press the zip → **Extract**.
3. In Termux, run:
   ```
   termux-setup-storage
   pkg install python
   cd ~/storage/downloads/bill-tracker
   python -m http.server 8080
   ```
   (Adjust the `cd` path if you extracted the folder somewhere other than Downloads. Leave Termux running.)
4. Open Chrome and go to `http://localhost:8080`.
5. Tap **⋮ → Install app**.
6. Once installed and opened once, you can close Termux. The installed app runs from its offline copy.

Note: the app's data belongs to the address it was installed from. Always use the same address (`localhost:8080`), or use **Backup / Restore** (below) to move your data.

### Option C: Just try it: copy `index.html` and open it

For a quick look you can copy `index.html` to the phone and open it in Chrome (Files app → tap the file → open with Chrome).
It works, but this way it **cannot be installed**, and Android may not reliably keep your data between visits. Use Option A or B for real use.

### Option D: Turn it into a real APK (optional)

If you host the app (Option A), the free tool **PWABuilder** (<https://www.pwabuilder.com>) can package your address as an Android `.apk`. Enter your address, choose **Package for stores → Android**, and download the result. To install an APK you download yourself, Android will ask you to allow **Install unknown apps** for the app you opened it from.

---

## Using the app

| I want to… | Do this |
|---|---|
| **Add a payment** | Tap **Add payment**. Enter a name. Amount and due day are optional. |
| **Mark it paid** | Tap the circle on its row. It turns green and shows **Paid** with the date. |
| **Fix the date** (paid on another day) | Tap the green **Paid …** badge, pick the date, **Save date**. |
| **Undo a tick** | Tap **Undo** in the message at the bottom, or tap the green circle again. |
| **Skip it just this month** | Tap the payment's name → **Skip … only**. It returns next month. |
| **Stop a payment for good** | Tap the payment's name → **Remove payment…** and choose from when to remove it. Earlier months keep their history. |
| **One-time payment** | When adding, switch off **Repeats every month**. It appears only in that month. |
| **Check a previous month** | Use the arrows at the top, or tap a month under **Earlier months**. |
| **Get back to today** | Tap **Back to this month**. |

Good to know:

- **Nothing to reset.** Each month's list is built from your payments, so a new month simply starts with every payment unticked.
- **Overdue hints.** If you set a due day, unpaid payments show "Due tomorrow" or "3 days overdue", and the progress bar segment turns red.
- **Short months.** A due day of 31 automatically counts as the last day in shorter months.
- **Currency.** Set your symbol under **Settings** (the sliders icon at the top right), for example `$`, `€` or `zł`.
- Changing a payment's amount does not rewrite past months: paid months remember what you paid at the time.

## Backing up your data

Your data lives only in the app's storage on your phone. Uninstalling the app or clearing Chrome's site data erases it.

- **Settings → Save backup file** downloads a small `.json` file. Do this now and then and keep it somewhere safe (Google Drive, email to yourself).
- **Settings → Restore from backup file** loads it back, for example on a new phone.

## Updating the app

If you change any file, open `sw.js` and change `bill-tracker-v1` to `bill-tracker-v2` (and so on), then upload the files again. This makes phones download the new version instead of the saved old one. Your data is not affected.

## Troubleshooting

- **No "Install app" in the menu.** You are probably not on an `https://` or `localhost` address (see Option A or B). Also check that Chrome is up to date. If you already installed it, the option is replaced by **Open**.
- **The app doesn't seem to update.** Close it fully and reopen it twice, or bump the version in `sw.js` as above.
- **My data disappeared.** Clearing Chrome's storage or uninstalling deletes it. Restore from a backup file. Also, if you move the app to a new web address, it starts empty because the data belongs to the old address. Restore your backup there.
- **Dates look in a different format than I expect.** Dates follow your phone's language and region settings.

## Technical notes

Plain HTML, CSS and JavaScript in one file with no libraries and no internet requests. Data is kept in the browser's `localStorage` under the key `billTracker.v1`. It works in Chrome, Edge and Samsung Internet on Android, and in most modern desktop browsers too.
