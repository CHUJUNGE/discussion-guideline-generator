# discussion-guideline-generator

`discussion-guideline-generator` 是给研究员使用的 Codex skill 套件，用来把客户 brief、proposal、内部资料和 desk research，整理成可审阅、可导出的 Digital Diary（DG）讨论提纲。

你不需要先把材料整理成固定格式。把项目材料发给 Codex，用自然语言说明你想做一版 DG；Codex 会先理解项目和研究问题，再完成题目设计、题型检核与题面润色，最后按统一 Markdown 模板生成讨论提纲。需要 Word 时，再将已确认的内容转换为 Word。

这套能力由三个分工明确的 skills 协作完成：

| Skill | 负责什么 |
| --- | --- |
| `discussion-guideline-generator` | 理解项目、拆解研究问题、设计模块、题目、任务与 Diary / IDI 分工。 |
| `dg-question-type-setter` | 审阅并标注平台题型、模块类型、打卡频次和必填媒体要求。 |
| `dg-question-wording-editor` | 将研究逻辑完整的草稿改成受访者可理解、自然、低负担的题面。 |

## 适合什么时候用

- 已有 brief、proposal、客户内部资料或 desk research，需要生成一版 Digital Diary / discussion guideline。
- 需要把商业问题拆成受访者可完成的模块、任务和问题。
- 需要设计 Diary、IDI、家访、陪访、community 或其他定性研究中的讨论提纲。
- 已有一版 DG，希望只修改研究逻辑、题面自然度或平台题型。
- 需要输出供研究员、客户或平台继续审阅的 Word 版 DG。

## 如何在 Codex 里安装

在 Codex 新任务里对 Codex 说：

```text
请帮我从这个 GitHub 仓库安装 discussion-guideline-generator 套件中的三个 skills：
https://github.com/CHUJUNGE/discussion-guideline-generator
```

Codex 应安装以下三个目录：

```text
discussion-guideline-generator/
dg-question-type-setter/
dg-question-wording-editor/
```

安装成功后，请开启新任务，再输入：

```text
Use $discussion-guideline-generator 帮我根据附件里的 proposal 做一版 DG。
```

## 如何更新到最新版

当仓库更新后，在 Codex 新任务里说：

```text
请帮我从这个 GitHub 仓库更新 discussion-guideline-generator、
dg-question-type-setter 和 dg-question-wording-editor 到最新版：
https://github.com/CHUJUNGE/discussion-guideline-generator
```

更新后开启新任务再使用，以确保 Codex 重新加载最新规则。

## 你可以怎么和 Codex 说

```text
帮我根据这个 proposal 做一版 Digital Diary。
```

```text
客户 brief、proposal 和 desk research 都在附件里。Use $discussion-guideline-generator
先梳理项目理解和研究问题，再生成 DG 初稿。
```

```text
这版 DG 的研究逻辑不要改，只把题面改得更自然、少一点 checklist 感。
```

```text
请帮我检查这版 DG 的题型、打卡题设置和图片/视频要求是否合理。
```

```text
请保留模块结构，只把模块 4 和模块 5 改成更适合 45+ 人群完成的表达。
```

## Codex 会怎么工作

默认按以下顺序完成：

```text
项目材料
→ discussion-guideline-generator：项目理解、研究问题、模块与题目设计
→ dg-question-type-setter：研究员审阅版题型检核
→ dg-question-wording-editor：受访者题面润色
→ dg-question-type-setter：最终题型标注
→ Word 模板导出
```

具体来说，Codex 会：

1. 阅读 brief、proposal、内部资料和 desk research，区分已知信息与待探索问题。
2. 梳理商业问题、研究目标、目标人群、研究方法、品牌/刺激物限制和已有研究沉淀。
3. 先设计模块和观察点，再写题目；不会直接从材料跳到问题清单。
4. 判断哪些内容适合 Diary、哪些应保留给 IDI 或其他研究环节。
5. 检核每个模块的题型、打卡任务、频次和必填媒体要求。
6. 在不改变研究逻辑的前提下，降低题面的命令感、括号堆叠和受访者负担。
7. 只提出少量真正影响设计的待确认问题；其他不完整信息会明确标为待确认。
8. 按统一 Word 模板生成最终讨论提纲，并检查编号、题型、模块顺序和版式。

## 重要规则

- 默认先在聊天里给出可讨论的 DG 草稿；你明确要求“直接出 Word”时，才跳过确认直接导出。
- 不会把客户、品牌、产品刺激物或研究假设过早暴露给受访者。
- 不会为了润色而改变模块顺序、研究目的、Diary / IDI 分工、任务时机或必填素材要求。
- 题面润色采用最小必要改写：原文已经自然、具体、可回答时会保留。
- 不完整材料不会阻止起草；Codex 会给出可讨论版本，并将关键缺口标为“待确认”。
- 历史项目和最终 DG 仅用于离线评估与规则迭代，不应直接复制到新项目中。

## 产出类型

### 1. 聊天内 DG 设计草稿

用于先和研究员对齐，默认包含：

- 项目理解。
- 核心研究问题。
- 模块结构总览。
- 详细题目设计。

### 2. Word 版 Digital Diary / discussion guideline

在你确认草稿，或明确要求直接导出后，Codex 使用固定模板生成 Word 文件。

最终 Word 默认保留：

- 项目标题和项目理解。
- 核心研究问题与模块结构。
- 模块引导语、题目和结束语。
- `访谈题` / `打卡题` 模块类型。
- 简答、单选、多选、打分、排序、AI-bot、开场白、结束画面等题型标签。
- 打卡事件、重复频次、单位与必填图片/视频要求。

## 文件架构

```text
discussion-guideline-generator/
├── README.md
├── discussion-guideline-generator/
│   ├── SKILL.md
│   ├── agents/
│   │   └── openai.yaml
│   ├── assets/
│   │   └── dg-output-template.md    # 唯一强制的 DG 输出结构模板
│   └── references/
│       ├── agent-workflow.md
│       ├── generation-logic.md
│       ├── research-rules.md
│       ├── research-design-ai-agent-rules.md
│       ├── eval-rubric.md
│       ├── data-contracts.md
│       └── case-cards/
├── dg-question-wording-editor/
│   ├── SKILL.md
│   ├── agents/
│   │   └── openai.yaml
│   └── references/
│       ├── style-rules.md
│       ├── rewrite-patterns.md
│       ├── module-tone-guides.md
│       └── wording-eval-rubric.md
└── dg-question-type-setter/
    ├── SKILL.md
    └── references/
        └── question-type-rules.md
```

## 维护说明

只维护三个 skill 目录中的规则、案例卡、模板和版本文件。

不要把真实客户 brief、proposal、未脱敏项目材料、受访者信息、历史 DG 原件或任何敏感数据提交到仓库。历史案例应先脱敏并提炼成可复用规则或 case card，再进入 skill。
