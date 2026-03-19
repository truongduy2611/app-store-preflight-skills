# Rule: Requiring Unnecessary Personal Data
- **Guideline**: 5.1.1 – Legal – Privacy – Data Collection and Storage
- **Severity**: REJECTION
- **Category**: privacy

## What to Check
Apps must only require personal information that is **directly relevant** to the app's core functionality. If information is useful but not essential, it must be **optional**.

### Commonly Flagged Required Fields
- **Phone number** — unless the app's core function requires calling/SMS
- **Gender** — unless medically or fitness-relevant
- **Marital status** — rarely relevant
- **Date of birth** — unless age-gating is legally required
- **Home address** — unless shipping or location-specific services are core

### Context Matters
- A fitness app may reasonably require gender (for calorie calculations)
- A dating app may reasonably require age and gender
- A shopping app should NOT require marital status
- A note-taking app should NOT require phone number

## How to Detect

### Code Inspection
```bash
# Find registration/onboarding/profile forms
grep -rn "phone\|gender\|marital\|birthdate\|date.of.birth\|address\|registration\|onboarding\|signup\|sign.up\|profile" --include="*.swift" --include="*.dart" .

# Check if fields are marked as required vs optional
grep -rn "required\|validator\|isRequired\|optional" --include="*.swift" --include="*.dart" .
```

### UI Inspection
1. Run the app and complete the onboarding/registration flow
2. For each personal data field, check:
   - Is it required (blocks progress if empty)?
   - Is it relevant to the app's core feature?
3. Flag any required field that isn't directly relevant to what the app does

## Resolution
1. Make non-essential personal data fields **optional** (remove validation requirements)
2. Add "Skip" or "Not now" options for optional profile information
3. If collecting data for personalization, clearly explain why and make it opt-in
4. Review the App Privacy label in App Store Connect to ensure it matches what you actually collect

## Example Rejection
> **Guideline 5.1.1 - Legal - Privacy - Data Collection and Storage**
>
> Issue Description
>
> The app requires users to provide personal information that is not directly relevant to the app's core functionality.
>
> Apps should only require users to provide information that is necessary for the app to function. If information is useful for a non-essential feature, apps may request the information but make it optional.
>
> Next Steps
>
> Update the app to not require users to provide the following personal information:
>
> - Phone number
> - Gender
