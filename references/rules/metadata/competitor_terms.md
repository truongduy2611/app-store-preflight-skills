# Rule: Competitor Platform Terms in Metadata
- **Guideline**: 2.3.1 – Performance – Accurate Metadata
- **Severity**: REJECTION
- **Category**: metadata

## What to Check
App Store metadata (name, subtitle, description, keywords, promotional text, What's New) must not reference competing platforms or brands.

### Banned Terms
- `Android`, `Google Play`, `Google Play Store`
- `Samsung`, `Galaxy Store`
- `Huawei`, `AppGallery`
- `Amazon Appstore`
- `Windows Store`, `Microsoft Store`
- `APK`, `sideload`

## How to Detect

### Using asc CLI (pulled metadata)
```bash
# Pull metadata first
asc metadata pull --output-dir ./metadata

# Search across all locales
grep -ri "android\|google play\|samsung\|huawei\|apk\|amazon appstore\|windows store\|microsoft store" ./metadata/
```

### Using local fastlane metadata
```bash
grep -ri "android\|google play\|samsung\|huawei\|apk\|amazon appstore\|windows store\|microsoft store" ./fastlane/metadata/
```

### In Xcode project (Info.plist)
```bash
grep -ri "android\|google play" *.xcodeproj/project.pbxproj
```

## Resolution
1. Remove all references to competing platforms from metadata fields
2. Replace with generic terms:
   - "Available on Android" → "Available on multiple platforms"
   - "Also on Google Play" → remove entirely
   - "Transfer from Android" → "Transfer from your previous device"
3. Re-verify using `asc metadata push --dry-run` before uploading

## Example Rejection
> **Guideline 2.3.1 - Performance - Accurate Metadata**
>
> We noticed that your app's metadata includes references to other mobile platforms, which is not appropriate for the App Store. Specifically, the following content was found:
> - "Android" mentioned in the app description
>
> **Next Steps**: Remove all references to other mobile platforms from the app's metadata.
