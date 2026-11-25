Notebook – Android project (WebView app)

BUILD (Android Studio):
  1. File > Open > select this folder (NotebookApp), wait for Gradle sync.
  2. Build > Build Bundle(s) / APK(s) > Build APK(s)
     Output: app/build/outputs/apk/release/app-release.apk  (already signed)

BUILD (command line, if Gradle 8.7+ and Android SDK are installed):
  gradle assembleRelease
  (ANDROID_HOME or local.properties with sdk.dir=... must point to the SDK)

SIGNING:
  Keystore : app/notebook-release.jks
  Alias    : notebook
  Store/Key password : notebook123
  Used for both debug and release builds (see app/build.gradle).
  Keep this keystore: future updates must be signed with the same key.

The app source is app/src/main/assets/index.html.
Min Android 8.0 (API 26). Needs internet only for the first Gradle sync.
