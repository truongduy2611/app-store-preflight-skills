# Rule: App Preview Contains Device Frames
- **Guideline**: 2.3.4 – Performance – Accurate Metadata
- **Severity**: REJECTION
- **Category**: metadata

## What to Check
App preview videos must only contain capture footage of the app running. They must **not** include:

- Device images or device frames (e.g., an iPhone bezel around the screen)
- Framing around the video screen capture
- Non-app content that obscures the app experience

> **Note**: This applies to **app preview videos**, not static screenshots. Static screenshots _may_ use device frames.

## How to Detect

### Manual Inspection
1. Open App Store Connect → your app version → Previews and Screenshots
2. Play each app preview video in full screen
3. Check for:
   - Device bezels or phone outlines visible in the video
   - Borders, frames, or decorative elements around the screen capture
   - Non-app scenes (e.g., lifestyle shots with a person holding a phone)

### Using asc CLI
```bash
# List current preview assets
asc screenshots list --app-id <YOUR_APP_ID> --type previews
```

### Automated Check (ffmpeg frame analysis)
```bash
# Extract first frame of each preview for visual inspection
for preview in ./previews/*.mp4; do
  ffmpeg -i "$preview" -vframes 1 -q:v 2 "${preview%.mp4}_frame.jpg"
done
```
Then visually inspect extracted frames for device imagery.

## Resolution
1. Re-record app previews using **only screen capture** (e.g., Xcode Simulator recording, QuickTime screen recording)
2. Remove any device frame overlays from the video
3. Narration and text overlays are allowed for clarity
4. Upload via App Store Connect → "View All Sizes in Media Manager"

## Example Rejection
> **Guideline 2.3.4 - Performance - Accurate Metadata**
>
> The app preview includes content that does not sufficiently show the app in use. Specifically, the app preview:
>
> - Includes framing around the video screen capture.
> - Includes device images and/or device frames.
>
> App previews should allow users to see what the app does and how it will appear on their device when the preview is played in full screen.
>
> Next Steps
>
> To resolve this issue, revise the app preview to only use video screen captures of the app that may include narration and video or textual overlays for added clarity.
