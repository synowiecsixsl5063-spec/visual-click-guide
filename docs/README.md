# Visual-Click-Guide

> Turn textual software instructions into renderable SVG visual guides.

---

## Background

Text-based software tutorials often impose a high cognitive load. Readers must mentally map lengthy descriptions onto actual interface elements, which frequently leads to mis-clicks and frustration. **Visual-Click-Guide** solves this by providing a structured system prompt that instructs AI models to generate self-contained SVG illustrations—delivering a "what you see is what you do" experience that significantly improves accuracy and comprehension.

---

## Core Features

This project ships a single **system prompt** (`/prompt/visual-click-guide-prompt.txt`). Once injected, the AI gains the ability to:

1. **Simplified UI Mockups** — Abstract target software interfaces into clean card-style diagrams. The goal is recognizability, not pixel-perfect replication.
2. **Step Indicators** — Label every click target with a red numbered badge (①, ②, ③…) and a dashed outline so users know exactly where to click.
3. **Action Banners** — Render non-click actions (typing, keyboard shortcuts, drag-to-select) as color-coded horizontal banners with emoji prefixes, visually separated from UI panels.
4. **Flow Arrows** — Connect panels and banners with red arrows to form a clear top-to-bottom timeline.
5. **Cross-Platform Output** — Produce raw SVG code that renders in any modern browser, Markdown renderer, chat client, or document editor.

---

## Usage

### Step 1: Copy the Prompt

Open `/prompt/visual-click-guide-prompt.txt` and copy the entire contents.

### Step 2: Inject as a System Prompt

Paste the prompt into the **system instruction** area of your AI platform:

- **Claude (Anthropic)**: Project settings or the `system` field at the start of a conversation.
- **ChatGPT (OpenAI)**: Custom Instructions (web) or the `system` role via API.
- **Doubao / ERNIE / Tongyi Qianwen**: Paste into the "Character Settings" or system-level input box before the user turn.
- **Gemini**: Use the System Instruction feature.

### Step 3: Ask for a Guide

In the **same session**, describe the task in natural language. For example:

> "Generate a visual guide showing me how to open Settings on Windows 11."

The AI will return raw SVG code ready to render.

### Example

**User request:**
> How do I generate a visual guide for opening Settings?

**AI output:** (see `settings-windows-11.svg` below)

---

## Test Results

The following tests were executed by **Qwen 3.7 Max** against five common scenarios. All SVG code is copied directly from the test report and renders in modern browsers.

### Scenario 1: Open the Settings App in Windows 11

A simple two-click linear flow: taskbar → Start menu → Settings icon.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 400" width="680" height="400">
  <defs><marker id="arr" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#EF4444"/></marker></defs>
  <rect width="680" height="400" fill="#F3F4F6"/>
  <!-- Panel 1: Taskbar -->
  <rect x="40" y="20" width="600" height="80" fill="#FFF" stroke="#D1D5DB" rx="8"/>
  <rect x="40" y="60" width="600" height="40" fill="#E5E7EB" rx="4"/>
  <rect x="320" y="68" width="24" height="24" fill="#3B82F6" rx="6"/>
  <rect x="316" y="64" width="32" height="32" fill="none" stroke="#EF4444" stroke-width="1.5" stroke-dasharray="4 2" rx="6"/>
  <circle cx="300" cy="64" r="12" fill="#EF4444"/><text x="300" y="69" text-anchor="middle" fill="#FFF" font-size="12" font-family="sans-serif">①</text>
  <!-- Arrow -->
  <line x1="340" y1="108" x2="340" y2="140" stroke="#EF4444" marker-end="url(#arr)"/>
  <!-- Panel 2: Start Menu -->
  <rect x="40" y="148" width="600" height="220" fill="#FFF" stroke="#D1D5DB" rx="8"/>
  <rect x="240" y="160" width="200" height="196" fill="#FFF" stroke="#D1D5DB" rx="8"/>
  <rect x="320" y="220" width="60" height="60" fill="#F3F4F6" rx="8"/>
  <text x="350" y="255" text-anchor="middle" font-size="11" fill="#374151" font-family="sans-serif">Settings</text>
  <rect x="316" y="216" width="68" height="68" fill="none" stroke="#EF4444" stroke-width="1.5" stroke-dasharray="4 2" rx="8"/>
  <circle cx="300" cy="216" r="12" fill="#EF4444"/><text x="300" y="221" text-anchor="middle" fill="#FFF" font-size="12" font-family="sans-serif">②</text>
</svg>
```

**Result:** Passed. Layers 1, 2, and 4 handled the linear flow correctly.

---

### Scenario 2: Export the Current Chrome Page as PDF

Involves a menu expansion and a keyboard-shortcut banner.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 500" width="680" height="500">
  <defs><marker id="arr" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#EF4444"/></marker></defs>
  <rect width="680" height="500" fill="#F3F4F6"/>
  <!-- Panel 1: Chrome -->
  <rect x="40" y="20" width="600" height="120" fill="#FFF" stroke="#D1D5DB" rx="8"/>
  <rect x="600" y="40" width="24" height="24" fill="#E5E7EB" rx="6"/>
  <text x="612" y="56" text-anchor="middle" font-size="14" fill="#374151">⋮</text>
  <circle cx="584" cy="40" r="12" fill="#EF4444"/><text x="584" y="45" text-anchor="middle" fill="#FFF" font-size="12">①</text>
  <!-- Arrow -->
  <line x1="340" y1="148" x2="340" y2="180" stroke="#EF4444" marker-end="url(#arr)"/>
  <!-- Panel 2: Menu -->
  <rect x="40" y="188" width="600" height="140" fill="#FFF" stroke="#D1D5DB" rx="8"/>
  <rect x="480" y="196" width="140" height="120" fill="#FFF" stroke="#D1D5DB" rx="8"/>
  <text x="496" y="240" font-size="12" fill="#374151">Print...</text>
  <circle cx="464" cy="236" r="12" fill="#EF4444"/><text x="464" y="241" text-anchor="middle" fill="#FFF" font-size="12">②</text>
  <!-- Arrow -->
  <line x1="340" y1="336" x2="340" y2="368" stroke="#EF4444" marker-end="url(#arr)"/>
  <!-- Banner: Keyboard Shortcut -->
  <rect x="40" y="376" width="600" height="40" fill="#FEF3C7" rx="8"/>
  <text x="340" y="401" text-anchor="middle" font-size="13" fill="#92400E">🎹 Press Ctrl+P (or Cmd+P on Mac)</text>
</svg>
```

**Result:** Passed with a minor note. Layer 3 banner colors previously relied on implicit emoji inference; the current prompt now enforces explicit background fills (#FEF3C7 / #DBEAFE).

---

### Scenario 3: Log In to a Web Page

Mixed interaction involving input fields and a login button.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 600" width="680" height="600">
  <defs><marker id="arr" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#EF4444"/></marker></defs>
  <rect width="680" height="600" fill="#F3F4F6"/>
  <!-- Panel 1: Login Form -->
  <rect x="40" y="20" width="600" height="300" fill="#FFF" stroke="#D1D5DB" rx="8"/>
  <text x="340" y="60" text-anchor="middle" font-size="16" fill="#374151" font-weight="bold">Login</text>
  <!-- Username -->
  <rect x="200" y="90" width="280" height="36" fill="#F9FAFB" stroke="#D1D5DB" rx="6"/>
  <text x="210" y="113" font-size="12" fill="#9CA3AF">Username</text>
  <circle cx="180" cy="108" r="12" fill="#EF4444"/><text x="180" y="113" text-anchor="middle" fill="#FFF" font-size="12">①</text>
  <!-- Banner: Type Username -->
  <rect x="40" y="340" width="600" height="36" fill="#FEF3C7" rx="8"/>
  <text x="340" y="363" text-anchor="middle" font-size="13" fill="#92400E">⌨️ Type your username</text>
  <!-- Password -->
  <rect x="200" y="150" width="280" height="36" fill="#F9FAFB" stroke="#D1D5DB" rx="6"/>
  <text x="210" y="173" font-size="12" fill="#9CA3AF">Password</text>
  <circle cx="180" cy="168" r="12" fill="#EF4444"/><text x="180" y="173" text-anchor="middle" fill="#FFF" font-size="12">②</text>
  <!-- Login Button -->
  <rect x="240" y="220" width="200" height="40" fill="#3B82F6" rx="8"/>
  <text x="340" y="245" text-anchor="middle" font-size="14" fill="#FFF">Log In</text>
  <circle cx="220" cy="220" r="12" fill="#EF4444"/><text x="220" y="225" text-anchor="middle" fill="#FFF" font-size="12">③</text>
</svg>
```

**Result:** Layout algorithm previously struggled when non-click actions were interleaved inside a single panel. The current prompt now requires splitting the panel into Before/After states, or placing the banner below the panel and looping back with an arrow.

---

### Scenario 4: Insert an Image into a Word Document

Involves ribbon tabs and an OS-native file dialog.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 400" width="680" height="400">
  <defs><marker id="arr" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#EF4444"/></marker></defs>
  <rect width="680" height="400" fill="#F3F4F6"/>
  <!-- Panel 1: Word Ribbon -->
  <rect x="40" y="20" width="600" height="120" fill="#FFF" stroke="#D1D5DB" rx="8"/>
  <rect x="40" y="20" width="600" height="30" fill="#E5E7EB" rx="4"/>
  <text x="60" y="40" font-size="12" fill="#374151">Home</text>
  <text x="120" y="40" font-size="12" fill="#374151" font-weight="bold">Insert</text>
  <rect x="110" y="44" width="50" height="2" fill="#3B82F6"/>
  <circle cx="100" cy="30" r="12" fill="#EF4444"/><text x="100" y="35" text-anchor="middle" fill="#FFF" font-size="12">①</text>
  <rect x="60" y="70" width="60" height="50" fill="#F3F4F6" rx="6"/>
  <text x="90" y="100" text-anchor="middle" font-size="11" fill="#374151">Pictures</text>
  <circle cx="50" cy="70" r="12" fill="#EF4444"/><text x="50" y="75" text-anchor="middle" fill="#FFF" font-size="12">②</text>
  <!-- Arrow -->
  <line x1="340" y1="148" x2="340" y2="180" stroke="#EF4444" marker-end="url(#arr)"/>
  <!-- Panel 2: File Dialog (Simplified) -->
  <rect x="40" y="188" width="600" height="180" fill="#FFF" stroke="#D1D5DB" rx="8"/>
  <text x="60" y="220" font-size="14" fill="#374151" font-weight="bold">Insert Picture</text>
  <rect x="60" y="240" width="400" height="100" fill="#F9FAFB" stroke="#D1D5DB" rx="6"/>
  <text x="80" y="270" font-size="12" fill="#374151">📄 image1.png</text>
  <rect x="480" y="320" width="80" height="30" fill="#3B82F6" rx="6"/>
  <text x="520" y="340" text-anchor="middle" font-size="12" fill="#FFF">Insert</text>
  <circle cx="460" cy="320" r="12" fill="#EF4444"/><text x="460" y="325" text-anchor="middle" fill="#FFF" font-size="12">③</text>
</svg>
```

**Result:** OS-native dialogs (file pickers) previously looked identical to the host application. Layer 1 now requires a distinct title bar (#E5E7EB) to signal a context switch.

---

### Scenario 5: Create a Chart in Excel

Involves data selection and chart insertion, including a drag-to-select state.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 680 500" width="680" height="500">
  <defs><marker id="arr" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#EF4444"/></marker></defs>
  <rect width="680" height="500" fill="#F3F4F6"/>
  <!-- Panel 1: Excel Data -->
  <rect x="40" y="20" width="600" height="200" fill="#FFF" stroke="#D1D5DB" rx="8"/>
  <rect x="40" y="20" width="600" height="30" fill="#217346" rx="4"/>
  <text x="60" y="40" font-size="12" fill="#FFF">Insert</text>
  <rect x="60" y="70" width="200" height="120" fill="none" stroke="#3B82F6" stroke-width="2" stroke-dasharray="4 2" rx="4"/>
  <text x="80" y="100" font-size="12" fill="#374151">A1: Month, B1: Sales</text>
  <text x="80" y="130" font-size="12" fill="#374151">A2: Jan, B2: 100</text>
  <circle cx="50" cy="70" r="12" fill="#EF4444"/><text x="50" y="75" text-anchor="middle" fill="#FFF" font-size="12">①</text>
  <!-- Banner: Select Data -->
  <rect x="40" y="240" width="600" height="36" fill="#FEF3C7" rx="8"/>
  <text x="340" y="263" text-anchor="middle" font-size="13" fill="#92400E">🖱️ Drag to select data range (A1:B5)</text>
  <!-- Arrow -->
  <line x1="340" y1="284" x2="340" y2="316" stroke="#EF4444" marker-end="url(#arr)"/>
  <!-- Panel 2: Insert Chart -->
  <rect x="40" y="324" width="600" height="140" fill="#FFF" stroke="#D1D5DB" rx="8"/>
  <rect x="60" y="350" width="80" height="80" fill="#F3F4F6" rx="8"/>
  <text x="100" y="395" text-anchor="middle" font-size="11" fill="#374151">Column</text>
  <circle cx="50" cy="350" r="12" fill="#EF4444"/><text x="50" y="355" text-anchor="middle" fill="#FFF" font-size="12">②</text>
</svg>
```

**Result:** Drag-to-select actions previously lacked a visual selection state. Layer 1 now mandates a highlighted bounding box (#DBEAFE fill, #3B82F6 dashed stroke) around selected elements before the next click target is shown.

---

## FAQ

**Q1: The AI returned text instead of an SVG.**

- **Cause:** The prompt was not recognized as a system-level instruction, or it was overridden by later context.
- **Fix:** Ensure the prompt is placed in the System field. If the web UI lacks one, prefix your first user message with `=== SYSTEM INSTRUCTION ===`, paste the prompt, and explicitly ask the model to reply with raw SVG only.

**Q2: The generated UI looks different from the real software.**

- **Cause:** This is by design. The prompt explicitly forbids pixel-perfect replication to keep SVG generation fast and reliable.
- **Fix:** If you need higher fidelity, supply key color values or a screenshot in your request, but keep the core prompt in simplified mode for consistency.

**Q3: Action banners visually blend into UI panels.**

- **Cause:** Older prompt versions inferred banner colors implicitly from emojis, causing inconsistent fills across models.
- **Fix:** Use the latest prompt in `/prompt/visual-click-guide-prompt.txt`. Layer 3 now enforces explicit banner background colors (#FEF3C7 / #DBEAFE) and text colors (#92400E / #1E40AF).

**Q4: Arrows are missing after a typing or drag action inside the same screen.**

- **Cause:** The old prompt only required separation between panels, not handling of intra-panel non-click actions.
- **Fix:** The current prompt adds a rule: split the panel into Before/After states, or place the banner below the panel and loop back with an arrow to the next target inside the same panel.

**Q5: OS-native dialogs (e.g., file picker) look identical to the host app.**

- **Cause:** The old prompt did not distinguish application UI from system dialogs.
- **Fix:** Layer 1 now requires a distinct title bar (#E5E7EB fill) for OS-native dialogs to signal a context switch.

**Q6: I cannot see a selection state after a drag-to-select action.**

- **Cause:** The old prompt only handled "click" actions and did not define a visual selection state.
- **Fix:** Layer 1 now requires rendering a highlighted bounding box (#DBEAFE fill, #3B82F6 dashed stroke) around selected elements after a drag action and before the next click target.

---

## Contributing

Issues and pull requests are welcome. Please read [`CONTRIBUTING.md`](./CONTRIBUTING.md) for workflow and style requirements.

---

## License

[MIT License](../LICENSE)
