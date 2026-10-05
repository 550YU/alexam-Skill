# alexam-SKII

A role-aware, bilingual AI exam-authoring skill for turning training materials into reusable, quality-controlled question banks and exam packages.

> High-quality authoring is not instant text generation. Correct answers and distractors require semantic reasoning, uniqueness proof, bilingual parity review, deduplication, and final artifact validation. Complex runs may take time; the skill reports progress by stage and does not trade correctness for speed.

## What it does

`alexam-SKII` guides an agent through:

1. Complete source reading and knowledge decomposition.
2. Interactive confirmation of the real audience, role, experience level, and workplace context.
3. Exact question-type and count confirmation.
4. Blueprinting by knowledge point, cognitive level, difficulty, score, and role authority.
5. Bilingual workplace-scenario question generation.
6. Correct-option and distractor design with bidirectional answer-uniqueness proof.
7. Semantic deduplication, quality review, and automatic repair.
8. Word/template and Kuxueyuan-compatible Excel delivery validation.
9. Exam configuration, result analysis, and relearning recommendations.

## Key principles

- **No assumed role:** TAC, GTAC, support engineer, and all other roles are input examples—not defaults.
- **User context wins:** the user's confirmed role and scenario override source personas and earlier exams.
- **Learning transfer:** scenarios connect concepts and mechanisms to realistic workplace decisions.
- **Bilingual parity:** Chinese and English preserve the same facts, qualifiers, authority limits, and causality.
- **Answer integrity:** every keyed choice must answer the task; every distractor must be provably incorrect under the stem.
- **Artifact-level acceptance:** generated files are reopened and audited before delivery.
- **Privacy boundary:** source documents and generated customer exams are not included in this repository.

## Repository layout

```text
.
├── SKILL.md                         # Main skill instructions
├── agents/openai.yaml               # Agent metadata and default prompt
├── references/quality-rules.md      # Detailed quality and release gates
├── examples/audience-dialog.md      # Interactive confirmation examples
├── examples/blueprint.example.json  # Sanitized machine-checkable blueprint
├── examples/question.example.json   # Sanitized structured question example
├── CHANGELOG.md
├── CONTRIBUTING.md
└── LICENSE
```

## Installation

Copy this repository into your Copilot user skills directory and retain the folder structure:

```powershell
Copy-Item -Recurse . "$HOME\.copilot\skills\zsexam"
```

Restart or reload the skill host after installation. Invoke it with prompts such as:

- `Use zsexam to generate a bilingual assessment from these training materials.`
- `根据这份培训资料出题，并导出酷学院模板。`
- `Audit this question bank for duplicate reasoning paths and ambiguous answers.`

## Required interaction flow

Before drafting, the skill confirms:

1. Target role or audience.
2. Relevant experience level.
3. Primary workplace scenarios.
4. Exact question types and counts.

If values are already explicit, it confirms them once rather than repeatedly asking. Free-form user input is authoritative.

## Output and quality gates

Each question can include bilingual stem/options/explanation/knowledge point, answer, Chinese difficulty, score, cognitive level, tags, role anchor, workplace task, audience fit, scenario relevance, auto-grading suitability, and version.

Release is blocked by ambiguous answers, implausible or nonparallel distractors, untranslated fields, semantic duplicates, off-theme questions, stale blueprint metadata, answer-mapping errors, template drift, or invalid Kuxueyuan Shared String serialization.

## Kuxueyuan compatibility

The skill preserves the uploaded workbook structure and verifies that populated answer cells use OOXML Shared Strings (`t="s"`) rather than inline strings. A visually correct workbook that fails importer-level serialization checks is not accepted.

## Safety and privacy

Do not commit proprietary courseware, customer documents, generated private exams, credentials, or personally identifiable information. The examples here are synthetic and technology-neutral.

## License

MIT License. See [LICENSE](LICENSE).
