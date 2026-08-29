---
name: modem-demo-screenshot-artwork
description: Capture polished Modem demo screenshots from a user-opened authenticated browser by calibrating CSS viewport size, native DPR2/Retina backing, proportional UI scale, width, zoom alternatives, page cleanup, and representative page selection before batching; optionally frame the verified raw captures on a user-supplied marketing background. Use when a user asks to take screenshots from a logged-in Modem or demo app, create crisp product-marketing screenshots, capture at 2x, make the UI larger without blur or distorted charts, adjust viewport width or apparent font size, remove demo/developer chrome, capture core pages, or produce framed browser artwork. Do not use for Slack mockups or invented product UI.
---

# Modem Demo Screenshot Artwork

Make browser capture the primary job. Produce native browser pixels that are crisp, legible, well-proportioned, and representative before doing any easy framing work.

## Require the real inputs

Require an open browser tab that is already signed into the target content. Prefer the user's existing tab and preserve its session.

If no reachable signed-in tab exists, ask the user to open the desired page, sign in there, and tell you when it is ready. Do not inspect cookies, password stores, profiles, or local storage.

Require a background only when the user wants framed artwork:

- If the user requests raw screenshots only, continue without a background.
- If the user requests framed images and supplied an attachment or exact path, use it.
- If framing is requested but no background is supplied or explicitly selected, ask: “Please attach or point me to the marketing background you want me to use.”
- Do not substitute an old or generated background unless the user asks.

Infer sensible defaults for count and dimensions when the request is otherwise clear. Do not burden the user with questions that one calibration sample can answer.

## Load the right capabilities

- Load `browser:control-in-app-browser` before connecting to or controlling the signed-in tab. Follow the browser the user explicitly names.
- Read the selected browser's complete runtime documentation before using its screenshot, viewport, page-evaluation, or CDP capabilities.
- Use `$frame-marketing-screenshots` only after verified raw masters exist.
- Load `imagegen` only when the user explicitly asks to generate or edit a decorative backdrop.

## Capture-first workflow

### 1. Inspect and preserve the live browser

Record the starting URL, visible page, and viewport so they can be restored. Reuse the existing authenticated tab rather than opening a duplicate.

Inspect real navigation and content before choosing the set. Obtain detail URLs from visible links instead of guessing entity routes. For a 5–10 image Modem set, prefer distinct populated views such as:

- Topics overview.
- Stories overview.
- A high-value problem Story.
- A positive-signal Story.
- An urgent Topic detail.
- A praise Topic detail.
- People directory and one Person detail.
- Companies directory and one Company detail.

Avoid duplicate, empty, loading, modal-covered, or visually weak states.

### 2. Separate the four sizing controls

Never conflate:

1. CSS viewport dimensions, which control layout and how large the UI appears.
2. Device-pixel ratio, which controls native pixel density.
3. Output PNG dimensions, which equal CSS dimensions multiplied by DPR.
4. Final artwork canvas, which adds framing around the untouched raw capture.

Use `output pixels = CSS viewport × DPR`.

A 1600×1200 final capture at DPR2 requires an 800×600 CSS viewport. That setting was crisp but too narrow for the Modem UI. Widening the CSS viewport by about 28–30% produced the proven default:

- CSS viewport: 1024×600.
- DPR: 2.
- Raw PNG: 2048×1200.

This made the page wider without making the UI tiny. Treat it as the starting point, not an unquestionable universal value.

Read [references/capture-playbook.md](references/capture-playbook.md) before changing viewport, DPR, browser zoom, CSS zoom, or font size.

### 3. Calibrate one sample before batching

Capture and inspect one representative page first. Do not capture the full set until all four checks pass:

- Page-scope metrics report the intended CSS width, CSS height, and DPR.
- File metadata reports the exact expected output dimensions.
- Text, icons, dividers, and avatars look crisp at original resolution.
- Charts and SVGs have normal geometry and the composition is neither too narrow nor too zoomed out.

Adjust the correct control for the symptom:

- Blurry: fix the native DPR/backing surface; never upscale afterward.
- Crisp but everything is tiny: reduce the CSS viewport or choose a tighter crop; adding pixels does not enlarge UI.
- Legible but too thin/narrow: increase CSS width while keeping DPR2 and the useful height.
- Text alone needs to be larger after proportional sizing is correct: use a reversible typography adjustment only when the user explicitly wants it, then check wrapping and layout.
- Charts or SVGs are stretched: remove CSS zoom and reload.

Prefer viewport calibration over CSS `zoom`. CSS zoom can reflow the page and distort charts even when the file has the requested pixel dimensions.

### 4. Establish a true native-Retina surface

Use the selected browser's documented CDP/device-metrics capability when available. For the proven in-app-browser path:

1. Set the browser viewport to 1024×600 CSS pixels.
2. Send `Emulation.setDeviceMetricsOverride` with width `1024`, height `600`, `deviceScaleFactor: 2`, and mobile disabled.
3. Immediately send `Emulation.clearDeviceMetricsOverride`.
4. Reload the page.
5. Verify `innerWidth === 1024`, `innerHeight === 600`, and `devicePixelRatio === 2`.
6. Capture a sample and require a real 2048×1200 PNG.
7. Inspect the actual pixels; metadata alone is insufficient.

The set-then-clear sequence is an observed in-app-browser latch, not a universal Playwright rule. If the current browser documentation exposes a different supported path, use it and validate the same invariants.

If the browser lacks the needed metrics/CDP capability and Developer Mode is not enabled, ask the user to enable Developer Mode and retry. Do not hide the limitation by capturing low-resolution pixels and enlarging them.

### 5. Apply reversible presentation cleanup

Use temporary page-scope DOM/CSS changes, never source-code or database edits. Keep cleanup idempotent and rerun it after navigation because React can recreate nodes.

Known Modem cleanup targets:

- Hide `[aria-label^="Topics engine:"]` for the V1/V2 selector.
- Hide a verified Intercom/support launcher.
- Hide warning-styled elements containing `Internal note`.
- Remove the literal `Demo ` prefix only from the visible organization-name node.
- Close or collapse an empty Agent panel when a visible `Close conversation` control proves it is open.

Preserve all genuine product and demo data. Do not invent replacements.

### 6. Capture immutable raw masters

For each selected page:

1. Navigate through a verified route.
2. Wait for DOM content, fonts, and an authoritative populated heading/table/card.
3. Reapply cleanup.
4. Confirm no tooltip, toast, skeleton, modal, or empty panel covers the subject.
5. Capture a viewport PNG directly from the browser.
6. Save with stable ordered names such as `01-topics-overview.png`.
7. Record URL, dimensions, and cleanup applied.

Verify every file's dimensions. Inspect at least an overview, a dense detail, and a visually different directory/entity page at original resolution. Keep this directory immutable.

### 7. Frame only after capture passes

If framed artwork is requested, invoke `$frame-marketing-screenshots` with the verified raw directory and supplied background. Keep raw and framed outputs in separate directories.

For the proven 2048×1200 raw set, use a 2304×1440 canvas, 68px deterministic toolbar, 22px corners, 128px horizontal margins, and 86px vertical margins. Preserve screenshot pixels at 1:1; resize the decorative background proportionally when needed.

Read [references/art-direction.md](references/art-direction.md) only for alternate visual treatments or when the framing helper is unavailable.

### 8. Validate, package, and restore

- Verify raw and framed file counts and dimensions programmatically.
- View representative raw and framed outputs at original resolution.
- Confirm no blur, tiling, distorted charts, cut content, unwanted selector, `Demo` label, support widget, or internal note.
- Package raw masters and framed derivatives separately; zip final sets when useful.
- Report clickable absolute paths, counts, dimensions, and whether the background—not the product capture—was resized.
- Restore the original page and temporary viewport/device-metrics state. Leave the user's authenticated tab open.

## Never fake quality

- Never upscale a low-resolution screenshot and call it Retina.
- Never use output dimensions alone as proof of sharpness.
- Never batch before the calibration sample passes visual inspection.
- Never use CSS zoom as the first fix for apparent font size.
- Never keep a DPR surface that tiles or repeats the page; output widths above roughly 4096px tiled in the observed browser compositor.
- Never AI-generate or redraw product UI.
- Never include the later Slack mockup workflow in this skill.
