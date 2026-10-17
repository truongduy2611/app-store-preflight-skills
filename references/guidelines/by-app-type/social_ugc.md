# Checklist: Social / User-Generated Content Apps

Guidelines specifically applying to social networking, messaging, community, and UGC platform apps.

## Critical (Will Reject)

- [ ] **1.2** — Content moderation: filter for objectionable material
- [ ] **1.2** — Report mechanism for offensive content with timely responses
- [ ] **1.2** — Ability to block abusive users
- [ ] **1.2** — Published contact information for user support
- [ ] **1.2** — Prevent and remove nonconsensual intimate imagery (including AI-generated)
- [ ] **1.2** — Process to remove violating content after notice — failing to remediate risks a Developer Code of Conduct violation and removal
- [ ] **4.8** — If offering third-party login (Facebook, Google, etc.), must also offer Sign in with Apple or equivalent
- [ ] **4.0** — Sign in with Apple: don't re-ask name/email after SIWA auth
- [ ] **5.1.1(v)** — If account creation exists, must also offer account deletion
- [ ] **5.1.1(v)** — Must provide access without social login if core functionality isn't social-network-specific
- [ ] **5.1.1(i)** — Privacy policy required (in-app + App Store Connect)

## Important (Common Rejections)

- [ ] **1.1.1** — No defamatory, discriminatory, or mean-spirited content
- [ ] **2.5.14** — Explicit consent for recording user activity (camera, microphone, screen)
- [ ] **5.1.1(ii)** — User consent for data collection; clear purpose strings
- [ ] **5.1.2(i)** — ATT framework required for cross-app tracking
- [ ] **5.1.1(viii)** — No compiling personal info from non-user sources (public databases)
- [ ] **4.5.4** — Push notifications: not required to function; opt-in for marketing
- [ ] **5.1.1(iii)** — Data minimization: only request data relevant to core functionality

## UGC-Specific Rules

- [ ] NSFW content from web services: hidden by default, opt-in via website only
- [ ] No Chatroulette-style random chat, anonymous bullying, or "hot-or-not" voting
- [ ] No apps primarily used for pornographic content
- [ ] **1.2** — Random or anonymous chat apps are subject to all UGC requirements

## Age Rating & Age Assurance

- [ ] **2.3.6** — Age rating questionnaire's **social media capability** questions answered (required since September 2026). A social feed or similar discovery of UGC counts; it puts the app in the Social Media Time Allowance category and adds a Social Media content descriptor
- [ ] **1.2.1(a)** — Creator apps: users can identify content above the app's age rating; access is restricted by verified or declared age
- [ ] **Australia** — Social media platforms must prevent under-16s from holding accounts (since December 10, 2025); use the Declared Age Range API and state the restriction in the app description
- [ ] **Texas / Utah / Louisiana** — Age assurance and parental consent for minors; use the Declared Age Range API and PermissionKit Significant Change API
