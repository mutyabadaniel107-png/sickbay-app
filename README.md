# New High Tech SS — Lab App

A native Android WebView wrapper for:
`https://newhightechsskajjansi.prophp.org/pages/lab/lab_login.php`

Splash screen shows the school crest with **"Built by Kn Soft"** underneath,
then loads the site full-screen with a real app icon, back-button navigation,
pull-to-refresh, an offline screen with retry, and file-download support.

## How to turn this into an installable .apk — using GitHub (no Android Studio needed)

This project already includes a GitHub Actions workflow
(`.github/workflows/build-apk.yml`) that builds the APK in the cloud every
time you push. You just need a free GitHub account.

**Steps:**
1. Go to [github.com](https://github.com) → log in → click the **+** in the
   top right → **New repository**. Name it anything (e.g. `lab-app`),
   leave it **Private** or **Public**, don't add a README, click **Create repository**.
2. On the next page, click **uploading an existing file**.
3. Unzip the file I gave you, then **drag the whole unzipped folder**
   (the one containing `app`, `.github`, `settings.gradle`, etc.) straight
   into the browser upload area. Modern browsers keep the folder structure
   intact. Click **Commit changes**.
4. Click the **Actions** tab at the top of the repo. You'll see a workflow
   run called "Build APK" already running (it starts automatically on the
   upload). Wait 2–4 minutes for the green checkmark.
5. Click into that finished run → scroll down to **Artifacts** → click
   **app-debug-apk** to download a zip. Inside is your `app-debug.apk`.
6. Send that `.apk` file to your phone (email, Drive, USB) and open it to
   install — you may need to allow "install unknown apps" once, since it
   isn't from the Play Store.

If nothing runs automatically after step 3, open the **Actions** tab, click
**Build APK** on the left, then **Run workflow** to trigger it manually.

### Alternative: using Android Studio instead
If you'd rather build locally: install Android Studio (free, from
developer.android.com/studio) → **File → Open** → select this folder → let
it sync → **Build → Build App Bundle(s) / APK(s) → Build APK(s)**. The APK
lands at `app/build/outputs/apk/debug/app-debug.apk`.

### Getting a signed "release" APK
The GitHub workflow currently produces a debug APK, which installs and works
completely fine for personal/internal use. If you want a properly signed
release build (e.g. to publish it more broadly or on the Play Store), let me
know and I'll extend the workflow to sign it, or use Android Studio's
**Build → Generate Signed Bundle / APK** instead.

## Customizing

| What | Where |
|---|---|
| The URL that loads | `app/src/main/res/values/strings.xml` → `site_url` |
| App name shown under the icon | `app/src/main/res/values/strings.xml` → `app_name` |
| Splash screen duration | `SplashActivity.java` → `SPLASH_DELAY_MS` (currently 1800ms) |
| "Built by Kn Soft" text | `app/src/main/res/values/strings.xml` → `splash_tagline` |
| Real Nativine script font | See `app/src/main/res/font/README.txt` |
| Brand colors | `app/src/main/res/values/colors.xml` (already sampled from your logo) |
| App icon / launcher image | `app/src/main/res/mipmap-*/ic_launcher.png` (regenerated from your logo at every density) |
| Package/app ID | `app/build.gradle` → `applicationId`, and matches the Java package `com.knsoft.newhightechlab` |

A 512×512 Play Store–ready icon is also included at the project root:
`ic_launcher_playstore_512.png` (only needed if you ever publish to Google Play).

## What's already handled
- Loads your site full-screen with no browser chrome
- Back button navigates WebView history before exiting the app
- Pull down to refresh the page
- Top progress bar while pages load
- Offline screen with a Retry button if there's no connection
- File downloads (e.g. any PDFs the portal serves) go to the phone's normal Downloads folder
- Links to other domains, `tel:`, `mailto:` open in the appropriate app instead of breaking the WebView
- HTTPS-only (matches your site being served over https)
