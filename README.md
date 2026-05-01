# cn-aigc-prompt-rewriter

## 价值：为什么要用这个 Skill

用语言去描述 **图像或视频**（两种完全不同的模态），中间往往会伴随 **九成以上的信息缺失**：你心里想的构图、光线、材质、层次和节奏，很难在一两句话里说全，模型只能「猜」。这正是 **文生图 / 文生视频** 特别容易陷入 **反复抽卡、大量作废出图** 的根本原因——不是运气差，而是 **输入里该有的视觉指令根本没写够、没写对**。

本 Skill 要做的，是把你的 **原始提示词当成半成品**：在此基础上 **拓展、润色与结构化**，并按 **GPT Image、Nano Banana、Seedance、Veo** 等不同模型的写法偏好做 **适配**，让模型更少瞎猜、更少跑偏，从而 **压低无效生成次数，把时间 Token 花在更接近成片的方向上**。

这是一套面向各类 **AI 助手 / 编码 Agent** 的可执行规则：在真正调用生图、生视频模型之前，先把中文草稿整理成 **可直接粘贴进模型**、且 **带模型标签与多版本对比** 的成稿。

> **`SKILL.md` 顶部的 YAML**（`name` / `description`）主要为 **Cursor Skills** 的发现机制设计；在其他工具里可 **忽略 frontmatter**，正文规则仍然全部适用。

## 能力概览

| 能力 | 说明 |
|------|------|
| **首轮输出** | 默认 **恰好 3 条**（版本 A/B/C），在构图、光线或镜头节奏上有 **肉眼可见差异**，核心意图保持一致 |
| **模型标注** | 每条标题包含 **「适用于：具体模型」**，避免贴错工具链 |
| **覆盖模型** | 图像：**GPT Image 2.0**、**Nano Banana（Gemini 图）**；视频：**Seedance**、**Veo** |
| **修订** | 指定某一版继续改 → 单条 **「版本 X · 修订」** 全文 |
| **跨模型适配** | 例如 Nano ↔ GPT Image、Seedance ↔ Veo，按目标模型 **重写结构**，保留创意内核 |
| **模板与依据** | `references/` 内提供图/视频骨架及与 **厂商文档对齐** 的说明链接 |

更细的规则、质量门与安全边界见 **[`SKILL.md`](SKILL.md)**；示例见 **[`examples.md`](examples.md)**。

## 仓库结构

```text
.
├── README.md                 # 本说明
├── SKILL.md                  # 主规则（含 YAML，Cursor 可用于发现）
├── examples.md               # 输出格式与场景示例
└── references/
    ├── image-templates.md    # 文生图模板（GPT Image / Nano Banana）
    ├── video-templates.md    # 文生视频模板（Seedance / Veo）
    └── official-sources.md   # 与官方文档对齐的摘要与链接
```

## 通用用法（任意工具）

1. 把整个文件夹放进 **当前工作区 / 仓库根目录下固定路径**（见下文各工具推荐路径）。
2. 在开始改写前，用工具支持的任一方式让模型 **读到 [`SKILL.md`](SKILL.md)**；需要细化风格时再让它参考 `references/` 与 [`examples.md`](examples.md)。
3. 对用户指令的建议话术示例：  
   **「严格按仓库里的 SKILL.md 输出三条带『适用于』的版本；参考 examples.md 的格式。」**

各产品界面名称不同（`@文件`、`#文件`、手动粘贴、`CLAUDE.md` 引用），本质是 **把 SKILL 正文注入上下文**。

---

## Cursor

**安装路径（推荐）：**

```text
<你的项目>/.cursor/skills/cn-aigc-prompt-rewriter/
```

目录名 **`cn-aigc-prompt-rewriter`** 建议与 `SKILL.md` 里的 `name` 一致。

**使用方式：**

1. 对话里 **`@`** 指向  
   `.cursor/skills/cn-aigc-prompt-rewriter/SKILL.md`，再粘贴原始需求。
2. 或在 **Cursor Rules / 项目规则** 中写明：进行中文 AIGC 提示词改写时优先遵循该 Skill。

自动挂载依赖 Cursor 对 `description` 的匹配；**最稳的是每次 `@ SKILL.md`**。

---

## Claude Code（Anthropic Claude Code CLI）

Claude Code 会读取项目里的 **`CLAUDE.md`** 作为长期项目说明；本仓库 **不会自动替代** 你的 `CLAUDE.md`，推荐二选一或组合：

**方式 A — 会话内显式引用（最直接）**  
在对话里说明：请先阅读工作区中的  
`cn-aigc-prompt-rewriter/SKILL.md`（路径按你实际放置位置），再按其中硬性规则改写提示词。若工具支持 **`@路径`** 或 **`Read`** 某文件，对 `SKILL.md` 使用该能力。

**方式 B — 写入 CLAUDE.md（省心）**  
在仓库根目录的 `CLAUDE.md` 末尾追加一段，例如：

```markdown
## 中文 AIGC 提示词改写
当用户要做文生图/文生视频提示词改写、润色或多版本输出时，必须遵循 `./cn-aigc-prompt-rewriter/SKILL.md` 的全文规则；模板与官方对齐说明见同目录 `references/`，示例见 `examples.md`。
```

将 `./cn-aigc-prompt-rewriter/` 换成你把本仓库解压后的 **实际相对路径**。

**方式 C — 单体仓库**  
若本项目 **就是** 提示词 Skill 仓库，也可直接把 **`SKILL.md` 全文**（去掉 YAML 或保留均可）合并进 `CLAUDE.md`，避免多层路径。

---

## Claude.ai / Claude Desktop（Projects）

1. 新建或打开一个 **Project**，在 **项目说明 / Project instructions / 知识库** 中：  
   - 粘贴 **`SKILL.md` 正文**（可省略 YAML），或  
   - 上传 **`SKILL.md` + `examples.md`**（若界面支持文件）。
2. 需要严格对齐某模型时，再上传 `references/` 下对应模板。
3. 每次任务开头可简短提醒：**「按项目里的 SKILL 规则输出三条」**。

---

## GitHub Copilot（VS Code / JetBrains）

1. 把工作区内的 **`SKILL.md`** 放在固定路径（例如仓库根下的 `docs/cn-aigc-prompt-rewriter/SKILL.md`）。
2. 使用 **Copilot Chat** 时 **`#`** 引用该文件（若当前编辑器支持 **attach file / 引用工作区文件**），或在对话中粘贴关键章节。
3. 可在仓库中添加 **`.github/copilot-instructions.md`**（或官方文档推荐的指令文件），用一段话指向「提示词改写须遵守某路径下的 SKILL.md」。具体文件名以 [GitHub Copilot 自定义指令文档](https://docs.github.com/en/copilot) 为准。

---

## Windsurf、Continue、Codeium 等（通用）

思路与上面相同：

- 找到该产品 **「Rules / Instructions / 上下文文件」** 配置入口；
- 写入：**改写中文生图/生视频提示词时，读取工作区 `<路径>/SKILL.md` 并遵守全文**；
- 会话中尽量 **附带 `SKILL.md`（或整个文件夹）** 再提问。

界面可能是 `@`、`Add context`、`Workspace` 选文件等，以各工具最新文档为准。

---

## 输出格式（首轮）

每条结构示意：

```text
【版本 A · 均衡 · 适用于：<模型>】

<完整提示词正文>
```

版本 B、C 同理；模型名须与任务类型一致（图任务不出现 Seedance/Veo，视频任务不出现 GPT Image/Nano Banana）。

---

## 手动上传到 GitHub

若不使用 Git，可在 GitHub 网页 **新建仓库** 后，用 **「Add file → Upload files」** 上传本仓库内文件，并保持 **`references/`** 子目录结构不变。

---

## 许可与声明

- 本 Skill 的 Markdown 文本可按需 **自用或分享**。
- 各模型 API、控制台参数以厂商为准；`references/official-sources.md` 中的外链著作权归原站点所有。

---

如有改进建议，欢迎通过 Issue / PR 交流（若你已启用仓库协作）。
