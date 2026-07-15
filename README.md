# CyberMind AI — Android App (WebView Wrapper)

This is a ready-to-build Android Studio project that wraps your live
Streamlit app (`https://cybermind-ai.streamlit.app/`) in a native Android
app shell.

## 🚀 Don't have Android Studio? Build the APK for free with GitHub (no install needed)

This project includes a GitHub Actions workflow (`.github/workflows/build-apk.yml`)
that builds the APK automatically in the cloud. Steps:

1. Create a **new GitHub repository** (e.g. `cybermind-ai-android`) — can be public or private.
2. Upload/push this **entire folder's contents** to that repo (same way you did for the
   main CyberMind-AI project — `git init`, `git add .`, `git commit`, `git push`, or use
   GitHub's "Upload files" button in the browser for a quick drag-and-drop).
3. Go to your repo on GitHub → click the **"Actions"** tab.
4. You should see a workflow run start automatically (triggered by your push). If not,
   click **"Build APK"** on the left → **"Run workflow"** → **"Run workflow"** button.
5. Wait 3–5 minutes for it to finish (green checkmark ✅).
6. Click on the completed run → scroll down to **"Artifacts"** → download
   **`CyberMindAI-app-debug`** — this is a zip containing your `app-debug.apk`.
7. Unzip it, transfer `app-debug.apk` to your Android phone, and install it
   (allow "Install from unknown sources" if prompted the first time).

That's it — no Android Studio, no local setup, completely free (GitHub Actions gives
free build minutes for both public and private repos).

**Note:** this builds a debug APK, good for installing and testing on your own phone.
For an actual Play Store submission you'll eventually need a *signed* release build,
which requires a one-time keystore setup — happy to walk through that separately when
you're ready to publish.

---

## What's included
- **Splash screen** — branded dark background with your shield logo, shown
  for ~1.2s on launch.
- **WebView wrapper** (`MainActivity.java`) that loads your live Streamlit
  URL, with:
  - Pull-to-refresh
  - Loading progress bar
  - Offline detection with a retry button
  - Native Android back button navigates WebView history (not just exits the app)
  - File picker support so **File Scanner** and **QR Code Scanner** uploads work
  - Camera permission handling
- **Adaptive app icon** (vector-based shield, no external image files needed)
- App ID: `com.cybermind.ai`, version `1.0.0`

## How to build the APK

1. Open **Android Studio** → **Open** → select this folder
   (`CyberMindAI-Android`).
2. Let Gradle sync (first time may take a few minutes — it downloads Gradle
   8.4 automatically via the wrapper).
3. Once synced, go to **Build → Build Bundle(s) / APK(s) → Build APK(s)**.
4. When it finishes, click **locate** in the notification, or find the file at:
   `app/build/outputs/apk/debug/app-debug.apk`
5. Transfer this APK to your Android phone and install it (you may need to
   allow "Install from unknown sources" the first time).

## For a Play Store–ready release build (signed AAB)

1. **Build → Generate Signed Bundle / APK**
2. Choose **Android App Bundle (AAB)**
3. Click **Create new...** to generate a keystore (a one-time signing key —
   **back this up somewhere safe**, you'll need the exact same one for every
   future update of this app).
4. Fill in the keystore details, choose `release`, and build.
5. The signed `.aab` file appears in `app/release/app-release.aab` — this is
   what you upload to the Google Play Console.

## Changing the live URL later

If you ever move off Streamlit Cloud to a custom domain, you only need to
change one line:
`app/src/main/res/values/strings.xml` → the `app_url` string.

## Notes
- The app requires an internet connection (it's a live wrapper, not an
  offline app) — this matches how the Streamlit app itself works.
- Camera permission is requested only if a page inside the app ever asks
  for it (e.g. a future live-camera QR feature); the current QR/File
  scanners use the standard file picker, which is already wired up.
- If Android Studio asks to update Gradle/AGP versions on first open, it's
  safe to accept — this project already targets recent stable versions.
