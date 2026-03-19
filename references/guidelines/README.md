# Apple App Store Review Guidelines — Complete Reference

> Source: [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)

This is a structured index of every guideline section, organized for quick lookup. Use the [app-type checklists](./by-app-type/) to find which guidelines apply to your specific type of app.

---

## Section 1: Safety

| Guideline | Title | Summary |
|-----------|-------|---------|
| 1.1 | Objectionable Content | No offensive, discriminatory, violent, sexual, or misleading content |
| 1.1.1 | Defamatory Content | No discrimination by religion, race, gender, etc. |
| 1.1.2 | Violence | No realistic portrayals of killing/torture; game enemies can't target real groups |
| 1.1.3 | Weapons | No encouragement of illegal weapon use; no facilitating firearm purchases |
| 1.1.4 | Sexual Content | No pornographic material; no hookup/prostitution facilitation |
| 1.1.5 | Religious Content | No inflammatory religious commentary |
| 1.1.6 | False Information | No fake features, fake location trackers, prank calls |
| 1.1.7 | Harmful Concepts | No profiting from recent tragedies |
| 1.2 | User-Generated Content | Must have: content filter, report mechanism, block users, contact info |
| 1.2.1 | Creator Content | Creator apps must moderate content and restrict by age |
| 1.3 | Kids Category | No external links, no third-party analytics/ads, strict privacy rules |
| 1.4 | Physical Harm | No apps risking physical harm |
| 1.4.1 | Medical Apps | Must disclose methodology; can't claim sensor-only diagnostics |
| 1.4.2 | Drug Dosage | Must come from approved medical entities |
| 1.4.3 | Substance Use | No encouraging tobacco, vape, drugs, excessive alcohol |
| 1.4.4 | DUI Checkpoints | Only law-enforcement-published checkpoints |
| 1.4.5 | Risky Activities | No encouraging dangerous bets/challenges |
| 1.5 | Developer Information | Must include easy contact info; Wallet passes need valid issuer info |
| 1.6 | Data Security | Appropriate security measures for user data |
| 1.7 | Reporting Criminal Activity | Must involve local law enforcement |

---

## Section 2: Performance

| Guideline | Title | Summary |
|-----------|-------|---------|
| 2.1 | App Completeness | App must be final, functional, no placeholder content, demo accounts required |
| 2.2 | Beta Testing | No demos/betas on App Store — use TestFlight |
| 2.3 | Accurate Metadata | All metadata must accurately reflect the app |
| 2.3.1 | Hidden Features | No undocumented features; all changes in review notes |
| 2.3.2 | IAP Disclosure | Description/screenshots must indicate IAP requirements |
| 2.3.3 | Screenshots | Must show app in use, not just splash/login screens |
| 2.3.4 | Previews | Video previews: screen captures only, no device frames |
| 2.3.5 | Category | Select the most appropriate category |
| 2.3.6 | Age Rating | Honest age rating answers |
| 2.3.7 | App Name/Keywords | Max 30 chars; no trademark stuffing, no pricing in metadata |
| 2.3.8 | Metadata Audience | Metadata must be 4+ appropriate; "For Kids" reserved for Kids Category |
| 2.3.9 | Rights | Secure rights for all icon/screenshot materials |
| 2.3.10 | Platform Focus | No other platform names/icons in metadata (no Android, Google Play) |
| 2.3.11 | Pre-Orders | Must be complete and match advertised features |
| 2.3.12 | What's New | Significant changes must be listed; generic OK for bug fixes |
| 2.3.13 | In-App Events | Event metadata must be accurate and timely |
| 2.4 | Hardware Compatibility | — |
| 2.4.1 | iPad Support | iPhone apps should run on iPad when possible |
| 2.4.2 | Power Efficiency | No battery drain, heat, crypto mining |
| 2.4.3 | Apple TV | Must work with Siri remote; explain if game controller needed |
| 2.4.4 | System Settings | No requiring device restart or disabling security features |
| 2.4.5 | Mac App Store | Must be sandboxed; no auto-launch; no third-party installers; no license screens |
| 2.5 | Software Requirements | — |
| 2.5.1 | Public APIs | Only public APIs; current OS; frameworks for intended purposes |
| 2.5.2 | Self-Contained | No reading/writing outside container; no downloading executable code |
| 2.5.3 | Malware | No viruses or harmful code |
| 2.5.4 | Background Services | Only for intended purposes (VoIP, audio, location, etc.) |
| 2.5.5 | IPv6 | Must be fully functional on IPv6-only networks |
| 2.5.6 | WebKit | Web browsing must use WebKit |
| 2.5.8 | Home Screen | No alternate desktop/home screen environments |
| 2.5.9 | System Controls | No altering standard switches or native UI elements |
| 2.5.11 | SiriKit/Shortcuts | Only register for relevant intents; no generic aliases |
| 2.5.12 | CallKit/SMS | Only block confirmed spam; explain blocking criteria |
| 2.5.13 | Face Recognition | Must use LocalAuthentication; alternate auth for under-13 |
| 2.5.14 | Recording Consent | Explicit consent required for recording user activity |
| 2.5.15 | File Access | Must include Files app and iCloud documents |
| 2.5.16 | Extensions | Widgets/extensions must relate to app functionality |
| 2.5.17 | Matter | Must use Apple's Matter support framework |
| 2.5.18 | Advertising | Ads only in main binary; no ads in extensions/widgets/keyboards |

---

## Section 3: Business

| Guideline | Title | Summary |
|-----------|-------|---------|
| 3.1 | Payments | — |
| 3.1.1 | In-App Purchase | Must use IAP for digital content/features; loot box odds required |
| 3.1.1(a) | External Purchase Links | Entitlement required for external purchase links (region-specific) |
| 3.1.2 | Subscriptions | Auto-renewable subscription rules |
| 3.1.2(a) | Permissible Uses | Must provide ongoing value; 7-day minimum; cross-device |
| 3.1.2(b) | Upgrades/Downgrades | Seamless experience; no accidental duplicate subscriptions |
| 3.1.2(c) | Subscription Info | Clear description of what user gets; ToS/PP links required |
| 3.1.3 | Other Purchase Methods | Reader apps, multiplatform, enterprise, person-to-person |
| 3.1.3(a) | Reader Apps | Can access previously purchased content |
| 3.1.3(b) | Multiplatform | Can access cross-platform content if IAP also available |
| 3.1.3(c) | Enterprise | B2B apps may allow pre-purchased content access |
| 3.1.3(d) | Person-to-Person | Real-time 1:1 services can use external payment |
| 3.1.3(e) | Physical Goods | Must use external payment (Apple Pay, credit card) |
| 3.1.3(f) | Free Companions | Free web-tool companions don't need IAP |
| 3.1.4 | Hardware Content | Hardware-dependent features can bypass IAP |
| 3.1.5 | Cryptocurrencies | Wallets (org only), no on-device mining, licensed exchanges |
| 3.2 | Other Business Issues | — |
| 3.2.1 | Acceptable | Gifts must be optional; no forcing ratings/reviews |
| 3.2.2 | Unacceptable | No binary options trading; loan APR ≤36%; no manipulating visibility |

---

## Section 4: Design

| Guideline | Title | Summary |
|-----------|-------|---------|
| 4.1 | Copycats | No cloning other apps; no using others' icons/brands |
| 4.2 | Minimum Functionality | Must be more than a repackaged website |
| 4.2.1 | ARKit | Must provide rich integrated AR experiences |
| 4.2.2 | Marketing Apps | Not primarily marketing materials or link collections |
| 4.2.3 | Self-Contained | Must work without installing another app |
| 4.2.6 | Template Apps | Commercialized template apps rejected unless by content provider |
| 4.2.7 | Remote Desktop | Must connect to user-owned device on local network |
| 4.3 | Spam | No duplicates, no spamming the store |
| 4.4 | Extensions | Keyboard and Safari extension rules |
| 4.5 | Apple Sites/Services | No scraping Apple sites; Apple Music rules |
| 4.5.4 | Push Notifications | Not required to function; no spam; opt-in for marketing |
| 4.5.6 | Apple Emoji | Unicode emoji OK; no embedding on other platforms |
| 4.7 | Third-Party Software | HTML5-based apps require explicit consent for data sharing |
| 4.8 | Login Services | If social login offered, must also offer SIWA-equivalent option |
| 4.9 | Apple Pay | Disclose recurring payment terms |
| 4.10 | Monetizing Built-In | Can't charge for OS capabilities (Push, camera, iCloud, etc.) |

---

## Section 5: Legal

| Guideline | Title | Summary |
|-----------|-------|---------|
| 5.1 | Privacy | Full privacy compliance required |
| 5.1.1 | Data Collection | Privacy policy required; consent required; data minimization |
| 5.1.1(v) | Account/Sign-In | Account deletion required if creation offered; no unnecessary login |
| 5.1.1(ix) | Regulated Fields | Banking, healthcare, gambling apps must be from legal entities |
| 5.1.2 | Data Use & Sharing | No selling user data; ATT required for tracking |
| 5.1.3 | Health & Fitness | HealthKit data can't be used for ads; no false data writing |
| 5.1.4 | Kids | COPPA/GDPR compliance; no third-party analytics in Kids apps |
| 5.1.5 | Location Services | Only when directly relevant; consent required |
| 5.2 | Intellectual Property | — |
| 5.2.1 | Generally | Don't use others' protected material |
| 5.2.2 | Third-Party Sites | Don't use third-party content without permission |
| 5.2.3 | Audio/Video | No unauthorized AV downloading |
| 5.2.5 | Apple Trademarks | No Apple product images in icons; no confusing Apple terms |
| 5.3 | Gaming & Gambling | Licensed gambling only; lottery apps from lottery entities only |
| 5.4 | VPN Apps | Must use NEVPNManager; no data collection; from org accounts only |
| 5.5 | Mobile Device Management | MDM from enterprises/education only; strict data use limits |
| 5.6 | Developer Code of Conduct | Respectful responses; no review manipulation; verifiable identity |
| 5.6.1 | App Store Reviews | Respect users; use API for review prompts |
| 5.6.3 | Discovery Fraud | No chart/search/review manipulation |
| 5.6.4 | App Quality | Must maintain quality; excessive complaints may cause removal |
