# Rule: Apple Trademark Violations
- **Guideline**: 5.2.5 – Legal – Intellectual Property
- **Severity**: REJECTION
- **Category**: metadata

## What to Check
App metadata, icons, and screenshots must not include content confusingly similar to Apple products, services, or trademarks.

### Flagged Patterns

**App Icon:**
- Apple device silhouettes or imagery (iPhone, iPad, Mac, Apple Watch)
- Apple logo or any variation of it
- Icons confusingly similar to Apple's own app icons

**App Name / Subtitle:**
- Using Apple product names as part of your app name (e.g., "iPhone Cleaner", "iPad Manager")
- Using Apple service names (e.g., "My iCloud Backup", "Siri Helper")

**Metadata Text:**
- Apple product names used as feature descriptors unnecessarily
- Phrases like "best app in the App Store" (using "App Store" generically)
- Terms like "iPhone app", "iPad edition" in subtitle or description

**Screenshots / Marketing:**
- Unauthorized 3D renders or simulations of Apple products
- Illustrations of Apple devices (unless for instructional use showing your app running)
- Apple device images placed alongside competitor product images
- Obscuring or exploiting the Apple logo on device images
- Die-cut promotions in the shape of an Apple product
- Using icons, logos, or images sourced directly from apple.com

### Commonly Flagged Terms
- `iPhone`, `iPad`, `Mac`, `MacBook`, `Apple Watch`, `Apple TV`, `Vision Pro`
- `iMessage`, `FaceTime`, `Siri`, `AirDrop`, `iCloud`
- `App Store` (when used generically)
- `Apple` (when implying endorsement or association)

## How to Detect

### App Icon
- Visually inspect the app icon asset (`AppIcon.appiconset/`) for device silhouettes or Apple product imagery
- Check `Assets.xcassets/AppIcon.appiconset/Contents.json` for references

### App Name
```bash
# Check app name for Apple product terms
grep -i "iphone\|ipad\|macbook\|apple watch\|apple tv\|imessage\|facetime\|siri\|icloud\|vision pro" \
  ./metadata/app-info/*.json
```

### Metadata Text
```bash
# Search all pulled metadata for Apple product terms
grep -ri "iphone\|ipad\|macbook\|apple watch\|apple tv\|imessage\|facetime\|siri\|airdrop\|vision pro" \
  ./metadata/app-info/ ./metadata/version/<VERSION>/
```

### Screenshots
- Visually inspect all screenshot assets for:
  - Unauthorized Apple device renders (3D models, illustrations, die-cuts)
  - Apple logo exploitation (centering on or enhancing the Apple logo)
  - Apple devices shown next to competitor devices (Samsung, Google, etc.)
- **Allowed**: Showing your app running on a real Apple device in screenshots, as long as the device illustrates natural use and is not the focal point

## Resolution
1. **App Icon**: Remove any Apple device imagery; use abstract or product-specific design instead
2. **App Name**: Remove Apple product names from app name/subtitle:
   - "iPhone Cleaner Pro" → "Phone Cleaner Pro"
   - "My iPad Manager" → "My Tablet Manager"
3. **Metadata**: Remove or rephrase Apple product references:
   - "Works with iPhone" → "Works with your phone" (if it's a universal claim)
   - "Download on App Store" → remove (users are already on the App Store)
   - "Best Siri alternative" → "Best voice assistant"
4. **Screenshots**: Replace unauthorized renders with real device screenshots or remove device frames entirely
5. **Apple device photos**: If showing an Apple device, ensure it shows your app in natural use; don't place alongside competitor products

## Example Rejection
> **Guideline 5.2.5 - Legal - Intellectual Property**
>
> Issue Description
>
> The app's metadata includes content that is similar to designs or terms used for Apple products and services and may cause confusion for users. Specifically, your metadata includes:
>
> - iPhone device found in the application icon
>
> Next Steps
>
> To resolve this issue, remove images and terms that are confusingly similar to an Apple product or service from the app's metadata.
>
> Resources
>
> - Learn more about appropriate and inappropriate use of Apple trademarks in the Guidelines for Using Apple's Trademarks and Copyrights.
