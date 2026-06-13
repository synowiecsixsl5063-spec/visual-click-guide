# Visual-Click-Guide（视觉点击向导）

> 让 AI 将文字操作步骤转化为可渲染的 SVG 视觉指引。

---

## 项目背景

在软件教学、技术支持与日常协作中，纯文字描述操作步骤往往导致较高的认知负荷。用户需要在大段文字中自行定位界面元素，极易产生误操作。**Visual-Click-Guide** 通过向 AI 注入结构化系统提示词，使其能够直接生成 SVG 格式的视觉操作指引图，以"所见即所得"的方式降低理解成本，提升操作准确性。

---

## 核心功能

本项目提供一套完整的**系统提示词（System Prompt）**。注入后，AI 具备以下能力：

1. **UI 简化模拟**：将目标软件界面抽象为简洁的卡片式示意图，不追求像素级复刻，但保留关键交互元素（按钮、菜单、输入框）。
2. **步骤标记**：以红色编号圆圈（①②③…）与虚线框精确标注每一步的点击位置。
3. **动作横幅**：对非点击类操作（输入文字、快捷键、拖拽选择）生成带 Emoji 前缀的彩色横幅，避免与界面面板混淆。
4. **流程箭头**：使用红色箭头串联各面板与横幅，形成自上而下的清晰时间线。
5. **跨平台输出**：输出为纯 SVG 代码，可直接嵌入网页、Markdown、文档或即时通讯工具中渲染。

---

## 使用方法

### 步骤一：获取提示词

复制 `/prompt/visual-click-guide-prompt.txt` 中的完整内容。

### 步骤二：注入系统提示词

根据你使用的 AI 平台，将提示词设置为**系统提示词（System Prompt）**或放在对话最开头的**系统级指令**位置：

- **Claude (Anthropic)**：在 Project 设置或对话开头的 `system` 字段中粘贴。
- **ChatGPT (OpenAI)**：通过 Custom Instructions（自定义说明）或 API 的 `system` 角色注入。
- **豆包 / 文心一言 / 通义千问**：在"角色设定"或对话开头的系统级输入框中粘贴。
- **Gemini**：通过 System Instruction 设置。

### 步骤三：发起请求

在注入提示词后的**同一会话**中，用自然语言描述你想完成的操作。例如：

> "请生成一个视觉指引，教我在 Windows 11 中打开设置应用。"

AI 将直接返回可渲染的 SVG 代码。

### 使用示例

**用户输入：**
> 如何让 AI 生成打开设置的视觉指引？

**AI 输出：**（见下方 `settings-windows-11.svg` 示例）

---

## 测试结果

以下测试由 Qwen 3.7 Max 执行，覆盖 5 个常见场景。所有 SVG 代码均直接复制自测试报告，可直接在浏览器中渲染。

### 场景 1：在 Windows 11 中打开"设置"应用

线性两步流程：任务栏点击开始菜单 → 点击设置图标。

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

**测试结论：** 简单线性流程处理完美，Layer 1、2、4 均正常工作。

---

### 场景 2：将 Chrome 当前页面导出为 PDF

涉及菜单展开与快捷键提示。

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

**测试结论：** 整体成功，但 Layer 3 横幅背景色此前依赖 Emoji 隐式推断，现已通过显式色值规则修正。

---

### 场景 3：登录网页（用户名/密码/登录按钮）

涉及输入框与按钮的混合交互。

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

**测试结论：** 同面板内出现非点击动作（输入用户名）时，布局算法曾出现箭头缺失。当前提示词已明确要求：若同屏出现非点击动作，应将面板拆分为 Before/After 状态，或将横幅置于面板下方并用箭头回指。

---

### 场景 4：在 Word 文档中插入图片

涉及功能区标签页与系统文件对话框。

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

**测试结论：** OS 原生对话框（文件选择器）曾与应用主界面混淆。当前提示词已要求对此类对话框添加独立标题栏（#E5E7EB 填充）以明示上下文切换。

---

### 场景 5：在 Excel 中创建图表

涉及数据选择与图表插入，包含拖拽选择状态。

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

**测试结论：** 拖拽选择动作曾缺乏选择状态可视化。当前提示词已要求在选择动作后、下一步点击前，渲染高亮边界框（#DBEAFE 填充，#3B82F6 虚线边框）以明确选中范围。

---

## 常见问题（FAQ）

**Q1：AI 没有输出 SVG，而是返回了文字说明？**

- **原因**：提示词未被识别为系统级指令，或被后续对话上下文覆盖。
- **解决**：确保将提示词置于对话最开头的 System 字段；若使用 Web 端无 System 字段，可在用户消息开头加 `=== SYSTEM INSTRUCTION ===` 再粘贴提示词，并强调"以下所有回复必须仅包含 SVG 代码"。

**Q2：生成的界面模拟与真实软件差异较大？**

- **原因**：这是预期行为。提示词明确要求"不追求像素级复刻"，以降低 SVG 复杂度并提升生成稳定性。
- **解决**：若需更高保真度，可在请求中补充关键色值或界面截图作为参考，但核心提示词仍建议保持简化风格以确保一致性。

**Q3：动作横幅的样式与界面面板混淆？**

- **原因**：旧版提示词中横幅背景色依赖 Emoji 隐式推断，导致部分模型填充色不一致。
- **解决**：请使用 `/prompt/visual-click-guide-prompt.txt` 中的最新版提示词，其中 Layer 3 已显式规定横幅背景色（#FEF3C7 / #DBEAFE）与文字色（#92400E / #1E40AF）。

**Q4：同屏内出现输入/拖拽动作后，下一步箭头缺失或布局混乱？**

- **原因**：旧版提示词仅要求"面板之间分离"，未规定同面板内非点击动作的处理方式。
- **解决**：新版提示词已增加规则：同屏非点击动作应将面板拆分为 Before/After 双状态，或将横幅置于面板下方并用箭头回指至面板内的下一个目标。

**Q5：OS 原生对话框（如文件选择器）看起来和主应用一样？**

- **原因**：旧版提示词未区分应用内 UI 与系统级对话框。
- **解决**：新版 Layer 1 已要求对 OS 原生对话框添加独立标题栏（#E5E7EB 填充）以区分上下文。

**Q6：拖拽选择后看不到选中区域？**

- **原因**：旧版提示词仅处理"点击"动作，未定义"选择状态"的可视化。
- **解决**：新版 Layer 1 已增加选择状态渲染规则：在拖拽动作后，于选中元素外围绘制高亮边界框（#DBEAFE 填充，#3B82F6 虚线边框）。

---

## 贡献指南

欢迎提交 Issue 与 Pull Request。详细流程与规范请查阅 [`CONTRIBUTING.md`](./CONTRIBUTING.md)。

---

## 许可证

本项目采用 [MIT 许可证](../LICENSE)。
