# Rule: Missing Privacy Manifest
- **Guideline**: 5.1.1 – Legal – Privacy (Spring 2024 requirement)
- **Severity**: REJECTION
- **Category**: privacy

## What to Check
Starting Spring 2024, apps must include a **Privacy Manifest** (`PrivacyInfo.xcprivacy`) if they use any of Apple's "Required Reason APIs". Apple will reject apps that use these APIs without declaring the reason.

### Required Reason API Categories

| Category | Common APIs | Example Reason Code |
|----------|------------|-------------------|
| **File Timestamp** | `NSFileCreationDate`, `NSFileModificationDate`, `stat()`, `getattrlist()` | `DDA9.1` – Display to user |
| **User Defaults** | `UserDefaults` (NSUserDefaults) | `CA92.1` – App-specific data |
| **System Boot Time** | `systemUptime`, `mach_absolute_time()` | `35F9.1` – Measure time intervals |
| **Disk Space** | `volumeAvailableCapacityKey`, `statfs()` | `E174.1` – Check for writes |

### What to Declare in the Manifest
- **NSPrivacyTracking**: Whether the app uses data for tracking (true/false)
- **NSPrivacyTrackingDomains**: List of tracking domains (if any)
- **NSPrivacyCollectedDataTypes**: What data types are collected
- **NSPrivacyAccessedAPITypes**: Required reason APIs used, with reason codes

## How to Detect

### Check for Privacy Manifest existence
```bash
# Look for PrivacyInfo.xcprivacy in the project
find . -name "PrivacyInfo.xcprivacy" -not -path "./.build/*"
```

### Check for Required Reason API usage
```bash
# UserDefaults (most common)
grep -rn "UserDefaults\|NSUserDefaults\|standardUserDefaults" --include="*.swift" --include="*.m" .

# File Timestamps
grep -rn "NSFileCreationDate\|NSFileModificationDate\|creationDate\|modificationDate" --include="*.swift" --include="*.m" .

# System Boot Time
grep -rn "systemUptime\|mach_absolute_time\|ProcessInfo.*systemUptime" --include="*.swift" --include="*.m" .

# Disk Space
grep -rn "volumeAvailableCapacity\|statfs\|statvfs" --include="*.swift" --include="*.m" .
```

### Check third-party SDK manifests
Many popular SDKs (Firebase, Analytics, etc.) now bundle their own `PrivacyInfo.xcprivacy`. Ensure your app's manifest covers APIs used in **your own code**.

## Resolution
1. Create `PrivacyInfo.xcprivacy` in your Xcode project root
2. Add it to your app target's "Copy Bundle Resources" build phase
3. Declare all Required Reason APIs with appropriate reason codes
4. For Flutter apps, place the manifest in `ios/Runner/PrivacyInfo.xcprivacy`

### Minimal Example
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>NSPrivacyTracking</key>
    <false/>
    <key>NSPrivacyAccessedAPITypes</key>
    <array>
        <dict>
            <key>NSPrivacyAccessedAPIType</key>
            <string>NSPrivacyAccessedAPICategoryUserDefaults</string>
            <key>NSPrivacyAccessedAPITypeReasons</key>
            <array>
                <string>CA92.1</string>
            </array>
        </dict>
    </array>
</dict>
</plist>
```

## Example Rejection
> Your app uses APIs that require a Privacy Manifest. Please add a PrivacyInfo.xcprivacy file to your app that includes the required reason codes for the APIs used by your app.
>
> The following APIs require reasons:
> - NSPrivacyAccessedAPICategoryUserDefaults
> - NSPrivacyAccessedAPICategoryFileTimestamp
