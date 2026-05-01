# 与官方文档对齐说明（权威链接）

本 Skill 的模板字段优先对齐下列 **厂商官方** 指南；第三方教程仅作补充，不作为硬性条款来源。

---

## GPT Image 2（OpenAI）

| 要点（摘自官方） | Skill 中的体现 |
|------------------|----------------|
| 稳定顺序：**背景/场景 → 主体 → 关键细节 → 约束**；复杂请求用短标签分段或换行 | `image-templates.md` GPT Image 2 骨架顺序 |
| 写明 **用途**（广告 / UI mock / 信息图等）以设定成片精度预期 | 每条提示词含「用途/成片类型」一句 |
| **正文文字**：用引号包住字面文案，并写字体气质、大小、位置 | 海报/UI 类强制引号 + 版式 |
| **密集小字 / 多字体**：对比 `medium` 或 `high` quality（由用户在调用 API 时设置；提示词侧写明「需高可读性」） | 文案中提示「小字需清晰可读」 |
| **编辑**：**只改 X**，并 **反复强调保留项**，减少 drift | `Change / Preserve / Constraints` |
| **写实**：可显式写 `photorealistic` 等（官方称有助于进入写实模式） | Nano/GPT 写实需求下写入 |

权威链接：

- [Image generation | OpenAI API](https://developers.openai.com/api/docs/guides/image-generation)
- [GPT Image Generation Models Prompting Guide（Cookbook）](https://developers.openai.com/cookbook/examples/multimodal/image-gen-models-prompting-guide)
- [GPT Image 2 Model](https://developers.openai.com/api/docs/models/gpt-image-2)

---

## Nano Banana / Gemini Image（Google）

| 要点（摘自官方） | Skill 中的体现 |
|------------------|----------------|
| **具体**：主体、光线、构图写清楚 | 模板清单全覆盖 |
| **正向描述**：描述「要什么」，少用空洞否定堆叠（可与「禁止水印」等硬约束并存） | 主段落正向写画面；否定放在句末约束 |
| **动词开头**：生成类可用强动词开启句子（官方 Creative Director 一节） | 可选用「生成 / 绘制 / 合成」等开头 |
| **公式倾向**：Subject + Action + Location/context + Composition + Style（Cloud Blog） | 与 image 模板字段一致 |
| **镜头与器材**：官方允许摄影/镜头语言（如浅景深、焦段感受）；**不再**写死「禁止 f-stop」——改为「不要用互相矛盾的多套器材描述」 | 已修正 SKILL 与模板 |
| **画中文字**：引号 + 字体气质（DeepMind / Cloud） | 与 GPT 类似处理 |
| **编辑**：只描述「改什么、保留什么」 | 独立编辑段落 |

权威链接：

- [How to create effective image prompts — Gemini Image（DeepMind）](https://deepmind.google/models/gemini-image/prompt-guide/)
- [Ultimate prompting guide for Nano Banana（Google Cloud Blog）](https://cloud.google.com/blog/products/ai-machine-learning/ultimate-prompting-guide-for-nano-banana)
- [Nano Banana Pro prompt tips（Google Blog）](https://blog.google/products/gemini/prompting-tips-nano-banana-pro)

---

## Seedance（ByteDance / 开放平台）

| 要点（官方体系共性） | Skill 中的体现 |
|----------------------|----------------|
| **主线公式**：主体 → 动作 → 环境 → **镜头（独立一句）** → 风格 → 约束/负面（火山引擎 Seedance 提示规范综述） | `video-templates.md` Seedance 六段式 |
| **镜头与主体动作分开写**，避免混成一句说不清 | 模板内分两字段 |
| **每条镜头指令宜单一主轴**（避免多个冲突运动并列） | 「一段描述仅一个主推拉/摇移」 |
| **对白**：英文文档常见写法为 **双引号** 包住台词以利于口型（见下游 API README） | 有台词时保留引号句 |
| **多模态引用**：英文 API 文档常用 **`[Image1]`、`[Video1]`、`[Audio1]`** 占位；国内 **即梦** 等产品界面常用 **`@图片1`**。改写时应 **询问或根据用户平台二选一**，避免混用两套占位符。 | SKILL + video-templates 注明双轨 |

权威链接（请以你实际接入的渠道为准，二者同属官方体系不同触点）：

- [火山引擎 Seedance / 视频生成相关文档索引](https://www.volcengine.com/docs/82379/2222480)（文档编号随版本更新，请在控制台内打开最新「提示词/提示规范」章节）
- [Seedance 2.0 | ByteDance on Replicate — README（多模态引用与对白示例）](https://replicate.com/bytedance/seedance-2.0/readme)

---

## Veo（Google）

| 要点（官方） | Skill 中的体现 |
|--------------|----------------|
| **拆解要素**：主体、动作、场景/语境、镜头角度与运动、风格与氛围（Vertex「Anatomy of a Veo prompt」） | Veo 模板分段 |
| **短片聚焦单一场景**（Vertex Best practices） | 默认不写超长多场景史诗 unless用户要求 |
| **图像转视频**：首帧已定 → 提示词侧重 **运动**，少重复描述静态画面（Vertex） | 若有参考图，补一句「以下仅描述运动与镜头」 |
| **负面提示**：Vertex 建议用 **正向描述你想要的缺失效果**，而非堆砌「不要」（与 Nano 正向描述一致） | 约束句优先正向 |
| **对白与音效**：DeepMind Veo 3 指南示例使用 **引号台词** + 可单独写 SFX / Ambient | 音乐效分支模板 |
| **注意**：Vertex「Best practices」文档另有 **Avoid quotation marks** 条目（面向部分接口场景的泛化建议）。**实操**：若用户明确走 **Vertex API**，对白可采用「角色清晰说出以下台词：……」等 **少嵌套引号** 写法；若用户走 **Gemini / DeepMind 文档示例**，可保留 **标准引号对白**。以用户声明的平台为准。 | SKILL 注明双轨 |

权威链接：

- [Veo on Vertex AI — video generation prompt guide](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/video/video-gen-prompt-guide)
- [Best practices for Veo on Vertex AI](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/video/best-practice)
- [How to create effective prompts with Veo 3 — DeepMind](https://deepmind.google/models/veo/prompt-guide/)

---

## 版本与渠道声明

不同控制台（即梦 / Vertex / OpenAI Dashboard）的参数名与默认时长会变。Skill **只约束提示词正文结构**；**分辨率、时长、negative prompt 字段是否单独提交** 以各平台 API/UI 为准。
