---
name: frame-marketing-screenshots
description: Frame an already-existing, verified set of crisp product screenshots on a user-supplied standardized marketing background, add deterministic browser chrome and a drop shadow, preserve product pixels at 1:1, validate the batch, and package the results. Use only when raw screenshots already exist and the task is limited to framing, reframing, or applying a supplied brand backdrop. Do not use when the user expects Codex to control an open signed-in browser or take new screenshots; use modem-demo-screenshot-artwork for that capture-first workflow. If no background is supplied or explicitly identified, ask the user to attach or provide it before compositing.
---

# Frame Marketing Screenshots

Create consistent marketing artwork from verified product captures and a supplied brand background. Treat the product screenshot as a locked 1:1 layer; resize the decorative background when necessary, not the product UI.

Use this as the secondary framing step only. If the request begins from an open authenticated browser or requires new screenshots, stop and load `$modem-demo-screenshot-artwork` instead.

## Gate on required inputs

Require both:

- One or more source screenshots, preferably equal-sized PNG raw masters.
- One user-supplied background image or an exact background path explicitly identified in the current request.

If the background is missing, ask one blocking question and stop:

> Please attach or point me to the standardized marketing background you want me to use.

Do not silently reuse an older background, approximate it, or generate a substitute. If the user asks to create a new background, load the `imagegen` skill and handle that as a separate step.

If several screenshot directories are plausible, prefer the verified native-resolution raw masters over already framed derivatives. Ask which set to use only when the choice remains materially ambiguous.

## Inspect before composing

1. View the supplied background and at least one source screenshot.
2. Read the background and screenshot pixel dimensions.
3. Count the source files and confirm they use stable names.
4. Confirm that the source images are crisp raw captures rather than enlarged or previously decorated files.
5. Preserve the source directory unchanged and write framed derivatives to a new directory.

## Choose the canvas without shrinking the UI

Keep these quantities separate:

- Raw screenshot dimensions.
- Browser toolbar height.
- Browser-window dimensions.
- Final canvas dimensions.

Calculate:

`window width = screenshot width`

`window height = screenshot height + toolbar height`

Choose a canvas large enough for that window plus the desired margins. Preserve the background's aspect ratio. Scale or center-crop the decorative background proportionally; never stretch it.

Use this proven Modem recipe for 2048×1200 captures:

- Final canvas: 2304×1440.
- Raw screenshot: 2048×1200, unchanged.
- Toolbar: 68px.
- Browser window: 2048×1268.
- Margins: 128px left/right and 86px top/bottom.
- Outer radius: 22px.

If the supplied background is smaller but has the same aspect ratio, allow proportional background enlargement and disclose it. Do not enlarge the product capture. If the requested canvas cannot fit the raw capture at 1:1, enlarge the canvas or ask the user to choose between a larger deliverable and an explicitly downscaled derivative.

## Compose deterministically

Use `scripts/frame-on-background.mjs` for an equal-sized PNG batch. Load the bundled workspace Node runtime if `sharp` is not available from the current workspace.

Example:

```bash
node scripts/frame-on-background.mjs \
    --input /absolute/path/to/raw-screenshots \
    --output /absolute/path/to/framed-screenshots \
    --background /absolute/path/to/background.png \
    --canvas-width 2304 \
    --canvas-height 1440
```

The compositor must:

- Preserve every screenshot pixel at 1:1 by default.
- Scale the background with proportional `cover` fitting.
- Add exact browser chrome, clipping, border/accent, and shadow with deterministic shapes.
- Keep the source filename for each derivative.
- Refuse mismatched screenshot dimensions.
- Refuse a canvas that cannot fit the browser window unless the user explicitly authorizes `--allow-resize`.

Do not use ImageGen to draw browser chrome, text, or product UI. Do not sharpen, denoise, color-grade, perspective-transform, or generatively edit the screenshot.

## Validate and package

1. Confirm the output count equals the source count.
2. Confirm every output has the requested canvas dimensions.
3. View at least three outputs at original resolution:
   - An overview or index page.
   - A dense detail page.
   - A visually different entity or directory page.
4. Check crisp text, normal chart/SVG geometry, consistent margins, rounded clipping, and a clean shadow.
5. Confirm that no screenshot content was cut off or scaled unexpectedly.
6. Zip the final directory for handoff.
7. Report clickable absolute paths to both the directory and ZIP, plus file count and dimensions.
8. State whether the background was resized and confirm that the product captures remained unscaled.

## Avoid these failures

- Do not proceed without a supplied or explicitly selected background.
- Do not treat a previously framed image as a raw master.
- Do not resize the product merely to match the background's original pixel dimensions.
- Do not stretch the background to a different aspect ratio.
- Do not overwrite the raw screenshots.
- Do not mix test files or alternate treatments into the final directory.
- Do not report success from metadata alone; visually inspect representative outputs.
