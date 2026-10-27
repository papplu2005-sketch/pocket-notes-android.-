# Pocket Notes Android starter

This is a starter project made from the uploaded `Pocket Notes (1).html` file. It adds a Capacitor Android wrapper, offline shell caching for web hosting, a local PDF library (IndexedDB), and an AI helper interface that can copy a prompt or call a secure `/api/ai` backend once you deploy one.

## Build an APK free using only your Android phone

This starter uses GitHub Actions as a cloud build computer. You need a free GitHub account and a browser on your phone. The generated artifact is a debug APK for personal testing, not a Play Store release.

1. Download and extract this ZIP on your phone (or upload the ZIP's files to a new GitHub repository using GitHub's website; GitHub's web upload accepts files, not an arbitrary ZIP as a source repository).
2. Create a new repository at https://github.com/new, e.g. `pocket-notes-android`.
3. Upload all files and folders from this project, preserving the `.github/workflows/build-apk.yml` path. If GitHub mobile upload hides dot-folders, use the browser's desktop-site mode or create the workflow file separately in GitHub's web editor.
4. Open the repository's **Actions** tab. Select **Build Pocket Notes APK** and press **Run workflow**. If the workflow has not appeared yet, push/commit the files to the `main` branch first.
5. Wait for the run to finish with a green check. Open that run, scroll to **Artifacts**, and download `pocket-notes-debug-apk`.
6. Extract the downloaded artifact ZIP on your phone to obtain `app-debug.apk`. Tap the APK to install. Android may ask you to allow installation from that browser/file manager; only enable it for the app you trust and turn it off afterwards.

## Important source fixes / limitations

- The original app saves notes in `localStorage` unless the Claude runtime database is present. APK data stays local to the app; uninstalling the app or clearing its data can erase notes. Export/backup is not implemented in this starter.
- PDF files are stored locally in IndexedDB and are not automatically synced. Large PDFs may exceed available storage. Keep backups of important documents.
- PDF preview uses the Android WebView/browser PDF support; behavior can vary by Android WebView version. The app currently stores and previews PDFs but does not extract PDF text or cite PDF pages.
- The AI helper does not have a live model connection until a secure `/api/ai` backend is deployed. The “Copy prompt” option works without a backend. Never embed a Gemini/API key in HTML or the APK.
- This is a debug APK workflow for personal use. A signed release APK / Play Store publication needs a separate signing and release setup.
- Test create/edit/reopen notes, folders, drawing, PDF import/open/delete, and app restart before relying on it. If the app doesn't launch, check the Actions build log.

## Architecture

- `www/index.html`: original app plus PDF/AI helper UI
- `www/manifest.webmanifest`, `www/sw.js`: installable web metadata and shell cache
- `capacitor.config.json`: Android wrapper configuration
- `.github/workflows/build-apk.yml`: free cloud debug build
- `server/README.md`: secure AI backend contract and safety notes
