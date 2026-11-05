# HCCJ - Android and iPhone app project

App name: HCCJ | Package ID: com.hccj.songbook (change it in capacitor.config.json before publishing if you want another ID)
The app itself is in `www/index.html` (all 738 songs, works offline).

## Easiest way to get an Android APK (no software to install)
1. Create a free account at github.com and make a new repository.
2. Upload everything in this folder to it (drag and drop on the repository page; keep the `.github` folder).
3. Open the **Actions** tab, choose **Build HCCJ Android APK**, press **Run workflow**.
4. After a few minutes open the finished run and download **HCCJ-apk**. Unzip it to get `app-debug.apk`.
5. Send the APK to a phone and install it (the phone will ask to allow installs from unknown sources).

This APK is for testing and sharing directly. The Play Store needs a signed release (next section).

## Android Studio route (needed for the Play Store)
Install Node.js 20, Android Studio and JDK 17, then in this folder:

    npm install
    npx cap add android
    npx capacitor-assets generate --android --iconBackgroundColor '#EC2625' --splashBackgroundColor '#EC2625'
    npx cap sync android
    npx cap open android

In Android Studio: **Build > Generate Signed App Bundle / APK > Android App Bundle**, create a keystore (keep the file and passwords safe forever; you need them for every update), and build the release `.aab`.
Upload the `.aab` in Google Play Console (one-time US$25 developer fee). To release an update, raise `versionCode` and `versionName` in `android/app/build.gradle`.

## iPhone
Needs a Mac with Xcode and an Apple Developer account (US$99 a year):

    npm install
    npx cap add ios
    npx capacitor-assets generate --ios
    npx cap sync ios
    npx cap open ios

In Xcode set your Team, then Product > Archive and upload to App Store Connect.

## Changing the songs or design
Edit `www/index.html`, then run `npx cap sync` and rebuild.
