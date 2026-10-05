---
name: zsexam
description: Professional AI exam authoring and intelligent test assembly for enterprise training, certification, onboarding, compliance, and role competency. Invoke implicitly across any project when users mention zsexam, 出题, 命题, 组卷, 考题, 试题, 题库, 考试题, 双语考试, 题目质检, 查重, 答案解析, Word/PDF/PPT 培训资料出题, 酷学院/Kuxueyuan 模板或 Excel 导入, or ask to generate, revise, audit, deduplicate, bilingualize, format, or export exams. Especially relevant to ZStack, TAC, GTAC, cloud computing, virtualization support, enterprise training, and role competency scenarios.
---

# zsexam

## Purpose

Turn source materials into a reusable, quality-controlled question bank and exam package. Complete the workflow: source understanding -> knowledge decomposition -> question generation -> deduplication and quality control -> exam assembly -> answers and explanations -> configuration -> result-analysis recommendations.

Rule set version: `1.5-role-and-workplace-context-assessment` (2026-10-05).

## Operating Rules

1. Read all supplied materials before drafting. If multiple files belong to one training, merge their knowledge and generate one exam unless the user explicitly requests separate papers.
2. Prefer the user's template and preserve its real layout. A field-oriented Word template without tables must remain a vertical, no-table document; do not introduce tables merely for convenience.
3. For ZStack content, use realistic cloud and virtualization support situations. Include precise resources, components, evidence, impact, constraints, and actions. Avoid vague non-cloud phrases such as "change the engine configuration" or generic "restart the server".
4. Default bilingual scope: stem, options, explanation, knowledge point, subjective scoring guidance, and scenario context. Keep the platform answer field untranslated and non-duplicated. Keep difficulty in Chinese only.
5. Do not generate fill-in-the-blank questions unless explicitly requested. Convert any planned fill-in item into a single-choice question with one unambiguous answer.
6. Prioritize auto-gradable questions, but retain subjective items when they assess application or analysis. Subjective items require reference answers, dimensions, points, and deduction rules.
7. Validate the measurable output: question count, total score, type distribution, difficulty distribution, answer uniqueness, bilingual completeness, template conformance, and absence of duplicate questions.
8. Treat a file as delivered only when it exists in the current session filesystem, is non-empty, can be reopened, and passes an independent content audit. Never rely only on a sub-agent report, console success message, or the generator's own assertions.
9. Keep source facts, exam data, rendering, and validation separate. Draft questions as structured data first, audit that data, then render the approved data into the user's template.
10. Treat contradictory type instructions as a blocking ambiguity. For example, if the user asks to convert short-answer items to multiple choice but also says not to use multiple choice, confirm one exact final allocation through the interactive dialog before editing or exporting.
11. Require task-to-answer alignment. A statement that is factually correct is not automatically a valid correct option; every correct option must directly answer the stem's stated selection, configuration, validation, troubleshooting, process, or expected-platform-behavior task.
12. Require operational representativeness as well as technical correctness. Prefer frequent, important, or high-risk tasks performed by the target role. Do not invent a rare symptom, unsupported boot method, or low-value interface action merely to fit a knowledge point. If a source example conflicts with verified current product behavior, flag the conflict and preserve the knowledge target through a realistic replacement scenario rather than repeating the example as product fact.
13. Enforce theme integrity. A source chapter is not automatically an exam-domain allocation. Every item must assess the named exam theme directly. Supporting domains such as networking, storage, operating systems, or security may appear only when the stem, decision, answer, and explanation are explicitly anchored to the primary theme's objects, workflows, or outcomes. Reject generic cross-domain recall that could be moved unchanged into another course.
14. Use an immutable option schema: `label`, `text.zh`, and `text.en`. Labels are presentation metadata, never content. Reordering options must move complete option objects and then recompute the answer from stable option identities; it must never parse, split, prepend, or retain old labels inside option text.
15. Fail closed on semantic corruption. Reject any item with a one-character fragment, label-only language field, embedded legacy option prefix, bilingual slash-composite stored in one language field, duplicated Chinese in an English field, blank option, or answer that cannot be resolved uniquely to the final rendered options.
16. Explanations must be item-specific. They must identify the correct option or options, explain why each is correct, and explain why every distractor fails under the stem. Reusing a generic rationale across multiple items is prohibited.
17. Validate the final delivered artifact, not a sibling or intermediate file. The exact DOCX/XLSX delivered to the user must independently contain the full approved question set and pass content, language, answer-mapping, theme, layout, and serialization audits.
18. Run a difficulty-feasibility gate before drafting. A difficult item must require evidence reconciliation, causal attribution, responsibility or acceptance boundaries, time-window reasoning, prerequisite discrimination, or trade-off analysis. If the source cannot support the requested number of genuinely difficult items, report the constraint instead of inflating difficulty labels or using caricatured distractors.
19. Build distractors at the same workflow stage, technical layer, decision granularity, and approximate information density as the correct option. Treat asymmetric cue words, conspicuous option length, unrelated layers, and obviously reckless actions as answer-leak risks. These are contextual risk signals, not words or ratios to ban mechanically.
20. Prove answer uniqueness in both directions: show why every keyed option directly answers the task and why every unkeyed option cannot be keyed under the stated evidence. For multiple choice, also verify that correct options do not overlap and that their union covers every dimension requested by the stem.
21. Apply a theme counterfactual test: if primary-theme objects and workflows can be removed while the same reasoning and answer remain valid in a neighboring-domain exam, reject or rewrite the item.
22. Freeze semantics before randomizing answers. After semantic approval, reorder only complete option objects and run whole-paper pattern checks for concentration, runs, short cycles, fixed blocks, repeated combinations, and predictable correct-option counts. Pattern checks must never override semantic correctness.
23. For time-, threshold-, sequence-, RTO-, SLA-, migration-, or asynchronous-event questions, state the start event, relevant timestamps or windows, measurement basis, deadline, and decision threshold needed for a deterministic answer.
24. Store reusable scoring policy as structured metadata when the schema permits. Render the approved bilingual scoring statement exactly once, at the end of each multiple-choice explanation, rather than mixing scoring prose into option analysis.
25. Complete one unified pre-release scan covering content, theme, difficulty, distractor strength, bidirectional answer uniqueness, semantic duplication, bilingual parity, answer-pattern security, timing determinism, requested-dimension coverage, and scoring placement before requesting independent release review.
26. Classify the assessment intent before blueprinting as `learning-oriented`, `certification/selection`, or another explicitly stated purpose. For learning-oriented enterprise training, prioritize concept understanding, mechanism operation, and transferable workplace judgment over expert-forensics difficulty. If the user asks for a "difficult" learning exam, do not assume that every item should be an advanced evidence puzzle; propose a mainly `较难` distribution with a limited number of `困难` items unless the user explicitly requests otherwise.
27. Require a workplace scenario in every substantive objective-question stem unless the user explicitly requests pure recall. The stem must connect the taught knowledge to a realistic role, object, task, symptom, decision, or operational consequence so the learner can understand where and why the concept is used at work. A customer or TAC label pasted onto a definition does not satisfy this rule.
28. Distinguish cognitive difficulty from information complexity. `较难` learning-oriented items should normally require one or two explicit reasoning steps. A `困难` item should normally center on one primary reasoning mechanism or conflict. Do not manufacture difficulty through hidden assumptions, excessive evidence types, long timelines, obscure identifiers, or unrelated constraints.
29. Apply an information budget to scenario stems. Include the minimum sufficient details that affect the answer; normally the role or object, observed symptom or need, relevant evidence or constraint, and one explicit task. Remove details that do not change the correct conclusion. More realism does not mean more noise.
30. Make explanations instructional. For learning-oriented items, close the loop as `workplace phenomenon -> key evidence -> concept or mechanism -> correct judgment -> why each alternative does not apply`. A learner who answered incorrectly should be able to explain the mechanism and the next appropriate check after reading the rationale.
31. Run an overload and semantic-overlap gate. Flag an item that requires more than three independent evidence categories, combines multiple primary learning objectives, or depends on specialist forensics beyond the audience level. Compare questions across core object, failure layer, evidence type, task type, correct conclusion, and cognitive operation; rewrite items whose six-dimensional reasoning path is substantially duplicated.
32. Keep blueprint metadata synchronized with approved questions. After replacing an item, update its learning objective, difficulty mechanism, knowledge point, theme anchor, source mapping, assessment-purpose tag, and any whole-paper matrices. A rendered paper may not be released when its blueprint still describes a superseded item.
33. Confirm the actual target role, experience level, and primary workplace scenario through interactive input before confirming question types and counts. Do not draft questions until both confirmations are complete.
34. Do not use TAC, GTAC, support engineer, or any other role as a default. These roles may appear only as selectable examples or input hints. The user's confirmed role and workplace scenario override every example, prior-session convention, source persona, and domain-specific scenario library.
35. Freeze the confirmed audience context as blueprint constraints: target audience, target role, experience level, primary workplace scenarios, frequent tasks, decision authority, out-of-role actions, and scenario language style. Every item must pass role relevance, authority, and experience-level checks.
36. Treat `regenerate`, `rewrite the exam`, `重新出题`, and equivalent requests as a new semantic design unless the user explicitly requests a revision. Create a new version, use earlier papers only as deduplication baselines, and reject cosmetic rewrites that preserve the same six-dimensional reasoning path.
37. After any content change, recalculate blueprint statistics and semantic metadata from the final question collection rather than retaining hand-entered values. This includes counts, points, difficulty, reasoning steps, module allocation, calculation items, answer patterns, correct conclusions, semantic signatures, and audience-fit fields.
38. In the final delivery message, provide the output directory and every complete filename with its purpose and acceptance status. A generic statement such as `Word and Excel were generated` is not a complete delivery.
39. Before substantial generation begins, tell the user that designing correct and incorrect options requires semantic reasoning, uniqueness proof, bilingual review, deduplication, and artifact validation, so a high-quality run may take time. Use concise stage-based status updates for long runs; never trade correctness for speed or report completion before the final artifacts pass acceptance.

## Default Configuration

Use defaults only when the user does not specify them:

- Target role: no default; must be confirmed interactively
- Experience level: no default; must be confirmed interactively
- Workplace scenario: no default; must be confirmed interactively
- Audience fallback wording, only after the user declines to specialize further: trained employees or ordinary learners
- Questions: 20
- Total: 100 points
- Passing score: 80
- Duration: 30-45 minutes, normally 40
- Types: single choice 40%, multiple choice 30%, true/false 10%, short answer/case 20%
- Difficulty: simple 30%, general 50%, difficult 20%
- Language: Chinese-English bilingual
- Difficulty values: `简单`, `一般`, `较难`, `困难`
- Answers: uppercase option letters; `对` or `错`; subjective keywords/rubric

## Mandatory Audience and Workplace Confirmation

After understanding the source materials and before confirming question types, use interactive dialogs (`ask_user`) to establish who will take the exam and where they use the knowledge. Do not infer a role from the source persona, an earlier exam, the course owner, or examples in this skill.

Run these interactions in order, one question per dialog:

1. **Target role or audience.** Ask: `Who is this exam primarily for? This choice controls terminology depth, workplace situations, distractors, and expected decisions.` Offer short, material-aware examples such as `new employee`, `technical support engineer`, `operations engineer`, `implementation engineer`, `solution architect`, `sales or presales`, `manager`, or `student`. TAC may be shown as one example when relevant, but never mark it as recommended or select it by default. Free-form input must remain available.
2. **Experience level.** Ask how much relevant experience the examinees have. Offer `completed training with little practice`, `basic knowledge and limited practice`, `independently handles common tasks`, and `handles complex diagnosis or design`. Do not recommend a level unless the user already supplied evidence for it.
3. **Primary workplace scenario.** Generate concise choices from the supplied materials, for example `daily operations`, `customer issue handling`, `deployment and delivery`, `pre-production validation`, `incident recovery`, `solution selection`, or `compliance execution`. These are prompts, not defaults. Accept a free-form description and preserve its qualifiers.

If the user has already supplied the role, experience, and workplace scenario explicitly, do not ask the same three discovery questions again. Instead, show one interactive confirmation that restates all three values and permits correction. If only some values are known, ask only for the missing value, one dialog at a time.

Record the approved context as machine-checkable blueprint fields:

- `target_audience`
- `target_role`
- `experience_level`
- `primary_workplace_scenarios`
- `frequent_tasks`
- `decision_authority`
- `out_of_role_actions`
- `scenario_language_style`

Treat the user's actual response as authoritative. Examples in the dialog, TAC standards, source personas, and previous-paper roles are non-binding hints only.

## Mandatory Type and Count Confirmation

After audience/workplace confirmation and before drafting any question, always use the interactive question dialog (`ask_user`) to confirm the question types and the exact count for each type. Do not start question generation until the user confirms both audience context and paper structure.

The dialog must:

- Show the proposed type-count allocation and calculated total, for example: `单选题 8、多选题 6、判断题 2、简答/案例题 4，共 20 题`.
- Derive the proposal from the user's explicit requirements; otherwise use the default distribution and round it into whole questions while preserving the requested total.
- Offer a clear confirmation choice such as `确认以上题型和数量（推荐）`.
- Allow the user to enter an adjusted allocation in the same interaction box. If the user chooses to adjust without providing exact counts, open one follow-up interaction box requesting counts in the format `单选题 N、多选题 N、判断题 N、简答/案例题 N`.
- Recalculate and display the total after adjustment. If counts are missing, negative, non-integer, or inconsistent with an explicitly requested total, request correction through the interaction dialog instead of assuming.
- Exclude fill-in-the-blank by default. Include it in the confirmation only when the user explicitly requests it.

This confirmation is mandatory even when the user already supplied type ratios or counts: present their configuration back to them for final confirmation. A normal chat paragraph does not satisfy this requirement; use the interactive dialog.

## Workflow

### 1. Understand Sources

Extract topic, possible audiences, purpose, core knowledge, competency targets, suitable question types, and recommended difficulty. Consolidate repeated knowledge points. Classify the assessment intent as learning-oriented, certification/selection, compliance, or another explicit purpose; record how that purpose changes scenario style, reasoning depth, and difficulty distribution. Possible audiences extracted from the source are suggestions for the interaction, not assumed defaults.

For DOCX, PPTX, or PDF input, use a format-aware parser. Do not interpret ZIP/OOXML binary output as document text. Preserve a traceable source digest containing modules, key rules, examples, and prohibited extrapolations.

### 2. Confirm Audience and Workplace Context

Run the mandatory audience and workplace interactions above. Record the approved role, experience level, scenarios, frequent tasks, authority boundary, out-of-role actions, and language style. Derive frequent tasks and authority boundaries from the user's answer and source; if a material decision would substantially change the exam, confirm it interactively rather than assuming.

### 3. Confirm Types and Counts

Run the mandatory type-and-count confirmation above and record the approved allocation as an exam blueprint constraint.

### 4. Build Knowledge Map

For each first-level module, list second-level knowledge point, assessment objective, recommended type, difficulty, and high-frequency suitability.

### 5. Design Exam Blueprint

Allocate count and points by knowledge, type, difficulty, and competency level. Ensure total points equal the target before drafting.

Freeze the confirmed blueprint as machine-checkable constraints before writing questions: assessment intent, target audience, target role, experience level, workplace scenarios, frequent tasks, decision authority, out-of-role actions, scenario language style, exact counts, points, permitted types, difficulty distribution, language coverage, template layout, scenario domain, reasoning-step budget, information budget, and forbidden content.

Add a theme-allocation matrix before drafting. For each module, distinguish `primary-theme knowledge`, `supporting knowledge anchored to the primary theme`, and `out of scope`. Set a maximum allocation for supporting-domain items. A supporting-domain question counts as in scope only when its stem names a primary-theme object or workflow, its answer changes a primary-theme decision or outcome, and its explanation closes the reasoning back to the primary theme.

### 6. Generate Questions

Every question includes type, a bilingual workplace-scenario stem, bilingual options where applicable, one platform-formatted answer, Chinese difficulty, bilingual detailed explanation, bilingual knowledge point, and points. Add capability level, labels, applicability, auto-scoring suitability, and version when the template supports them. Store `role_anchor`, `workplace_task`, `audience_fit`, and `scenario_relevance` as structured item metadata when the schema supports extension fields. Unless pure recall was explicitly requested, the stem must establish a realistic role or object, work need or observed symptom, answer-relevant evidence or constraint, and one explicit task that connects the knowledge point to actual work.

Store questions in a plain structured collection before Word generation. Prefer short, explicit string literals and typographic quotation marks inside content; avoid reconstructing executable code from serialized agent output. Question content must be grounded in the source digest. Domain context may make an example realistic, but must not introduce unrelated training concepts.

Represent every objective option as `{id, label, text: {zh, en}, correct}` or an equivalent typed structure. `id` remains stable through reordering; `label` is assigned only after final order is frozen. Never encode labels in `text.zh` or `text.en`, never split a combined `中文 / English` string to reconstruct fields, and never mutate approved question data inside a renderer. Renderers are pure consumers of audited data.

When a platform or template imposes a knowledge-point length limit, validate the entire rendered cell rather than individual fragments. For the established Kuxueyuan bilingual import workflow, use a concise ASCII/English keyword no longer than 30 characters unless the user supplies a different verified constraint.

Use explicit question and material-adaptation versions in structured data when a systematic design rule changes. Produce versioned output filenames instead of silently overwriting an already delivered paper, and keep the source digest aligned with the new version.

When converting an existing paper to objective-only types, preserve the assessed knowledge and scenario rather than mechanically relabeling the item:

- Convert a fill-in item to single choice by rewriting the blank as a complete question, removing every fill marker such as `【】`, creating one semantically complete correct option, and adding plausible same-domain distractors. Do not expose the answer through grammar, option length, or copied wording.
- Convert a short-answer or case item to multiple choice by mapping the reference-answer dimensions to correct action options and converting realistic omissions, unsafe shortcuts, or responsibility-shifting behaviors into distractors. Keep at least two correct options and include the multiple-choice scoring rule in both languages.
- Replace subjective-answer keywords and rubrics with a single platform-formatted option-letter answer. Rewrite the explanation so it identifies the correct options, explains why the distractors fail, and no longer refers to blank scoring, keyword scoring, or free-text grading.
- Renumber each destination type independently and recalculate the final type counts after conversion.

### 7. Quality Control and Repair

Check every item for uniqueness, one correct answer, mutual exclusivity, plausible distractors, clear wording, sufficient explanation, source grounding, difficulty fit, and non-duplication. Automatically repair detected defects before output.

Run three distinct reviews:

- Content review: source traceability, product-currentness, scenario frequency/importance/risk, domain realism, item-specific reasoning, answer uniqueness, distractor quality, stable object naming, and semantic deduplication.
- Theme review: every item must pass the primary-theme anchoring test; supporting-domain allocations must remain within the frozen blueprint, and no generic supporting-domain item may be counted merely because the source mentions it.
- Structural and language review: exact type counts, numbering, score total, answer syntax, field order, table count, template conformance, bilingual field-language correctness, semantic completeness, option-label purity, and final answer-to-option mapping.

Apply automatic hard-fail checks before rendering: reject label-only or one-character option fields; reject option text beginning with `A`-`H` plus a separator; reject `/`-joined bilingual text stored in only one language field; reject empty or whitespace-only translations; reject Chinese-dominant `en` fields or English-only `zh` fields; reject duplicate option meanings; reject duplicated explanations above the configured similarity threshold; and reject any answer key that does not resolve exactly against the final option order. These checks are release blockers, not warnings.

After any user-requested or automatic edit, run an impact review over the entire item. If a stem condition is added, removed, or changed, revalidate every option, the answer key, explanation, knowledge point, difficulty, scoring text, bilingual equivalence, and source mapping. Never patch only the stem when the changed condition affects the decision logic.

Use true/false items for meaningful, role-relevant misconceptions, critical safety boundaries, or core process order. Avoid testing low-frequency tab names, incidental UI locations, or statements whose answer is obvious from loaded wording such as “always,” “never,” or an implausible unsafe action, unless that exact misconception is important and source-supported.

### 8. Deliver and Verify

Produce the requested Word/template output plus an exam design and QC report when appropriate. Reopen generated files and verify their actual content rather than relying on script output alone.

Use this mandatory local acceptance sequence:

1. Compile or syntax-check the generator before execution.
2. Run the generator in the current session, not only in a delegated environment.
3. Confirm every expected output path exists and has non-zero size.
4. Reopen the exact final DOCX with an independent reader and inspect paragraphs and tables; confirm every expected question number and every required field occurs exactly once.
5. Recalculate counts and scores from the rendered document, not only from shared source data, and compare the rendered questions against the approved structured records.
6. Search for forbidden remnants, missing bilingual fields, old option labels inside option text, one-character fragments, duplicated knowledge-point languages, generic repeated explanations, and skipped question numbers.
7. Resolve each rendered answer letter back to its rendered option text and compare that option identity with the audited correct option. Any mismatch blocks delivery.
8. Re-run the theme-allocation audit against rendered stems, answers, and explanations; a structurally valid artifact with off-theme content fails acceptance.
9. For Kuxueyuan XLSX exports, inspect the OOXML package and verify that populated text cells, especially every answer cell, use the Shared String representation (`t="s"` with an index in `xl/sharedStrings.xml`). Do not deliver raw `openpyxl` output that stores answers as inline strings (`t="inlineStr"`), because the Kuxueyuan importer may report those populated cells as missing answers.
10. Deliver only after all checks pass; otherwise repair and rerun.

If sub-agents assist with drafting or review, treat their output as advisory until artifacts are present and validated locally. Do not restore scripts from escaped or truncated tool transcripts when a clean local rebuild is safer.

## Theme Integrity Standard

Use the declared exam title as a release constraint. A question passes only if a reviewer can explain, in one sentence, why answering it demonstrates competence in that title rather than merely in a neighboring discipline.

For a virtualization fundamentals exam:

- Core areas include virtualization value and limits, hypervisor architecture, KVM/QEMU/libvirt responsibilities, VM lifecycle and evidence, virtual resource mapping and contention, migration, HA, snapshots, backups, and virtualization troubleshooting.
- Networking is supporting knowledge. It is valid when anchored to vNICs, virtual switches/bridges, VM VLAN membership, guest reachability, migration networks, HA recovery connectivity, or an end-to-end VM application path.
- Generic OSI recall, standalone DNS/TCP facts, generic ARP routing, and physical-switch mode definitions are out of scope unless the item makes their virtualization decision or diagnostic consequence explicit.
- Storage and operating-system knowledge follow the same rule: they must change a VM lifecycle, performance, availability, migration, recovery, or diagnostic conclusion.

## ZStack Scenario Standard

Use scenarios such as VM live migration, HA, compute-node evacuation, libvirt/QEMU errors, primary-storage latency, backup/snapshot windows, VPC router packet loss, north-south connectivity, image upload, console access, management-server.log, host logs, resource UUIDs, maintenance windows, rollback, capacity, and customer impact.

Every applied question must establish a realistic role or object, a concrete business/operational need, constraint, symptom, or evidence, and one explicit task. Prefer stems such as “which product should be selected,” “which configuration should be applied,” “which evidence proves readiness,” “which checks diagnose this symptom,” “which sequence is correct,” or “which platform behaviors are expected.” Avoid abstract prompts such as “which statements follow the material” or “which boundaries should remain.”

A technically possible scenario is not automatically a good assessment scenario. Prefer common deployment, configuration, capacity-planning, go-live, acceptance, migration, and incident-handling tasks. Use rare events only when they are operationally important and explicitly supported. Do not portray unsupported or atypical behavior—such as a boot method the product does not use or a symptom that is seldom observed—as routine product operation.

Classify each question as selection, configuration, pre-production validation, troubleshooting, correct process, or expected platform behavior before writing options. Do not mix these categories unless the stem explicitly requests an end-to-end process. Troubleshooting requires an observed symptom, failed check, log, alert, or business impact; validation requires a stated readiness, acceptance, failure-injection, or go-live objective.

For network-mode questions, state the conditions that determine the answer: the named host or switch interface, number of VLANs, tagged versus untagged traffic, allowed VLANs, and whether a PVID/native VLAN is required. Do not present Access, Trunk, and Trunk+PVID as interchangeable answers without distinct requirements. Use stable business-facing object names such as `management uplink` and `service uplink` from stem through options and explanation; do not switch from categories to unexplained numeric labels.

Treat built-in asynchronous execution, dependency orchestration, same-resource conflict ordering, retries, and compensation as platform mechanisms. Ask what an administrator should observe or verify; do not incorrectly require the administrator to manually split, order, or compensate internal platform tasks.

If separate requirements need separate products, resource pools, sites, or delivery modes, state that separation explicitly. Every correct option must directly support the stated requirement or decision; a true product fact that does not answer the task is a distractor, not a correct answer.

Every operational scenario should include only the answer-relevant details needed to connect learning with work: the role or object, operational need or symptom, decisive evidence or constraint, and one explicit task. Add environment, resource, version, timestamp, topology, impact, prerequisite, rollback, owner, or ETA only when it changes the reasoning or answer. Do not pile on UUIDs, PIDs, clocks, logs, and unrelated constraints merely to make an item look realistic or difficult.

## TAC Semantic and Authority Boundaries

Apply this section only when the user has confirmed TAC, GTAC, technical support, or an equivalent customer-support role or scenario. It is a conditional role-specific module, never a default audience or scenario.

Write TAC scenarios and options in the correct business context. Do not use incident-impact language for an unsupported feature request unless the scenario establishes an actual service impact. First distinguish capability exploration, efficiency improvement, and a go-live prerequisite with no viable alternative; do not assume that every unsupported request blocks production or go-live.

Separate service responsiveness from factual conclusions and authorized commitments:

- TAC may acknowledge business importance without accepting the customer's incident classification as fact. Severity must follow verified impact, affected scope, duration, and available alternatives.
- Additional resources, parallel investigation, or escalation show responsiveness but do not prove that a major incident has been confirmed. Prefer neutral wording such as "coordinate additional resources" over status-signaling phrases such as "engage senior resources" unless that fact is verified and relevant.
- TAC may commit to actions within its control, such as clarification, escalation, evaluation, and a next-update time. It must not independently commit to product outcomes, fix results, or release timelines that lack formal confirmation or authorization.
- Avoid absolute prohibitions when the real rule is an authority boundary. For example, use "do not commit to a release timeline without formal confirmation or authorization" rather than "never provide a release timeline."
- Keep observation, customer claim, working hypothesis, verified fact, response action, and final classification distinct in stems, options, ticket fields, and explanations.

Chinese and English must preserve the same qualifiers, authority limits, causality, and action status. Terms such as `擅自`, `正在协调`, `已引入`, `仅凭`, and `未经正式确认或授权` must not disappear in translation. Prefer natural role-appropriate English over literal wording, for example `additional resources are being coordinated` and `without formal confirmation or authorization`.

## Kuxueyuan Vertical Word Format

For each item use this order:

`N. 题型` -> `题目` -> `A/B/C...` -> `正确答案` -> `题目难度` -> optional `作答上传图片` -> `答案解析` -> `知识点` -> `建议分值`.

- Answer is a single machine-readable value, never `B / B` or translated duplicates.
- Multiple-choice answers concatenate uppercase letters, e.g. `ABCD`.
- Multiple-choice explanations include scoring: proportional credit for omitted correct choices; zero for wrong or extra choices, unless the user specifies another policy.
- Do not display tables in the vertical version.

## Kuxueyuan XLSX Compatibility

- Preserve the uploaded workbook's sheet names, order, instructions, headers, merged ranges, option columns, validation rules, and unused-sheet headers.
- When a confirmed allocation removes a question type, clear only that sheet's data rows. Keep the sheet itself, its original position, instructions, headers, merged ranges, formatting, and validation rules; do not delete or rename it.
- After type conversion, verify both positive and negative constraints: destination sheets contain the exact confirmed counts, removed-type sheets contain zero data rows, and converted stems contain no obsolete markers or type wording such as `【】`, `填空题`, or free-text instructions.
- A cell value visible through `openpyxl` is not sufficient evidence of import compatibility. The Kuxueyuan importer may ignore OOXML inline strings even when Excel displays them correctly.
- Store populated strings through the workbook Shared String Table: `xl/sharedStrings.xml` must exist, and answer cells must be serialized as `<c ... t="s"><v>INDEX</v></c>` rather than `<c ... t="inlineStr"><is><t>ANSWER</t></is></c>`.
- Treat a Microsoft Excel open-and-save round trip as the known compatibility reference because it converts inline strings to shared strings. For automated delivery, reproduce and verify that representation instead of requiring the user to copy or resave manually.
- Audit every populated answer cell at the OOXML level after final save. Confirm the shared-string index resolves exactly to the intended single-choice, multiple-choice, or true/false answer.
- If the export library cannot produce Shared String cells reliably, stop and use a compatible writer or a controlled post-processing step; do not deliver an XLSX that only passes high-level cell-value checks.

## Output Package

When no custom template is supplied, structure the response or report as: exam overview, knowledge map, paper structure, formal questions, answers and explanations, import fields, configuration, anti-cheating/randomization, result analysis, and remediation recommendations.

Read `references/quality-rules.md` when performing detailed QC, template conversion, or ZStack scenario review.
