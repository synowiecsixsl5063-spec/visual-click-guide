# Release v1.0.0

## Overview

Visual-Click-Guide v1.0 is the first stable release of the prompt-based SVG tutorial generator. It provides a battle-tested system prompt that instructs AI models to produce self-contained, step-by-step visual operation guides in SVG format.

## What's Included

- `prompt/visual-click-guide-prompt.txt` — The core system prompt (4 layers).
- `docs/README.md` & `docs/README.zh-CN.md` — Full documentation in English and Chinese.
- `docs/CONTRIBUTING.md` — Contribution workflow, prompt authoring rules, and Qwen-based testing requirements.
- `examples/` — 5 validated SVG samples covering Windows, Chrome, Web, Word, and Excel scenarios.
- `LICENSE` — MIT License.

## Key Features

- **Simplified UI Mockups** — Recognizable without being pixel-perfect.
- **Strict Visual Grammar** — Canonical color values, step badges, action banners, and flow arrows.
- **Cross-Model Compatibility** — Tested on Claude, ChatGPT, Qwen, and Doubao.
- **Zero Runtime Dependencies** — Pure prompt-to-SVG workflow; no build step required.

## Usage Summary

1. Inject the prompt as a system instruction.
2. Describe your task (e.g., "Show me how to export a PDF in Chrome").
3. Copy the returned SVG code and paste it into any HTML/Markdown renderer.

## Known Limitations

- Complex multi-path workflows (branching logic, conditional steps) may require manual SVG editing after generation.
- Highly stylized or dark-themed applications may need minor color hints in the user request.
- Drag-and-drop paths are simplified to straight arrows; curved bezier routing is not yet supported.

## Future Roadmap

- v1.1: Add support for dark-mode canvas variants.
- v1.2: Introduce branching flow support (decision diamonds, yes/no paths).
- v1.3: Curved arrow routing and animated step-reveal SVGs.
- v2.0: Community-curated scenario library (50+ common software workflows).

## Credits

- Core prompt engineered with Claude 4.6.
- Test harness and validation by Qwen 3.7 Max.
- Documentation and release integration by Kimi K2.6.
