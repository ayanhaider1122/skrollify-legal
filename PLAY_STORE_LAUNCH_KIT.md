# 🚀 Skrollify - Google Play Store Launch Kit

This guide contains everything required to publish **Skrollify** (`com.ayanhaider.skrollify`) to the Google Play Store, including exact store listing copy, policy compliance forms, Accessibility declaration answers, signing instructions, and asset specs.

---

## 1. Store Listing Metadata

### App Title (max 30 characters)
```text
Skrollify: Reels & Shorts Stop
```
*(Alternative: `Skrollify: Screen Time & Reels`)*

### Short Description (max 80 characters)
```text
Stop doomscrolling short videos. Real-time counter, avatar moods & focus limits.
```

### Full Description (max 4000 characters)
```text
Are hours disappearing into endless short-form videos? Reclaim your focus and conquer doomscrolling with Skrollify!

Skrollify is the intelligent digital-wellbeing companion designed specifically to tackle short-form video addiction across Instagram Reels, YouTube Shorts, TikTok, Facebook Reels, and Snapchat Spotlight.

Unlike generic screen-time timers that you easily ignore, Skrollify introduces a live floating counter and an emotional companion avatar that reacts in real-time as you scroll.

⚡ KEY FEATURES

🎯 Real-Time Short Video Counter
See exactly how many Reels, Shorts, and Spotlights you've watched right as you scroll. Our lightweight, non-intrusive floating HUD keeps you conscious of every swipe.

🌱 Emotional Companion Avatar
Customize your mindful companion! Watch your avatar thrive when you stay focused, and react with changing expressions when you binge past your daily goals.

🛑 Smart Focus Controls & Tab Lock
Take back control with customizable limits:
• Auto-Exit Reels: Automatically redirects you out of short-video feeds when your session target is reached.
• Strict Limit: Enforces cooling-off periods to break infinite scroll dopamine loops.
• Custom Allowances: Tailor daily reel goals for weekdays vs weekends.

📊 In-Depth Analytics & History
• Day & Week Breakdown: Review detailed historical usage day-by-day (Today, Yesterday, past days) or week-by-week.
• Cross-App Monitoring: Track short-form videos alongside full screen time for apps like WhatsApp, Reddit, and LinkedIn.
• Clean Visual Charts: Spot your peak scrolling hours and celebrate your progress over time.

👥 Accountability Groups & Leaderboards (Optional)
Create private groups with friends or family! Compete in friendly leaderboards to see who can maintain the lowest reel count each week.

🔒 PRIVACY-FIRST & BATTERY EFFICIENT
• Zero tracking of personal content: Skrollify NEVER reads typed text, passwords, private chats, photos, or searches.
• 100% on-device detection: Video counting is computed locally in memory with negligible battery impact.
• No account required: You can use all core tracking features completely offline without signing in.

---------------------------------------------------
ACCESSIBILITY SERVICE API DISCLOSURE:
Skrollify uses Android's AccessibilityService API solely to detect when short-video player screens (Instagram Reels, YouTube Shorts, TikTok, Facebook Reels, Snapchat Spotlight) are active on your device. This allows Skrollify to increment the video counter and enforce your chosen digital wellbeing limits. Skrollify does NOT record, log, or transmit any keystrokes, personal messages, camera, or audio data.
---------------------------------------------------

Download Skrollify today and turn mindless scrolling into mindful living!
```

### Category & Tags
- **Primary Category:** Tools (or Productivity / Health & Fitness > Digital Wellbeing)
- **Tags:** Digital Wellbeing, Screen Time, Focus, Habit Tracker, Productivity

---

## 2. Google Play Policy & Declarations (CRITICAL)

### Accessibility Service Declaration (Play Console Question)
When Google Play Console asks for the Accessibility Service declaration:

**Q1: Is this an Accessibility tool designed primarily for people with disabilities?**
> Select: **No**

**Q2: What features does the Accessibility API support in your app?**
> Check: **Other (Digital Wellbeing / Focus Management)**

**Q3: Describe how the Accessibility API is used and why it is necessary:**
> *Paste this exact text:*
> `"Skrollify uses the AccessibilityService API solely to detect user-initiated transitions inside short-form video player interfaces (specifically Instagram Reels, YouTube Shorts, TikTok, Facebook Reels, and Snapchat Spotlight). This is strictly required to increment the user's daily video count and trigger user-configured digital wellbeing boundaries (such as auto-exiting the short-form video container when their self-imposed reel goal is exceeded). The service inspects window and scroll events in-memory on the device; it NEVER captures screenshots, NEVER logs typed text, passwords, private messages, or personal communications, and NEVER transmits accessibility data off the device."`

**Q4: Demonstration Video Link:**
> Google Play requires a publicly accessible video link (e.g. unlisted YouTube video) demonstrating:
> 1. The in-app prominent disclosure dialog explaining why Accessibility is requested before the user is taken to Android Settings.
> 2. The user granting permission.
> 3. The feature in action (e.g., scrolling a short video and the counter incrementing).
> *(Note: You can easily upload a 30-45s screen recording to YouTube as Unlisted and paste the link here).*

---

### Data Safety Form Answers
In the Google Play Console **Data safety** section:
- **Does your app collect or share any user data?** Yes (if using Firebase Auth/Cloud Sync) or No (if strictly local).
  - *If Yes:*
    - **App info and performance:** Crash logs / Diagnostics (No personal data).
    - **Personal info:** Email address & User ID (Only if user signs in via Google or Email for group sync).
    - **Is all data encrypted in transit?** Yes (HTTPS/TLS).
    - **Do you provide a way for users to request data deletion?** Yes (in-app under Account Settings or via contact email).
    - **Is data collection optional?** Yes (users can use the app without signing in).

---

## 3. Store Listing Graphics & Asset Requirements

| Asset | Dimensions | Format | Requirement |
| :--- | :--- | :--- | :--- |
| **App Icon** | 512 x 512 px | PNG (32-bit, max 1024 KB) | Mandatory |
| **Feature Graphic** | 1024 x 500 px | JPEG or PNG (max 1024 KB) | Mandatory |
| **Phone Screenshots** | Min 2, Max 8 (16:9 or 9:16) | PNG or JPEG (min 1080x1920 recommended) | Mandatory |

---

## 4. Release Keystore & App Bundle Generation

Google Play requires an **Android App Bundle (.aab)** signed with a release upload key.

### Step 1: Generate Release Keystore (One-Time Command)
Run this command in PowerShell or Terminal to generate your production release keystore:
```powershell
keytool -genkeypair -v -keystore skrollify-release-key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias skrollify -storepass "YourSecurePassword" -keypass "YourSecurePassword"
```
*(Store `skrollify-release-key.jks` and your password in a safe, secure backup!)*

### Step 2: Build the Production AAB Bundle
Run:
```powershell
.\gradlew bundleRelease
```
The output file is generated at:
```text
app/build/outputs/bundle/release/app-release.aab
```
*Current AAB Size:* **~22.5 MB** *(delivers ~15-18 MB to user devices!)*

---

## 5. Google Play Console Submission Steps

1. **Log in to [Google Play Console](https://play.google.com/console)** with your developer account ($25 one-time registration).
2. Click **Create app**:
   - App name: `Skrollify`
   - Default language: `English (United States)`
   - App or game: `App`
   - Free or paid: `Free`
3. Under **Set up your app**:
   - **Privacy Policy:** Paste your live URL: `https://ayanhaider1122.github.io/skrollify-legal/privacy-policy.html`
   - **App Access:** "All functionality is available without special access".
   - **Ads:** "No, my app does not contain ads".
   - **Content Rating:** Complete questionnaire (Select "Utility/Productivity" -> Rating will be Everyone / Teen).
   - **Target Audience:** Select `13-15`, `16-17`, `18 and over` (Do NOT select under 13 to avoid COPPA restrictions).
   - **Accessibility Declaration:** Fill out using Section 2 above.
   - **Data Safety:** Fill out using Section 2 above.
4. Under **Store presence > Main store listing**:
   - Paste App Title, Short Description, and Full Description from Section 1 above.
   - Upload 512x512 App Icon, 1024x500 Feature Graphic, and Screenshots.
5. Under **Release > Production (or Internal testing)**:
   - Create new release.
   - Upload `app-release.aab`.
   - Release name: `1.0 (1)`.
   - Release notes: `"Initial launch of Skrollify - Reclaim your focus from short-form video doomscrolling."`
   - Review and rollout!
