# Rule: AI Service References for China Storefront
- **Guideline**: 5 – Legal (Chinese DST Regulations)
- **Severity**: REJECTION
- **Category**: metadata

## What to Check
Apps distributed on the **China mainland storefront** must not reference AI services that lack the required Chinese government permits (MIIT license). This applies to both **metadata** and **in-app functionality**.

### Banned Terms (China Storefront)
- `ChatGPT`, `GPT-4`, `GPT-4o`, `GPT`
- `OpenAI`
- `Gemini` (Google), `Bard`
- `Claude`, `Anthropic`
- `Midjourney`, `DALL-E`, `DALL·E`
- `Copilot` (in AI context)
- `Stable Diffusion` (when referencing cloud API)
- Any **deep synthesis technology (DST)** service without a Chinese MIIT license

### Metadata Fields to Check
- App name
- Subtitle
- Promotional text
- App description
- Keywords
- Screenshots (text overlays)
- What's New

## How to Detect

### Using asc CLI
```bash
# Pull canonical metadata for all locales in the version under review
asc metadata pull --app "<APP_ID>" --version "<VERSION>" --dir ./metadata

# Check Chinese locale specifically
grep -i "chatgpt\|openai\|gpt-4\|gemini\|claude\|anthropic\|midjourney\|dall-e\|copilot\|bard" \
  ./metadata/app-info/zh-Hans.json ./metadata/version/<VERSION>/zh-Hans.json 2>/dev/null
```

### Check all locales (Apple reviews all, not just zh-Hans)
```bash
# Apple may flag ANY locale if the app is distributed in China
grep -ri "chatgpt\|openai\|gpt-4\|gemini\|claude\|anthropic\|midjourney\|dall-e" \
  ./metadata/app-info/ ./metadata/version/<VERSION>/
```

### Check storefront availability
Verify whether China mainland is included in the app's availability settings in App Store Connect.

## Resolution

### Option A: Remove references (keep China distribution)
1. Remove all AI service brand names from metadata across **all locales**
2. Use generic terms: "AI-powered" or "smart assistant" instead of brand names
3. Suppress AI functionality specifically for the China storefront build
4. Update Review Notes to confirm AI functionality is suppressed in China

### Option B: Exclude China storefront
1. In App Store Connect → Pricing and Availability → Deselect "China mainland"
2. Keep AI references in metadata for all other storefronts

### Option C: Obtain compliance
Seek professional advice on compliance with the *Administrative Provisions on Deep Synthesis of Internet-based Information Services* to obtain the required MIIT permits.

## Example Rejection
> **Guideline 5 - Legal**
>
> Issue Description
>
> As you may know, the Chinese government has been tightening regulations associated with deep synthesis technologies (DST) and generative AI services, including ChatGPT. DST must fulfill permitting requirements to operate in China, including securing a license from the Ministry of Industry and Information Technology (MIIT) if the services are provided while connected to the Internet.
>
> Based on our review, the app appears to be associated with ChatGPT, which does not have requisite permits to operate in China. Specifically, the app's metadata includes the following references to ChatGPT and/or OpenAI: OpenAI.
>
> Accordingly, pursuant to local Chinese law, this functionality must be deactivated in the version of the app that you make available on the China App Store and all references to ChatGPT or OpenAI must be removed from metadata fields such as app name, subtitle, promotional text, app description, and screenshots.
