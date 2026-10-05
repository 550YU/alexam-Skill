# alexam-Skill

面向岗位与真实工作场景的双语 AI 考试命题 Skill，可将培训资料转化为可复用、经过质量控制的题库与考试交付包。

A role-aware, workplace-oriented bilingual AI exam-authoring skill that turns training materials into reusable, quality-controlled question banks and exam packages.

> 高质量命题不是即时生成文本。正确选项与干扰项的设计需要经过语义推理、答案唯一性证明、双语一致性审核、语义查重和最终交付物验证。复杂任务可能需要一定时间；本 Skill 会按阶段反馈进度，不会以牺牲质量换取速度。
>
> High-quality authoring is not instant text generation. Correct answers and distractors require semantic reasoning, uniqueness proof, bilingual parity review, deduplication, and final artifact validation. Complex runs may take time; the skill reports progress by stage and does not trade correctness for speed.

## 功能概览 / What It Does

`alexam-Skill` 引导 Agent 完成以下流程：

`alexam-Skill` guides an agent through the following workflow:

1. 完整阅读源材料并拆解知识点。 / Read all source materials and decompose their knowledge completely.
2. 互动确认真实的目标人群、岗位、经验层级和工作场景。 / Interactively confirm the actual audience, role, experience level, and workplace context.
3. 确认准确的题型与题目数量。 / Confirm the exact question types and counts.
4. 按知识点、认知层级、难度、分值和岗位权限设计蓝图。 / Build a blueprint by knowledge point, cognitive level, difficulty, score, and role authority.
5. 生成中英双语的工作场景题目。 / Generate bilingual workplace-scenario questions.
6. 设计正确选项与干扰项，并双向证明答案唯一性。 / Design correct options and distractors with bidirectional answer-uniqueness proof.
7. 执行语义查重、质量审核和自动修复。 / Perform semantic deduplication, quality review, and automatic repair.
8. 验证 Word、用户模板及 Excel 交付物。 / Validate Word, user-template, and Excel deliverables.
9. 提供考试配置、结果分析和补学建议。 / Provide exam configuration, result analysis, and relearning recommendations.

## 核心原则 / Key Principles

- **不预设岗位 / No assumed role：** TAC、GTAC、支持工程师和其他岗位都只是输入示例，不是默认值。 / TAC, GTAC, support engineer, and all other roles are input examples—not defaults.
- **用户场景优先 / User context wins：** 用户确认的岗位和场景优先于材料人物设定及历史试卷。 / The user's confirmed role and scenario override source personas and earlier exams.
- **促进学习迁移 / Learning transfer：** 通过场景把概念和机制连接到真实工作决策。 / Scenarios connect concepts and mechanisms to realistic workplace decisions.
- **双语语义一致 / Bilingual parity：** 中英文必须保留相同的事实、限定条件、权限边界和因果关系。 / Chinese and English preserve the same facts, qualifiers, authority limits, and causality.
- **保障答案完整性 / Answer integrity：** 每个正确选项必须直接回答任务，每个干扰项都必须能够依据题干证明为错误。 / Every keyed choice must answer the task, and every distractor must be provably incorrect under the stem.
- **交付物级验收 / Artifact-level acceptance：** 生成文件必须在交付前重新打开并独立审核。 / Generated files are reopened and independently audited before delivery.
- **隐私边界 / Privacy boundary：** 本仓库不包含源文档和为客户生成的考试。 / Source documents and generated customer exams are not included in this repository.

## 仓库结构 / Repository Layout

```text
.
├── SKILL.md                         # Skill 主执行规则 / Main skill instructions
├── agents/openai.yaml               # Agent 元数据与默认提示 / Agent metadata and default prompt
├── references/quality-rules.md      # 详细质量与发布门禁 / Detailed quality and release gates
├── examples/audience-dialog.md      # 互动确认示例 / Interactive confirmation examples
├── examples/blueprint.example.json  # 脱敏的可机读蓝图 / Sanitized machine-checkable blueprint
├── examples/question.example.json   # 脱敏的结构化题目示例 / Sanitized structured question example
├── CHANGELOG.md                     # 版本记录 / Changelog
├── CONTRIBUTING.md                  # 贡献指南 / Contribution guide
└── LICENSE                          # MIT 许可证 / MIT License
```

## 安装 / Installation

将本仓库复制到 Copilot 用户级 Skills 目录，并保留现有目录结构：

Copy this repository into your Copilot user skills directory and retain the existing folder structure:

```powershell
Copy-Item -Recurse . "$HOME\.copilot\skills\zsexam"
```

安装后请重启或重新加载 Skill 宿主。可使用以下提示词调用：

Restart or reload the skill host after installation. Invoke it with prompts such as:

- `使用 zsexam 根据这些培训材料生成一套双语考试。 / Use zsexam to generate a bilingual assessment from these training materials.`
- `根据这份培训资料出题，并按照上传的模板导出。 / Generate questions from this training material and export them using the uploaded template.`
- `审核这个题库是否存在重复推理路径和歧义答案。 / Audit this question bank for duplicate reasoning paths and ambiguous answers.`

## 必需互动流程 / Required Interaction Flow

开始命题前，Skill 会确认以下信息：

Before drafting, the skill confirms the following information:

1. 目标岗位或人群。 / Target role or audience.
2. 相关经验层级。 / Relevant experience level.
3. 主要工作场景。 / Primary workplace scenarios.
4. 准确的题型和题目数量。 / Exact question types and counts.

如果用户已明确提供这些信息，Skill 只需统一回显确认，不会重复询问。用户自由输入的内容具有最高优先级。

If these values are already explicit, the skill confirms them once rather than repeatedly asking. Free-form user input is authoritative.

## 输出与质量门禁 / Output and Quality Gates

每道题可包含双语题干、选项、解析和知识点，以及答案、中文难度、分值、认知层级、标签、岗位锚点、工作任务、受众适配度、场景相关性、自动评分适用性和版本号。

Each question can include a bilingual stem, options, explanation, and knowledge point, together with the answer, Chinese difficulty, score, cognitive level, tags, role anchor, workplace task, audience fit, scenario relevance, auto-grading suitability, and version.

以下问题会阻止发布：答案存在歧义、干扰项不合理或不平行、字段未翻译、语义重复、题目偏离主题、蓝图元数据过期、答案映射错误或模板结构偏移。

Release is blocked by ambiguous answers, implausible or nonparallel distractors, untranslated fields, semantic duplicates, off-theme questions, stale blueprint metadata, answer-mapping errors, or template drift.

## 安全与隐私 / Safety and Privacy

请勿提交专有课程资料、客户文档、生成的私有考试、凭据或个人身份信息。本仓库中的示例均为合成内容且不依赖特定技术产品。

Do not commit proprietary courseware, customer documents, generated private exams, credentials, or personally identifiable information. The examples in this repository are synthetic and technology-neutral.

## 许可证 / License

本项目采用 MIT License，详见 [LICENSE](LICENSE)。

This project is licensed under the MIT License. See [LICENSE](LICENSE).
