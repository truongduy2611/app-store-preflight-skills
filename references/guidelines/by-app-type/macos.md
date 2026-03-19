# Checklist: macOS / Mac App Store Apps

Guidelines specifically applying to apps distributed via the Mac App Store, including sandboxing, entitlements, and macOS-specific requirements.

## Critical (Will Reject)

- [ ] **2.4.5(i)** — App must be appropriately sandboxed
- [ ] **2.4.5(i)** — Only use appropriate macOS APIs for modifying data from other apps
- [ ] **2.4.5(i)** — Entitlements must match actual app functionality (Apple will ask for justification)
- [ ] **2.4.5(ii)** — Packaged and submitted using Xcode; no third-party installers
- [ ] **2.4.5(ii)** — Self-contained, single app installation bundle
- [ ] **2.4.5(iii)** — No auto-launch at startup/login without consent
- [ ] **2.4.5(iii)** — No spawning background processes after user quits
- [ ] **2.4.5(iii)** — No auto-adding icons to Dock or desktop shortcuts
- [ ] **2.4.5(iv)** — No downloading standalone apps, kexts, or additional code
- [ ] **2.4.5(v)** — No requesting root privileges or setuid attributes
- [ ] **2.4.5(vi)** — No license screens at launch; no license keys; no custom copy protection
- [ ] **2.4.5(vii)** — Updates distributed via Mac App Store only
- [ ] **2.4.5(viii)** — Must run on currently shipping OS; no deprecated technologies (Java)
- [ ] **2.4.5(ix)** — All localizations in a single app bundle

## Important (Common Rejections)

- [ ] **2.5.1** — Only public APIs; frameworks used for intended purposes
- [ ] **2.5.2** — Self-contained in bundle; no reading/writing outside designated container
- [ ] **2.3.10** — Metadata focused on macOS experience; no iOS-only language in description
- [ ] **5.2.5** — No Apple device images in app icon
- [ ] **5.1.1(i)** — Privacy policy required
- [ ] **2.5.5** — Fully functional on IPv6-only networks

## Entitlements Audit

Common entitlements that trigger Apple review questions:
- [ ] `com.apple.security.network.server` — Justify if app acts as a local server
- [ ] `com.apple.security.network.client` — Standard for network requests
- [ ] `com.apple.security.files.downloads.read-only` — Justify Downloads folder access
- [ ] `com.apple.security.files.user-selected.read-write` — Standard for file picker
- [ ] `com.apple.security.temporary-exception.*` — Will draw extra scrutiny
