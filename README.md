# Anchor — build your APK

Your whole app lives in `www/index.html` — one file, easy to keep editing the way you like.
Everything else here just wraps it into a real Android app using Capacitor.

## Fastest path: let GitHub build the APK for you (no Android Studio needed)

1. Create a new **public or private** repo on GitHub (e.g. `anchor-app`).
2. Upload everything in this folder to that repo (keep the same folder structure —
   `www/index.html`, `capacitor.config.json`, `package.json`, and the `.github/workflows` folder).
3. Push to the `main` branch (or just upload via the GitHub website).
4. Go to the **Actions** tab of your repo — a workflow called "Build Anchor APK" will run
   automatically (takes ~3-5 minutes).
5. When it finishes, click into the run → scroll to **Artifacts** → download `anchor-debug-apk`.
6. Unzip it, you'll have `app-debug.apk`. Transfer that to your phone (email it to yourself,
   Google Drive, or a USB cable) and tap it to install.
   - Android will ask you to allow "install from unknown sources" the first time — that's normal
     for any app installed outside the Play Store.

You don't need Android Studio, a Mac, or any local setup for this path — GitHub's servers do the build.

## Alternative: build it yourself locally (if you have Android Studio)

```bash
npm install
npx cap add android
npx cap sync android
npx cap open android
```

This opens the project in Android Studio. From there: **Build → Build Bundle(s)/APK(s) → Build APK(s)**.
The signed/debug APK will appear under `android/app/build/outputs/apk/`.

## Editing the app

Everything — every screen, every feature — is in `www/index.html`. Change the HTML/CSS/JS there,
then re-run `npx cap sync android` (or just push to GitHub again to get a fresh APK) to see it
in the app.

## Next real upgrade: live step counting + synced data

Right now steps are logged manually and everything is stored on-device (`localStorage`).
When you're ready:
- Add `@capacitor-community/step-counter` for a real step count from the phone's sensor.
- Swap `localStorage` calls in `index.html` for Supabase (auth + a `user_stats` table) so a
  person's streaks, badges, and journal survive a reinstall or work across devices.

Happy to build either of those next whenever you want.
