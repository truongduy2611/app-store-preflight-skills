# Checklist: Kids Category Apps

Guidelines specifically applying to apps in the Kids Category or apps targeting children.

## Critical (Will Reject)

- [ ] **1.3** — No external links (unless behind parental gate)
- [ ] **1.3** — No purchasing opportunities (unless behind parental gate)
- [ ] **1.3** — No third-party advertising
- [ ] **1.3** — No third-party analytics (limited exceptions: no IDFA, no PII, no location)
- [ ] **5.1.4(a)** — COPPA / GDPR compliance for children's data
- [ ] **5.1.4** — No sending PII or device info to third parties
- [ ] **5.1.4** — Privacy policy required and must comply with children's privacy statutes
- [ ] **5.1.1(i)** — Privacy policy linked in App Store Connect AND accessible in-app

## Important (Common Rejections)

- [ ] **2.3.8 / 5.1.4** — "For Kids" / "For Children" in metadata is reserved for Kids Category; apps outside it can't imply children are the main audience in name, subtitle, icon, screenshots, or description
- [ ] **1.3** — Once in Kids Category, must continue meeting guidelines in all subsequent updates
- [ ] **5.1.4(b)** — Third-party contextual ads only if service has documented Kids-specific policies with human review
- [ ] **2.3.6** — Age rating accurately reflects content
- [ ] **2.5.18** — No ads in extensions, widgets, App Clips, keyboards, or watchOS

## Parental Gate Requirements

- [ ] Areas with external links, purchases, or distractions must be behind a parental gate
- [ ] [Parental gate guidance](https://developer.apple.com/app-store/kids-apps/) followed

## Age Assurance Laws (Any App With Minor Users)

Apple's age-assurance tools apply to every app with minor users, not just the Kids Category:

- [ ] **Texas (since June 4, 2026), Utah, Louisiana** — Parental consent is required for minors' downloads, IAP, and significant app changes. Request the age category via the **Declared Age Range API**, and use the **PermissionKit Significant Change API** for significant updates. Handle the App Store server notification for revoked consent
- [ ] **Brazil, Australia, Singapore** — 18+ apps are blocked for unconfirmed adults; you may still need your own age confirmation
- [ ] **Brazil** — Declaring loot boxes in the age rating questionnaire sets the Brazil rating to 18+
- [ ] **Australia** — The 15+ rating is gone; apps with unrestricted web access, frequent medical info, or loot boxes are rated 16+
- [ ] **Vietnam** — Region-specific rating (00+, 12+, 16+, 18+) derived from questionnaire answers
- [ ] Reference: [Age assurance frameworks Q&A](https://developer.apple.com/support/age-assurance)
