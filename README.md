# Bubble Tap 🫧

Color-changing bubble puzzles, free play and Bubble Rush for kids and anyone who stims. Works on phones, tablets and iPads, upright or sideways, fully offline.

| Path | What it is |
|---|---|
| `www/` | The game itself (Cloudflare serves this folder) |
| `www/privacy.html` | Privacy policy page (fill in the two blanks) |
| `.github/workflows/android-apk.yml` | Builds the Android APK and the Play Store bundle on GitHub |
| `.github/workflows/ios-build.yml` | Builds the iPhone + iPad app on GitHub's Macs and sends it to TestFlight |
| `assets/` | App icon and splash screen for Android and iOS |
| `capacitor.config.json`, `package.json` | Wrap the game as an Android/iOS app (Capacitor 8, Android 16 target) |
| `STORE-GUIDE.md` | Step by step: GitHub, Cloudflare, Google Play, App Store |

## Quick start
1. Upload `bubble-tap.zip` to the GitHub repo, then add the two build files (STORE-GUIDE.md step 0D).
2. **Actions → Build Android APK** runs by itself. When it's green: **Releases → Bubble Tap (latest build) → BubbleTap.apk**.
3. Cloudflare Pages → connect the repo → output directory `www` → share the link. On iPhone/iPad: Safari → Share → Add to Home Screen.

## Updating the game
Edit `www/index.html`, and change `VERSION` in `www/sw.js` (for example to `bubble-tap-v7`) so installed copies pick up the change. Every change on `main` builds a new APK automatically.
