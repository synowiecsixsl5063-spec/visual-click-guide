# Contributing to Visual-Click-Guide

Thank you for your interest in improving Visual-Click-Guide. This document covers the contribution workflow, prompt authoring rules, and testing requirements.

---

## Contribution Workflow

1. **Fork the repository** on GitHub.
2. **Create a feature branch** from `main`:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. **Make your changes** following the code style rules below.
4. **Test your changes** using the Qwen test procedure (see Testing Requirements).
5. **Commit with a clear message**:
   ```bash
   git commit -m "fix: add explicit banner fill rules for Layer 3"
   ```
6. **Push to your fork** and open a Pull Request against `main`.
7. **Describe your PR** with:
   - What problem it solves
   - Which layer(s) are affected
   - Test results (pass/fail with SVG sample)

---

## Prompt Authoring Rules

All changes to `/prompt/visual-click-guide-prompt.txt` must satisfy the following constraints:

### Visual Specification Constraints
- **Color palette is fixed.** Do not introduce new colors unless the change is explicitly justified and tested across light and dark themes. Current canonical colors:
  - Canvas background: `#F3F4F6`
  - Panel background: `#FFF`
  - Panel stroke: `#D1D5DB`
  - Accent / click target: `#3B82F6`
  - Step indicator: `#EF4444`
  - Banner yellow: `#FEF3C7` with text `#92400E`
  - Banner blue: `#DBEAFE` with text `#1E40AF`
  - Selection highlight: `#DBEAFE` fill, `#3B82F6` dashed stroke
  - OS dialog title bar: `#E5E7EB`
- **Geometry is simplified.** Rectangles, text, and basic shapes only. No embedded raster images, no external CSS, no JavaScript.
- **Output must be a single self-contained SVG.** No markdown fences, no conversational wrapper.

### Layer Modification Rules
The prompt is organized into four layers. When editing, preserve the layer boundaries and update the relevant section header:

- **Layer 1 (UI Mockup):** Any change to how interfaces are drawn (new widget types, OS dialog handling, selection states).
- **Layer 2 (Step Indicators):** Changes to numbering, badge placement, or target outlining.
- **Layer 3 (Action Banners):** Changes to non-click action rendering, emoji prefixes, or banner colors.
- **Layer 4 (Flow Arrows):** Changes to panel sequencing, arrow routing, or intra-panel loop-back logic.

### Backward Compatibility
- Do not remove existing rules unless they are proven harmful.
- New rules should be additive and placed in the appropriate layer.
- If a rule contradicts an older one, explicitly mark the old rule as deprecated in the commit message and update the FAQ.

---

## Testing Requirements

Every functional change to the prompt must be validated using the following procedure before submitting a PR:

### Test Harness
Use **Qwen 3.7 Max** (or the latest available Qwen Max model) as the test harness. This model has been benchmarked to reliably evaluate SVG structure and visual logic.

### Mandatory Test Scenarios
At minimum, generate and verify SVG output for:

1. **Linear click flow** (e.g., open Settings) — validates Layers 1, 2, 4.
2. **Menu + keyboard shortcut** (e.g., Chrome print to PDF) — validates Layer 3 banner placement and color consistency.
3. **Form input with interleaved typing** (e.g., web login) — validates intra-panel banner handling and arrow continuity.
4. **OS-native dialog** (e.g., Word insert picture) — validates Layer 1 context-switch title bar.
5. **Drag-to-select** (e.g., Excel chart creation) — validates selection state rendering and bounding box logic.

### Validation Checklist
For each generated SVG, confirm:

- [ ] Valid XML with `xmlns="http://www.w3.org/2000/svg"`.
- [ ] No markdown code fences or conversational text outside the SVG tag.
- [ ] All step indicators are sequential (①, ②, ③…) with no duplicates or skips.
- [ ] Red arrow marker (`#arr`) is defined in `<defs>` and used correctly.
- [ ] Action banners use the canonical color values, not inferred or omitted fills.
- [ ] OS-native dialogs include a distinct title bar (`#E5E7EB`).
- [ ] Selection actions render a highlighted bounding box before the next click target.
- [ ] The SVG renders correctly in Chrome, Firefox, and Safari.

### Reporting Test Results
Include a `TEST_REPORT.md` snippet in your PR description with:
- Scenario name
- Pass / Fail status
- Attached SVG code (or link to the file in `/examples`)
- Any deviations from the canonical color values or layout rules

---

## Code of Conduct

- Be respectful and constructive in all discussions.
- Focus on objective improvements: reproducibility, visual clarity, and cross-model compatibility.
- When proposing color or layout changes, provide before/after SVG samples.

---

## Questions?

Open a GitHub Issue with the label `question` or start a Discussion.
