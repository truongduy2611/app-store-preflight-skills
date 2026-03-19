# Checklist: AI-Powered / Generative AI Apps

Guidelines specifically applying to apps that use AI services (ChatGPT, Gemini, Claude, etc.), generative AI, or deep synthesis technology.

## Critical (Will Reject)

- [ ] **5 (China DST)** — If distributing in China: remove all references to OpenAI, ChatGPT, GPT, Gemini, Claude, Anthropic, Midjourney, DALL-E from metadata
- [ ] **5 (China DST)** — If distributing in China: suppress AI functionality or obtain MIIT license
- [ ] **1.1.6** — No false information or misleading AI capabilities (e.g., "AI doctor")
- [ ] **1.4.1** — AI health advice: must include medical disclaimers; can't substitute for professional diagnosis
- [ ] **2.3.1** — All AI features documented in review notes; no hidden AI capabilities

## Important (Common Rejections)

- [ ] **5.2.5** — Don't use "GPT", "ChatGPT", "OpenAI", "Gemini" as part of app name unless you are the brand owner
- [ ] **2.3.7** — Don't keyword-stuff with AI brand names (ChatGPT, GPT-4, Gemini, etc.)
- [ ] **1.2** — If AI generates user-facing content: implement content moderation/filtering
- [ ] **5.1.1** — Disclose AI data processing in privacy policy
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
