---
name: discussion-guideline-generator
description: Design Digital Diary (DG) and qualitative discussion guidelines from Briefs, Proposals, client materials, and researcher feedback. Use when the user asks to generate, review, revise, or systematize DG / Digital Diary project understanding, commercial and research questions, module structure, observation points, Diary vs IDI split, task logic, case cards, research rules, or evaluation rubrics. Use dg-question-wording-editor for respondent-facing wording polish and dg-question-type-setter for type review or final labels.
---

# Discussion Guideline Generator

Use this skill to help design Digital Diary / DG question plans from project materials.

In production, treat this skill as a versioned research-logic specification layer. It should work with historical project inputs, final DG gold answers, model runs, and automated evaluation results. Do not treat the skill as the only source of model quality.

## Gold Data Priority

When `gold_data/reports/designer_patterns.json` or other database-derived final DG pattern files are available, use them as empirical reference only:

- Existing skill rules, research rules, generation logic, Brief, Proposal, and explicit client requirements take priority.
- Gold data patterns can suggest common module sequences, task patterns, question type distributions, and evaluation checks.
- Do not copy historical final DG questions mechanically.
- If a gold pattern conflicts with an existing rule, follow the existing rule and treat the conflict as a review/eval note.
- Promote a gold-data insight into `research-rules.md` only when it is repeated across cases or carries high research risk.
- Do not inject raw database JSON or full pattern files into normal generation prompts. Use gold data offline to distill compact rule candidates, then promote reviewed rules into this skill.

## Core Workflow

Always work in this order:

```text
Project understanding
-> Commercial problem
-> Core research questions
-> Module structure
-> Module observation points
-> Research-complete question draft
-> Wording handoff
-> Agent self-check
-> Necessary confirmation questions
```

Do not jump directly from project files to questions.

## Required References

Before generating a first draft, read:

- `references/agent-workflow.md`
- `references/generation-logic.md`
- `references/research-rules.md`
- `references/research-design-ai-agent-rules.md` (researcher-authored rules; must not be truncated in prompts)

When implementing backend, database, training, or evaluation integration, also read:

- `references/data-contracts.md`
- `references/eval-rubric.md`
- `VERSION.json`

Then select relevant case cards only when useful:

- `references/case-cards/case-001-gum.md`: gum / mouth-related category growth, functional + emotional occasions, shopping task.
- `references/case-cards/case-002-chocolate.md`: chocolate / snacking / emotional demand spaces / daily frequency growth.
- `references/case-cards/case-003-wonton.md`: continuous listening / repeat wave / existing sample logic.
- `references/case-cards/case-004-45plus-health.md`: 45+ / health / VMS / trust and category expansion.

Use case cards for design logic only. Do not copy case questions mechanically.

## Versioned Inputs

When the surrounding system provides versions, preserve or report:

- `skill_version`
- `generation_logic_version`
- `research_rules_version`
- `case_card_version`
- `fixed_template_version`
- `eval_rubric_version`
- `model_version`

These versions are required for later regression testing against final DG gold answers.

Follow the complete stage contract in `references/agent-workflow.md`. Use Codex-native reasoning and document tools rather than an external model API or a prompt-builder script.

## Output Format

For every researcher-facing first draft, read and follow `assets/dg-output-template.md`. Preserve its heading order, section names, module table, and module-level `引导语 / 题目 / 结束语` structure.

Keep sections 1-3 concise. Put most detail in section 4. The researcher-facing final output ends after the detailed question design.

For each module in section 4, use the template structure and include the module type. Use `访谈题` by default; use `打卡题` only for a repeated diary task and then state its event name, frequency, and unit. Label module introductions `【开场白】` and endings `【结束画面】`; add a user-facing platform type label before every question.

```markdown
### 模块x：我/我的/我是/我怎么...模块名
模块类型：访谈题

**引导语：**

**题目：**

【简答】1.

**结束语：**
```

Do not write “建议题目示例”, “示例题”, or “建议题量”.

Do not add research purpose, design explanation, internal logic, Wording Handoff, or `题型检核摘要` to the researcher-facing final output. Keep those details only for internal handoff or when the user explicitly asks for a review or audit trail.

Respondent-facing module titles in section 4 must default to first-person "我 / 我的 / 我是 / 我怎么..." wording, such as "我的一天", "我的文具全家福", "我是怎么选笔的", or "我的下一支笔". Use research-style module names only in internal structure tables or when the client explicitly requires fixed titles.

## Wording Handoff

This skill owns research logic, not detailed respondent-facing style rules.

After generating or revising a research-complete DG draft, hand off the detailed wording pass to `dg-question-wording-editor` when:

- the user asks for more natural,口语化, less rigid, or less checklist-like wording;
- the draft contains many parenthetical examples, hard counts, ranking/scoring language, or forced media uploads;
- the next production step is a separate wording agent.

Preserve in the handoff:

- module order and module purpose;
- corresponding research questions;
- required observation points;
- Diary vs IDI split and task timing;
- repeated diary/check-in module details, including event name, frequency, and unit when known;
- mandatory image/video upload intent when the source or research design requires media to be compulsory;
- brand/product exposure constraints;
- any fixed template or client-required wording.

## Revision Workflow

When the user gives feedback:

1. Identify which modules or questions are affected.
2. Preserve unaffected content.
3. Revise the relevant section or provide a complete revised version if asked.
4. If the feedback reveals a reusable rule, propose where to store it:
   - `references/research-rules.md`
   - a case card
   - an eval rubric
   - a fixed template

If the user says the output is “太死板 / 太像 checklist / 括号太多 / 太命令式”, preserve the research logic and route the affected sections through `dg-question-wording-editor`.

## Data-Driven Iteration Workflow

When historical gold-answer data is available, use this workflow:

```text
historical input materials
-> current model generates DG
-> compare with final DG gold answer
-> identify module, logic, wording, and burden gaps
-> produce eval result and gap report
-> propose updates to rules, case cards, templates, retrieval, or training data
-> run regression test before updating production
```

Prefer database-driven gold-answer comparison over endless manual prompt tweaking.

Gap types to classify:

- missing module
- extra module
- wrong module order
- wrong research logic
- too generic
- too rigid / checklist-like
- too many examples or parentheses
- respondent burden too high
- brand exposed too early
- Diary vs IDI split wrong
- fixed template violation

Only promote a rule into `research-rules.md` when it appears across cases or is high risk.

Use `generation-logic.md` for workflow-level constraints.

Use case cards for case-specific but reusable design logic.

Use training data when the gap requires pattern learning across many examples rather than one explicit rule.

## Codex-Native Execution

Read the supplied project files directly. Do not require API keys, ChatAnywhere, an OpenAI-compatible endpoint, or `scripts/prompt.py`.

For a complete final output, coordinate the fixed workflow with `dg-question-type-setter` and `dg-question-wording-editor`; preserve their role boundaries and the stage order defined in `references/agent-workflow.md`.

## Quality Check

Before finalizing, check:

- Does each module map to a core research question?
- Are early modules about the person and life context, not the target brand?
- Are Diary tasks logically answerable before wording polish?
- Are repeated diary/check-in modules clearly identifiable for later `打卡题` labeling?
- Are mandatory image/video tasks distinguished from optional media suggestions?
- Are tasks too heavy from a research-design perspective?
- Are confirmation questions limited to at most 3?
- Did the output avoid exposing internal research labels to respondents?

## Gold Answer Evaluation

When comparing against a final DG gold answer, evaluate at three levels:

1. Structure: module presence, module order, task modules, diary days.
2. Research logic: mapping to commercial questions, Proposal coverage, Diary vs IDI split.
3. Question wording: naturalness, openness, fixed templates, respondent burden, brand exposure.

Do not rely only on text similarity. Different wording can be acceptable if the research logic and respondent task are equivalent.
