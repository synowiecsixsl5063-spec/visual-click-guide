# Visual-Click-Guide · 视觉点击向导

> **这个项目只做一件事：把"教别人操作电脑"变成一张带箭头、带编号的示意图。**
>
> 你给 AI 一段话（比如"怎么在 Excel 里做图表"），AI 直接画出一张步骤图——每一步点哪里、输入什么，红圈编号 + 红色箭头串联，像说明书一样从上看到下就行。

**This project does one thing:** turns "how to do X on a computer" into a numbered, arrow-linked visual diagram. Give an AI the prompt, tell it what you need — it draws a step-by-step SVG guide with click targets, action banners, and flow arrows.

---

## 它是怎么工作的？（超级简单）

| 步骤 | 你做什么 | AI 做什么 |
|------|----------|-----------|
| ① | 复制一段"说明书"（提示词） | — |
| ② | 塞进 AI 的系统提示词里 | — |
| ③ | 说一句人话，比如"教我在 Word 里插入图片" | — |
| ④ | — | AI 吐出一张 SVG 步骤图，直接能看 |

**核心文件就一个**：[`prompt/visual-click-guide-prompt.txt`](./prompt/visual-click-guide-prompt.txt)，复制它 → 粘贴到任何 AI 的系统提示词 → 完事。

---

## 能干什么？

帮任何人（你爸妈、你同事、你自己）生成软件操作教程图：

- 🖥️ **操作系统**：打开设置、改壁纸、装驱动
- 🌐 **浏览器**：导出 PDF、清缓存、装插件
- 📝 **Office**：Word 插入图片、Excel 做图表、PPT 加动画
- 🔐 **网页**：登录、注册、重置密码

AI 画出来的图长这样（5 个真实例子 → [`examples/`](./examples/)）：

| 场景 | 效果 |
|------|------|
| Win11 打开设置 | 任务栏 → 开始菜单 → 设置，两步红箭头串联 |
| Chrome 导出 PDF | 菜单点击 → 快捷键横幅，三步到位 |
| 网页登录 | 输用户名 → 输密码 → 点登录，输入框+按钮全标号 |
| Word 插入图片 | 功能区切标签 → 点按钮 → 系统弹窗选文件 |
| Excel 创建图表 | 拖选数据 → 点插入图表，选择态+点击全可视 |

---

## 文档导航

- 📖 **中文文档**：[docs/README.zh-CN.md](./docs/README.zh-CN.md)
- 📖 **English Docs**：[docs/README.md](./docs/README.md)
- 🤝 **贡献指南**：[docs/CONTRIBUTING.md](./docs/CONTRIBUTING.md)
- 📋 **发布说明**：[RELEASE.md](./RELEASE.md)
- ⚖️ **许可证**：[MIT](./LICENSE)
