# Rule: Sharing Personal Data with Third-Party AI Without Consent
- **Guideline**: 5.1.2(i) – Legal – Privacy – Data Use and Sharing
- **Severity**: REJECTION
- **Category**: privacy

## What to Check
Before the app sends personal data to a **third-party AI** service, it must:

1. **Clearly disclose** what data is sent, and **which provider** it goes to
2. **Get explicit permission**: an affirmative user action (a button, toggle, or checkbox). A line buried in the ToS doesn't count.
3. Let users **withdraw consent** easily (5.1.1(ii))
4. Name the provider in the **privacy policy** (5.1.1(i)) and in the App Privacy "Data Shared" answers

"Personal data" includes prompts and chat text, photos, voice recordings, documents, contacts, health data, and anything else the user creates or that identifies them.

### Scope
| Setup | Third-party AI? |
|-------|-----------------|
| App calls OpenAI / Gemini / Anthropic / etc. directly | ✅ Yes |
| App calls **your backend**, which forwards to an AI provider | ✅ Yes — a proxy doesn't change who receives the data |
| Firebase AI Logic / Vertex AI (Gemini) | ✅ Yes |
| Apple Foundation Models (on-device) | ❌ No |
| Your own self-hosted model on your servers | ❌ Not third-party, but 5.1.1 consent and privacy policy still apply |

## How to Detect

### Direct AI SDKs and endpoints
```bash
# Endpoints
grep -rnE "api\.openai\.com|generativelanguage\.googleapis\.com|aiplatform\.googleapis\.com|api\.anthropic\.com|api\.x\.ai|api\.mistral\.ai|api\.groq\.com|openrouter\.ai|api\.together\.xyz|api\.replicate\.com|api\.stability\.ai|api\.elevenlabs\.io|api\.deepgram\.com|api\.assemblyai\.com|api\.perplexity\.ai|api\.deepseek\.com" .

# SDKs (Swift / Flutter / React Native)
grep -rnE "import (OpenAI|GoogleGenerativeAI|FirebaseAI|FirebaseVertexAI|SwiftAnthropic|SwiftOpenAI)|dart_openai|google_generative_ai|firebase_ai|firebase_vertexai|@anthropic-ai/sdk|@google/generative-ai|from ['\"]openai['\"]" \
  --include="*.swift" --include="*.dart" --include="*.ts" --include="*.tsx" --include="*.js" --include="Package.swift" --include="Package.resolved" --include="pubspec.yaml" --include="package.json" --include="Podfile" .
```

### Backend-proxied AI
If the app talks to its own backend, check the server code (or ask the developer) whether requests go on to an AI provider. Look for app endpoints with names like `/chat`, `/generate`, `/ai`, `/completion`, `/transcribe`, or `/summarize`:
```bash
grep -rnE "\"/(v1/)?(chat|generate|ai|completion|completions|transcribe|summarize|assistant)" \
  --include="*.swift" --include="*.dart" --include="*.ts" --include="*.tsx" --include="*.js" .
```

### Consent gate
```bash
grep -rnE "aiConsent|AIConsent|ai_consent|hasAcceptedAI|aiDataSharing|ai_data_sharing|consentToAI|thirdPartyAI" \
  --include="*.swift" --include="*.dart" --include="*.ts" --include="*.tsx" --include="*.js" .
```
If an AI call is found but no consent gate → ❌. If a gate exists, check:
- It runs **before the first** AI request, not after
- The consent text **names the provider** and lists the data types sent
- Declining still leaves the rest of the app usable (5.1.1(iv)), or the AI feature is clearly optional
- There's a way to withdraw consent later (for example a Settings toggle)

### Privacy policy & App Privacy
```bash
asc metadata pull --app "<APP_ID>" --version "<VERSION>" --dir ./metadata
# Get the privacy policy URL, then check the page names the AI provider(s)
jq -r '.privacyPolicyUrl // empty' ./metadata/app-info/*.json
```
Make sure the App Privacy answers in App Store Connect list the data types as shared with third parties.

## Resolution
1. **Add a consent screen** that appears before the first AI request:
   > *"To generate responses, [App] sends your messages and attached photos to **OpenAI**. OpenAI processes this data under its own privacy policy. [Allow] [Not now]"*
2. **Store the choice** and check it before every AI call. Don't send anything if consent is missing or withdrawn.
3. **Add a withdraw option** in Settings, which also stops future sharing.
4. **Update the privacy policy** to name each AI provider, what data it receives, and its retention terms.
5. **Update the App Privacy** answers in App Store Connect.
6. **Mention it in review notes**: which provider, what data, and where the consent screen appears.

## Example Rejection
> *Illustrative wording; Apple's message may differ.*
>
> **Guideline 5.1.2(i) - Legal - Privacy - Data Use and Sharing**
>
> The app appears to share the user's personal data with a third-party AI service but does not clearly explain what data is sent or to whom, and does not obtain the user's permission before sharing it.
>
> **Next Steps**: Disclose what personal data will be shared with the third-party AI service, identify the service, and obtain the user's explicit permission before sharing data.
