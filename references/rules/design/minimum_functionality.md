# Rule: Minimum Functionality
- **Guideline**: 4.2
- **Severity**: REJECTION
- **Category**: design

## What to Check

Apple requires apps to provide "valuable utility or entertainment" and be more than a repackaged website, simple wrapper, or thin shell. Apps rejected under 4.2 typically:

- Have only 1-2 screens with minimal interactivity
- Are essentially a WebView wrapping a website
- Provide no functionality beyond what Safari offers
- Are a simple collection of links or RSS feed
- Consist primarily of marketing material or a product catalog
- Are a book or game guide that should be on Apple Books instead
- Are template-generated apps with no unique content

### Related Sub-Guidelines

| Guideline | What It Covers |
|-----------|---------------|
| 4.2.1 | ARKit apps must provide rich integrated AR — not just dropping a model |
| 4.2.2 | Not primarily marketing materials, ads, web clippings, or link aggregators |
| 4.2.3(i) | App must work on its own without requiring another app |
| 4.2.3(ii) | Disclose size of additional required downloads before user proceeds |
| 4.2.6 | Template/app-generator apps rejected unless submitted by content provider |

## How to Detect

### Code-Level Signals

```bash
# Check if app is primarily a WebView wrapper
grep -rn "WKWebView\|UIWebView\|WebView\|SFSafariViewController" --include="*.swift" --include="*.m" .

# Count total view controllers / screens
grep -rn "class.*:.*UIViewController\|class.*:.*View {" --include="*.swift" . | wc -l

# Check for meaningful model/data layer
find . -name "*.swift" -path "*/Model*" -o -name "*.swift" -path "*/Models*" | wc -l

# Check if app has any local data persistence
grep -rn "CoreData\|SwiftData\|UserDefaults\|Realm\|SQLite\|KeychainSwift" --include="*.swift" .
```

### Red Flags

- **< 3 unique screens** → Very likely to trigger 4.2
- **Single WebView** loading an external URL as the primary experience
- **No model layer** — no local data structures beyond what the web provides
- **No offline functionality** — completely dependent on network
- **Only static content** — no user interaction beyond scrolling

### App Store Connect Metadata

```bash
# Pull and check description — if it's hard to describe what the app DOES, it may lack functionality
asc metadata pull --output-dir ./metadata
cat ./metadata/en-US/description.txt | wc -w
# Very short descriptions (< 50 words) can indicate minimal functionality
```

## Resolution

1. **Add unique features** that go beyond what a website offers:
   - Offline mode / local data caching
   - Push notifications for relevant events
   - Device-specific integrations (camera, location, HealthKit, etc.)
   - User-generated content or personalization
   - Native UI patterns (swipe actions, drag & drop, widgets)

2. **If your app is a web wrapper**, consider:
   - Adding native authentication (Sign in with Apple, biometrics)
   - Implementing native navigation instead of web-based nav
   - Adding local storage so the app works offline
   - Integrating Apple frameworks (Share Sheet, Spotlight, Shortcuts)

3. **In your review notes**, clearly explain:
   - What the app does that a website can't
   - The target audience and use case
   - Any features that might not be immediately obvious to the reviewer

## Example Rejection

```
Guideline 4.2 - Design - Minimum Functionality

The usefulness of the app is limited by the minimal functionality it currently
provides.

Specifically, the app does not provide sufficient content and features to be
useful, unique, and "app-like."

Apps should provide valuable utility or entertainment, draw people in by
offering compelling capabilities or content, or enable people to do something
they couldn't do before or in a way they couldn't do it before.

Next Steps

We encourage you to review your app concept and incorporate different content
and features that are in compliance with the App Review Guidelines.
```
