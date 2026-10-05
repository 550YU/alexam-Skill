# alexam-Skill

## English

A role-aware, workplace-oriented bilingual AI exam-authoring skill that turns training materials into reusable, quality-controlled question banks and exam packages.

> High-quality authoring is not instant text generation. Correct answers and distractors require semantic reasoning, uniqueness proof, bilingual parity review, deduplication, and final artifact validation. Complex runs may take time; the skill reports progress by stage and does not trade correctness for speed.

### What It Does

`alexam-Skill` guides an agent through the following workflow:

1. Read all source materials and decompose their knowledge completely.
2. Interactively confirm the actual audience, role, experience level, and workplace context.
3. Confirm the exact question types and counts.
4. Build a blueprint by knowledge point, cognitive level, difficulty, score, and role authority.
5. Generate bilingual workplace-scenario questions.
6. Design correct options and distractors with bidirectional answer-uniqueness proof.
7. Perform semantic deduplication, quality review, and automatic repair.
8. Validate Word, user-template, and Excel deliverables.
9. Provide exam configuration, result analysis, and relearning recommendations.

### Key Principles

- **No assumed role:** TAC, GTAC, support engineer, and all other roles are input examples—not defaults.
- **User context wins:** The user's confirmed role and scenario override source personas and earlier exams.
- **Learning transfer:** Scenarios connect concepts and mechanisms to realistic workplace decisions.
- **Bilingual parity:** Chinese and English preserve the same facts, qualifiers, authority limits, and causality.
- **Answer integrity:** Every keyed choice must answer the task, and every distractor must be provably incorrect under the stem.
- **Artifact-level acceptance:** Generated files are reopened and independently audited before delivery.
- **Privacy boundary:** Source documents and generated customer exams are not included in this repository.

### Repository Layout

```text
.
├── SKILL.md                         # Main skill instructions
├── agents/openai.yaml               # Agent metadata and default prompt
├── references/quality-rules.md      # Detailed quality and release gates
├── examples/audience-dialog.md      # Interactive confirmation examples
├── examples/blueprint.example.json  # Sanitized machine-checkable blueprint
├── examples/question.example.json   # Sanitized structured question example
├── CHANGELOG.md                     # Changelog
├── CONTRIBUTING.md                  # Contribution guide
└── LICENSE                          # MIT License
```

### Installation

Copy this repository into your Copilot user skills directory and retain the existing folder structure:

```powershell
Copy-Item -Recurse . "$HOME\.copilot\skills\zsexam"
```

Restart or reload the skill host after installation. Invoke it with prompts such as:

- `Use zsexam to generate a bilingual assessment from these training materials.`
- `Generate questions from this training material and export them using the uploaded template.`
- `Audit this question bank for duplicate reasoning paths and ambiguous answers.`

### Required Interaction Flow

Before drafting, the skill confirms:

1. Target role or audience.
2. Relevant experience level.
3. Primary workplace scenarios.
4. Exact question types and counts.

If these values are already explicit, the skill confirms them once rather than repeatedly asking. Free-form user input is authoritative.

### Output and Quality Gates

Each question can include a bilingual stem, options, explanation, and knowledge point, together with the answer, Chinese difficulty, score, cognitive level, tags, role anchor, workplace task, audience fit, scenario relevance, auto-grading suitability, and version.

Release is blocked by ambiguous answers, implausible or nonparallel distractors, untranslated fields, semantic duplicates, off-theme questions, stale blueprint metadata, answer-mapping errors, or template drift.

### Safety and Privacy

Do not commit proprietary courseware, customer documents, generated private exams, credentials, or personally identifiable information. The examples in this repository are synthetic and technology-neutral.

### License

This project is licensed under the MIT License. See [LICENSE](LICENSE).

---

## 中文

这是一个面向岗位与真实工作场景的双语 AI 考试命题 Skill，可将培训资料转化为可复用、经过质量控制的题库与考试交付包。

> 高质量命题不是即时生成文本。正确选项与干扰项的设计需要经过语义推理、答案唯一性证明、双语一致性审核、语义查重和最终交付物验证。复杂任务可能需要一定时间；本 Skill 会按阶段反馈进度，不会以牺牲质量换取速度。

### 功能概览

`alexam-Skill` 引导 Agent 完成以下流程：

1. 完整阅读源材料并拆解知识点。
2. 互动确认真实的目标人群、岗位、经验层级和工作场景。
3. 确认准确的题型与题目数量。
4. 按知识点、认知层级、难度、分值和岗位权限设计蓝图。
5. 生成中英双语的工作场景题目。
6. 设计正确选项与干扰项，并双向证明答案唯一性。
7. 执行语义查重、质量审核和自动修复。
8. 验证 Word、用户模板及 Excel 交付物。
9. 提供考试配置、结果分析和补学建议。

### 核心原则

- **不预设岗位：** TAC、GTAC、支持工程师和其他岗位都只是输入示例，不是默认值。
- **用户场景优先：** 用户确认的岗位和场景优先于材料人物设定及历史试卷。
- **促进学习迁移：** 通过场景把概念和机制连接到真实工作决策。
- **双语语义一致：** 中英文必须保留相同的事实、限定条件、权限边界和因果关系。
- **保障答案完整性：** 每个正确选项必须直接回答任务，每个干扰项都必须能够依据题干证明为错误。
- **交付物级验收：** 生成文件必须在交付前重新打开并独立审核。
- **隐私边界：** 本仓库不包含源文档和为客户生成的考试。

### 仓库结构

```text
.
├── SKILL.md                         # Skill 主执行规则
├── agents/openai.yaml               # Agent 元数据与默认提示
├── references/quality-rules.md      # 详细质量与发布门禁
├── examples/audience-dialog.md      # 互动确认示例
├── examples/blueprint.example.json  # 脱敏的可机读蓝图
├── examples/question.example.json   # 脱敏的结构化题目示例
├── CHANGELOG.md                     # 版本记录
├── CONTRIBUTING.md                  # 贡献指南
└── LICENSE                          # MIT 许可证
```

### 安装

将本仓库复制到 Copilot 用户级 Skills 目录，并保留现有目录结构：

```powershell
Copy-Item -Recurse . "$HOME\.copilot\skills\zsexam"
```

安装后请重启或重新加载 Skill 宿主。可使用以下提示词调用：

- `使用 zsexam 根据这些培训材料生成一套双语考试。`
- `根据这份培训资料出题，并按照上传的模板导出。`
- `审核这个题库是否存在重复推理路径和歧义答案。`

### 必需互动流程

开始命题前，Skill 会确认：

1. 目标岗位或人群。
2. 相关经验层级。
3. 主要工作场景。
4. 准确的题型和题目数量。

如果用户已明确提供这些信息，Skill 只需统一回显确认，不会重复询问。用户自由输入的内容具有最高优先级。

### 输出与质量门禁

每道题可包含双语题干、选项、解析和知识点，以及答案、中文难度、分值、认知层级、标签、岗位锚点、工作任务、受众适配度、场景相关性、自动评分适用性和版本号。

以下问题会阻止发布：答案存在歧义、干扰项不合理或不平行、字段未翻译、语义重复、题目偏离主题、蓝图元数据过期、答案映射错误或模板结构偏移。

### 安全与隐私

请勿提交专有课程资料、客户文档、生成的私有考试、凭据或个人身份信息。本仓库中的示例均为合成内容且不依赖特定技术产品。

### 许可证

本项目采用 MIT License，详见 [LICENSE](LICENSE)。
