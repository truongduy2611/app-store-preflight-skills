# Checklist: AI-Powered / Generative AI Apps

Guidelines specifically applying to apps that use AI services (ChatGPT, Gemini, Claude, etc.), generative AI, or deep synthesis technology.

## Critical (Will Reject)

- [ ] **5 (China DST)** — If distributing in China: remove all references to OpenAI, ChatGPT, GPT, Gemini, Claude, Anthropic, Midjourney, DALL-E from metadata
- [ ] **5 (China DST)** — If distributing in China: suppress AI functionality or obtain MIIT license
- [ ] **1.1.6** — No false information or misleading AI capabilities (e.g., "AI doctor")
- [ ] **1.4.1** — AI health advice: must include medical disclaimers; can't substitute for professional diagnosis
- [ ] **2.3.1(a)** — All AI features described with specificity in review notes
- [ ] **2.5.19** — No hidden or dormant AI capabilities that appear only after approval (see `references/rules/design/hidden_features.md`)
- [ ] **5.1.2(i)** — Explicit user permission **before** sending personal data to a third-party AI provider, with the provider named (see `references/rules/privacy/third_party_ai_consent.md`)
- [ ] **1.2** — AI content creation apps are UGC apps: filter objectionable output, report mechanism, block abusive users, published contact info
- [ ] **1.2** — Prevent and remove nonconsensual intimate imagery, including AI-generated imagery of real people ("nudification", face-swap porn)
- [ ] **1.1.4** — No generating nudity or sexually explicit imagery

## Important (Common Rejections)

- [ ] **4.1(c)** — Don't use "GPT", "ChatGPT", "OpenAI", "Gemini", "Claude" (or their logos) in your app name or icon without the brand owner's approval
- [ ] **2.3.7** — Don't keyword-stuff with AI brand names (ChatGPT, GPT-4, Gemini, etc.)
- [ ] **5.1.1(i)** — Privacy policy names the AI providers user data is shared with and how they protect it
- [ ] **4.7** — Chatbots / plug-ins / mini apps not embedded in the binary: moderation, per-instance consent for data sharing, no exposing native APIs, index with universal links, age restriction (4.7.1–4.7.5)
- [ ] **2.5.14** — Explicit consent required for AI processing of user recordings/inputs
- [ ] **5.1.1(iii)** — Data minimization: don't send more data to AI than necessary
- [ ] **3.1.1** — AI features/credits unlocked via IAP (not external payment for digital content)

## China Storefront Specific

Banned AI terms in metadata for China (all locales, not just zh-Hans):
- `ChatGPT`, `GPT-4`, `GPT-4o`, `GPT`  
- `OpenAI`
- `Gemini`, `Bard` (Google)
- `Claude`, `Anthropic`
- `Midjourney`, `DALL-E`, `DALL·E`
- `Copilot` (in AI context)
- `Stable Diffusion` (cloud API context)

### Options
1. **Remove references** → Use "AI-powered" / "smart assistant" generically
2. **Exclude China** → Deselect China mainland in App Store Connect
3. **Obtain compliance** → Get MIIT license for DST services
