# Android APK — How to get it now

You have two quick options to download an APK without a Mac:

## Option A — Codemagic (simplest, no setup)
1. Go to https://codemagic.io and sign in with GitHub/Google.
2. Click **Add application** → **App repos** → select your repo (or **Add app manually** and upload the ZIP).
3. Ensure the repo has `codemagic.yaml` at root (already included).
4. Start the workflow **Android Debug APK**.
5. When it finishes, download **app-debug.apk** from the Artifacts section.

## Option B — GitHub Actions (free)
1. Push this project to a new GitHub repo.
2. Go to **Actions** tab → Run the workflow **Android Debug APK** (already included).
3. After it completes, open the run → **Artifacts** → download **personal-trainer-debug-apk** (contains `app-debug.apk`).

## Install on phone
- Copy `app-debug.apk` to your Android device and open it.
- Allow installs from unknown sources when prompted.

## Want a signed release APK? (optional)
1. Create a keystore on your machine:
   ```bash
   keytool -genkey -v -keystore my-release-key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias upload
   ```
2. Put `my-release-key.jks` in `android/app/`.
3. Create `android/key.properties` with:
   ```
   storePassword=YOUR_PASSWORD
   keyPassword=YOUR_PASSWORD
   keyAlias=upload
   storeFile=../app/my-release-key.jks
   ```
4. In `android/app/build.gradle`, ensure signing config reads from key.properties (Flutter template already supports this).
5. Build:
   ```bash
   flutter build apk --release
   ```
6. Your APK is at `build/app/outputs/flutter-apk/app-release.apk`.
