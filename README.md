# ✈️ App Store Preflight

An AI agent skill that runs pre-submission checks on your iOS/macOS project to catch common mistakes that lead to App Store rejection.

## Overview

Preflight helps developers catch potential App Store Review guideline violations **before** submitting their app. It scans your Xcode project, source code, metadata, and configuration files to flag issues that commonly result in rejections from Apple.

This skill integrates with the [`asc` CLI](https://github.com/rudrankriyam/App-Store-Connect-CLI) (`brew install asc`) and the [ASC CLI Skills](https://github.com/rudrankriyam/app-store-connect-cli-skills) to pull and inspect App Store metadata.

Most metadata examples assume the canonical JSON layout written by
`asc metadata pull`. If you are starting from fastlane metadata, adapt the path
examples or pull the canonical `asc` layout first.

## Install

```bash
npx skills add truongduy2611/app-store-preflight-skills
```

## Guideline Index (by App Type)

The `references/guidelines/` directory contains a **complete index of all 100+ Apple Review Guidelines** and **10 app-type specific checklists**:

| Checklist | App Type |
|-----------|----------|
| [all_apps.md](./references/guidelines/by-app-type/all_apps.md) | Universal (every submission) |
| [subscription_iap.md](./references/guidelines/by-app-type/subscription_iap.md) | Subscriptions / In-App Purchases |
| [social_ugc.md](./references/guidelines/by-app-type/social_ugc.md) | Social / User-Generated Content |
| [kids.md](./references/guidelines/by-app-type/kids.md) | Kids Category |
| [health_fitness.md](./references/guidelines/by-app-type/health_fitness.md) | Health, Fitness & Medical |
| [games.md](./references/guidelines/by-app-type/games.md) | Games |
| [macos.md](./references/guidelines/by-app-type/macos.md) | macOS / Mac App Store |
| [ai_apps.md](./references/guidelines/by-app-type/ai_apps.md) | AI / Generative AI |
| [crypto_finance.md](./references/guidelines/by-app-type/crypto_finance.md) | Crypto, Finance & Trading |
| [vpn.md](./references/guidelines/by-app-type/vpn.md) | VPN & Networking |

📖 Full guideline reference: [references/guidelines/README.md](./references/guidelines/README.md)

## How It Works

1. **Identify app type** → load the matching checklist from `references/guidelines/by-app-type/`
2. **Pull metadata** using `asc metadata pull --app "<APP_ID>" --version "<VERSION>" --dir ./metadata` (or the `asc-metadata-sync` skill)
3. **Scan** against rejection rules in `references/rules/`
4. **Report** findings with severity, affected files, and resolution steps
5. **Autofix + Validate** — apply fixes, re-run affected checks

See [`SKILL.md`](./SKILL.md) for the full AI agent instructions.

## Rejection Rules

All rules live in `references/rules/`, organized by category:

### Metadata (`references/rules/metadata/`)

| Rule | Guideline | What It Catches |
|------|-----------|----------------|
| [competitor_terms](./references/rules/metadata/competitor_terms.md) | 2.3.1 | Android, Google Play, and other competitor brands |
| [apple_trademark](./references/rules/metadata/apple_trademark.md) | 5.2.5 | Apple device images in icon, Apple trademark misuse |
| [china_storefront](./references/rules/metadata/china_storefront.md) | 5 | OpenAI/ChatGPT/Gemini references (China) |
| [accurate_metadata](./references/rules/metadata/accurate_metadata.md) | 2.3.4 | Device frames in app preview videos |
| [subscription_metadata](./references/rules/metadata/subscription_metadata.md) | 3.1.2 | Missing ToS/EULA and Privacy Policy links |

### Subscriptions (`references/rules/subscription/`)

| Rule | Guideline | What It Catches |
|------|-----------|----------------|
| [missing_tos_pp](./references/rules/subscription/missing_tos_pp.md) | 3.1.2 | No Terms or Privacy Policy in app/metadata |
| [misleading_pricing](./references/rules/subscription/misleading_pricing.md) | 3.1.2 | Monthly price more prominent than billed amount |

### Privacy (`references/rules/privacy/`)

| Rule | Guideline | What It Catches |
|------|-----------|----------------|
| [unnecessary_data](./references/rules/privacy/unnecessary_data.md) | 5.1.1 | Requiring irrelevant personal data |
| [privacy_manifest](./references/rules/privacy/privacy_manifest.md) | 5.1.1 | Missing `PrivacyInfo.xcprivacy` |

### Design (`references/rules/design/`)

| Rule | Guideline | What It Catches |
|------|-----------|----------------|
| [sign_in_with_apple](./references/rules/design/sign_in_with_apple.md) | 4.0 | Asking name/email after SIWA |
| [minimum_functionality](./references/rules/design/minimum_functionality.md) | 4.2 | WebView wrappers, apps with < 3 screens, no unique value |

### Entitlements (`references/rules/entitlements/`)

| Rule | Guideline | What It Catches |
|------|-----------|----------------|
| [unused_entitlements](./references/rules/entitlements/unused_entitlements.md) | 2.4.5(i) | Unused entitlements in Xcode project |

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

## Related Skills

- [app-store-connect-cli-skills](https://github.com/rudrankriyam/app-store-connect-cli-skills) — ASC CLI skills for metadata sync, ASO audit, release flow

## License

MIT
