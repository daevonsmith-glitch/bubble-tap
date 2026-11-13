# Bubble Tap

Color-changing bubble tap puzzles and free play for kids and people who stim.

- **Android:** GitHub builds the `.apk` for you on its own servers. You don't need Android Studio.
- **iPhone:** Cloudflare Pages hosts the game, and you install it from Safari with **Add to Home Screen**. It gets its own icon, opens full-screen and works offline.

---

## 1. Android APK with GitHub

1. Create a new repository on github.com (for example `bubble-tap`).
2. Upload **everything in this folder** to it, including the hidden `.github` folder.
   - From a computer: unzip, then drag all files onto the repo's *Add file → Upload files* page. On a Mac, press **Cmd + Shift + .** in Finder to show the `.github` folder.
   - Or use git: `git init && git add . && git commit -m "Bubble Tap" && git branch -M main && git remote add origin https://github.com/YOU/bubble-tap.git && git push -u origin main`
3. Open the repo's **Actions** tab. The **Build Android APK** run starts by itself; if not, open it and tap **Run workflow**. It takes about 5–8 minutes.
4. When it shows a green ✓, open the run, scroll to **Artifacts** and download **BubbleTap-android**. It's a zip with `BubbleTap.apk` inside.
5. On the Android phone, open `BubbleTap.apk`. If asked, allow *Install unknown apps* for your browser or file app.

### A permanent download link (GitHub Release)
Create a tag that starts with `v`. On the website: **Releases → Draft a new release → Choose a tag → type `v1.0.0` → Create new tag → Publish**. The workflow then attaches `BubbleTap.apk` to that release. Anyone can download it from:
`https://github.com/YOU/bubble-tap/releases/latest`

### Optional: signed release for Google Play
The basic APK is fine for installing on your own phones. Google Play needs a signed `.aab`:

1. Make a keystore once, on any computer with Java, and **keep it safe forever**. You can't update the app on Play without it.
   `keytool -genkey -v -keystore bubbletap.keystore -alias bubbletap -keyalg RSA -keysize 2048 -validity 10000`
2. Turn it into text: `base64 -w0 bubbletap.keystore` (Mac: `base64 -i bubbletap.keystore`).
3. In the repo, go to **Settings → Secrets and variables → Actions** and add:
   `KEYSTORE_BASE64` (that text), `KEYSTORE_PASSWORD`, `KEY_ALIAS` (`bubbletap`), `KEY_PASSWORD`.
4. The next run also produces `BubbleTap-release.apk` and `BubbleTap-play-store.aab`. Upload the `.aab` in the Google Play Console.

Before publishing on Play, change `appId` in `capacitor.config.json` to a unique name you own, e.g. `com.yourbusiness.bubbletap`. It can't change after the first Play upload.

---

## 2. iPhone app with Cloudflare Pages

**Option A – connect to GitHub (updates itself every time you change the repo)**
1. In the Cloudflare dashboard go to **Workers & Pages → Create → Pages → Connect to Git**.
2. Pick the `bubble-tap` repo.
3. Set **Framework preset:** None, **Build command:** *(leave empty)*, **Build output directory:** `www`.
4. Tap **Save and Deploy**. You'll get a link like `https://bubble-tap.pages.dev`.

**Option B – no GitHub needed**
**Workers & Pages → Create → Pages → Upload assets**, name the project, then upload the `www` folder (or `bubble-tap-www.zip`).

**Install on iPhone**
Open the `pages.dev` link in **Safari** → tap **Share** → **Add to Home Screen**. The game shows a reminder bar for this on iPhones. On Android, Chrome shows an **Install** button.

**Why not an App Store `.ipa`?** Apple only lets you build iPhone apps with Xcode on a Mac, and the App Store needs a paid Apple Developer account ($99/year). Cloudflare can't build one. If you get that later, run `npm install && npx cap add ios && npx cap open ios` on a Mac and archive it in Xcode. The Home Screen version is the same game, for free.

---

## What's in here
| Path | What it is |
|---|---|
| `www/` | The game itself (Cloudflare serves this folder) |
| `.github/workflows/android-apk.yml` | Tells GitHub how to build the APK |
| `capacitor.config.json`, `package.json` | Wraps the game as an Android/iOS app |
| `assets/` | App icon and splash screen source images |

Bubble Tap collects no data, shows no ads and needs no account.
