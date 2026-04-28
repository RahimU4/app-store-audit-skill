# App Store Audit Skill — Rule Engine v2.0.0

> This file is read by AI coding assistants to audit mobile apps before Apple App Store & Google Play Store submission.
> **95+ rules** across **21 categories** — works with **any** mobile framework.
> Flutter • React Native • Swift/SwiftUI • Kotlin/Jetpack Compose • KMP • Java • Xamarin • .NET MAUI

---

## 🧠 Platform Focus Areas

Before auditing, understand what each store focuses on:

| Apple App Store | Google Play Store |
|----------------|-------------------|
| Quality & polish | Policy compliance |
| UI/UX excellence | Security & malware |
| Real user value | Permissions abuse |
| Privacy first | Content rules |

---

# 🍎 APPLE APP STORE RULES

## 1. Payments & Subscriptions (3.1.x) — MOST CRITICAL

| ID | Severity | Rule | What to Search |
|----|----------|------|----------------|
| `AAPL-PAY-001` | 🔴 | **No custom promo/discount/coupon code fields on payment screens** | Any TextField with "Apply" near subscribe buttons. "promo", "coupon", "discount", "referral" on paywall |
| `AAPL-PAY-002` | 🔴 | **No external payment links** | stripe.com, paypal.com, square.com, external checkout URLs |
| `AAPL-PAY-003` | 🔴 | **No price manipulation** | Custom price overrides, dynamic pricing different from StoreKit |
| `AAPL-PAY-004` | 🔴 | **No mention of cheaper prices elsewhere** | "cheaper on website", "save by subscribing at", external pricing links |
| `AAPL-PAY-005` | 🔴 | **No crypto/NFT for digital content** | Crypto wallet, NFT, blockchain payment imports |
| `AAPL-PAY-006` | 🟡 | **Restore Purchases button MUST exist** | Every paywall must have "Restore Purchases" |
| `AAPL-PAY-007` | 🟡 | **Subscription terms visible on paywall** | Auto-renewal text, price, duration, cancellation info |
| `AAPL-PAY-008` | 🟡 | **Terms of Use link on paywall** | Must link to ToS on subscription screen |
| `AAPL-PAY-009` | 🟡 | **Privacy Policy link on paywall** | Must link to Privacy Policy on subscription screen |
| `AAPL-PAY-010` | 🟡 | **Free trial terms clear** | If trial exists, state what happens when it ends |
| `AAPL-PAY-011` | 🟡 | **Prices from StoreKit, not hardcoded** | Display prices should come from store API |

---

## 2. Privacy & Data (5.1.x)

| ID | Severity | Rule | What to Search |
|----|----------|------|----------------|
| `AAPL-PRIV-001` | 🔴 | **Privacy Policy URL required** | Must exist in App Store Connect AND in app |
| `AAPL-PRIV-002` | 🔴 | **No data collection without consent** | Must get user consent before collecting personal data |
| `AAPL-PRIV-003` | 🔴 | **ATT required if tracking** | If using IDFA, AdMob, Facebook SDK → must call `requestTrackingAuthorization` |
| `AAPL-PRIV-004` | 🟡 | **App Privacy labels accurate** | Data collection in App Store Connect must match actual collection |
| `AAPL-PRIV-005` | 🟡 | **NSUsageDescription strings required** | All permissions need purpose strings in Info.plist |
| `AAPL-PRIV-006` | 🟡 | **Only request needed permissions** | Unused permission requests = rejection |
| `AAPL-PRIV-007` | 🔴 | **No hidden data collection** | Don't collect contacts, photos, location without clear disclosure |

**Info.plist keys to verify:**
```
NSCameraUsageDescription, NSPhotoLibraryUsageDescription,
NSLocationWhenInUseUsageDescription, NSMicrophoneUsageDescription,
NSContactsUsageDescription, NSUserTrackingUsageDescription,
ITSAppUsesNonExemptEncryption (set NO if no custom encryption)
```

---

## 3. Intellectual Property (5.2.x)

| ID | Severity | Rule | What to Search |
|----|----------|------|----------------|
| `AAPL-IP-001` | 🔴 | **Must own/license all content** | All images, videos, music, text must be owned or licensed |
| `AAPL-IP-002` | 🔴 | **No copyrighted media without license** | Using copyrighted images/music/video = instant rejection |
| `AAPL-IP-003` | 🔴 | **No video/audio download capability** | Streaming apps must not allow saving media locally |
| `AAPL-IP-004` | 🟡 | **Content rights docs ready** | For streaming apps: prepare ownership statement for Resolution Center |
| `AAPL-IP-005` | 🟡 | **No trademark misuse** | Don't use Apple/Google logos inappropriately |

---

## 4. App Completeness & Functionality (2.1, 4.0)

| ID | Severity | Rule | What to Search |
|----|----------|------|----------------|
| `AAPL-FUNC-001` | 🔴 | **App must not crash on launch** | Test on latest iOS, all supported devices |
| `AAPL-FUNC-002` | 🔴 | **All buttons must work** | No dead buttons, broken navigation, missing actions |
| `AAPL-FUNC-003` | 🔴 | **Login/auth must work** | If app has login, it must work during review |
| `AAPL-FUNC-004` | 🔴 | **Backend APIs must be connected** | No "connection failed" screens. APIs must be live |
| `AAPL-FUNC-005` | 🔴 | **No placeholder content** | Search: "Lorem ipsum", "TODO", "Coming soon", "Test", placeholder images |
| `AAPL-FUNC-006` | 🔴 | **No demo/dummy data** | All content must be real, production-ready |
| `AAPL-FUNC-007` | 🟡 | **Minimum functionality required** | WebView-only apps rejected. Must have native features |
| `AAPL-FUNC-008` | 🟡 | **Works in airplane mode** | Must handle no-network gracefully (error messages, not crashes) |

---

## 5. UI/UX Quality (4.x)

| ID | Severity | Rule | What to Search |
|----|----------|------|----------------|
| `AAPL-UI-001` | 🔴 | **No broken layouts** | Test on all screen sizes (iPhone SE to Pro Max, iPad) |
| `AAPL-UI-002` | 🟡 | **No confusing navigation** | Users must be able to find all features easily |
| `AAPL-UI-003` | 🟡 | **Readable text** | No tiny/unreadable text, proper contrast ratios |
| `AAPL-UI-004` | 🟡 | **Follow platform design guidelines** | Use iOS patterns (no Material bottom nav on iOS) |
| `AAPL-UI-005` | 🔴 | **No beta/test/debug labels in UI** | Search: "beta", "test", "debug", "staging" in visible text |
| `AAPL-UI-006` | 🔴 | **No debug features in production** | Remove debug menus, test buttons, dev tools |

---

## 6. Spam & Duplicate Apps (4.3)

| ID | Severity | Rule | What to Search |
|----|----------|------|----------------|
| `AAPL-SPAM-001` | 🔴 | **No duplicate apps** | App must be meaningfully different from your other apps |
| `AAPL-SPAM-002` | 🔴 | **Must provide real user value** | Template apps (wallpaper, quotes) with no uniqueness = rejected |
| `AAPL-SPAM-003` | 🔴 | **No copy of another app** | Must be original work, not a clone |

---

## 7. Performance (2.x)

| ID | Severity | Rule | What to Search |
|----|----------|------|----------------|
| `AAPL-PERF-001` | 🔴 | **No laggy/slow UI** | Smooth 60fps animations, no jank |
| `AAPL-PERF-002` | 🔴 | **No excessive battery drain** | Check for background processes, location polling |
| `AAPL-PERF-003` | 🟡 | **No memory leaks** | Test for memory growth over time |
| `AAPL-PERF-004` | 🔴 | **No API secrets in client code** | Search: hardcoded API keys, backend secrets, admin tokens |
| `AAPL-PERF-005` | 🔴 | **No private Apple API usage** | Don't use undocumented APIs |

---

## 8. Security & Malware (2.3)

| ID | Severity | Rule | What to Search |
|----|----------|------|----------------|
| `AAPL-SEC-001` | 🔴 | **No malware/spyware behavior** | No hidden data collection, no keylogging |
| `AAPL-SEC-002` | 🔴 | **No hidden features** | All features must be visible during review |
| `AAPL-SEC-003` | 🔴 | **No obfuscated malicious code** | No encrypted payloads that activate post-review |

---

## 9. Content Policy (5.x)

| ID | Severity | Rule | What to Search |
|----|----------|------|----------------|
| `AAPL-CONT-001` | 🔴 | **No adult content without age gate** | If 17+ content, must have proper age verification |
| `AAPL-CONT-002` | 🔴 | **No hate speech** | No discriminatory or offensive content |
| `AAPL-CONT-003` | 🔴 | **No violence glorification** | No graphic violence encouragement |
| `AAPL-CONT-004` | 🔴 | **Gambling requires license** | Real-money gambling needs proof of license |
| `AAPL-CONT-005` | 🔴 | **No dangerous activities** | No encouraging unsafe behavior (e.g., phone use while driving) |
| `AAPL-CONT-006` | 🟡 | **UGC needs moderation** | User-generated content must have: reporting, blocking, filtering, ToS |
| `AAPL-CONT-007` | 🟡 | **Age rating must be accurate** | Set correct rating based on content |

---

## 10. Metadata & Store Listing

| ID | Severity | Rule | What to Check |
|----|----------|------|---------------|
| `AAPL-META-001` | 🔴 | **Screenshots must show actual app** | No mockups, no misleading images |
| `AAPL-META-002` | 🔴 | **No misleading description** | Description must match actual functionality |
| `AAPL-META-003` | 🔴 | **Version number must match** | Version in app UI must match App Store Connect |
| `AAPL-META-004` | 🟡 | **iPad screenshots if universal** | If `TARGETED_DEVICE_FAMILY = "1,2"`, iPad 13" screenshots needed |
| `AAPL-META-005` | 🟡 | **Subscription disclosure in description** | If subscriptions exist, describe pricing/renewal terms |
| `AAPL-META-006` | 🔴 | **App Privacy section completed** | Must be filled by Admin role — cannot submit without it |
| `AAPL-META-007` | 🟡 | **Support URL required** | Must provide working support URL |
| `AAPL-META-008` | 🟡 | **Review notes with test credentials** | If login required, provide test account |
| `AAPL-META-009` | 🟡 | **Correct app category** | Must be in the right category |
| `AAPL-META-010` | 🟡 | **SUPPORTED_PLATFORMS = iphoneos** | Not simulator. Check before archive |

---

## 11. Misleading & Hidden Functionality

| ID | Severity | Rule | What to Search |
|----|----------|------|----------------|
| `AAPL-MISLEAD-001` | 🔴 | **No fake features in description** | Don't promise features that don't exist |
| `AAPL-MISLEAD-002` | 🔴 | **No hidden functionality** | All features must be testable during review |
| `AAPL-MISLEAD-003` | 🔴 | **No fake buttons/links** | Every button must have real functionality |

---

# 🤖 GOOGLE PLAY STORE RULES

## 1. Billing & Payments

| ID | Severity | Rule | What to Search |
|----|----------|------|----------------|
| `GOOG-PAY-001` | 🔴 | **Use Play Billing for digital goods** | All in-app digital purchases must use Google Play Billing |
| `GOOG-PAY-002` | ✅ | **Physical goods can use external payment** | Stripe/PayPal OK for physical goods only |
| `GOOG-PAY-003` | ✅ | **Custom promo codes allowed (tracking)** | Google is more flexible than Apple — tracking codes OK |
| `GOOG-PAY-004` | 🟡 | **Subscription transparency required** | Must disclose pricing, billing cycle, cancellation |

---

## 2. Privacy & Permissions

| ID | Severity | Rule | What to Search |
|----|----------|------|----------------|
| `GOOG-PRIV-001` | 🔴 | **Privacy Policy required** | URL in Play Console AND in app |
| `GOOG-PRIV-002` | 🔴 | **Data Safety section required** | Must accurately fill out Data Safety form |
| `GOOG-PRIV-003` | 🔴 | **No unnecessary permissions** | Only request what app actually uses |
| `GOOG-PRIV-004` | 🟡 | **Runtime permissions for dangerous APIs** | Request at runtime, not just AndroidManifest |
| `GOOG-PRIV-005` | 🔴 | **Background location needs approval** | Requires justification and Google approval |
| `GOOG-PRIV-006` | 🔴 | **MANAGE_EXTERNAL_STORAGE restricted** | Requires declaration form |
| `GOOG-PRIV-007` | 🔴 | **SMS/Call Log restricted** | Requires declaration and approval |
| `GOOG-PRIV-008` | 🟡 | **Use READ_MEDIA_* on Android 13+** | Replace READ_EXTERNAL_STORAGE with READ_MEDIA_IMAGES/VIDEO |
| `GOOG-PRIV-009` | 🔴 | **No data harvesting** | Don't collect contacts, storage, location without need |

---

## 3. Content & IP

| ID | Severity | Rule | What to Search |
|----|----------|------|----------------|
| `GOOG-CONT-001` | 🔴 | **No misleading claims** | Don't promise features that don't exist |
| `GOOG-CONT-002` | 🔴 | **Content rating required** | Must complete IARC questionnaire |
| `GOOG-CONT-003` | 🟡 | **UGC needs moderation** | Reporting, blocking, moderation, ToS |
| `GOOG-CONT-004` | 🔴 | **Must own/license all content** | No copyright infringement |
| `GOOG-CONT-005` | 🔴 | **No restricted content** | No hate speech, violence, adult, gambling without license |

---

## 4. Security & Malware

| ID | Severity | Rule | What to Search |
|----|----------|------|----------------|
| `GOOG-SEC-001` | 🔴 | **No malware/spyware** | No hidden data collection, keylogging, trojans |
| `GOOG-SEC-002` | 🔴 | **No hidden features** | All functionality must be visible |
| `GOOG-SEC-003` | 🔴 | **No obfuscated malicious code** | No encrypted payloads activating post-review |

---

## 5. Spam & Duplicate

| ID | Severity | Rule | What to Search |
|----|----------|------|----------------|
| `GOOG-SPAM-001` | 🔴 | **No duplicate apps** | Must be meaningfully unique |
| `GOOG-SPAM-002` | 🔴 | **No app clones** | Must be original work |
| `GOOG-SPAM-003` | 🔴 | **Must provide real value** | Template/wallpaper apps with no uniqueness rejected |

---

## 6. Store Listing

| ID | Severity | Rule | What to Check |
|----|----------|------|---------------|
| `GOOG-LIST-001` | 🔴 | **App title ≤ 30 characters** | Google enforces max 30 chars |
| `GOOG-LIST-002` | 🟡 | **Feature graphic required** | 1024 x 500 px |
| `GOOG-LIST-003` | 🟡 | **Short description ≤ 80 characters** | Keep concise |
| `GOOG-LIST-004` | 🔴 | **No keyword stuffing** | Don't spam keywords in title/description |
| `GOOG-LIST-005` | 🟡 | **Contact info required** | Developer email, may need address |
| `GOOG-LIST-006` | 🔴 | **Screenshots must be accurate** | Must show actual app, not misleading |

---

## 7. Technical Requirements

| ID | Severity | Rule | What to Check |
|----|----------|------|---------------|
| `GOOG-TECH-001` | 🔴 | **Target SDK current (API 34+)** | Check targetSdkVersion in build.gradle |
| `GOOG-TECH-002` | 🔴 | **64-bit required (arm64-v8a)** | Must include arm64 architecture |
| `GOOG-TECH-003` | 🔴 | **AAB format required** | Upload .aab, not .apk |
| `GOOG-TECH-004` | 🔴 | **Version code must increment** | Higher versionCode than previous upload |
| `GOOG-TECH-005` | 🔴 | **No debuggable=true in release** | Check AndroidManifest for debug flags |
| `GOOG-TECH-006` | 🟡 | **Upload ProGuard mapping** | Debug symbols / obfuscation mapping |
| `GOOG-TECH-007` | 🔴 | **No ANR (App Not Responding)** | Test for hangs, slow operations on main thread |

---

## 8. Performance

| ID | Severity | Rule | What to Check |
|----|----------|------|---------------|
| `GOOG-PERF-001` | 🔴 | **No crashes on launch** | Test on multiple Android versions |
| `GOOG-PERF-002` | 🟡 | **No excessive battery drain** | Check background processes |
| `GOOG-PERF-003` | 🟡 | **No memory leaks** | Test for memory growth |
| `GOOG-PERF-004` | 🔴 | **No laggy UI** | Smooth scrolling, responsive interactions |

---

# ⚠️ ACCOUNT RISK WARNING

| Risk | Details |
|------|---------|
| **Repeated rejections** | Multiple rejections → account strikes |
| **Policy violations** | Repeated violations can **terminate developer account** |
| **Ban is permanent** | Google account termination is extremely difficult to reverse |
| **Apple is strict** | Too many rejections can delay future reviews |

> **Always fix ALL issues before resubmitting. Don't spam resubmissions.**

---

# ✅ MASTER PRE-SUBMISSION CHECKLIST

### App Quality
- [ ] App fully working — no crashes on any device
- [ ] All buttons/links functional
- [ ] No placeholder/dummy/test content
- [ ] Real production data (no static/fake API responses)
- [ ] No beta/debug labels visible
- [ ] No debug features in release build
- [ ] App provides real user value (not a clone/spam)
- [ ] Works offline gracefully (error messages, not crashes)
- [ ] No mixed/broken translations
- [ ] Tested on multiple devices and OS versions

### Payments (if applicable)
- [ ] All digital purchases use native IAP (Apple/Google)
- [ ] Restore Purchases button exists and works
- [ ] Subscription terms displayed (price, duration, renewal, cancellation)
- [ ] Terms of Use and Privacy Policy linked on paywall
- [ ] **No promo/coupon code fields on iOS paywall**
- [ ] Free trial terms clearly stated
- [ ] No external payment links
- [ ] No hidden paywalls (feature looks free then suddenly asks for payment)

### Privacy & Security
- [ ] Privacy Policy URL in store listing AND in app
- [ ] All permission descriptions filled (Info.plist / AndroidManifest)
- [ ] Only necessary permissions requested
- [ ] Data collection accurately declared (App Privacy / Data Safety)
- [ ] ATT prompt if using tracking (iOS)
- [ ] No hardcoded API secrets in client code
- [ ] No hidden data collection
- [ ] Account deletion option available (if login exists)

### Content & IP
- [ ] All media owned or licensed
- [ ] Content ownership docs prepared (streaming apps)
- [ ] Content rating accurately set
- [ ] No copyrighted material without license
- [ ] Age-appropriate content

### Store Listing
- [ ] Accurate screenshots of actual app
- [ ] All required screenshot sizes uploaded
- [ ] Description matches actual functionality — no misleading claims
- [ ] Subscription disclosure in description
- [ ] Contact/support info provided
- [ ] Test account in review notes (if login required)
- [ ] Version numbers match (app UI ↔ store listing)
- [ ] Correct app category selected
- [ ] No keyword stuffing

### Reviewer Experience (CRITICAL)
- [ ] Test account provided with clear instructions
- [ ] All features accessible without special hardware
- [ ] App works from any region (or provide VPN/demo mode)
- [ ] OTP/2FA works for test account
- [ ] Clear reviewer notes explaining non-obvious features
- [ ] Demo video provided (if hardware-dependent features)

### iOS Specific
- [ ] `ITSAppUsesNonExemptEncryption` set in Info.plist
- [ ] App Privacy section completed by Admin
- [ ] iPad screenshots uploaded (if universal app)
- [ ] `SUPPORTED_PLATFORMS = iphoneos` for archive
- [ ] Correct app category

### Android Specific
- [ ] Target SDK ≥ API 34
- [ ] 64-bit (arm64-v8a) included
- [ ] Uploaded as .aab
- [ ] Version code incremented
- [ ] Data Safety form completed — matches actual data collection
- [ ] No ANR issues

---

# 🔥 ADVANCED RULES — Edge Cases & Silent Killers

> These are the rules most developers don't know about. They cause "surprise rejections" that seem random but are actually predictable.

## 12. Reviewer Access & Experience (Silent Killer)

Apple & Google reviewers test from different devices, regions, and accounts. If they can't access your full app in 30 seconds → rejection.

| ID | Severity | Rule | What to Check |
|----|----------|------|---------------|
| `ADV-REV-001` | 🔴 | **Test account MUST be provided** | If login required, provide working credentials in review notes |
| `ADV-REV-002` | 🔴 | **OTP/2FA must work for test account** | If using OTP, provide a bypass or static code |
| `ADV-REV-003` | 🔴 | **Geo-restricted features must be accessible** | If features are country-locked, provide demo mode or VPN instructions |
| `ADV-REV-004` | 🔴 | **First 30 seconds must work perfectly** | Reviewer forms opinion in first 30 seconds. Splash → Home must be flawless |
| `ADV-REV-005` | 🟡 | **Clear reviewer notes** | Explain non-obvious features, navigation paths, special requirements |

---

## 13. External Hardware & Dependencies

| ID | Severity | Rule | What to Check |
|----|----------|------|---------------|
| `ADV-HW-001` | 🔴 | **Hardware-dependent features need demo mode** | If app needs Bluetooth device, IoT, car system → provide simulation/demo |
| `ADV-HW-002` | 🟡 | **Video proof for hardware features** | Record video showing hardware features working, attach to review notes |
| `ADV-HW-003` | 🔴 | **App must be usable without hardware** | Core experience should work even without connected device |

---

## 14. Push Notifications & Background Activity

| ID | Severity | Rule | What to Check |
|----|----------|------|---------------|
| `ADV-PUSH-001` | 🔴 | **No spam notifications** | Don't send excessive promotional push notifications |
| `ADV-PUSH-002` | 🔴 | **No promotional push without consent** | Must get user permission before marketing notifications |
| `ADV-PUSH-003` | 🔴 | **No misleading alerts** | Push content must match what user sees when opening |
| `ADV-BG-001` | 🔴 | **No unnecessary background services** | Don't run services that aren't needed |
| `ADV-BG-002` | 🔴 | **No background tracking without reason** | Location/activity tracking must have visible purpose |
| `ADV-BG-003` | 🟡 | **No excessive battery drain** | Test battery usage with profiling tools |

---

## 15. Account Management

| ID | Severity | Rule | What to Check |
|----|----------|------|---------------|
| `ADV-ACCT-001` | 🔴 | **Account deletion MUST be available in-app** | If users can create accounts, they MUST be able to delete them inside the app. Apple requires this since 2022 |
| `ADV-ACCT-002` | 🟡 | **Account deletion must actually work** | Don't just show a button — data must actually be deleted |
| `ADV-ACCT-003` | 🟡 | **Clear data retention policy** | Tell users what happens to their data after deletion |

---

## 16. Ads Implementation

| ID | Severity | Rule | What to Check |
|----|----------|------|---------------|
| `ADV-ADS-001` | 🔴 | **Ads must not cover UI** | No full-screen ads blocking essential navigation |
| `ADV-ADS-002` | 🔴 | **No accidental ad triggers** | Ads must not appear where users accidentally tap them |
| `ADV-ADS-003` | 🔴 | **No ads before app loads** | Don't show interstitial before user sees home screen |
| `ADV-ADS-004` | 🟡 | **Reasonable ad frequency** | Too many ads = poor experience = rejection |
| `ADV-ADS-005` | 🟡 | **Ads appropriate for content rating** | Ads must match app's age rating |

---

## 17. Fake Engagement & Manipulation

| ID | Severity | Rule | What to Check |
|----|----------|------|---------------|
| `ADV-ENGAGE-001` | 🔴 | **No fake ratings system** | Don't manipulate or fake review scores |
| `ADV-ENGAGE-002` | 🔴 | **No rewarding users for reviews** | Don't give coins/rewards for App Store reviews |
| `ADV-ENGAGE-003` | 🔴 | **No incentivized installs** | Don't pay users to install or rate the app |

---

## 18. Localization & Language

| ID | Severity | Rule | What to Check |
|----|----------|------|---------------|
| `ADV-LOC-001` | 🟡 | **No mixed languages in UI** | If app is English, everything must be English (no random Arabic/Chinese) |
| `ADV-LOC-002` | 🟡 | **No broken translations** | If localized, verify all strings are translated correctly |
| `ADV-LOC-003` | 🟡 | **Store listing language must match** | App Store language = app language |

---

## 19. Accessibility (Increasingly Important)

| ID | Severity | Rule | What to Check |
|----|----------|------|---------------|
| `ADV-A11Y-001` | 🟡 | **Support screen readers** | VoiceOver (iOS) / TalkBack (Android) should work |
| `ADV-A11Y-002` | 🟡 | **Support dynamic text sizes** | UI should adapt to system font size settings |
| `ADV-A11Y-003` | 🟡 | **Sufficient color contrast** | Text must be readable (WCAG AA minimum) |

---

## 20. Update & Version Issues

| ID | Severity | Rule | What to Check |
|----|----------|------|---------------|
| `ADV-VER-001` | 🔴 | **Updates must not break existing features** | Don't remove features existing users depend on |
| `ADV-VER-002` | 🔴 | **Unstable backend = rejection** | If server is down during review → rejected |
| `ADV-VER-003` | 🟡 | **Don't use beta/unstable APIs** | Backend must be stable during review period |

---

## 21. Hidden Paywall Traps

| ID | Severity | Rule | What to Check |
|----|----------|------|---------------|
| `ADV-PAYWALL-001` | 🔴 | **No hidden paid features** | Don't make features look free then suddenly ask payment |
| `ADV-PAYWALL-002` | 🔴 | **Free app must offer real value** | If freemium, free tier must be actually useful |
| `ADV-PAYWALL-003` | 🟡 | **Clear pricing before purchase** | User must know exact price before any payment action |

---

# 🧠 THE 4 LAYERS OF REJECTION

> **Pro insight:** Most developers only fix Layer 1 and get rejected again. You must pass ALL 4 layers.

```
┌─────────────────────────────────────┐
│  Layer 4: TRUST                     │
│  Privacy, transparency, honesty     │
├─────────────────────────────────────┤
│  Layer 3: EXPERIENCE                │
│  UI/UX quality, design, polish      │
├─────────────────────────────────────┤
│  Layer 2: POLICY                    │
│  Rules, permissions, billing        │
├─────────────────────────────────────┤
│  Layer 1: TECHNICAL                 │
│  Bugs, crashes, performance         │
└─────────────────────────────────────┘
```

| Layer | What Reviewers Check | Common Mistake |
|-------|---------------------|----------------|
| **Technical** | Does it crash? Does it work? | Devs fix this and think they're done |
| **Policy** | Does it follow the rules? | Devs don't read guidelines |
| **Experience** | Is it good to use? | Devs ignore polish and UX |
| **Trust** | Is it honest and transparent? | Devs hide limitations |

> **The hidden truth:** Many rejections happen because the reviewer had a **bad experience in the first 30 seconds** — couldn't login, didn't understand the app, feature didn't work instantly. It's not always about complex rules.

---

# 🤖 AI AGENT AUDIT INSTRUCTIONS

### Step 0: Detect Framework
Before scanning, identify which framework the project uses:

| Indicator File | Framework |
|---|---|
| `pubspec.yaml` | **Flutter** (Dart) |
| `package.json` + `react-native` dep | **React Native** (JS/TS) |
| `*.xcodeproj` + `*.swift` files only | **Native iOS** (Swift / SwiftUI) |
| `build.gradle.kts` + `*.kt` + no `pubspec.yaml` | **Native Android** (Kotlin / Jetpack Compose) |
| `build.gradle` + `*.java` files | **Native Android** (Java) |
| `shared/` + `androidApp/` + `iosApp/` | **Kotlin Multiplatform (KMP)** |
| `*.csproj` + `*.xaml` | **Xamarin / .NET MAUI** |

### Step 1: Identify App Type
- Free, paid, or subscription?
- Has login/accounts?
- Streams media?
- Has user-generated content?
- Which platforms? (iOS / Android / Both)
- Requires external hardware?
- Has ads?
- **Which framework?** (detected in Step 0)

### Step 2: Scan These Files

Scan the files relevant to the detected framework. Always scan the **Common** and **Platform Config** files, then scan the framework-specific source files.

#### Common (All Frameworks)
```
ios/Info.plist                    → Permissions, encryption flags
ios/**/Info.plist                  → (may be nested differently per framework)
android/**/AndroidManifest.xml    → Permissions, queries, debuggable flag
```

#### Platform Config by Framework

**Flutter:**
```
pubspec.yaml                      → Version, dependencies
ios/Runner.xcodeproj/             → SUPPORTED_PLATFORMS, DEVICE_FAMILY
android/app/build.gradle           → targetSdk, versionCode, arm64
```

**React Native:**
```
package.json                      → Version, dependencies
ios/*.xcodeproj/                  → Build settings, device family
android/app/build.gradle           → targetSdk, versionCode, arm64
app.json / app.config.js          → Expo config (if using Expo)
```

**Native iOS (Swift / SwiftUI):**
```
*.xcodeproj / *.xcworkspace       → Build settings, signing
Podfile / Package.swift           → Dependencies
*.plist                           → All Info.plist variants
*.entitlements                    → Capabilities (IAP, push, etc.)
```

**Native Android (Kotlin / Java / Jetpack Compose):**
```
build.gradle / build.gradle.kts   → targetSdk, versionCode, dependencies
gradle.properties                 → Build config flags
proguard-rules.pro                → Obfuscation rules
```

**Kotlin Multiplatform (KMP):**
```
shared/build.gradle.kts           → Shared module config
androidApp/build.gradle.kts       → Android target config
iosApp/*.xcodeproj                → iOS target config
gradle.properties                 → Build flags
```

**Xamarin / .NET MAUI:**
```
*.csproj                          → Project config, target frameworks
Properties/AndroidManifest.xml    → Android permissions
Platforms/iOS/Info.plist          → iOS permissions
```

#### Source Files to Search (by framework)

**Flutter (Dart):**
```
lib/**/*paywall*                  → Subscription UI (CRITICAL)
lib/**/*subscription*             → Payment logic
lib/**/*purchase*                 → IAP integration
lib/**/*profile*                  → Version display, legal links, account deletion
lib/**/*constants*                → API keys, URLs, flags
lib/**/*notification*             → Push notification handling
lib/**/*auth*                     → Login/account management
```

**React Native (JS/TS):**
```
src/**/*paywall*                  → Subscription UI (CRITICAL)
src/**/*subscription*             → Payment logic
src/**/*purchase*                 → IAP integration (react-native-iap)
src/**/*profile*                  → Version display, legal links
src/**/*config*                   → API keys, URLs, flags
src/**/*notification*             → Push notifications (FCM, APNs)
src/**/*auth*                     → Login/account management
.env / .env.production            → Environment variables / secrets
```

**Native iOS (Swift / SwiftUI):**
```
**/*Paywall*                      → Subscription UI (CRITICAL)
**/*StoreKit* / **/*Purchase*     → IAP / StoreKit 2 integration
**/*Subscription*                 → Payment logic
**/*Profile*                      → Version display, legal links
**/*Constants* / **/*Config*      → API keys, URLs, flags
**/*Notification*                 → Push notification handling
**/*Auth* / **/*Login*            → Login/account management
**/*AppDelegate*                  → App lifecycle, permissions
```

**Native Android (Kotlin / Java / Jetpack Compose):**
```
**/*Paywall*                      → Subscription UI (CRITICAL)
**/*Billing* / **/*Purchase*      → Google Play Billing integration
**/*Subscription*                 → Payment logic
**/*Profile*                      → Version display, legal links
**/*Constants* / **/*Config*      → API keys, URLs, flags
**/*Notification* / **/*FCM*      → Push notification handling
**/*Auth* / **/*Login*            → Login/account management
**/*Application.kt / .java*      → App lifecycle
```

**KMP (Kotlin Multiplatform):**
```
shared/src/commonMain/**          → Shared business logic
shared/src/androidMain/**         → Android-specific code
shared/src/iosMain/**             → iOS-specific code
androidApp/src/**                 → Android app layer
iosApp/iosApp/**                  → iOS app layer
```

### Step 3: Check Every Rule
For each rule in this document:
1. Search the codebase for relevant patterns
2. Flag any violations with the Rule ID and severity
3. Provide the exact file path and line number
4. Write a clear, step-by-step fix instruction the developer can follow immediately

### Step 4: Generate the Audit Report

**IMPORTANT:** The report is the most critical output. It must be professional, clear, and actionable. The developer should be able to read the report and fix every issue without asking follow-up questions.

Use this EXACT format:

```markdown
# 🛡️ App Store Audit Report

| Field | Value |
|-------|-------|
| **App** | [App Name] |
| **Version** | [Version + Build Number] |
| **Platforms** | iOS / Android / Both |
| **Audit Date** | [Date] |
| **Rules Checked** | 95+ |
| **Result** | 🔴 NOT READY / 🟡 NEEDS FIXES / ✅ READY TO SUBMIT |

---

## 📊 Summary

| Category | Status | Issues |
|----------|--------|--------|
| Payments & Billing | ✅ / 🔴 / 🟡 | [count] |
| Privacy & Data | ✅ / 🔴 / 🟡 | [count] |
| Intellectual Property | ✅ / 🔴 / 🟡 | [count] |
| App Completeness | ✅ / 🔴 / 🟡 | [count] |
| UI/UX Quality | ✅ / 🔴 / 🟡 | [count] |
| Store Metadata | ✅ / 🔴 / 🟡 | [count] |
| Security | ✅ / 🔴 / 🟡 | [count] |
| Reviewer Experience | ✅ / 🔴 / 🟡 | [count] |
| Advanced Checks | ✅ / 🔴 / 🟡 | [count] |

### Layer Assessment
| Layer | Status | Notes |
|-------|--------|-------|
| 🔧 Technical | ✅ / 🔴 | [Does app crash? Does everything work?] |
| 📜 Policy | ✅ / 🔴 | [Does it follow store rules?] |
| 🎨 Experience | ✅ / 🔴 | [Is it polished and user-friendly?] |
| 🤝 Trust | ✅ / 🔴 | [Is it honest and transparent?] |

---

## 🔴 Critical Issues — Will Cause Rejection

> Fix ALL of these before submitting. Any single critical issue = guaranteed rejection.

### Issue 1: [Short Title]
| Field | Detail |
|-------|--------|
| **Rule** | `[RULE-ID]` — [Rule Name] |
| **Severity** | 🔴 Critical |
| **Store** | Apple / Google / Both |
| **Location** | `[file_path]` line [number] |
| **What's Wrong** | [Clear explanation of the problem] |
| **Why It's Rejected** | [Which guideline and why reviewers flag this] |
| **How to Fix** | See steps below |

**Fix Steps:**
1. Open `[file_path]`
2. Go to line [number]
3. [Exact change to make — show before/after code if applicable]
4. [Any additional steps — rebuild, update config, etc.]

**Before (problematic):**
```
// Show the code that causes the issue (use the project's language)
```

**After (fixed):**
```
// Show the corrected code (use the project's language)
```

---

### Issue 2: [Short Title]
[Same format as above for each critical issue]

---

## 🟡 Warnings — May Cause Rejection

> These are lower risk but should be fixed for a smooth review.

### Warning 1: [Short Title]
| Field | Detail |
|-------|--------|
| **Rule** | `[RULE-ID]` — [Rule Name] |
| **Severity** | 🟡 Warning |
| **Store** | Apple / Google / Both |
| **Location** | `[file_path]` line [number] or [App Store Connect / Play Console] |
| **What's Wrong** | [Clear explanation] |
| **How to Fix** | [Clear step-by-step fix] |

---

## ✅ Passed Checks

> These categories passed all checks. No action needed.

| Category | Rules Checked | Result |
|----------|:------------:|--------|
| [Category Name] | [count] | ✅ All passed |
| [Category Name] | [count] | ✅ All passed |

---

## ⚠️ Platform Differences

> Things that work on one platform but NOT the other.

| Feature | Android | iOS | Action Needed |
|---------|:-------:|:---:|---------------|
| [Feature] | ✅ Allowed | 🔴 Not Allowed | [What to do] |
| [Feature] | [status] | [status] | [What to do] |

---

## 📋 Recommended Reviewer Notes

> Copy-paste this into App Store Connect / Play Console review notes.

**For Apple App Store:**
```
Test Account:
Email: [test@example.com]
Password: [password]

App Overview:
[Brief description of what the app does]

How to Test Key Features:
1. [Feature 1]: [How to access and test]
2. [Feature 2]: [How to access and test]

Notes:
- [Any special instructions]
- [Hardware/geo requirements and workarounds]
```

**For Google Play:**
```
[Similar template for Play Console]
```

---

## 🔄 Action Items Summary

> Quick reference of everything you need to fix, in priority order.

### 🔴 Must Fix (Before Submission)
| # | Action | File / Location | Est. Time |
|---|--------|----------------|-----------|
| 1 | [Action description] | `[file]` | [time] |
| 2 | [Action description] | `[file]` | [time] |

### 🟡 Should Fix (Recommended)
| # | Action | File / Location | Est. Time |
|---|--------|----------------|-----------|
| 1 | [Action description] | `[file]` | [time] |

### 📋 Store Console Actions (Non-Code)
| # | Action | Where |
|---|--------|-------|
| 1 | [Action] | App Store Connect / Play Console |
| 2 | [Action] | App Store Connect / Play Console |

---

## ✅ Ready to Submit?

| Criteria | Status |
|----------|--------|
| All 🔴 critical issues fixed | ⬜ / ✅ |
| All 🟡 warnings reviewed | ⬜ / ✅ |
| Reviewer notes prepared | ⬜ / ✅ |
| Store listing complete | ⬜ / ✅ |
| **VERDICT** | 🔴 NOT READY / ✅ READY |

> Run this audit again after fixing all issues to verify.
```

### Step 5: Flag Platform Differences
- ✅ Allowed on Android but NOT iOS (e.g., custom promo codes)
- ✅ Allowed on iOS but NOT Android (e.g., certain patterns)
- ⚠️ Different requirements per store

### Step 6: Evaluate 4 Layers
For each layer (Technical, Policy, Experience, Trust), give a pass/fail:
```
Layer Assessment:
✅ Technical  — No crashes, all features work
🟡 Policy     — Missing subscription disclosure in description
✅ Experience  — Clean UI, good navigation
🔴 Trust      — No account deletion option
```

---

## 📚 Official References

| Resource | URL |
|----------|-----|
| Apple Review Guidelines | https://developer.apple.com/app-store/review/guidelines/ |
| Apple HIG | https://developer.apple.com/design/human-interface-guidelines/ |
| Google Play Policy | https://play.google.com/about/developer-content-policy/ |
| Google Play Billing | https://developer.android.com/google/play/billing |
| Apple StoreKit | https://developer.apple.com/storekit/ |
| Apple Account Deletion Requirement | https://developer.apple.com/support/offering-account-deletion-in-your-app/ |

---

## Known Rejection Cases (Real-World)

| App | Store | Rule | What Happened |
|-----|-------|------|---------------|
| B3G TV | Apple | `AAPL-PAY-001` | Promo code field on paywall — rejected even tracking-only |
| B3G TV | Apple | `AAPL-IP-004` | Content rights questioned for streaming app |
| B3G TV | Apple | `AAPL-META-006` | App Privacy not filled — requires Admin role |

> **Add your rejection cases here to help the community!**

---

## Changelog

### v2.0.0 (April 2026)
- **🌐 Multi-platform support** — Now works with Flutter, React Native, Swift, Kotlin, Jetpack Compose, KMP, Java, Xamarin, .NET MAUI
- Added framework auto-detection (Step 0) for AI agents
- Added platform-specific file scan paths for all major frameworks
- Code examples are now language-agnostic
- **Total: 95+ rules across 21 categories, all frameworks**

### v1.2.0 (April 2026)
- Added 25+ advanced edge-case rules (Sections 12–21)
- Added "4 Layers of Rejection" framework
- Added: Reviewer Access, Hardware Dependencies, Push Notifications, Account Deletion, Ads, Fake Engagement, Localization, Accessibility, Version Issues, Hidden Paywalls
- Expanded checklist with Reviewer Experience section
- Updated AI instructions with Layer Assessment
- **Total: 95+ rules across 21 categories**

### v1.1.0 (April 2026)
- Expanded to 15 categories, 70+ rules
- Added severity levels (🔴 Critical, 🟡 Warning)
- Added Master Pre-Submission Checklist

### v1.0.0 (April 2026)
- Initial release — 50+ rules for Apple & Google

