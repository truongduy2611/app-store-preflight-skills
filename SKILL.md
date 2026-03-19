---
name: app-store-preflight-skills
description: >
  Scan an iOS/macOS Xcode project for common App Store rejection patterns before
  submission. Use when preparing an app for App Store review, after receiving a
  rejection from Apple, or when auditing metadata, subscriptions, privacy manifests,
  entitlements, or design compliance. Integrates with the asc CLI for metadata inspection.
metadata:
  author: truongduy2611
  version: "1.0"
---

# App Store Preflight Skill

Run pre-submission checks on your iOS/macOS project to catch common App Store rejection patterns.

## Prerequisites

- **asc CLI** — Install via Homebrew: `brew install asc` ([App-Store-Connect-CLI](https://github.com/rudrankriyam/App-Store-Connect-CLI))
- **ASC CLI Skills** — [app-store-connect-cli-skills](https://github.com/rudrankriyam/app-store-connect-cli-skills) for `asc` usage patterns

## Step 1: Identify App Type → Load Checklist

Determine which guidelines apply by loading the relevant checklist from `references/guidelines/by-app-type/`. Always start with `all_apps.md`, then add the app-type-specific one:

| App Type | Checklist |
|----------|-----------|
| Every app | `references/guidelines/by-app-type/all_apps.md` |
| Subscriptions / IAP | `references/guidelines/by-app-type/subscription_iap.md` |
| Social / UGC | `references/guidelines/by-app-type/social_ugc.md` |
| Kids Category | `references/guidelines/by-app-type/kids.md` |
| Health & Fitness | `references/guidelines/by-app-type/health_fitness.md` |
| Games | `references/guidelines/by-app-type/games.md` |
| macOS | `references/guidelines/by-app-type/macos.md` |
| AI / Generative AI | `references/guidelines/by-app-type/ai_apps.md` |
| Crypto & Finance | `references/guidelines/by-app-type/crypto_finance.md` |
| VPN | `references/guidelines/by-app-type/vpn.md` |

Full guideline index: `references/guidelines/README.md`

## Step 2: Pull Metadata for Inspection

Pull the latest App Store metadata using the `asc` CLI:

```bash
asc metadata pull --output-dir ./metadata
```

If metadata already exists locally (e.g., fastlane `metadata/` directory), skip this step and point the scan at that directory.

## Step 3: Run Rejection Rule Checks

For each category, load the relevant rule files from `references/rules/` and inspect. Each rule contains: **What to Check**, **How to Detect**, **Resolution**, and **Example Rejection**.

| Category | Rule Files |
|----------|------------|
| Metadata | `references/rules/metadata/*.md` |
| Subscription | `references/rules/subscription/*.md` |
| Privacy | `references/rules/privacy/*.md` |
| Design | `references/rules/design/*.md` |
| Entitlements | `references/rules/entitlements/*.md` |

## Step 4: Report Findings

Produce a summary report using this template:

```markdown
## Preflight Report

### ❌ Rejections Found (N)
- [GUIDELINE X.X.X] Description of issue
  - File: path/to/offending/file
  - Fix: What to do

### ⚠️ Warnings (N)
- [GUIDELINE X.X.X] Potential issue

### ✅ Passed (N)
- [Category] All checks passed
```

Order by severity: rejections first, then warnings, then passed.

## Step 5: Autofix + Validate

Some issues can be auto-fixed:
- **Competitor terms** → Suggest replacement text with competitor names removed
- **Metadata character limits** → Show current vs. max length
- **Missing links** → Generate template ToS/PP URLs

After applying any auto-fix, **re-run the affected checks** to confirm the fix resolved the violation. Only mark as resolved once the re-scan passes.

For issues requiring manual intervention (screenshots, UI redesign), provide clear instructions but do not auto-fix.

## Gotchas

- **China storefront** — Banned AI terms (ChatGPT, Gemini, etc.) are checked across ALL locales, not just `zh-Hans`. Apple checks every locale visible in the China storefront.
- **Privacy manifests** — `PrivacyInfo.xcprivacy` is required even if your app doesn't call Required Reason APIs directly. Third-party SDKs (Firebase, Amplitude, etc.) that use `UserDefaults` or `NSFileManager` trigger this requirement transitively.
- **asc auth** — `asc metadata pull` requires App Store Connect authentication. Run `asc auth` first or set `ASC_API_KEY` / `ASC_ISSUER_ID` environment variables.
- **Subscription metadata** — Apple requires ToS/PP links in BOTH the App Store description AND the in-app subscription purchase screen. Missing either one is a separate rejection.
- **macOS entitlements** — Apple will ask you to justify every temporary exception entitlement (`com.apple.security.temporary-exception.*`). Remove entitlements you don't actively use.

## Adding New Rules

Create a `.md` file in the appropriate `references/rules/` subdirectory:

```markdown
# Rule: [Short Title]
- **Guideline**: [Apple Guideline Number]
- **Severity**: REJECTION | WARNING
- **Category**: metadata | subscription | privacy | design | entitlements

## What to Check
## How to Detect
## Resolution
## Example Rejection
```
