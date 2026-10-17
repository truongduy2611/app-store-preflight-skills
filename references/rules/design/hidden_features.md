# Rule: Hidden, Dormant, or Undocumented Features
- **Guideline**: 2.5.19 – Performance – Software Requirements (new October 16, 2026; formerly part of 2.3.1)
- **Severity**: REJECTION (can also lead to app removal and developer account termination)
- **Category**: design

## What to Check
Everything the app can do must be visible to App Review and to users. Apple rejects apps that:

- Contain **hidden, dormant, or undocumented features**
- **Behave differently during review** and change after approval ("bait-and-switch"), for example by turning on features through a server flag once the app is live
- Use **code obfuscation** or similar techniques to hide functionality in the binary
- Misrepresent their purpose during review and only reveal harmful capabilities later (for example "nudification" behind an innocent photo editor)

Feature flags are not banned. What matters is that every feature a flag can turn on is in the reviewed build, reachable by the reviewer, and described in the review notes (2.3.1(a)).

## How to Detect

### Review-environment detection (highest risk)
Code that checks whether it's running under review, then changes behavior, is the classic bait-and-switch pattern. App Review uses sandbox receipts, which is why sandbox checks show up here.
```bash
grep -rnE "sandboxReceipt|isTestFlight|isInReview|inReview|reviewMode|isReviewer|appReview|underReview|AppTransaction.*environment|\.sandbox\b|\.xcode\b" \
  --include="*.swift" --include="*.m" --include="*.dart" --include="*.ts" --include="*.tsx" --include="*.js" .
```
For each hit, check what is enabled or disabled. Gating **features** on these checks → ❌. Gating only analytics, logging, or receipt-validation endpoints → ✅.

### Time-bomb and date gates
```bash
grep -rnE "timeIntervalSince1970 *[<>]|Date\(\) *[<>]|DateComponents\(year: *20[2-9][0-9]|DateTime\.now\(\)\.isAfter|new Date\(\) *[<>]" \
  --include="*.swift" --include="*.m" --include="*.dart" --include="*.ts" --include="*.tsx" --include="*.js" .
```
A hard-coded date that unlocks functionality (rather than ending a promotion or rental) → ❌.

### Remote feature flags
```bash
grep -rnE "RemoteConfig|remoteConfig|LaunchDarkly|LDClient|Statsig|GrowthBook|Optimizely|ConfigCat|featureFlag|FeatureFlag|isEnabled\(\"" \
  --include="*.swift" --include="*.m" --include="*.dart" --include="*.ts" --include="*.tsx" --include="*.js" .
```
List every flag that gates a user-facing feature. For each one, check:
- The code for the feature is in this build (not downloaded later; see 2.5.2)
- The reviewer can reach it: flag is on for review, or how to enable it is explained in the notes
- The review notes describe it

### Region / storefront gates
```bash
grep -rnE "Storefront\.current|SKStorefront|countryCode|Locale\.current\.(region|regionCode)|ipapi|ip-api|geoip" \
  --include="*.swift" --include="*.m" --include="*.dart" --include="*.ts" --include="*.tsx" --include="*.js" .
```
Region gating for legal reasons (China DST, gambling licenses) is fine if the review notes say so. Hiding features from the review region (usually US) → ❌.

### Downloaded or obfuscated code
```bash
# Remote code execution paths (also 2.5.2)
grep -rnE "dlopen|NSClassFromString\(|JSContext|evaluateScript|evaluateJavaScript|eval\(" \
  --include="*.swift" --include="*.m" --include="*.ts" --include="*.tsx" --include="*.js" .

# Obfuscated strings / URLs
grep -rnE "base64EncodedString|Data\(base64Encoded|atob\(|base64Decode|xorDecode|deobfuscate|SwiftShield|obfuscat" \
  --include="*.swift" --include="*.m" --include="*.dart" --include="*.ts" --include="*.tsx" --include="*.js" .
```
Decoding hidden URLs, endpoints, or class names that turn on features → ❌. Base64 for images or payloads → ✅.

### Review notes cross-check
```bash
# Every gated feature found above should be mentioned in the review notes
asc metadata pull --app "<APP_ID>" --version "<VERSION>" --dir ./metadata
grep -ril "flag\|remote config\|region\|enable" ./metadata/
```

## Resolution
1. **Remove review-detection logic** that changes features. Use sandbox checks only to pick receipt-validation endpoints.
2. **Ship what you review**: every feature reachable in production must be in the submitted build and reachable by the reviewer.
3. **Document flags in review notes**: list each gated feature, its default state, and how the reviewer can turn it on.
4. **New capability = new submission**: don't turn on features by server flag that App Review hasn't seen. Submit a new version and describe the change (2.3.1(a), 2.3.12).
5. **Explain legitimate region gating** in the review notes (for example "AI chat disabled in China mainland: no DST license").
6. **Remove obfuscation** that hides functionality. Encrypting secrets is fine; hiding features is not.

## Example Rejection
> *Illustrative wording; Apple's message may differ.*
>
> **Guideline 2.5.19 - Performance - Software Requirements**
>
> We discovered that your app contains hidden or undocumented features that were not disclosed in the review notes. Specifically, features can be enabled through a remote configuration that was not active during review.
>
> **Next Steps**: Remove the hidden functionality, or include it in the reviewed build and describe it in the App Review notes. Attempting to hide features from App Review may result in removal of your app from the App Store and termination of your developer account.
