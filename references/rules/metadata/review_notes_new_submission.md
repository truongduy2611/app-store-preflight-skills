# Rule: Review Notes — New Submission Completeness

- **Guideline**: 2.1 (also 2.3.1(a), 2.5.19)
- **Severity**: REJECTION
- **Category**: metadata

## What to Check

For **every new app submission** (first-time apps or major new versions), review notes must include all six of the following sections. Omitting any section commonly triggers a rejection or an Information Needed response from Apple.

### 1. Screen Recording on a Physical Device

A screen recording captured on a physical device demonstrating the app's functionality. The recording must:

- Begin with launching the app
- Show the typical user flow through core features

If the app includes **any** of the following, they must appear in the recording:

- Account registration, login, and account deletion flows
- Accessing paid content or features, including any purchase or subscription flows
- User-generated content, including content reporting and blocking mechanisms
- Any prompts requesting access to sensitive data or device capabilities (e.g., location, contacts, camera, microphone)

### 2. App Purpose Description

A description of the app's purpose, including:

- The problem it solves
- The value it provides to its intended audience

### 3. Access Instructions and Test Credentials

Instructions for accessing and reviewing the app's main features, including:

- Any required test or login credentials (username/password, demo account)
- Steps to reach non-obvious or gated features
- Every remote feature flag that gates a user-facing feature, and how to turn it on (2.5.19 — see `references/rules/design/hidden_features.md`)

New features and product changes must be described **with specificity**. Under 2.3.1(a), generic notes ("bug fixes and improvements", "new features") are rejected.

### 4. External Services List

A list of the external services, tools, or platforms the app uses to deliver its core functionality. Examples:

- Data providers
- Authentication services (Firebase Auth, Auth0, etc.)
- Payment processors (Stripe, RevenueCat, etc.)
- AI services (OpenAI, Google AI, etc.), plus where the third-party AI consent screen appears (5.1.2(i))
- Analytics platforms
- Cloud storage providers

### 5. Regional Differences

One of the following:

- A description of any regional differences in the app's features or content
- A confirmation that the app functions consistently across all regions

### 6. Regulated Industry Documentation (if applicable)

If the app operates in a highly regulated industry (healthcare, finance, gambling, insurance, legal, etc.), include:

- Relevant documentation or credentials demonstrating authorization to provide these services
- Applicable licenses, certifications, or regulatory approvals

Specific cases Apple calls out:

- **VPN (5.4)**: license information in the Notes field if the app is available in a territory that requires a VPN license
- **Medical (1.4.1)**: a link to the regulatory clearance (FDA, etc.), consistent with the regulated medical device status in App Store Connect
- **Fixed-odds betting in Brazil (5.3.4)**: SPA license details in Notes and supporting documents attached. Only a new app version starts license verification

## How to Detect

1. **Pull review notes** from App Store Connect metadata:
   ```bash
   asc metadata pull --output-dir ./metadata
   ```
   Or inspect the local `metadata/review_information/notes.txt` (fastlane convention).

2. **Scan the review-notes text** for the presence of each section. Look for:
   - A link to a screen recording (URL, or mention of "screen recording" / "video" / "demo recording")
   - Keywords indicating app purpose ("purpose", "problem", "value", "solves")
   - Test credentials or login instructions ("test account", "demo account", "username", "password", "credentials")
   - External service mentions (any service names, or a section labeled "external services" / "third-party services")
   - Regional info ("region", "all regions", "consistent across", "regional differences")
   - Regulated industry docs (only required if app type is in a regulated category)

3. **Flag missing sections** — any of the 6 sections not found in the review notes should be flagged as a rejection risk.

## Resolution

Fill in all missing sections in the review notes. Use the template at [`review_notes_template.md`](./review_notes_template.md) as a starting point.

Key tips:
- **Screen recording**: Record on a real device (not simulator). Upload to a hosting service and paste the URL in review notes. Keep it under 5 minutes.
- **Test credentials**: Create a dedicated demo account that won't expire during review (allow at least 2 weeks).
- **External services**: Be thorough — Apple wants to understand your app's dependencies.
- **Regional differences**: If your app behaves the same everywhere, a single sentence confirming this is sufficient.

## Example Rejection

> **Guideline 2.1 — Information Needed**
>
> We need additional information to continue the review of your app.
>
> Next Steps: Please provide the following information for us to proceed with your review:
>
> - A screen recording, captured on a physical device, that demonstrates the app's functionality. The recording should begin from launching the app and include the typical user flow.
> - A description of the app's purpose, including the problem it solves and the value it provides.
> - Instructions for accessing the app's main features, including any required test credentials.
> - A list of external services used to deliver the app's core functionality.
> - Describe any regional differences, or confirm that the app functions consistently across all regions.
