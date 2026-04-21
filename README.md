# TaskFlow ⚡

> Priority management + Time blocking + Daily habits — all in one beautiful app.

---

## 🚀 Deploy to GitHub & Build APK in 5 Steps

### Step 1 — Create a GitHub Repository

1. Go to [github.com/new](https://github.com/new)
2. Name it `taskflow-app` (or anything you like)
3. Set it to **Public** (required for free GitHub Actions minutes)
4. **Do NOT** initialize with README — you'll push these files directly
5. Click **Create repository**

---

### Step 2 — Upload these files to GitHub

**Option A — GitHub Web UI (easiest, no terminal needed)**

1. On your new empty repo page, click **"uploading an existing file"**
2. Drag and drop **all files and folders** from this zip:
   - `src/` folder
   - `.github/` folder
   - `package.json`
   - `capacitor.config.json`
   - `.gitignore`
   - `README.md`
3. Scroll down → write a commit message → click **Commit changes**

**Option B — Git CLI**

```bash
cd taskflow-app
git init
git add .
git commit -m "Initial commit — TaskFlow app"
git remote add origin https://github.com/YOUR_USERNAME/taskflow-app.git
git branch -M main
git push -u origin main
```

---

### Step 3 — Watch the APK build automatically

1. Go to your repo on GitHub
2. Click the **Actions** tab
3. You'll see **"Build Android APK"** workflow running (takes ~5–8 minutes)
4. Once it turns ✅ green, click into it

---

### Step 4 — Download your APK

**From Actions artifacts:**
- Click the workflow run → scroll to **Artifacts** section → download **TaskFlow-debug-apk**

**From Releases (on every push to main):**
- Go to your repo → **Releases** (right sidebar) → download `app-debug.apk`

---

### Step 5 — Install on Android

1. Transfer the APK to your Android phone (AirDrop, email, Google Drive, USB)
2. On your phone: **Settings → Security → Install unknown apps** → allow your file manager
3. Tap the APK file → Install
4. Open **TaskFlow** from your app drawer 🎉

---

## 📁 Project Structure

```
taskflow-app/
├── src/
│   └── index.html          ← Your entire TaskFlow app (self-contained)
├── .github/
│   └── workflows/
│       └── build-apk.yml   ← GitHub Actions: auto-builds APK on every push
├── package.json            ← Capacitor dependencies
├── capacitor.config.json   ← App ID, name, web directory config
├── .gitignore
└── README.md
```

---

## ⚙️ How It Works

```
Your HTML file (src/index.html)
        │
        ▼
  Capacitor CLI
  (npx cap sync)
        │
        ▼
  Android Project
  (native wrapper)
        │
        ▼
  Gradle build
  (./gradlew assembleDebug)
        │
        ▼
  app-debug.apk ✅
```

Capacitor wraps your HTML/CSS/JS app in a native Android WebView — no code changes needed. Your app works exactly the same as in the browser.

---

## 🔧 Customizing the App ID

Edit `capacitor.config.json`:

```json
{
  "appId": "com.yourname.taskflow",   ← change this
  "appName": "TaskFlow",              ← change this (appears on phone)
  "webDir": "src"
}
```

App IDs must be unique if you ever publish to Google Play Store (e.g. `com.john.taskflow`).

---

## 🔐 Production / Signed APK (optional)

The workflow builds a **debug APK** — fine for personal use. For Google Play Store you need a signed release APK:

1. Generate a keystore:
   ```bash
   keytool -genkey -v -keystore taskflow.keystore -alias taskflow -keyalg RSA -keysize 2048 -validity 10000
   ```

2. Add these GitHub Secrets (repo → Settings → Secrets → Actions):
   - `KEYSTORE_FILE` — base64-encoded keystore (`base64 taskflow.keystore`)
   - `KEYSTORE_PASSWORD` — your keystore password
   - `KEY_ALIAS` — `taskflow`
   - `KEY_PASSWORD` — your key password

3. Update the workflow to use `assembleRelease` and sign with the keystore.

---

## 🛠 Local Development (optional)

If you want to build locally instead of via GitHub:

```bash
# Install dependencies
npm install

# Add Android platform (first time only)
npx cap add android

# Sync your web files into Android project
npx cap sync android

# Open in Android Studio
npx cap open android
# Then: Build → Build Bundle(s)/APK(s) → Build APK(s)
```

**Requirements for local build:**
- Node.js 18+
- Java JDK 17
- Android Studio + Android SDK

---

## ❓ Troubleshooting

| Problem | Fix |
|---|---|
| Actions tab not visible | Make sure repo is **Public** or you have a paid plan |
| Build fails — SDK licenses | Re-run the workflow (transient issue) |
| APK installs but crashes | Check the `webDir` in `capacitor.config.json` points to `src` |
| "Unknown sources" blocked | Phone settings vary — search "install unknown apps" in settings |
| Want a custom app icon | Replace icons in `android/app/src/main/res/` after first sync |

---

## 📱 Features

- ✅ Priority board (Must / Need / Want to do)
- ✅ Drag & drop between priority columns
- ✅ Time block timeline view
- ✅ Daily habits tracker with streaks
- ✅ Subtasks with progress tracking
- ✅ Recurring tasks
- ✅ Dark mode
- ✅ Data export (JSON)
- ✅ Fully offline — no server needed
