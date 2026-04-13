# WriterDNA

![](https://ljf-write.oss-cn-hangzhou.aliyuncs.com/pageIndex.png)

**[WriterDNA 官网](http://writer-dna.tasai.top)** · [GitHub](https://github.com/liangjfblue/writer-dna) · [Gitee](https://gitee.com/aiami/writer-dna)

> 从你的原始素材中蒸馏出个人写作风格，生成专属于你的 AI 写作 Skill。支持任何写作类型——公众号、小说、公文、学术、文案等。

**你的风格，你的规则。框架从你的素材中自动推导。**

---

## 它是什么

WriterDNA 是一个写作风格蒸馏工具。你把原始素材（文章、聊天记录、喜欢的作者）扔进去，它分析写作风格，从素材中自动推导写作框架，最终生成一个可以安装到 Claude Code 的个人写作 Skill。不预设任何写作类型——公众号、小说、公文、学术、文案都能用。

```
你的素材（raw/）
    ↓ 双轨分析
风格知识库（wiki/）
    ↓ 框架推导 + 风格注入
你的写作 Skill（outputs/）
```

## 它不是什么

- 不是一个 AI 写作工具——它不替你写文章，它生成的 Skill 才是替你写文章的
- 不是一个通用模板——它从你的真实素材中提取风格，每个输出都是独一无二的
- 不是一个风格分析报告——它直接产出可安装、可执行的 Skill 包

## 三个概念

### 知识库（Karpathy 式 LLM 知识库方法论）

![](https://ljf-write.oss-cn-hangzhou.aliyuncs.com/pageIndex2.png)

像 Karpathy 把 LLM 的知识拆解成结构化、可理解、可学习的模块一样，WriterDNA 把一个人的写作风格拆解成结构化的知识体系：

- **人格轨**：核心价值观、语气节奏、情绪表达方式
- **技法轨**：词库、写作技法、个性化自检规则

不是一篇"风格分析报告"，而是一个可查询、可迭代、可注入 Skill 的风格知识库。

### Skill（卡兹克式）

最终输出是一个符合 Agent Skills 开放标准的写作 Skill：

```
<你的名字>-writer/
├── SKILL.md              ← 写作规则（风格内核 + 五层自检）
└── references/
    ├── style_examples.md  ← 风格示例库
    ├── content_methodology.md  ← 选题方法论
    └── scenes/           ← 场景插件（按文章类型）
```

安装后，对 Claude 说"帮我写一篇关于 XX 的文章"，就会自动用你的风格写。不限于公众号——小说、公文、学术、文案等任何类型都支持。

### 蒸馏（Distill）

从原始素材中"蒸馏"出风格基因——

- **情况 A**（有自己文章的写作者）：从文章 + 聊天记录中提取个人风格
- **情况 B**（纯新手）：从喜欢的作者的文章中学习目标风格，标注 [LEARNED]

写作过程中说"这句不像我"，系统自动记录纠错，持续迭代。

## 为什么是 WriterDNA

![](https://ljf-write.oss-cn-hangzhou.aliyuncs.com/pageIndex3.png)

- **零假设架构** — 不预设写作类型、技法列表或质量标准。框架从你的素材中自动推导，公众号、小说、公文、学术都能处理。
- **插件化场景** — 每种作品原型是独立的场景插件，包含专属的开头模式、结构模板和收尾方式。新增类型零侵入，核心 SKILL.md 不动。
- **五层渐进式自检** — L1 硬性规则（零容忍）→ L2 风格一致性 → L3 内容质量 → L4 作者声音一致性 → L5 运行时纠错。L5 是杀手级功能：写作中说"这句不像我"，自动记录，优先级高于 L1。
- **双用户类型自动适配** — 有经验写作者提取自己的风格（标 [CONFIRMED]），纯新手从喜欢的作者学习（标 [LEARNED]），同一套系统不同策略，随用户成长自动过渡。
- **可追溯的风格知识库** — wiki/ 不是黑盒，每个技法有证据标签，补充素材后增量更新，随时可审可调。

## 快速开始

### 1. 准备素材

把你的素材放到对应目录：

```
raw/
├── profile.md         ← 基础信息（AI 引导生成）
├── articles/          ← 你自己写的文章（越多样越好）
├── chats/             ← 聊天记录、朋友圈截图
├── references/        ← 你喜欢的作者的文章
└── interviews/        ← 访谈、演讲文字稿
```

### 2. 运行分析

在 Claude Code 中打开项目，说：

> "帮我创建一个写作风格 Skill"

系统会引导你完成三步：收集信息 → 风格分析 → 生成 Skill。

### 3. 安装 Skill

**macOS / Linux：**
```bash
cp -r outputs/<skill英文名>-writer ~/.claude/skills/
```

**Windows (PowerShell)：**
```powershell
Copy-Item -Recurse "outputs\<skill英文名>-writer" "$env:USERPROFILE\.claude\skills\"
```

### 4. 开始写作

```
"帮我写一篇关于 XX 的文章"
```

### 5. 用多个模型交叉验证

写完第一篇文章后，建议找其他大模型评价文章风格，然后拿反馈回来优化 Skill。

```
"请评价这篇文章的写作风格，是否符合xxx的风格"
```

推荐用以下模型分别评价，收集反馈后丢给 Claude Code：

| 模型 | 地址 | 特点 |
|------|------|------|
| [DeepSeek](https://chat.deepseek.com) | chat.deepseek.com | 中文理解强，风格分析细腻 |
| [GLM](https://chatglm.cn) | chatglm.cn | 国产模型代表，审美偏好不同 |
| [MiniMax](https://www.minimaxi.com) | minimaxi.com | 对话感强，适合评价"活人感" |
| [Gemini](https://gemini.google.com) | gemini.google.com | 多语言对比，提供国际视角 |

```
"以下是 DeepSeek/GLM/MiniMax/Gemini 对我文章的评价：<反馈内容>。
请根据这些反馈优化我的写作 Skill。"
```

不同模型有不同的审美偏好，交叉验证能帮你发现盲点。写作过程中说"这句不像我"会自动触发 L5 纠错记录，持续迭代。

## 项目结构

```
writer-dna/
├── CLAUDE.md              ← 蒸馏引擎规则（AI 指令）
├── templates/             ← 参考实现（完整 skill 示例，不要修改）
│   └── khazix-writer/     ←   公众号ai、科技写作的参考实现
├── raw/                   ← 你的原始素材（只读不改）
├── wiki/                  ← 风格知识库（AI 分析生成）
├── outputs/               ← 生成的 Skill 包
└── docs/                  ← 文档和落地页
```

## 致谢

- [数字生命卡兹克](https://github.com/KKKKhazix/Khazix-Skills) — 参考实现和五层自检体系
- [Karpathy 的 LLM 知识库方法论](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) — 结构化、可理解、可学习
- 万维钢 — 风格参考标杆
