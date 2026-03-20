# Rule: Missing Subscription Metadata in App Store Listing
- **Guideline**: 3.1.2 – Business – Payments – Subscriptions
- **Severity**: REJECTION
- **Category**: metadata

## What to Check
Apps offering **auto-renewable subscriptions** must include all of the following in both the app and App Store metadata:

### Required in the App
- Title of auto-renewing subscription
- Length of subscription
- Price of subscription (and price per unit if appropriate)
- Functional link to **Privacy Policy**
- Functional link to **Terms of Use (EULA)**

### Required in App Store Metadata
- **Privacy Policy URL** — Set in the Privacy Policy field in App Store Connect
- **Terms of Use (EULA)** — Either:
  - A functional link in the **App Description**, OR
  - A custom EULA added in the **EULA field** in App Store Connect
  - If using Apple's standard EULA, include a link to it in the description

## How to Detect

### Check App Store Connect fields
```bash
# Pull canonical metadata JSON
asc metadata pull --app "<APP_ID>" --version "<VERSION>" --dir ./metadata

# Check if version descriptions mention ToS / EULA links
grep -i "terms of use\|terms of service\|terms and conditions\|eula\|end user license" \
  ./metadata/version/<VERSION>/*.json

# Check whether the App Store Connect Privacy Policy URL field is present
grep -i "privacyPolicyUrl" ./metadata/app-info/*.json
```

### Check for URL patterns in descriptions
```bash
# Look for actual URLs (http/https links) in descriptions
grep -oE 'https?://[^" ]+' ./metadata/version/<VERSION>/*.json
```

### Check App Store Connect EULA field
In App Store Connect → App Information → scroll to EULA section. Verify a custom EULA is uploaded or the standard Apple EULA is referenced.

### Check in-app subscription flow
Verify the app's subscription purchase screen includes:
- Subscription title and duration
- Price
- Tappable Privacy Policy link
- Tappable Terms of Use link
- "Restore Purchases" button

## Resolution
1. Add a Terms of Use / EULA link to the app description for **every locale**
2. Add a Privacy Policy URL in App Store Connect → App Information → Privacy Policy URL
3. Optionally, add a custom EULA in App Store Connect → App Information → EULA
4. Ensure the in-app subscription screen shows all required information with working links

### Description Template
Add this block at the bottom of your app description:
```
Terms of Use: https://yourdomain.com/terms
Privacy Policy: https://yourdomain.com/privacy
```

## Example Rejection
> **Guideline 3.1.2 - Business - Payments - Subscriptions**
>
> Issue Description
>
> The submission did not include all the required information for apps offering auto-renewable subscriptions.
>
> The following information needs to be included in the App Store metadata:
>
> - A functional link to the Terms of Use (EULA). If you are using the standard Apple Terms of Use (EULA), include a link to the Terms of Use in the App Description. If you are using a custom EULA, add it in App Store Connect.
>
> Next Steps
>
> Update the App Store metadata to include the information specified above.
