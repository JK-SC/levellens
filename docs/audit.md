# Final-model error audit

中文版：[audit.zh-CN.md](audit.zh-CN.md)

**Owner and human reviewer:** Wenyue. **Completed on 15 November 2026:** Wenyue confirmed reading all 15 full cases and accepted every judgement and reason below. The final counts are **7 model error, 0 label noise and 8 unclear**. All cases have a recorded reviewer and date. These counts describe this selected set only.

## Frozen cases and provenance

The public [case list](../results/audit/worst_errors.csv) now contains five full-test errors per dataset from the three runs below, replacing the earlier ten BiLSTM cases. The runs match the best development-set quadratic weighted kappa (QWK) among the saved runs. No test result was used to select a model or tune it.

Cases are ordered by descending absolute ordinal error, then descending confidence in the predicted level rounded to four decimals, then item ID, matching `levellens/explain/errors.py`. All 15 IDs, source labels, predictions, probabilities, confidence values and top-five positions were reproduced. The local test splits match the frozen manifest: RACE++ 5,642 items, ARC 3,530 and MATH 5,000. The supplied full texts match those splits and remain private.

| Dataset | Frozen run ID | Prediction-file SHA-256 |
|---|---|---|
| RACE++ | `race-deberta-v3-corn-s0` | `552a88e051d822dd820cf28c0c09fd5199aef3d15b49bed3610b65a8bc9c9e52` |
| ARC | `arc-distilbert-corn-optuna-s0` | `73ff2c5693892798be0e0e71545bb4115b7ba9c1d970c5a76b63ec9ac3b53072` |
| MATH | `math-deberta-v3-corn-s0` | `210c8c5fa73cceb0392a31e349296515ac06c1aa1f40eeae418d15c6d9f087e6` |

## Decision rules

| Category | Evidence needed |
|---|---|
| model error | The source label is plausible for its source exam or level, the model misses it, and no concrete data defect explains the case; record the reasoning demand or relevant cue. |
| label noise | A concrete source-label inconsistency, source metadata error or corrupted item supports a label concern; apparent ease alone is insufficient, and original test labels are retained. |
| unclear | The source level cannot be adjudicated reliably, necessary context is unavailable, or plausible explanations conflict; record the missing evidence. |

These categories are operational judgements, not causal proof. Labels are **target levels**, not difficulty calibrated from student responses. Omitted context and markup are secondary flags, not automatic evidence of label noise. In particular, the short solutions of MATH-2 and MATH-4 motivate uncertainty but do not establish an incorrect source rating.

Wenyue is the actual human reviewer for all 15 cases and confirmed the full-case reading, judgements and reasons on 15 November 2026. No second-member review is claimed. An unclear judgement is a completed review outcome, not an unread case.

## Fifteen-case worksheet

All 15 categories and reasons below were accepted by Wenyue after reading the full cases. Secondary flags follow the table.

| Slot | Dataset | Item ID | Run ID | True / predicted level | Category | Reason / evidence | Human reviewer / date |
|---|---|---|---|---|---|---|---|
| RACE-1 | RACE++ | `race-test-college696-q1` | `race-deberta-v3-corn-s0` | college / middle school | unclear | The question retrieves a weather event from an omitted passage, so its short wording cannot settle the college source level or explain the middle-school prediction. | Wenyue / 2026-11-15 |
| RACE-2 | RACE++ | `race-test-college696-q0` | `race-deberta-v3-corn-s0` | college / middle school | unclear | The reason for a habitual conversation topic comes from an omitted passage, and simple wording alone does not establish that the college source label is wrong. | Wenyue / 2026-11-15 |
| RACE-3 | RACE++ | `race-test-college696-q3` | `race-deberta-v3-corn-s0` | college / middle school | unclear | The everyday precaution is interpreted through an omitted passage, leaving insufficient evidence to separate missing context from a questionable college source level. | Wenyue / 2026-11-15 |
| RACE-4 | RACE++ | `race-test-middle3379-q0` | `race-deberta-v3-corn-s0` | middle school / college | unclear | The question asks for a passage-specific explanation of a metaphor, but the model receives no passage and the supplied metadata alone cannot explain its college prediction. | Wenyue / 2026-11-15 |
| RACE-5 | RACE++ | `race-test-college696-q2` | `race-deberta-v3-corn-s0` | college / middle school | unclear | A phrase is interpreted within an omitted passage, while its familiar vocabulary is insufficient evidence for changing the recorded college source level. | Wenyue / 2026-11-15 |
| ARC-1 | ARC | `TIMSS_1995_8_N2` | `arc-distilbert-corn-optuna-s0` | grade 8 / grade 3 | model error | The complete item compares nutrient coverage across meals and the raw TIMSS record specifies grade 8, with no observed data defect supporting the grade-3 prediction. | Wenyue / 2026-11-15 |
| ARC-2 | ARC | `Mercury_SC_LBS10946` | `arc-distilbert-corn-optuna-s0` | grade 4 / grade 9 | model error | The raw ARC item records grade 4 and presents a complete single-rule inheritance question, so technical vocabulary alone does not justify predicting a grade-9 source. | Wenyue / 2026-11-15 |
| ARC-3 | ARC | `NCEOGA_2013_8_36` | `arc-distilbert-corn-optuna-s0` | grade 8 / grade 3 | model error | The original North Carolina assessment record specifies grade 8 and the energy-source question is complete, so elementary content alone does not invalidate its source grade. | Wenyue / 2026-11-15 |
| ARC-4 | ARC | `MCAS_2004_9_6-v1` | `arc-distilbert-corn-optuna-s0` | grade 9 / grade 4 | model error | The complete MCAS item requires identifying a wave example and its raw record specifies grade 9, with no observed source-label conflict to support grade 4. | Wenyue / 2026-11-15 |
| ARC-5 | ARC | `WASL_2005_8_12` | `arc-distilbert-corn-optuna-s0` | grade 8 / grade 3 | model error | The complete WASL item requires choosing a relevant before-and-after observation and its raw grade-8 record provides no evidence for the grade-3 prediction. | Wenyue / 2026-11-15 |
| MATH-1 | MATH | `math-test-prealgebra-0581` | `math-deberta-v3-corn-s0` | Level 5 / Level 1 | unclear | The table is supplied only as Asymptote drawing code, so the Level-5 versus Level-1 disagreement cannot be separated reliably from the input representation. | Wenyue / 2026-11-15 |
| MATH-2 | MATH | `math-test-prealgebra-0784` | `math-deberta-v3-corn-s0` | Level 5 / Level 1 | unclear | The supplied solution uses a short product-rule count, but no item-specific rating rationale establishes whether the recorded Level 5 or the predicted Level 1 is the more defensible target. | Wenyue / 2026-11-15 |
| MATH-3 | MATH | `math-test-number_theory-0044` | `math-deberta-v3-corn-s0` | Level 5 / Level 1 | model error | Coordinating leap years, interval endpoints and weekday arithmetic makes the source target plausible, while the Level-1 prediction misses this multistep demand and no concrete data defect was found. | Wenyue / 2026-11-15 |
| MATH-4 | MATH | `math-test-algebra-1029` | `math-deberta-v3-corn-s0` | Level 5 / Level 1 | unclear | The supplied solution is a short symbolic rate substitution, but the absent item-specific rating rationale prevents adjudicating the Level-5 versus Level-1 disagreement. | Wenyue / 2026-11-15 |
| MATH-5 | MATH | `math-test-number_theory-0134` | `math-deberta-v3-corn-s0` | Level 5 / Level 1 | model error | The complete problem requires combining powers and reducing residues modulo a prime, making Level 5 plausible and the Level-1 prediction an unsupported underestimate. | Wenyue / 2026-11-15 |

**Secondary flags and scope.** All five RACE++ cases omit the passage from model input. RACE-1, RACE-2, RACE-3 and RACE-5 share passage `college696`; the five selected questions represent only two passages. RACE-4 also contains a source spacing artefact. MATH-1 embeds an unrendered table as Asymptote code. MATH-2 and MATH-4 lack an item-specific rating rationale. No selected case has an identical model input elsewhere in the primary train, dev and test splits. These checks do not exclude near duplicates or prove that the source labels are correct.

## Confirmed counts

| Dataset | Model error | Label noise | Unclear | Cases |
|---|---|---|---|---|
| RACE++ | 0 | 0 | 5 | 5 |
| ARC | 5 | 0 | 0 | 5 |
| MATH | 2 | 0 | 3 | 5 |
| Total | 7 | 0 | 8 | 15 |

Human-confirmed cases: **15 of 15**. Cases awaiting human confirmation: **0**. The zero is for supported label-noise judgements in this classification, not proof that all labels are clean. This severity-selected set cannot estimate population error or label-noise rates.

## Three slide examples

Use these confirmed-case paraphrases in the slides. Do not publish question text, passages or solutions. Keep the item ID and run ID in speaker notes.

| Slot | Source target / prediction | Decision | Slide wording |
|---|---|---|---|
| RACE-1 | college / middle school | unclear | Passage-dependent item with its passage omitted; source stage cannot be settled from the short input. |
| ARC-3 | grade 8 / grade 3 | model error | A basic science fact can still come from a grade-8 exam; target grade and perceived ease differ. |
| MATH-5 | Level 5 / Level 1 | model error | The model underestimates a multistep modular-arithmetic problem. |

Caption: Five worst full-test errors per frozen model, selected by ordinal gap and confidence; human review by Wenyue, 15 November 2026. Counts describe these 15 selected questions only.

## Completion check

- [x] All 15 cases match frozen test data and the supplied prediction hashes.
- [x] Top-five selection is reproduced for all three frozen runs.
- [x] Fifteen confirmed judgements and reasons, category counts and three examples are recorded in both languages.
- [x] Wenyue has read and confirmed each case; the actual reviewer and date are recorded.
- [x] Final counts total 15, with no cases awaiting human confirmation.

## Presentation handoff

B3 is complete. Slides 6–9 and the part-2 narration must use these confirmed counts and examples. The actual deck update and recording are separate deliverables and remain pending receipt of the deck and Wenyue's recording.
