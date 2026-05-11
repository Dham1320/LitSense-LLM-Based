# 🏪 ನಮ್ಮ ಸಂತೆ (Namma Santhe) - Digital Ledger App

A simplified digital khata (ledger) application for rural village market vendors to track credit (Udari) given to customers. Built with React + Vite + Tailwind CSS, designed to be wrapped as an Android app.

![App Logo](public/images/santhe-hero.jpg)

---

## 📱 Features

### Core Features
- ✅ **Quick Credit Entry** - Add Udari (credit) in 2 steps, under 5 seconds
- ✅ **Payment Recording** - Log when customers pay back
- ✅ **Customer Management** - Add, search, delete customers
- ✅ **Daily Summary** - View sales, payments, and pending dues
- ✅ **Total Outstanding** - Dashboard shows total money owed
- ✅ **Transaction History** - Full ledger per customer

### AI & Accessibility Features (for rural/uneducated users)
- 🎙️ **Voice Input** - Speak customer names, amounts, notes in Kannada/Hindi/English
- 🔊 **Voice Output** - App reads out balances and OTP aloud
- 🌐 **Multi-Language** - Full UI in Kannada (ಕನ್ನಡ), Hindi (हिंदी), and English
- 📱 **Large Touch Targets** - Big buttons and numeric keypad for easy use

### Authentication
- 🔐 **OTP Login** - Phone number verification with 4-digit OTP
- 👤 **Role-based Access** - Separate views for Creditors (vendors) and Debtors (customers)
- 🔊 **Voice OTP** - OTP is spoken aloud for illiterate users

### Reminder System
- 📲 **WhatsApp Reminders** - One-tap payment reminder via WhatsApp
- 💬 **SMS Reminders** - Send SMS payment reminders
- ⏰ **Auto Reminders** - Schedule daily/weekly/monthly automatic reminders
- 🔔 **Due Notifications** - Floating badge shows pending reminder count

---

## 🛠️ Tech Stack

| Technology | Purpose |
|------------|---------|
| React 19 | UI Framework |
| Vite 7 | Build Tool |
| TypeScript | Type Safety |
| Tailwind CSS 4 | Styling |
| LocalStorage | Data Persistence (simulates Room DB) |
| Web Speech API | Voice Input/Output |
| Capacitor | Android/iOS Wrapper |

---

## 📂 Project Structure

```
namma-santhe-ledger/
├── public/
│   └── images/
│       └── santhe-hero.jpg
├── src/
│   ├── components/
│   │   ├── LoginPage.tsx          # OTP Login with voice support
│   │   ├── HomePage.tsx           # Main dashboard
│   │   ├── CustomersPage.tsx      # Customer list & management
│   │   ├── CustomerDetailPage.tsx # Individual customer ledger
│   │   ├── QuickEntryPage.tsx     # 2-step credit/payment entry
│   │   ├── DailySummaryPage.tsx   # Daily profit/loss summary
│   │   ├── DebtorDashboard.tsx    # View for customers (debtors)
│   │   ├── NumericKeypad.tsx      # Large touch-friendly keypad
│   │   ├── VoiceButton.tsx        # Microphone button component
│   │   ├── ReminderModal.tsx      # WhatsApp/SMS reminder setup
│   │   ├── ReminderNotification.tsx # Due reminder alerts
│   │   └── SplashScreen.tsx       # App loading screen
│   ├── context/
│   │   └── AppContext.tsx         # Global state (user, language)
│   ├── hooks/
│   │   └── useSpeech.ts           # Voice recognition hook
│   ├── i18n/
│   │   └── translations.ts        # Kannada/Hindi/English strings
│   ├── services/
│   │   └── reminderService.ts     # Reminder scheduling logic
│   ├── store.ts                   # LocalStorage CRUD operations
│   ├── types.ts                   # TypeScript interfaces
│   ├── App.tsx                    # Main app with routing
│   ├── main.tsx                   # Entry point
│   └── index.css                  # Tailwind + custom animations
├── index.html
├── package.json
├── vite.config.ts
├── tsconfig.json
└── README.md
```

---

## 🚀 Running as Web App

### Prerequisites
- Node.js 18+ 
- npm 9+

### Installation

```bash
# Clone the repository
git clone https://github.com/your-repo/namma-santhe-ledger.git
cd namma-santhe-ledger

# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

---

## 📱 Converting to Android App (Android Studio)

### Option 1: Using Capacitor (Recommended)

Capacitor wraps your web app in a native WebView and provides access to native APIs.

#### Step 1: Install Capacitor

```bash
# Install Capacitor core and CLI
npm install @capacitor/core @capacitor/cli

# Initialize Capacitor
npx cap init "Namma Santhe" "com.nammasanthe.ledger" --web-dir dist

# Install Android platform
npm install @capacitor/android

# Add Android project
npx cap add android
```

#### Step 2: Configure Capacitor

Edit `capacitor.config.ts`:

```typescript
import { CapacitorConfig } from '@capacitor/core';

const config: CapacitorConfig = {
  appId: 'com.nammasanthe.ledger',
  appName: 'Namma Santhe',
  webDir: 'dist',
  server: {
    androidScheme: 'https'
  },
  plugins: {
    SplashScreen: {
      launchShowDuration: 2000,
      backgroundColor: '#f97316',
      showSpinner: false,
    },
  },
};

export default config;
```

#### Step 3: Build and Sync

```bash
# Build the web app
npm run build

# Copy web assets to Android project
npx cap sync android

# Open in Android Studio
npx cap open android
```

#### Step 4: Android Studio Setup

1. Open Android Studio
2. Wait for Gradle sync to complete
3. Connect Android device or start emulator
4. Click **Run** ▶️ to install the app

#### Step 5: Generate Signed APK

1. In Android Studio: **Build → Generate Signed Bundle / APK**
2. Select **APK**
3. Create or use existing keystore
4. Select **release** build variant
5. APK will be in `android/app/release/`

---

### Option 2: Using Android WebView (Manual)

If you prefer a pure Android project without Capacitor:

#### Step 1: Create Android Project

1. Open Android Studio
2. **New Project → Empty Activity**
3. Name: `NammaSanthe`
4. Package: `com.nammasanthe.ledger`
5. Language: Kotlin
6. Minimum SDK: API 24 (Android 7.0)

#### Step 2: Add WebView Layout

`app/src/main/res/layout/activity_main.xml`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <WebView
        android:id="@+id/webview"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

</RelativeLayout>
```

#### Step 3: Configure MainActivity

`app/src/main/java/com/nammasanthe/ledger/MainActivity.kt`:

```kotlin
package com.nammasanthe.ledger

import android.os.Bundle
import android.webkit.WebSettings
import android.webkit.WebView
import android.webkit.WebViewClient
import android.webkit.WebChromeClient
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {
    private lateinit var webView: WebView

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        webView = findViewById(R.id.webview)
        
        // Configure WebView settings
        webView.settings.apply {
            javaScriptEnabled = true
            domStorageEnabled = true  // Required for localStorage
            allowFileAccess = true
            mediaPlaybackRequiresUserGesture = false  // For speech synthesis
            setSupportZoom(false)
            builtInZoomControls = false
            displayZoomControls = false
            loadWithOverviewMode = true
            useWideViewPort = true
            cacheMode = WebSettings.LOAD_DEFAULT
        }

        webView.webViewClient = WebViewClient()
        webView.webChromeClient = WebChromeClient()

        // Load the app
        webView.loadUrl("file:///android_asset/index.html")
    }

    override fun onBackPressed() {
        if (webView.canGoBack()) {
            webView.goBack()
        } else {
            super.onBackPressed()
        }
    }
}
```

#### Step 4: Copy Build Files

1. Build the web app: `npm run build`
2. Copy contents of `dist/` folder to `app/src/main/assets/`

#### Step 5: Add Permissions

`app/src/main/AndroidManifest.xml`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.nammasanthe.ledger">

    <!-- Permissions -->
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.RECORD_AUDIO" />
    <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.NammaSanthe"
        android:usesCleartextTraffic="true">
        
        <activity
            android:name=".MainActivity"
            android:exported="true"
            android:configChanges="orientation|screenSize|keyboard|keyboardHidden"
            android:screenOrientation="portrait">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        
    </application>

</manifest>
```

#### Step 6: App Theme (No Action Bar)

`app/src/main/res/values/themes.xml`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <style name="Theme.NammaSanthe" parent="Theme.MaterialComponents.DayNight.NoActionBar">
        <item name="colorPrimary">#F97316</item>
        <item name="colorPrimaryVariant">#EA580C</item>
        <item name="colorOnPrimary">#FFFFFF</item>
        <item name="android:statusBarColor">#F97316</item>
        <item name="android:navigationBarColor">#FFFFFF</item>
        <item name="android:windowLightStatusBar">false</item>
    </style>
</resources>
```

---

## 🎨 App Icons

Create app icons for Android:

1. Use Android Studio: **Right-click res → New → Image Asset**
2. Select **Launcher Icons**
3. Use the shop emoji 🏪 or create a custom icon
4. Generate all density variants

---

## 🔧 Build Commands

```bash
# Development
npm run dev              # Start dev server at localhost:5173

# Production
npm run build            # Build to dist/ folder
npm run preview          # Preview production build

# Capacitor (after setup)
npx cap sync android     # Sync web build to Android
npx cap open android     # Open in Android Studio
npx cap run android      # Build and run on device
```

---

## 📋 Environment Variables

No environment variables required. The app uses:
- `localStorage` for data persistence
- Web Speech API for voice features
- WhatsApp/SMS URL schemes for reminders

---

## 🧪 Testing the App

### Test Credentials
The app uses OTP verification. In demo mode:
- OTP is displayed on screen
- OTP is spoken aloud
- Any name and 10-digit phone number works

### Test Scenarios
1. **Login as Creditor** → Full vendor dashboard
2. **Login as Debtor** → Customer view with dues
3. **Add Customer** → Use voice to speak name
4. **Add Credit** → Use numeric keypad or voice
5. **Send Reminder** → Opens WhatsApp with pre-filled message
6. **Set Auto Reminder** → Weekly reminder scheduling

---

## 🌍 Supported Languages

| Language | Code | Voice Recognition | Voice Output |
|----------|------|-------------------|--------------|
| Kannada | kn-IN | ✅ | ✅ |
| Hindi | hi-IN | ✅ | ✅ |
| English | en-IN | ✅ | ✅ |

---

## 📱 Minimum Requirements

### Android
- Android 7.0 (API 24) or higher
- WebView with JavaScript enabled
- Microphone permission (for voice features)
- Internet permission (for WhatsApp links)

### Web Browser
- Chrome 80+
- Firefox 75+
- Safari 13+
- Edge 80+

---

## 🐛 Known Issues

1. **Voice Recognition on Android WebView** - May require additional permissions and Chrome WebView
2. **Speech Synthesis** - Voice selection limited on some devices
3. **WhatsApp Deep Links** - Requires WhatsApp installed on device

---

## 🤝 Contributing

1. Fork the repository
2. Create feature branch: `git checkout -b feature/new-feature`
3. Commit changes: `git commit -m 'Add new feature'`
4. Push to branch: `git push origin feature/new-feature`
5. Submit pull request

---

## 📄 License

MIT License - Free to use and modify

---

## 👨‍💻 Developer Notes for Codex/AI Assistants

### Key Files to Modify

| Task | File(s) |
|------|---------|
| Add new language | `src/i18n/translations.ts` |
| Modify login flow | `src/components/LoginPage.tsx` |
| Change data storage | `src/store.ts` |
| Add new screens | `src/components/` + `src/App.tsx` |
| Modify voice features | `src/hooks/useSpeech.ts` |
| Update reminder logic | `src/services/reminderService.ts` |

### State Management
- Global state in `src/context/AppContext.tsx`
- User, language, and auth state
- No external state library (uses React Context)

### Data Models
```typescript
// Customer
interface Customer {
  id: string;
  name: string;
  phone: string;
  createdAt: string;
}

// Transaction
interface Transaction {
  id: string;
  customerId: string;
  amount: number;
  type: 'credit' | 'payment';
  note: string;
  date: string;
  createdAt: string;
}

// User (logged in)
interface User {
  id: string;
  name: string;
  phone: string;
  role: 'creditor' | 'debtor';
  shopName?: string;
}
```

### Converting to Backend API
To replace localStorage with a real backend:
1. Modify functions in `src/store.ts`
2. Replace `localStorage.getItem/setItem` with `fetch()` calls
3. Add authentication tokens to API requests
4. Update `AppContext` to handle async login

---

## 📞 Support

For issues or questions:
- Create a GitHub issue
- Contact: support@nammasanthe.com

---

**Made with ❤️ for Rural India**
