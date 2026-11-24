# 💳 Skrollify - In-App Purchases & Regional Pricing Guide

This guide explains how the payment system is built in **Skrollify**, why **Google Play Billing** is used, and gives step-by-step instructions to configure the 3 pricing tiers and local Purchasing Power Parity (PPP) in the **Google Play Console**.

---

## 1. Which Payment System to Use?

For Android apps published on the **Google Play Store**, you **must use Google Play Billing**.

> [!IMPORTANT]
> **Google Play Policy Requirement:**  
> Google strictly forbids third-party payment gateways (like Stripe, PayPal, Razorpay, or external web links) for in-app digital features, focus tools, and digital unlocks. If an app tries to use external payment links, Google will reject or suspend the app.
>
> **The Great Advantage of Google Play Billing:**  
> • Handles all local payment methods automatically: **UPI & Netbanking** in India, **Easypaisa, JazzCash & Cards** in Pakistan, **bKash & Cards** in Bangladesh, Google Pay, Carrier Billing, and Credit/Debit cards worldwide.  
> • Automatically converts currencies and lets you set custom Purchasing Power Parity (PPP) prices per country (e.g. 200 PKR in Pakistan, ₹69 in India, $0.79 in the US).  
> • Users trust Google's 1-tap fingerprint/PIN checkout.

---

## 2. The 3 Skrollify Pricing Categories

The app is configured in code (`PlayBillingManager.kt` & `ProPaywallDialog.kt`) to query and handle these 3 tiers:

| Tier | Category | Product ID | Type | Default USD | Pakistan (PKR) | India (INR) | Bangladesh (BDT) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Tier 1** | **Monthly Support / Starter** | `skrollify_starter_monthly` | **Subscription** | **$0.79 / month** | **Rs. 200 / mo** | **₹69 / mo** | **85 BDT / mo** |
| **Tier 2** | **Annual Pro (Most Popular)** | `skrollify_pro_annual` | **Subscription** | **$2.99 / year** | **Rs. 750 / yr** | **₹249 / yr** | **320 BDT / yr** |
| **Tier 3** | **Lifetime Access (Best Value)** | `skrollify_lifetime_vip` | **In-App (One-Time)** | **$4.99 once** | **Rs. 1,350 once**| **₹399 once** | **550 BDT once** |

---

## 3. Step-by-Step: Setting Up the Products in Google Play Console

Once you create your app in Google Play Console:

### Step 3.1: Create Tier 3 (Lifetime Access - One-Time Purchase)
1. Go to **Google Play Console** > select **Skrollify**.
2. In the left navigation, scroll to **Monetize with Play** > **Products** > click **In-app products**.
3. Click **Create product**:
   - **Product ID:** `skrollify_lifetime_vip`
   - **Name:** `Skrollify Lifetime VIP`
   - **Description:** `Lifetime access to all Pro features, custom 2.5D avatar looks, and unlimited reports.`
4. Under **Price**, click **Set price**:
   - Set Default price to **USD 4.99**.
   - Google Play will automatically calculate local country prices.
   - Click **Edit country / region prices** to customize:
     - **Pakistan:** Set to `1350 PKR`
     - **India:** Set to `399 INR`
     - **Bangladesh:** Set to `550 BDT`
5. Click **Apply**, then **Save**, and click **Activate**.

---

### Step 3.2: Create Tier 1 (Monthly Support - Subscription)
1. In the left menu, go to **Monetize with Play** > **Products** > click **Subscriptions**.
2. Click **Create subscription**:
   - **Subscription ID:** `skrollify_starter_monthly`
   - **Name:** `Skrollify Monthly Support`
   - **Description:** `Billed monthly. Unlocks all Pro focus tools and custom avatar options.`
3. Click **Create**.
4. In the subscription details, click **Add base plan**:
   - **Base plan ID:** `starter-monthly-plan`
   - **Type:** **Auto-renewing**
   - **Billing period:** **Monthly**
   - **Grace period:** 7 days
5. Under **Set prices**:
   - Set Default price to **USD 0.79**.
   - Click **Set prices per country / region**:
     - **Pakistan:** Set to `200 PKR`
     - **India:** Set to `69 INR`
     - **Bangladesh:** Set to `85 BDT`
6. Click **Save** > **Activate base plan** > **Activate subscription**.

---

### Step 3.3: Create Tier 2 (Annual Pro - Subscription)
1. In **Subscriptions**, click **Create subscription**:
   - **Subscription ID:** `skrollify_pro_annual`
   - **Name:** `Skrollify Annual Pro`
   - **Description:** `1 full year of all Pro features at a 70% discount compared to monthly.`
2. Click **Add base plan**:
   - **Base plan ID:** `annual-pro-plan`
   - **Type:** **Auto-renewing**
   - **Billing period:** **Yearly**
   - **Grace period:** 14 days
3. Under **Set prices**:
   - Set Default price to **USD 2.99**.
   - Custom country prices:
     - **Pakistan:** Set to `750 PKR`
     - **India:** Set to `249 INR`
     - **Bangladesh:** Set to `320 BDT`
4. Click **Save** > **Activate base plan** > **Activate subscription**.

---

## 4. How to Test Payments For Free (License Testing)

You and your testers do not need to spend real money to test payments!

1. In Google Play Console, go to **Setup** > **License testing**.
2. In the **Add license testers** field, add your Gmail account (and any tester emails).
3. Under **License response**, select:
   - `RESPOND_NORMALLY` (allows you to test real and test cards).
4. When testing the app installed via Internal Testing track or signed with your debug key:
   - When you tap **Lifetime Access**, **Annual Pro**, or **Monthly Support**, Google Play displays a test bottom sheet with:
     `"Test card, always approves"` or `"Test card, always declines"`.
   - Tap **Subscribe** or **1-Tap Buy** -> Pro unlocks instantly without charging your card!

---

## 5. Summary of Architecture in Code

- **`PlayBillingManager.kt`**: Connects to Google Play Billing Library 7.x, queries product IDs, launches purchase flows with `offerToken`, acknowledges purchases, and caches Pro status locally in encrypted/private SharedPreferences.
- **`ProPaywallDialog.kt`**: Shows the 3 tiers with live currency formatting parsed directly from Google Play (falls back gracefully to `$4.99`, `$2.99`, and `$0.79` if offline).
- **Offline & Cross-Device Protection**: When user signs in, their purchase token is automatically synced to Firebase Firestore so they never lose Pro when switching phones.
