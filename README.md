# ReelSong AI

Android app starter project for identifying music in Instagram Reels.

## Included
- Paste an Instagram Reel URL (with a clear limitation: Instagram links often cannot be fetched directly).
- Android Share Sheet receiver for shared videos/audio.
- Pick a downloaded video/audio file.
- Extract the first audio track from a video into an M4A file.
- Submit the audio to AudD for song recognition.
- Display title, artist, album, release date, label and a Spotify link when returned.

## Important
A song-recognition provider API key is required. This project uses AudD's API:
https://audd.io/

The project does not contain an API key. Obtain your own key and add it to the project root `local.properties`:

```properties
AUDD_API_TOKEN=YOUR_AUDD_API_TOKEN
```

Do not commit `local.properties` to GitHub. The app sends the selected audio file to AudD when the user taps **Identify song**. Obtain consent before using it with private media.

## Open and build
1. Install Android Studio (current stable) with Android SDK Platform 35 and JDK 17.
2. Open this folder in Android Studio.
3. Add the AudD token to `local.properties`.
4. Allow Gradle sync to finish.
5. Build > Build Bundle(s) / APK(s) > Build APK(s).
6. The debug APK will be at `app/build/outputs/apk/debug/app-debug.apk`.

Or from a terminal with Gradle installed:
```bash
gradle assembleDebug
```

## Import methods
- **Share:** In Instagram, use Share and choose ReelSong AI if the app is offered. Some Instagram versions share only a URL, not the actual video. In that case use Download/Save video where permitted, then import the file.
- **Upload:** Use Import Reel to select a locally saved video or audio file.
- **Paste link:** The app accepts and validates an Instagram URL, but does not scrape private/login-protected Instagram pages. For reliable identification, import/share the actual video file.

## Current limitations
- Recognition depends on AudD coverage and a valid API subscription/key.
- Recognition may fail for very short clips, heavy voice-over, remixes, sped-up tracks or noisy audio.
- BPM, mood, genre and vocal/instrumental analysis are not included in this first build. They require additional audio-analysis services/models and are intentionally not fabricated.
- This workspace did not have Android SDK/Gradle installed, so an APK could not be compiled or verified here. Build it in Android Studio using the steps above.


## Build APK automatically on GitHub
1. Upload/push the complete project to a GitHub repository (keep `.github/workflows/android-apk.yml`).
2. In GitHub, open **Settings > Secrets and variables > Actions > New repository secret**.
3. Add a secret named `AUDD_API_TOKEN` with your AudD API token. This is optional for compilation, but required for real song recognition at runtime.
4. Open the repository's **Actions** tab.
5. Select **Build ReelSong AI APK** and click **Run workflow**, or push a commit to `main`/`master`.
6. When the run finishes, open the workflow run and download the **ReelSong-AI-debug-APK** artifact.

The artifact is a ZIP containing `app-debug.apk`. It is a debug-signed APK for testing, not a Play Store release.
