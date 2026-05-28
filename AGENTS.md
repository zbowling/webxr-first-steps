# Agent Instructions — WebXR First Steps

A staged WebXR tutorial that walks web developers through building a Three.js target-practice VR game from scratch, chapter by chapter.

## Source-of-truth files (read these first, do not duplicate their contents in this file)

For setup, build steps, SDK versions, and project layout, read:

- `README.md` — official setup, headset/emulator access instructions, and GitHub Pages deploy flow
- `package.json` — Node / npm dependencies and scripts (`dev`, `build`)
- `webpack.config.cjs` — dev server and bundler configuration
- `src/` — `index.html`, `index.js`, `init.js`, and `assets/`; `init.js` wires the IWER emulator when native WebXR is missing
- `tutorial/chapter1.md` … `tutorial/chapter6.md` — the actual tutorial content (the product)
- `.github/workflows/deploy.yml` — GitHub Pages build/deploy pipeline
- `LICENSE` — MIT license terms

## Quest / Horizon-specific notes

- The Webpack dev server runs over HTTPS with a self-signed certificate; both the headset browser and desktop Chrome will show a cert warning that the README explicitly tells users to dismiss. Do not chase this as a bug.
- IWER (the bundled WebXR emulator) only auto-activates when no native WebXR runtime is detected. If the user has the `Immersive Web Emulator` Chrome extension installed, the extension takes precedence and the in-page IWER stays dormant — do not try to force both.
- The tutorial chapters in `tutorial/chapter*.md` are the product. When changing code under `src/`, keep the corresponding chapter markdown in sync.
- This is a pure Three.js / WebXR project — do not suggest installing Oculus integration packages, Meta XR Unity SDK, or any native Android SDK pieces.

## Meta Quest tooling

This repository is part of the Meta Quest / Horizon OS ecosystem (a sample, library, template, or related project — the bespoke intro above describes which). Use that intro and the source-of-truth files it references for project-specific decisions; don't restate or invent facts from memory.

When the user asks anything about Quest device behavior, build / deploy / debug / capture flows, on-device performance, or Horizon OS APIs, reach for these tools instead of generic WebXR answers:

- **`hzdb`** — Quest-aware ADB wrapper (device list, install / launch / stop, logs, screenshots, Perfetto traces, on-device docs search). Already wired up as an MCP server via `.mcp.json`, `.vscode/mcp.json`, and `.cursor/mcp.json`. Also runnable directly: `npx -y @meta-quest/hzdb <subcommand>`.
- **Meta Quest Agentic Tools** — the full skill set, including WebXR-specific skills: [github.com/meta-quest/agentic-tools](https://github.com/meta-quest/agentic-tools). Install per your client (Claude Code: `/plugin install meta-vr@meta-quest`; Gemini CLI: `gemini extensions install https://github.com/meta-quest/agentic-tools`; Cursor / VS Code: install the **Meta Horizon** extension from the Marketplace).

A few behavior expectations:

- **Read this repo's files first.** Before answering anything project-specific, read `README.md` and whichever source-of-truth files the intro above points at. Don't restate their contents in chat — quote or link instead.
- **Use `hzdb` for device-side work.** Anything that touches an attached Quest (install, launch, logs, screenshot, capture, manifest inspection) goes through `hzdb`, not raw `adb`.
- **Check live Horizon OS docs before answering API questions.** `hzdb docs search "..."` queries the live docs; training data on Horizon OS APIs goes stale fast.
- **Don't fabricate SDK / engine versions.** If a version isn't visible in this repo's files, say so rather than guessing.
