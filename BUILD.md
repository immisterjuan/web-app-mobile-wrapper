# QR Browser — Android APK Build Guide

## What you get
A full-screen native-feeling Android app that:
- **Opens directly to the camera** — ready to scan
- **Scans QR codes** in real time using your device camera
- **Loads the URL** in a full-screen browser view with a toolbar
- **Camera button** in the toolbar lets you scan a new QR anytime
- **Android back button** returns to the scanner

---

## Method 1 — Capacitor (recommended, produces a real signed APK)

### Prerequisites
| Tool | Download |
|------|----------|
| Node.js 18+ | https://nodejs.org |
| Android Studio | https://developer.android.com/studio |
| Java JDK 17 | bundled with Android Studio |

### Steps

```bash
# 1. Install dependencies
cd mobile-app-wrapper
npm install

# 2. Add Android platform
npx cap add android

# 3. Sync web assets into the Android project
npx cap sync android

# 4. Open in Android Studio
npx cap open android
```

Inside Android Studio:
- Wait for Gradle sync to finish
- **Build → Generate Signed Bundle/APK → APK**
- Choose a keystore (create one if first time)
- Select **release** build variant → Finish
- APK is saved to `android/app/release/app-release.apk`

Transfer the APK to your phone and install it  
*(Settings → Install unknown apps → allow for your file manager)*

---

## Method 2 — Online builder (no coding tools needed)

1. Go to **https://gonative.io** or **https://median.co**
2. Enter any URL (you'll replace it) — or use `https://example.com`
3. Download the sample project
4. Replace their `index.html` with the `index.html` from this folder
5. Build & download APK

Alternatively, upload `index.html` to **GitHub Pages** (free), then use
https://www.pwabuilder.com to generate an APK from the hosted URL.

---

## Method 3 — Self-host + PWA Install (easiest, no APK)

1. Upload `index.html` to any HTTPS host (GitHub Pages, Netlify, Vercel — all free)
2. Open the URL in Chrome on Android
3. Chrome will prompt **"Add to Home Screen"** — tap it
4. The app icon appears on your home screen and opens full-screen, just like a native app

> **Note:** Camera access requires HTTPS. All three methods handle this correctly.

---

## Capacitor: enabling camera on older Android

The `android/app/src/main/AndroidManifest.xml` should already contain:
```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-feature android:name="android.hardware.camera" />
<uses-feature android:name="android.hardware.camera.autofocus" />
```
Capacitor adds these automatically when you run `cap sync`.
