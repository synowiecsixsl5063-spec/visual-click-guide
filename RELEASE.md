# Release v2.0.0

## Why v2.0?

v1.0 used SVG code as the output format. We discovered a fatal flaw: **web-based AI chatbots (Doubao, Kimi, DeepSeek, Tongyi Qianwen) cannot render SVG code in their chat windows.** Users saw raw code instead of visual guides.

v2.0 drops SVG entirely and replaces it with **emoji-driven plain-text visual typography** — 100% compatible with every AI chat interface, WeChat, DingTalk, and even printed paper.

## What Changed

- **Output format**: SVG code → emoji + 【】highlighted plain text
- **Platform support**: Claude/ChatGPT only → every AI chatbot on earth
- **Example files**: 5 `.svg` files → 5 `.txt` files
- **Prompt architecture**: 4-layer SVG spec → minimalist emoji typography spec

## What Stays the Same

- Zero dependencies, prompt-only project
- MIT License
- Same usage: copy prompt → inject → ask in natural language

## v2.0 Prompt Design

| Rule | Purpose |
|------|---------|
| 👉 emoji = click action | Visual "click here" signal, no text reading needed |
| 【】wraps target element | Makes button/menu names visually pop |
| ⌨️ 🎹 ⏳ 👆 🖱️ = action types | Instant recognition of input/shortcut/wait/scroll/drag |
| ────── = step divider | Visual flow line between steps |
| 📦 【window name】 = group header | Clear context switching between screens |
| One line per step, no paragraphs | Scannable at a glance, like texting a friend |

## Known Limitations

- No actual UI mockup images (trade-off for universal compatibility)
- Relies on emoji rendering (some old terminals may show tofu)
- Best suited for linear workflows; branching logic is verbose

## Future Roadmap

- v2.1: Community-contributed prompt translations (Japanese, Korean, etc.)
- v2.2: Mermaid flowchart variant for Markdown-capable platforms
- v2.3: Multi-language emoji set adaptation (WeChat-style vs. Western-style)
- v3.0: Hybrid mode — detect platform capability, auto-select SVG vs text

## Credits

- v1.0 core prompt: Claude 4.6
- v1.0 test harness: Qwen 3.7 Max
- v1.0 docs & release: Kimi K2.6
- v2.0 pivot insight & direction: Kimi K2.6 (DeepSeek conversation)
- v2.0 prompt rewrite: Claude Code
