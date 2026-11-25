# Notebook

**English** · [বাংলা](#বাংলা)

A simple, fast, offline notebook app. The app is a single HTML page (`index.html`) that runs inside an Android WebView, so it works without an internet connection.

## Features

- **Notes**: title and body, with word and character count and last-edited time
- **Pin**: keep important notes at the top of the list
- **Tags**: add comma-separated tags and filter by tag
- **Folders**: create your own folders to organize notes
- **Checklists**: add to-do items inside any note and tick them off
- **Search**: across titles, text, tags and checklist items
- **Trash**: deleted notes go to the trash and can be restored; they are removed automatically after 30 days
- **History**: a calendar heatmap of the days you wrote notes, with active-day and streak counts
- **Backup**: copy all notes as text, keep it somewhere safe, and paste it back to import
- **Dark mode**: follows the phone's light or dark theme

## Screenshots

<p>
  <img src="screenshots/1.png" width="240" alt="Home">
  <img src="screenshots/2.png" width="240" alt="Editor">
  <img src="screenshots/3.png" width="240" alt="History">
  <img src="screenshots/4.png" width="240" alt="History">
  <img src="screenshots/5.png" width="240" alt="History">
</p>
## Where your data lives

Notes stay on the phone and are never sent to a server. They are stored in the app's WebView localStorage.

- Uninstalling the app, or clearing the app's data in system settings, deletes your notes.
- Back up regularly with **Backup > Copy all notes** and keep the text somewhere safe.
- On a new phone, or after reinstalling, paste it into **Backup** and tap **Import** to restore.

## Project structure

```
.
├── .github/workflows/build.yml     GitHub Actions: build and release
├── app/
│   ├── build.gradle                app config and signing
│   ├── notebook-release.jks        signing keystore
│   └── src/main/
│       ├── AndroidManifest.xml
│       ├── assets/index.html       the whole app UI and logic
│       ├── java/com/notebook/app/MainActivity.java   WebView, Back button, Copy bridge
│       └── res/                    icon, theme
├── build.gradle
├── settings.gradle
└── gradle.properties
```

- Package: `com.notebook.app`
- Minimum Android: 8.0 (API 26)
- No extra libraries are used

## Building it yourself

### With Android Studio

1. Open this folder in Android Studio and let Gradle sync finish (internet is needed the first time).
2. Choose **Build > Build APK(s)**.
3. The APK is at `app/build/outputs/apk/release/app-release.apk`.

### From the command line

With Gradle 8.7+ and the Android SDK installed:

```
gradle assembleRelease
```

## Build and release with GitHub Actions

`.github/workflows/build.yml` runs in three ways:

| When | What happens |
| --- | --- |
| Push to `main` or `master` | Builds the APK; `Notebook-dev.apk` appears under Artifacts |
| Push a tag like `v1.0.0` | Builds the APK and creates a GitHub Release |
| Actions > **Run workflow** (manual) | Enter a **version** (e.g. `1.0.0`) to create a release; leave it empty to only build |

When a version is given, `versionName` is set to it and `versionCode` is set to the workflow run number, so each new release installs as an update over the previous one. Use a new version number every time.

If creating the release fails with a permission error, enable "Read and write permissions" under Settings > Actions > General > Workflow permissions in your repo.

## Signing

The APK is signed with `app/notebook-release.jks`.

| Item | Value |
| --- | --- |
| Alias | `notebook` |
| Store and key password | `notebook123` |

Both debug and release builds use this key (configured in `app/build.gradle`).

> **Warning:** the keystore and its password are in the repo. If the repo is public, anyone can sign with this key. Keep the repo private for personal use. To publish on the Play Store, create a new key and keep its password secret (for example in GitHub Secrets). Future updates must be signed with the same keystore, so do not lose it.

## App behavior

- The phone's Back button returns from the editor, Trash or Backup page to the previous page. On the main page it closes the app.
- The note's **Copy** button copies the title, text and checklist to the phone's clipboard.

---

# বাংলা

[English](#notebook) · **বাংলা**

একটি সহজ, দ্রুত ও অফলাইন নোটবুক অ্যাপ। অ্যাপটি একটি HTML পেজ (`index.html`) যা Android WebView-র ভেতরে চলে, তাই ইন্টারনেট ছাড়াই ব্যবহার করা যায়।

## ফিচার

- **নোট লেখা**: শিরোনাম ও লেখা, সাথে শব্দ ও অক্ষর গণনা এবং সর্বশেষ সম্পাদনার সময়
- **Pin**: গুরুত্বপূর্ণ নোট তালিকার উপরে রাখা
- **Tags**: কমা দিয়ে ট্যাগ যোগ করা এবং ট্যাগ ধরে ফিল্টার করা
- **Folders**: নিজের ফোল্ডার বানিয়ে নোট সাজানো
- **Checklist**: প্রতিটি নোটের ভেতরে করণীয় তালিকা, টিক দিয়ে সম্পন্ন চিহ্নিত করা যায়
- **Search**: শিরোনাম, লেখা, ট্যাগ ও checklist জুড়ে খোঁজা
- **Trash**: মুছলে নোট ট্র্যাশে যায়, সেখান থেকে ফেরত আনা যায়। ৩০ দিন পরে নিজে থেকে মুছে যায়
- **History**: ক্যালেন্ডার হিটম্যাপে কোন দিন নোট লেখা হয়েছে তা দেখা যায়, সাথে সক্রিয় দিন ও টানা দিনের (streak) হিসাব
- **Backup**: সব নোট কপি করে অন্য কোথাও রেখে পরে পেস্ট করে ফেরত আনা (Import)
- **Dark mode**: ফোনের থিম অনুযায়ী লাইট বা ডার্ক চলে

## তথ্য কোথায় থাকে

নোট ফোনেই থাকে, কোনো সার্ভারে যায় না। অ্যাপের WebView-র localStorage-এ জমা হয়।

- অ্যাপ uninstall করলে বা সেটিংস থেকে অ্যাপের data clear করলে নোট মুছে যাবে।
- তাই নিয়মিত **Backup > Copy all notes** দিয়ে নোট কপি করে নিরাপদ জায়গায় রাখুন।
- নতুন ফোনে বা পুনরায় install করার পর **Backup** পাতায় পেস্ট করে **Import** দিলে নোট ফিরে আসে।

## প্রজেক্টের গঠন

```
.
├── .github/workflows/build.yml     GitHub Actions: build ও release
├── app/
│   ├── build.gradle                অ্যাপের কনফিগ ও signing
│   ├── notebook-release.jks        signing keystore
│   └── src/main/
│       ├── AndroidManifest.xml
│       ├── assets/index.html       পুরো অ্যাপের ইন্টারফেস ও লজিক
│       ├── java/com/notebook/app/MainActivity.java   WebView, Back বাটন, Copy bridge
│       └── res/                    আইকন, থিম
├── build.gradle
├── settings.gradle
└── gradle.properties
```

- Package: `com.notebook.app`
- Minimum Android: 8.0 (API 26)
- অতিরিক্ত কোনো library ব্যবহার হয়নি

## নিজে build করা

### Android Studio দিয়ে

1. Android Studio-তে এই ফোল্ডারটি খুলুন এবং Gradle sync শেষ হতে দিন (প্রথমবার ইন্টারনেট লাগবে)।
2. **Build > Build APK(s)** চাপুন।
3. APK পাবেন `app/build/outputs/apk/release/app-release.apk`-এ।

### কমান্ড লাইন দিয়ে

Gradle 8.7+ ও Android SDK থাকলে:

```
gradle assembleRelease
```

## GitHub Actions দিয়ে build ও release

`.github/workflows/build.yml` তিনভাবে চলে:

| কখন | কী হয় |
| --- | --- |
| `main` বা `master`-এ push | APK build হয়, Artifacts-এ `Notebook-dev.apk` আসে |
| `v1.0.0`-এর মতো tag push | APK build হয় এবং GitHub Release তৈরি হয় |
| Actions > **Run workflow** (ম্যানুয়াল) | **version** ঘরে সংখ্যা (যেমন `1.0.0`) দিলে release হয়, ফাঁকা রাখলে শুধু build হয় |

version দিলে `versionName` সেই version হয় এবং `versionCode` হয় workflow run নম্বর। তাই নতুন release আগেরটির ওপর update হিসেবে install করা যায়। প্রতিবার নতুন version নম্বর ব্যবহার করুন।

release বানাতে permission error এলে repo-র Settings > Actions > General > Workflow permissions-এ "Read and write permissions" চালু করুন।

## Signing

APK `app/notebook-release.jks` দিয়ে sign হয়।

| বিষয় | মান |
| --- | --- |
| Alias | `notebook` |
| Store ও key password | `notebook123` |

debug ও release দুই build-ই এই key ব্যবহার করে (`app/build.gradle`-এ কনফিগ করা)।

> **সতর্কতা:** keystore ও password repo-তেই আছে। repo public হলে যে কেউ এই key দিয়ে sign করতে পারবে। শুধু নিজের ব্যবহারের হলে repo private রাখুন। Play Store-এ প্রকাশ করতে চাইলে নতুন key বানিয়ে password গোপন রাখুন (যেমন GitHub Secrets-এ)। পরে update দিতে হলে একই keystore লাগবে, তাই এটি হারাবেন না।

## অ্যাপের আচরণ

- ফোনের Back বাটন নোট সম্পাদনা, Trash বা Backup পাতা থেকে আগের পাতায় ফেরায়। মূল পাতায় থাকলে অ্যাপ বন্ধ হয়।
- নোটের **Copy** বাটন নোটের শিরোনাম, লেখা ও checklist ফোনের clipboard-এ কপি করে।
