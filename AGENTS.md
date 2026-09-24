# Agent Instructions — Unreal Passthrough Sample

Unreal sample demonstrating Meta Quest Passthrough features. One level per capability — passthrough-as-background AR, color-curve styling, color maps, color LUTs (single and interpolated), color scale & offset, and masked/projected passthrough ("poke-a-hole").

## Source-of-truth files (read these first, do not duplicate their contents in this file)

For setup, build steps, SDK versions, and project layout, read:

- `README.md` — official setup and per-level walkthrough
- `PTSamples.uproject` — Unreal engine version, plugins, target platforms (Android only)
- `Config/` — project settings (Meta XR plugin, rendering)
- `Content/Passthrough/Data/` — color-map curve assets referenced by the PTStyles level
- `.gitattributes` — Git LFS (required for media and binary UAssets)
- `LICENSE` — license terms (Meta License; MIT only where explicitly marked)

## Quest / Horizon-specific notes

- The project targets Android only. Editor preview works on Windows/macOS but device build requires the Android toolchain. The README's recommended path is the Meta fork of UE; the Epic Launcher + MetaXR plugin path also works.
- Navigation between sample levels is via the left controller's Menu button in-headset; there is no editor-side scene picker. Right controller aims, right trigger travels, right thumbstick scrolls the list.
- Common pawn / passthrough wiring lives in `VRTPPawn`; when adapting a level, always inspect both the Level Blueprint and `VRTPPawn`. Most logic lives in Blueprint and widget assets (`W_PT*.uasset`), not C++.
- The PTStyles / PTColorMap / PTColorScaleAndOffset levels can produce flashing color sequences — the README's photosensitivity caution should not be stripped when summarizing.
- The `mPokeAHoleMask` material is the canonical masked-passthrough primitive. Reuse it instead of reimplementing.

# Meta Quest tooling

This is a Meta Quest / Horizon OS sample. The bespoke intro above is the source of truth for what this project is and how it's built — use it (and the files it points at) instead of restating facts from memory.

When the user asks anything about Quest device behavior, build / deploy / debug / capture flows, on-device performance, or Horizon OS APIs, reach for these tools instead of generic Unreal answers:

- **`hzdb`** — Quest-aware ADB wrapper (device list, install / launch / stop, logs, screenshots, Perfetto traces, on-device docs search). Already wired up as an MCP server via `.mcp.json`, `.vscode/mcp.json`, and `.cursor/mcp.json`. Also runnable directly: `npx -y @meta-quest/hzdb <subcommand>`.
- **Meta Quest Agentic Tools** — the full skill set, including Unreal-specific skills: <https://github.com/meta-quest/agentic-tools>. Install per your client (Claude Code: `/plugin install meta-vr@meta-quest`; Gemini CLI: `gemini extensions install https://github.com/meta-quest/agentic-tools`; Cursor / VS Code: install the **Meta Horizon** extension from the Marketplace).

A few behavior expectations:

- **Read this repo's files first.** Before answering anything project-specific, read `README.md` and whichever source-of-truth files the intro above points at. Don't restate their contents in chat — quote or link instead.
- **Use `hzdb` for device-side work.** Anything that touches an attached Quest (install, launch, logs, screenshot, capture, manifest inspection) goes through `hzdb`, not raw `adb`.
- **Check live Horizon OS docs before answering API questions.** `hzdb docs search "..."` queries the live docs; training data on Horizon OS APIs goes stale fast.
- **Don't fabricate SDK / engine versions.** If a version isn't visible in this repo's files, say so rather than guessing.
