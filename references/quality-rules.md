# Quality and Formatting Rules

## Per-question checks

- The stem contains enough constraints to make the answer unique.
- Single-choice has exactly one correct option.
- Multiple-choice states or explains scoring and has no overlapping correct/distractor semantics.
- Distractors are plausible errors from the same domain, not absurd statements.
- True/false tests a meaningful, role-relevant misconception, safety boundary, or core process—not incidental UI location or low-value memorization.
- The scenario is not only technically possible but representative of a frequent, important, or high-risk task for the target role.
- Explanation states why the answer is correct and, when useful, why alternatives fail.
- Chinese and English express the same scenario, constraints, and intent naturally.
- Answer and difficulty comply with platform formats.
- Knowledge point and difficulty match the actual cognitive demand.

## Pre-generation gate

- Confirm the target role or audience, experience level, and primary workplace scenario through `ask_user` before confirming paper structure or drafting any item.
- TAC, GTAC, support engineer, and other roles are examples only. Do not recommend, preselect, or infer them as defaults; the user's confirmed role and scenario are authoritative.
- If all three audience values were already supplied, restate them in one interactive confirmation. If any are missing, ask only for the missing values, one question per dialog.
- Freeze `target_audience`, `target_role`, `experience_level`, `primary_workplace_scenarios`, `frequent_tasks`, `decision_authority`, `out_of_role_actions`, and `scenario_language_style` in the blueprint.
- Confirm question types and exact counts through `ask_user` before drafting any item.
- Before substantial generation begins, explain that correct-option and distractor design, logic review, bilingual parity checks, deduplication, and final artifact validation may take time; provide stage-based status for long runs without weakening quality gates.
- Preserve the confirmed allocation throughout generation and final validation.
- If the final type counts differ from the confirmed allocation, repair the paper before delivery.
- If one instruction requires a type while another forbids it, do not infer intent from the last phrase or silently choose a type. Present concrete, internally consistent allocations through `ask_user` and proceed only after one is confirmed.

## Objective-only conversion checks

- Fill-in to single choice: remove all `【】` markers and fill-in wording; express the same knowledge target as a complete bilingual question; provide exactly one correct option and plausible same-domain distractors; replace answer groups with one uppercase option letter.
- Short answer or case to multiple choice: convert each reference-answer dimension into a distinct correct action where practical; use realistic unsafe shortcuts, missing controls, or ownership failures as distractors; require at least two correct options.
- Rebuild explanations after conversion. They must name the correct option or options, explain the distractors, remain bilingual, and remove obsolete references to blanks, keywords, per-dimension points, or free-text grading.
- Every converted multiple-choice explanation includes the approved scoring rule in Chinese and English: proportional credit for omitted correct choices and zero for any wrong or extra selection, unless the user explicitly specifies another policy.
- Recalculate destination numbering and exact type counts. Do not retain the source type merely because the source document still labels the item as fill-in or short answer.

## Theme-integrity checks

- Treat the exam title and declared learning objective as hard scope boundaries, not decorative metadata.
- Classify each source module as primary-theme, supporting-domain, or out-of-scope before allocating questions.
- A supporting-domain item must name a primary-theme object or workflow, affect a primary-theme decision or outcome, and close its explanation back to the primary theme.
- Reject a supporting-domain item if it could be copied unchanged into a generic networking, storage, operating-system, or security exam.
- Measure supporting-domain allocation against the frozen blueprint. Source length alone does not justify question share.
- For virtualization exams, reject standalone OSI, DNS, TCP, ARP, IP, VLAN, or switch-mode recall unless the question is explicitly tied to a VM, vNIC, virtual switch/bridge, migration, HA recovery, or VM application path.

## Data-integrity and bilingual-field checks

- Store objective options as complete typed objects with stable identity, independent bilingual text, and correctness metadata.
- Option labels are generated only after final ordering. They must not appear inside either language text field.
- Reordering moves whole option objects and recomputes the answer key from stable identities; never manually permute text and answer letters separately.
- Reject `zh` fields that are only `A`-`H`, English-only text, or suspicious one-character fragments.
- Reject `en` fields that are Chinese-dominant, one-character fragments, or combined `中文 / English` strings.
- Reject blank translations, duplicate options, truncated clauses, and repeated fragments such as `把/平`, `仅/凭`, `只/验`, or equivalent corruption patterns.
- Resolve every final answer letter against the final rendered option order and compare it with the structured correct-option identity.
- Require item-specific explanations: name the correct option or options, justify each, and reject each distractor under the stem. A rationale reused across multiple items is a release blocker.
- Knowledge-point translations must be semantically bilingual; equality between Chinese and English fields is a failure when the shared value is not a recognized language-neutral term.

## Assessment intent and learning-transfer gate

Before blueprinting, classify the exam as `learning-oriented`, `certification/selection`, `compliance`, or another explicit purpose.

- A learning-oriented exam uses assessment to reinforce understanding: questions connect taught concepts and mechanisms to frequent, important, or high-risk workplace situations.
- Do not translate a request for "difficult" into an all-expert-forensics paper. For learning-oriented training, recommend mostly `较难` items and reserve `困难` for a small number of high-value mechanism or trade-off questions unless the user explicitly confirms otherwise.
- Record an explicit learning objective and workplace transfer target for every item: what concept or mechanism the learner should understand, and where that understanding is used on the job.
- Reject a question that measures tolerance for dense wording, obscure identifiers, or hidden assumptions rather than mastery of the intended knowledge.

## Audience, role, and authority gate

Before approving a blueprint or item:

- Treat dialog choices as prompts, not defaults. The selected or free-form user response controls the exam.
- Verify that the task is frequent, important, or high-risk for the confirmed role and workplace scenario.
- Match terminology, evidence depth, and reasoning load to the confirmed experience level.
- Keep every correct action within the confirmed role's decision authority; actions owned by another role must be framed as coordination, escalation, evidence collection, or handoff when appropriate.
- Reject specialist-forensics, architecture, management, sales, or operator tasks assigned to the wrong audience merely because the source mentions them.
- Store `role_anchor`, `workplace_task`, `audience_fit`, and `scenario_relevance` for each item when the schema permits.
- If the confirmed role or scenario changes, invalidate the old blueprint and revalidate every question rather than patching role names in stems.

## Scenario-stem and workplace-transfer gate

Unless pure recall is explicitly requested, every substantive objective item must use a meaningful workplace scenario grounded in the confirmed audience context.

- The stem includes: a realistic role or operational object; a work need, symptom, decision, or consequence; only the evidence or constraint needed to reason; and one explicit task.
- The scenario must make the knowledge useful. A learner should be able to say, "This is where the concept appears in my work and why the mechanism matters."
- A decorative wrapper fails: merely adding "a customer asks" or "a TAC engineer sees" to a definition-recall question does not create workplace transfer.
- Prefer common deployment, configuration, migration, HA, capacity, acceptance, recovery, and troubleshooting situations. Rare cases require clear operational importance and source support.
- Preserve one primary learning target per item. If a stem teaches several independent mechanisms, split or rewrite it.

## Reasoning-step and information-budget gate

- A learning-oriented `较难` item normally requires one or two explicit reasoning steps from the supplied evidence to the judgment.
- A learning-oriented `困难` item normally uses one primary difficulty mechanism: evidence reconciliation, causal attribution, responsibility boundary, time-window reasoning, prerequisite discrimination, or constrained trade-off analysis. Do not stack several merely to raise difficulty.
- Flag for rewrite when an item requires more than three independent evidence categories, multiple unrelated clocks, specialist identifiers, or assumptions not stated in the stem.
- Every detail must earn its place by changing the reasoning, excluding an alternative, establishing a boundary, or proving the result. Remove realistic-looking noise that does none of these.
- Difficulty is cognitive demand, not stem length, number of logs, number of acronyms, or volume of constraints.

## Instructional-explanation gate

For learning-oriented items, explanations must close the learning-transfer loop:

1. Identify the workplace phenomenon or task.
2. Point out the decisive evidence in the stem.
3. Explain the underlying concept or mechanism chain.
4. Derive the correct judgment or action.
5. Explain why every alternative does not apply under the same scenario.
6. State the next appropriate check or reusable workplace takeaway when relevant.

Reject explanations that merely restate the answer, enumerate letters without teaching the mechanism, or introduce an unstated condition to defend the answer key.

## Difficulty-feasibility gate

Before drafting, map each requested difficult item to at least one legitimate source-supported reasoning mechanism: conflicting evidence, cross-layer state reconciliation, causal attribution, responsibility or acceptance boundaries, time-window reasoning, prerequisite discrimination, or constrained trade-off analysis.

- Do not classify direct recall, simple timestamp arithmetic, or an answer copied from the stem as `困难`.
- If the source cannot support the requested difficult-item count without repetition or unsupported invention, report the capacity gap and propose a smaller count, broader source set, or lower difficulty mix.
- A scenario wrapper does not create difficulty by itself. Difficulty must come from the decision logic.
- In a learning-oriented item, apply only one primary difficult reasoning mechanism unless the user explicitly requests an expert diagnostic or selection examination. More simultaneous mechanisms usually indicate overload, not better assessment.

## Distractor-strength and answer-cue checks

- Keep options at the same workflow stage, technical layer, decision granularity, grammatical form, and similar information density.
- Use realistic nearby errors: wrong attribution, incomplete evidence, mismatched observation window, adjacent ownership boundary, insufficient prerequisite, or premature but plausible conclusion.
- Flag asymmetric cues such as `只/仅/忽略/不核对/盲目`, `only/simply/ignore/without checking/blindly`, uniquely long or comprehensive correct options, unrelated-layer distractors, and caricatured unsafe actions.
- Cue terms and length ratios are contextual warning signals, not absolute prohibitions. Reject when they allow answer selection without mastering the target knowledge.
- Challenge each item with: “Could a test-wise learner choose the most comprehensive or cautious option without using domain reasoning?” If yes, rewrite the options.

## Bidirectional answer-uniqueness checks

For every item, record both sides of the proof:

- Positive proof: why every keyed option directly completes the stem's task under the stated evidence.
- Negative proof: the exact item-specific reason every unkeyed option cannot also be correct.
- For multiple choice, check that correct options do not overlap semantically, no unkeyed option independently satisfies the task, and the keyed set jointly covers every requested domain or objective.
- A true statement that is irrelevant to the requested decision remains incorrect; a diagnostic action that can locate the requested failure cannot remain unkeyed merely to preserve an answer pattern.

## Regeneration and versioning checks

- Interpret `regenerate`, `rewrite the exam`, `重新出题`, and equivalent wording as a new semantic design unless the user explicitly asks to revise the existing paper.
- Create a new version and preserve previously delivered files.
- Use earlier papers as semantic-deduplication baselines, not as question sources.
- Reject cosmetic rewrites that change names, numbers, role labels, or word order while preserving the same core object, failure or decision layer, evidence type, task type, correct conclusion, and cognitive operation.
- When revision rather than regeneration is requested, document inherited, substantively rewritten, and metadata-only items without classifying intentional inheritance as accidental duplication.

## Whole-paper checks

- Merge duplicated source knowledge before generating variants.
- Cover concepts from different angles: recognition, application, error diagnosis, risk judgment, and case analysis.
- Check stem similarity and semantic duplication, not just identical strings. Compare core object, failure layer, evidence type, task type, correct conclusion, and cognitive operation. If the same reasoning path remains after cosmetic scenario changes, rewrite one item.
- Recalculate question count, points, type count, difficulty count, knowledge coverage, reasoning-step distribution, module allocation, calculation-item list, answer patterns, correct conclusions, semantic signatures, and audience-fit metadata from the final question collection.
- Confirm the generated DOCX layout matches the uploaded template.
- Search final content for forbidden leftovers such as fill-in markers `【】`, `填空题`, duplicate answers, untranslated substantive fields, and generic non-cloud scenarios.

## Scenario and task-alignment checks

- Unless pure recall is explicitly requested, a scenario-bearing stem is mandatory, not optional. It must connect the knowledge point to a realistic workplace task and show why the mechanism matters.
- Use the minimum sufficient scenario: role/object + need or symptom + decisive evidence/constraint + explicit task. Extra details are defects when they do not affect the answer.
- Reject definition questions disguised by a customer/TAC prefix. The scenario must change what the learner has to interpret, decide, verify, or do.
- Every applied item identifies a realistic role or object, a concrete business/operational need, constraint, symptom, or evidence, and one explicit assessment task.
- Classify the task before drafting: product selection, configuration, pre-production validation, troubleshooting, correct process, or expected platform behavior. Do not mix these task types unless the stem explicitly asks for an end-to-end process.
- Every correct option must directly answer that task. A factually true but decision-irrelevant statement must not be scored as correct.
- Keep options parallel in grammar, granularity, and decision level.
- Troubleshooting items require an actual symptom, log, alert, failed check, or observed impact. Validation items state the readiness, acceptance, failure-injection, or go-live objective.
- When separate requirements need separate products, pools, sites, or delivery modes, state that separation in the stem. Do not imply that one product must satisfy incompatible requirements.
- Distinguish platform mechanisms from human operations. Built-in asynchronous execution, dependency orchestration, same-resource conflict ordering, retries, and compensation must be described as platform behavior or observable results, not as manual administrator task choreography.
- Reject artificial scenario wrappers that exist only to force a knowledge point. Prefer normal deployment planning, go-live, acceptance, capacity, migration, or incident work. Rare scenarios require explicit source support and operational significance.
- For Access/Trunk/PVID items, state the named interface, VLAN count, tagging behavior, allowed VLANs, and native/PVID requirement. Give each mode a distinct scenario; never score multiple modes as correct under an underspecified condition.
- Preserve object identity across the full item. If the stem names `management uplink` and `service uplink`, options and explanations use the same names rather than switching to `port 1`, `port 2`, or an undefined category.

## Source-grounding checks

- Maintain a source digest and map every question to at least one source knowledge point.
- Reject generic business concepts that are absent from the training, even if they are broadly correct.
- Use ZStack/cloud details to contextualize the taught communication method, not to invent unsupported product rules.
- Review scenario details for technical plausibility: affected resource, environment, evidence, impact, constraints, safe action, and escalation boundary.
- Compare source examples with verified current product practice. If they conflict, record the conflict, do not restate the obsolete or unsupported example as product fact, and replace only the scenario while preserving the supported knowledge objective.
- Do not infer product behavior from generic industry practice. Product-specific claims such as host boot method, supported storage mode, automatic optimization, or interface workflow require source or verified product support.

## TAC semantic-boundary checks

Run this section only when the user has confirmed TAC, GTAC, technical support, or an equivalent customer-support role or scenario. Do not apply it as a default audience model.

- Match terminology to the business context. Unsupported capabilities belong to requirement clarification and expectation management; outages and degradation belong to incident-impact assessment. Do not turn an unsupported request into a confirmed business blocker without evidence.
- For requirement scenarios, determine whether the request is capability exploration, efficiency improvement, or a go-live prerequisite with no viable alternative. Use parallel, professional categories rather than casual or prematurely severe labels.
- Distinguish acknowledging business importance from confirming incident severity. A customer's phrase such as "major incident" is a claim until verified against impact, scope, duration, and alternatives.
- Distinguish resource response from factual classification. Coordinating additional resources may demonstrate urgency but must not be presented as proof that a major incident is confirmed.
- Distinguish commitments to controllable actions from commitments to uncertain outcomes. TAC may promise escalation, evaluation, follow-up, and update times, but not independently promise a fix, feature, version, or release date without formal confirmation or authorization.
- Prefer qualified authority-boundary wording over overbroad rules: `不得擅自承诺` is normally more accurate than `不得承诺` when authorized communication remains possible.
- Keep customer wording, observed symptom, working hypothesis, verified fact, planned action, and official classification separate. Do not copy an unverified customer label into factual ticket fields.
- Avoid prestige-signaling resource language such as `高级资源` unless the scenario verifies it. Prefer precise actions such as `协调更多资源并行排查` when personnel grade is irrelevant.
- Audit bilingual qualifier parity. Chinese and English must preserve limits and state: `擅自` -> `without formal confirmation or authorization`; `正在协调` -> `are being coordinated`; `已引入` -> `have been engaged`; `仅凭/因此` -> `solely on that basis`.
- Check tense and completion state across languages. Do not translate an in-progress coordination action as a completed engagement.

Use these challenge questions during review:

1. Does the wording assume an impact, severity, authorization, or schedule that the scenario has not established?
2. Does an action intended to reassure the customer accidentally imply a factual classification or guaranteed outcome?
3. Would the statement remain correct if an authorized owner later formally confirmed the classification or schedule?
4. Do Chinese and English impose exactly the same boundary on TAC behavior?

## Determinism and coverage checks

- For RTO, SLA, timeout, sequence, migration, log-correlation, and asynchronous-event questions, require the start event, start time or observation basis, relevant clock/window assumptions, deadline or threshold, and measured result.
- Do not infer a missed deadline from two later timestamps when the contractual start time is absent.
- Extract every domain, stage, or objective named in the stem and verify that the keyed option set covers all of them. If the answer covers only a subset, narrow the stem or redesign the options.
- For competing evidence, distinguish control-plane state, process existence, guest boot completion, guest-agent readiness, network path, and business transaction success; do not collapse these into one proof state.

## Theme counterfactual and overlap checks

- Apply the removal test: delete the named primary-theme objects from the item. If the same task and answer still work unchanged as a generic networking, storage, database, operating-system, or cloud-service question, the theme anchor is superficial.
- Compare each pair of questions using core object, failure layer, evidence type, task type, correct conclusion, and cognitive operation. High agreement indicates semantic duplication even when wording differs.
- Replacement items must be checked against neighboring items so that fixing one duplicate does not create another.

## Answer-pattern security checks

Run only after content and correctness are frozen:

- Inspect single-choice concentration, maximum runs, short periodic sequences, fixed-size permutation blocks, and visually obvious clusters.
- Inspect multiple-choice combination reuse and predictable correct-option-count sequences.
- Reorder complete option objects and recompute answers and explanations from stable identities.
- Balance is a security objective, not a semantic constraint: never flip correctness, delete a valid answer, or add an invalid answer merely to improve distribution.

## Structured scoring-policy checks

- When supported, store multiple-choice scoring as metadata such as `partial_credit_wrong_zero` rather than freehand prose.
- The renderer owns the canonical bilingual scoring sentence and appends it exactly once at the absolute end of each language's explanation.
- Reject duplicated, paraphrased, mid-analysis, or language-mismatched scoring rules.

## Unified pre-release scan

Before independent release review, run one consolidated scan across the full structured bank:

1. Source fidelity and operational representativeness.
2. Primary-theme integrity and the counterfactual removal test.
3. Real difficulty and distractor strength.
4. Bidirectional answer uniqueness and requested-dimension coverage.
5. Semantic overlap across the whole paper.
6. Bilingual qualifier, timing, ownership, and causality parity.
7. Answer-position and correct-count pattern security.
8. Timing/threshold determinism and scoring-policy placement.
9. Structural counts, scores, labels, mappings, and template constraints.
10. Assessment-purpose fit, reasoning-step budget, information budget, and workplace-transfer value.
11. Blueprint/question consistency for learning objectives, difficulty mechanisms, knowledge points, theme anchors, source mappings, and whole-paper matrices.

Do not defer known checks to successive reviewer rounds. Independent review begins only after this scan passes.

## Revision-impact checks

After changing any condition, object, requirement, or task in an item:

- Re-evaluate every option under the revised stem; remove answers that depended on a deleted condition.
- Recompute the answer key instead of retaining it by default.
- Rewrite the explanation so it addresses the revised decision and no longer cites removed facts.
- Recheck Chinese-English equivalence, object naming, knowledge point, difficulty, scoring statement, source mapping, learning objective, difficulty mechanism, workplace-transfer target, theme anchor, assessment-purpose tag, and blueprint metadata.
- Check neighboring questions for new duplication caused by the replacement.
- Treat a user correction about product reality as a product-boundary signal: update the item and, when systematic, the source digest or reusable rules.

## Generator and artifact checks

- Keep question data independent from DOCX rendering code so the same data drives generation and validation.
- Syntax-check the generator before execution; do not patch serialized or truncated scripts repeatedly when a clean rebuild is more reliable.
- A delegated agent's success report is not evidence that a file exists in the current session.
- Check expected paths, non-zero sizes, and reopen every generated DOCX locally.
- Validate rendered paragraph/table counts and required section headings independently of generator log output.
- For Kuxueyuan XLSX files, validate both logical cell values and their OOXML serialization. `openpyxl` commonly writes strings as `inlineStr`; Kuxueyuan may ignore that representation and report a populated answer cell as missing.
- Require `xl/sharedStrings.xml` and Shared String answer cells (`t="s"` plus `<v>` index). Resolve each index and compare it with the expected answer. Reject answer cells serialized as `t="inlineStr"` even when Excel or `openpyxl` displays the correct value.
- Use a Microsoft Excel-resaved workbook as the proven compatibility reference when diagnosing imports. Do not assume two visually identical workbooks are structurally equivalent.
- Fail closed: if any quantitative, semantic, language, theme, answer-mapping, or format assertion fails, do not deliver the artifact until repaired.
- Validate the exact path intended for delivery. Passing an intermediate file, sibling version, or in-memory dataset does not validate the delivered artifact.
- Parse the final DOCX/XLSX independently and require continuous numbering, exact field counts, complete option sets, and no missing questions.
- Compare rendered option text and answer mappings with the approved structured data; renderers must not mutate source data.

## Regression checklist

- Exact confirmed question-type allocation and total question count.
- No unresolved contradiction between required and forbidden question types.
- Total score and continuous numbering.
- No unrequested fill-in questions or fill-in markers.
- Removed-type worksheets retain their template structure but contain zero data rows; no worksheet is deleted or renamed.
- Converted items use destination-type answer syntax and contain no obsolete subjective-scoring language.
- One untranslated, non-duplicated platform answer per item.
- Chinese-only difficulty and bilingual substantive fields.
- For the established Kuxueyuan bilingual workflow, the complete knowledge-point cell is an ASCII/English keyword no longer than 30 characters unless a different verified template limit applies.
- Systematic design changes increment the question/material-adaptation version and produce versioned deliverables rather than silently overwriting an accepted release.
- Template field order and table policy preserved.
- Kuxueyuan XLSX answer cells use Shared Strings, not inline strings; `xl/sharedStrings.xml` is present and all answer indexes resolve correctly.
- Multiple-choice scoring statement present.
- No option text contains an embedded or legacy option label; no one-character or truncated semantic fragments exist.
- Every bilingual field passes language-direction and semantic-equivalence checks; knowledge-point translations are not duplicated Chinese.
- Every rendered answer resolves to the audited correct option identity after final ordering.
- Explanations are item-specific and explain all correct options and all distractors; repeated boilerplate is prohibited.
- Every question passes the primary-theme anchoring test and supporting-domain allocation remains within blueprint limits.
- Answer positions reasonably distributed without compromising correctness; balancing must reorder complete option objects and recompute keys.
- Scenarios pass the frequency/importance/risk test and contain no known unsupported product behavior.
- Configuration questions expose every condition needed to distinguish the correct modes.
- Object names remain stable across stem, options, answer explanation, and both languages.
- Edited items pass the full revision-impact check; no answer or rationale depends on a removed condition.
- True/false items assess meaningful misconceptions or process risks rather than incidental UI memory.
- QC report includes overview, confirmed role, experience level, workplace scenarios, audience authority boundary, objective, structure, coverage, difficulty, configuration, anti-cheating, analysis, remediation, and conclusion.
- The final user-facing delivery message lists the output directory and every complete filename, identifies each file's purpose, and states its acceptance result.

## Subjective scoring

Provide a reference framework, named scoring dimensions, points per dimension, acceptable equivalents, and deduction conditions. Keywords support system pregrading but do not replace a rubric.

## Result analysis

Recommend reporting total score, pass status, knowledge mastery, type performance, difficulty performance, weak-point diagnosis, error attribution, role competency indicators, and targeted relearning actions.
