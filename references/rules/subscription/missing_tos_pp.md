# Rule: Missing Terms of Use and Privacy Policy for Subscriptions
- **Guideline**: 3.1.2 – Business – Payments – Subscriptions
- **Severity**: REJECTION
- **Category**: subscription

## What to Check
The in-app subscription purchase flow and the app itself must include:

1. **Title** of the auto-renewing subscription
2. **Length** of subscription (e.g., 1 month, 1 year)
3. **Price** of subscription (and price per unit if appropriate)
4. **Functional link** to Privacy Policy
5. **Functional link** to Terms of Use (EULA)

And the App Store metadata must include:
- Privacy Policy URL in the Privacy Policy field in App Store Connect
- Terms of Use (EULA) link in either the app description or the EULA field

## How to Detect

### Check in-app subscription screens
Search the codebase for subscription paywall / purchase views:
```bash
# Find subscription-related UI files
grep -rn "subscribe\|paywall\|purchase\|StoreKit\|RevenueCat\|Superwall" --include="*.swift" --include="*.dart" .

# Check if terms/privacy links exist in those files
grep -rn "terms\|privacy\|eula\|TermsOfService\|PrivacyPolicy" --include="*.swift" --include="*.dart" .
```

### Check metadata descriptions
```bash
# Verify ToS/PP links in descriptions
grep -i "terms\|privacy\|eula" ./metadata/*/description.txt
```

### Check App Store Connect
- App Information → Privacy Policy URL field must not be empty
- App Information → EULA field should have custom EULA or description should reference Apple's standard EULA

## Resolution
1. Add tappable Terms of Use and Privacy Policy links to every subscription paywall screen
2. Add links to the app description in all locales
3. Set the Privacy Policy URL field in App Store Connect
4. If using a custom EULA, upload it in the EULA field

## Example Rejection
> **Guideline 3.1.2 - Business - Payments - Subscriptions**
>
> The submission did not include all the required information for apps offering auto-renewable subscriptions.
>
> The following information needs to be included in the App Store metadata:
>
> - A functional link to the Terms of Use (EULA). If you are using the standard Apple Terms of Use (EULA), include a link to the Terms of Use in the App Description. If you are using a custom EULA, add it in App Store Connect.
