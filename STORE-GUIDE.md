# It’s Bubble Pop – publishing on Google Play and the App Store

Step by step for both stores, publishing under your own name (personal accounts), including how the game gets built.

**What publishing as a person means:** no D-U-N-S number is needed, but your legal name is shown publicly as the seller on both stores, and Google makes every new game run a 14-day closed test with at least 12 testers before it can go public.

**What's already done:** the game (phones, tablets and iPads, upright or sideways), the new "It’s Bubble Pop" logo in colors, the Android build, the iPhone and iPad build, the Google signing key, the privacy policy page, the store text below, and the graphics for both stores.

**It’s Bubble Pop is for children as well as adults**, so both stores apply their children's rules. The game already meets them: no ads, no accounts, no purchases, no data collected, no links out of the game, and it works offline.

---

## Part 0. Before either store (do once)

### 0A. Fill in the privacy policy
In `www/privacy.html`, replace `[YOUR NAME]` with your name and `[YOUR CONTACT EMAIL]` with an email parents can write to.

### 0B. Decide the app ID
It is set to `com.bubbletap.app` in `capacitor.config.json`. Both stores use it as the game's permanent ID, and **it can never be changed after the first upload**. Keep it, or change it now (for example `com.yourname.bubbletap`: lowercase letters, numbers and dots only).

### Name on phones
The full name **It’s Bubble Pop** is used in both stores and inside the game. Under the icon on iPhones and iPads (and on the web version's home-screen icon) it shows as **Bubble Pop**, because iPhones cut off longer names.

### 0C. Clean up the GitHub repository
Your repository `daevonsmith-glitch/Bubble-Tap` still has the first test upload in it. In the repo on github.com:
1. Open `.github/workflows/blank.yml` → **⋯ → Delete file** → **Commit changes**. It's GitHub's example file and doesn't build anything.
2. Open `bubble-tap-app (1).zip` → **⋯ → Delete file** → **Commit changes**. It's an old version of the game.

### 0D. Put the new version on GitHub
1. **Add file → Upload files**, choose **`bubble-tap.zip`** (the zip itself, not unzipped), **Commit changes**.
2. **Add file → Create new file**. Name it exactly `.github/workflows/android-apk.yml`, paste the whole contents of **android-apk.yml**, **Commit changes**.
3. **Add file → Create new file** again. Name it exactly `.github/workflows/ios-build.yml`, paste the whole contents of **ios-build.yml**, **Commit changes**.
4. **Settings → Actions → General → Workflow permissions** → **Read and write permissions** → **Save**.

Step 2 starts the first Android build. It unpacks the zip into the repository (about 5–8 minutes). On a phone, do all of this in Safari or Chrome, not the GitHub app.

### 0E. Put it on Cloudflare (the free web/iPhone version and the privacy link)
1. dash.cloudflare.com → **Workers & Pages → Create → Pages → Connect to Git** → pick **Bubble-Tap**.
2. Framework preset **None**, build command **empty**, build output directory **`www`** → **Save and Deploy**.
3. You get a link like `https://bubble-tap.pages.dev`. Your privacy link is `https://bubble-tap.pages.dev/privacy.html`. Both stores need it.

Do this after the first GitHub build has finished, so the `www` folder exists in the repository.

---

## Part 1. Google Play

### 1A. Open the account (once – skip if you already did it for Word Pop: Definition)
1. Go to **play.google.com/console** and sign in with the Google account that should own the games. You must be 18 or older.
2. Choose **Personal** as the account type.
3. Enter a developer name (what players see), your legal name, address, email and phone. Verify the email and phone with the codes Google sends.
4. Pay the **$25** fee. It is charged once, with no renewal.
5. Upload a government photo ID when asked.
6. If asked, confirm you have a real Android phone by signing in to the **Play Console** app on it.

### 1B. Build the Play Store file
1. Open **play-store-signing-key.txt** (sent separately – never put it in GitHub).
2. In the GitHub repository: **Settings → Secrets and variables → Actions → New repository secret**.
3. Add `KEYSTORE_PASSWORD` with the password from the file.
4. Add `KEYSTORE_BASE64` with the long single line from the file.
5. **Actions → Build Android APK → Run workflow**.
6. After about 5–8 minutes, open **Releases → It’s Bubble Pop (latest build)**. You get two files:
   - `ItsBubblePop.apk` – install it on your own Android phone or tablet to test.
   - `ItsBubblePop.aab` – the file you upload to Google Play.

Every run gives the game a higher version number automatically, which Google requires. The build targets Android 16 (API level 36), which Google Play has required for new apps since August 31, 2026.

### 1C. Create the app and listing
1. Play Console → **Create app** → name `It’s Bubble Pop`, language English (United States), **Game**, **Free**. Tick the declarations.
2. **Store settings:** category **Games → Puzzle** (or **Casual**). Contact email: yours.
3. **Main store listing:** paste the text from "Store text" below. Upload:
   - App icon: `app-icon-512.png`
   - Feature graphic: `feature-graphic-1024x500.png`
   - Phone screenshots: `phone-1.png` to `phone-4.png`
   - 7-inch tablet screenshots **and** 10-inch tablet screenshots: `tablet-1.png` to `tablet-4.png` (the same four files in both). This is what lets Google show the game as tablet-ready.
4. **App content** (Policy → App content):

| Form | Answer |
|---|---|
| Privacy policy | `https://YOUR-CLOUDFLARE-LINK/privacy.html` |
| App access | All functionality is available without special access |
| Ads | No, my app does not contain ads |
| Content rating | Category **Game**. Answer **No** to every question (no violence, fear, sexuality, language, drugs, gambling, user interaction, sharing location, purchases). Expect **Everyone / PEGI 3**. |
| Target audience | Tick every age group **from 5 and under through 18 and over** (it's made for kids and adults who stim). |
| Families policy | Accept. It’s Bubble Pop already follows it (no ads, no data, no outside links). |
| Data safety | Does your app collect or share any of the required user data types? **No**. Is all data encrypted in transit? Not applicable – nothing is sent. |
| Government, financial, health, news | No |

Because children are in the target audience, Google reviews the game under its **Families** rules. That review can take a few extra days.

### 1D. The 14-day closed test (required for new personal accounts)
1. **Use the same 12+ testers as your other games.** The rule counts for each game separately, so add them to It’s Bubble Pop too.
2. **Testing → Closed testing → Create track** (or use **Closed testing – Alpha**).
3. **Testers:** add your email list with the 12+ Gmail addresses.
4. **Create new release**, upload `ItsBubblePop.aab`, accept **Play App Signing** when asked, release notes "First release", **Save → Review → Start rollout**.
5. Copy the **opt-in link** from the Testers tab and send it to everyone. Each tester opens it, taps **Become a tester**, then installs It’s Bubble Pop from Google Play.
6. All 12 must **stay opted in for 14 days in a row**. Ask them to play a few times (on a tablet too, if anyone has one).
7. On day 14 or after: **Dashboard → Apply for production**, and answer Google's questions about the test.
8. Google usually replies within about a week.

### 1E. Go live
1. **Production → Create new release** → choose the same `.aab` from the library → release notes → countries.
2. **Send for review.** A new account's first release usually takes a few days.

---

## Part 2. Apple App Store (iPhone and iPad)

### 2A. Open the account (once – skip if you already did it)
1. Your Apple Account needs **two-factor authentication** and your **legal name exactly as on your ID**.
2. Install the **Apple Developer** app on an iPhone or iPad.
3. In the app: **Account → Enroll Now → Individual**.
4. Enter your legal name, address and phone, then scan your driver's license or other government ID.
5. Accept the agreement and pay **$99 per year**.
6. Wait for the approval email. Your legal name becomes the seller name on the App Store.
7. Sign in at **appstoreconnect.apple.com** and accept the agreements on the home page.

### 2B. Register the game with Apple
1. **developer.apple.com → Account → Certificates, IDs & Profiles → Identifiers → +**.
2. **App IDs → App**. Description `It’s Bubble Pop`. **Explicit** bundle ID: the app ID from 0B (for example `com.bubbletap.app`). No extra capabilities. **Register**.
3. **App Store Connect → Apps → + → New App**:
   - Platform: **iOS**
   - Name: `It’s Bubble Pop`. If Apple says the name is taken, use `It’s Bubble Pop: Calm Stim`.
   - Primary language: English (U.S.)
   - Bundle ID: the one you just registered
   - SKU: `itsbubblepop`
   - User access: Full access

### 2C. Connect GitHub to your Apple account
GitHub's Mac machines build and sign the app, so you don't need a Mac. **If you already made the API key for Word Pop: Definition, reuse it**: just add the same four secrets to the Bubble-Tap repository (step 7).

1. **Team ID:** developer.apple.com → **Account → Membership details** → copy the 10-character **Team ID**.
2. **API key:** App Store Connect → **Users and Access → Integrations → App Store Connect API**. If you see **Request Access**, tap it and accept.
3. **Team Keys → +**, name `GitHub`, access **Admin**, **Generate**.
4. Copy the **Issuer ID** (above the list) and the **Key ID** (in the key's row).
5. **Download API Key** → `AuthKey_XXXXXXXXXX.p8`. Apple lets you download it **only once**; keep it private and safe.
6. Open the `.p8` file in a text editor and copy all of it, including the `BEGIN` and `END` lines.
7. GitHub → Bubble-Tap → **Settings → Secrets and variables → Actions → New repository secret**:

| Secret name | Value |
|---|---|
| `APPLE_TEAM_ID` | the Team ID |
| `ASC_ISSUER_ID` | the Issuer ID |
| `ASC_KEY_ID` | the Key ID |
| `ASC_KEY_P8` | the whole contents of the `.p8` file |

### 2D. Build and test
1. GitHub → **Actions → Build iPhone and iPad app → Run workflow**. About 10–20 minutes.
2. A green check means the build was sent to App Store Connect. Apple processes it for another 15–30 minutes.
3. App Store Connect → It’s Bubble Pop → **TestFlight**. Under **Internal Testing**, create a group, add yourself, select the build.
4. Install the **TestFlight** app on your iPhone (and iPad if you have one), open the invite, install It’s Bubble Pop. Try each mode, turn the iPad sideways, and check sounds (silent switch off).

### 2E. Store listing
App Store Connect → It’s Bubble Pop → **iOS App 1.0 / Prepare for Submission**:
1. **Screenshots:** `iphone-1.png` to `iphone-4.png` into **iPhone 6.9" Display**; `ipad-1.png` to `ipad-4.png` into **iPad 13" Display**. Apple needs both because the game runs on iPad.
2. **Text:** paste the App Store text from "Store text" below.
3. **Support URL:** your Cloudflare link. **Privacy Policy URL** (App Privacy page): the `privacy.html` link.
4. **Build:** tap **+** and select the TestFlight build.
5. **App Review Information:** your name, phone, email. No sign-in needed; leave the demo account empty. Notes: "Offline game, no accounts, no data collected."
6. **Age Rating:** answer **None/No** to everything → **4+**. (For the Kids section, see step 10.)
7. **App Privacy → Get Started** → "Do you or your third-party partners collect data from this app?" **No** → **Publish**.
8. **Pricing and Availability:** Free, all countries you want.
9. **App Information → Category:** primary **Games** (subcategories **Puzzle** and **Casual**), secondary **Education**.
10. **Kids section (optional):** in the **Age Rating** questions, turn on **Made for Kids** and pick the age range **6–8**. That lists It’s Bubble Pop in the App Store's Kids section. Its extra rules (no ads, no tracking, no outside links without a parental gate) are already met. To keep the first release simple, you can skip this and add it in a later version.

### 2F. Submit
1. **Add for Review → Submit to App Review**.
2. Apple usually replies within a day or two. If they reject it, the message says why; send it to me and I'll fix it.

---

## Store text

### Google Play

**App name:** `It’s Bubble Pop`

**Short description** (80 max):

    Calming color-changing bubbles: puzzles, free play and Bubble Rush. No ads.

### App Store

**Name:** `It’s Bubble Pop`

**Subtitle** (30 max): `Calming bubble puzzles`

**Keywords** (100 max, commas, no spaces):

    stim,sensory,fidget,calm,autism,adhd,bubbles,pop,kids,toddler,colors,puzzle,relax,anxiety,tap

**Promotional text** (optional): `Tap, pop and match calming bubbles. No ads, no accounts, works offline.`

### Full description (both stores)

    It’s Bubble Pop is a calming, color-changing bubble game made for kids and anyone who stims.

    THREE WAYS TO PLAY
    • Puzzle – tap a bubble and it changes color along with the bubbles next to it. Make every bubble match. Levels grow from 3×3 to 5×5, every puzzle can be solved, and a hint is always one tap away.
    • Free Pop – no rules at all. Tap or slide your finger across the bubbles and watch them change color with a soft sound.
    • Bubble Rush – bubbles fly up across the screen. Tap or swipe through them and see how many you can pop in 30 or 60 seconds, or relax with no timer.

    MADE TO BE CALMING
    • No losing in Puzzle or Free Pop, no fail sounds
    • Choose your sound: soap-bubble pop, water bloop, musical notes or a mix
    • Calm motion setting slows down animations
    • Gentle vibration you can turn off
    • Shapes on bubbles for players who find colors hard to tell apart
    • Pick any colors you like, or use the Bright, Soft or Bold sets
    • Dark mode

    WORKS EVERYWHERE
    Phones and tablets, upright or sideways. Plays fully offline.

    SAFE FOR KIDS
    No ads, no accounts, no purchases, no chat and no data collected.

---

## Files

| File | For |
|---|---|
| `bubble-tap.zip` | The game, this guide, both build files |
| `android-apk.yml`, `ios-build.yml` | The two build files to paste in step 0D |
| `play-store-signing-key.txt`, `bubble-tap-upload.jks` | Google signing key. **Private – never in GitHub.** Back them up. |
| `app-icon-512.png`, `feature-graphic-1024x500.png` | Google Play listing |
| `phone-1` to `-4` (1080 × 1920) | Google Play phone screenshots |
| `tablet-1` to `-4` (1440 × 2560) | Google Play 7-inch and 10-inch tablet screenshots |
| `iphone-1` to `-4` (1290 × 2796) | App Store iPhone 6.9" screenshots |
| `ipad-1` to `-4` (2048 × 2732) | App Store iPad 13" screenshots |
| `AuthKey_XXXXXXXXXX.p8` | Apple API key you download in 2C. **Private.** |

## If a build fails
**Actions** → the failed run → the job → the step with the red ❌. Send me the step's name and the red lines near the bottom. On the iPhone build, the **Build and sign** step is the one most likely to need an adjustment on its first run.

## Costs

| | Google Play | App Store |
|---|---|---|
| Account | $25 once | $99 per year |
| Per game | Free | Free |
| GitHub builds | Free for public repositories | Free for public repositories |
