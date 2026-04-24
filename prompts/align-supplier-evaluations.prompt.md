---
name: "Align Supplier Evaluations"
description: "Normalize and compare independently generated supplier evaluation reports on common ground, then produce a cross-supplier comparative assessment."
argument-hint: "Report paths or supplier names to compare, plus optional comparison focus"
---

# Align Supplier Evaluations

Compare supplier evaluation reports that were generated independently and align them onto a common scoring and evidence frame.

Treat the user input as:
- one or more supplier names, report filenames, or report paths under `reports/`
- optional focus areas, such as AI-native SDLC, compliance depth, speed-to-value, enterprise readiness, or proof quality

If no reports are specified, discover the latest supplier evaluation reports under `reports/` and use those.

## Primary Goal

Produce a second-pass comparative analysis that:
- normalizes independently written supplier evaluations to a common frame
- compares sub-dimension scores to identify where differentiation is real versus where scoring drifted
- compares pattern taxonomy profiles to surface genuine architectural differences
- identifies where scoring confidence differs because evidence posture differs
- compares accelerator adaptation quality against `project-proof-root` and `implementation-proof-root` depth using the shared proof-weight vocabulary from the evaluation prompt
- inventories and compares the same mandatory Harness Engineering dimensions across suppliers
- compares agentic development system engineering maturity as a cross-cutting lens
- compares suppliers fairly despite different stacks, repo shapes, levels of accelerator reuse, and proof availability
- produces a comparative ranking or grouping only after adjusting for evidence quality and comparability limits

Do not re-run full repository evaluation unless a report is missing critical metadata or the report itself appears insufficient for alignment. Prefer comparing reports first.

## Pattern Taxonomy Reference

**Read [`.github/prompts/evaluation-taxonomy.md`](evaluation-taxonomy.md) for the full tag definitions** used in Pattern Profile sections of supplier reports. Use that file to interpret pattern tags consistently when comparing suppliers.

## Common Alignment Frame

Use these common dimensions across all supplier reports:

1. AI-native SDLC quality and operational depth (including sub-dimension score comparison)
2. Compliance, regulation, and governance operationalization (including sub-dimension score comparison)
3. Delivered project credibility and architectural coherence (including sub-dimension score comparison)
4. Documented intent versus proven execution
5. Deterministic guardrails (separated from LLM-eval guardrails)
6. LLM-eval guardrails (separated from deterministic guardrails)
7. Agentic operating loop / orchestration approach
8. Evaluation and verification approach
9. Human gates and policy boundaries
10. Agentic development system engineering (extensibility, coding agent leverage, compounding, team scalability, adaptability, drift resistance)
11. Estimated harness effectiveness
12. Evidence quality
13. Delivery speed and leverage within the 3-week showcase constraint
14. Accelerator or prior-asset reuse, and the quality of adaptation
15. Enterprise applicability and maintainability
16. Evidence source quality and freshness for collaboration, delivery-process proof, and harness assessment confidence
17. Pattern taxonomy profile comparison (agent architecture, workflow model, orchestration style, feedback loops, guardrails, extensibility)

## Shared Proof-Weight Frame

Reuse the same proof-weight vocabulary as the evaluation prompt when aligning reports:
- `accelerator-root`: reusable framework, template, starter, skeleton, bootstrap, or factory asset. Default proof-weight: `reuse-capability`.
- `project-proof-root`: the strongest current-submission design, scope, decision, or problem-framing artifacts. Default proof-weight: `primary`.
- `implementation-proof-root`: instantiated source, tests, infra, generated outputs, or other concrete execution artifacts. Default proof-weight: `implementation`.
- `supporting-process-root`: workflow state, logs, exported collaboration data, SDLC metadata, or other supporting evidence that informs confidence but should not outrank direct project proof. Default proof-weight: `supporting`.

Also keep accelerator instantiation strength aligned with the evaluation prompt: `template-only`, `lightly-instantiated`, or `meaningfully-adapted`.

When suppliers are close, meaningful OSS MIT accelerator adaptation can count as a positive transferable capability signal, but only when the accelerator-root is `meaningfully-adapted` and the report also shows credible `project-proof-root` or `implementation-proof-root` evidence. Do not let `template-only` or `lightly-instantiated` accelerator roots outrank stronger current-project proof.

## Alignment Rules

1. Use the per-supplier report as the primary source.
2. Compare like with like. Do not reward breadth alone when another supplier shows stronger operational depth in a narrower scope.
3. Treat score differences carefully when one report is grounded mainly in `primary` and `implementation` proof while another leans more on `supporting` or `reuse-capability` evidence.
4. Separate these cases explicitly:
   - weaker solution
   - stronger solution with weaker local proof
   - template/platform-heavy submission with limited project-specific instantiation
   - high accelerator reuse with strong adaptation quality
   - high accelerator reuse with weak evidence of meaningful customization
5. In close comparisons, meaningful OSS MIT accelerator adaptation may favor the supplier that turned reusable assets into stronger current-project leverage, but only if that reuse is corroborated by instantiated project proof rather than template breadth alone.
6. If reports are missing normalization fields, key evidence notes, or explicit harness-section details, fill small gaps by reading the report body. Only go back to the repository if the report cannot be aligned reliably.
7. When comparing reports, account for whether each one used delivery-exported collaboration data, live GitHub evidence, local git only, or no collaboration metadata at all.
8. Keep `Deterministic guardrails` separate from `LLM-eval guardrails` and both separate from `Evaluation and verification approach` even if a supplier report blends them together. Normalize all fields explicitly.
9. Compare sub-dimension scores across suppliers to identify where apparent category-score parity hides genuine sub-dimension divergence. Two suppliers with SDLC score 82 might score very differently on guardrails vs. learning loops — surface this.
10. Compare pattern taxonomy profiles to identify architectural differences that scores alone cannot capture. A supplier tagged `orchestrated-coding-multi-agent` + `plan-execute` + `skill-based` has a fundamentally different approach from one tagged `coding-agent` + `ad-hoc` + `hardcoded`, even if both score similarly on category totals.
11. Compare evidence inventories and proof posture together so artifact counts, evidence channel usage, and confidence-reducing factors are interpreted alongside the share of `primary`, `implementation`, `supporting`, and `reuse-capability` evidence.

## Required Analysis Steps

### 1. Report Inventory

List the reports being compared and extract the normalization metadata from each:
- supplier
- evaluation confidence
- repo shape
- primary stacks
- AI operating model
- AI role classification
- dominant evidence posture
- accelerator or prior-asset reuse
- reuse adaptation quality
- speed-to-value assessment
- GitHub evidence source
- evidence freshness
- external-proof dependency

Extract the evidence inventory from each report:
- distinct operational proof artifacts count
- populated vs empty/templated artifact ratio
- claims with verifiable evidence ratio
- evidence channels available vs used
- confidence-reducing factors checked

Extract the proof posture from each report:
- strongest `project-proof-root` evidence
- strongest `implementation-proof-root` evidence
- strongest `supporting-process-root` evidence
- strongest `accelerator-root` evidence and its instantiation strength
- dominant proof-weight mix across `primary`, `implementation`, `supporting`, and `reuse-capability`
- whether accelerator reuse was converted into current-project proof or remained mostly transferable capability

Extract the pattern taxonomy profile from each report:
- agent architecture tags
- workflow model tags
- orchestration style tags
- feedback loop tags
- deterministic guardrail tags
- LLM-eval guardrail tags
- agent extensibility tags
- determinism level tags
- compliance integration tags
- AI role tag

Then extract the mandatory harness fields from each supplier report using the same labels as the evaluation prompt:
- `Deterministic guardrails`
- `LLM-eval guardrails`
- `Agentic operating loop / orchestration approach`
- `Evaluation and verification approach`
- `Human gates and policy boundaries`
- `Agentic development system engineering`
- `Estimated harness effectiveness`
- `Evidence quality`

If a report does not expose these fields cleanly, reconstruct them from the report body and note the confidence penalty in the comparison.

### 1b. Sub-Dimension Score Extraction

Extract sub-dimension scores for each category from each report and compile into comparison tables:

**SDLC sub-dimensions** (0–10 each): Planning and decomposition, Implementation and coding, Review and quality, Testing and verification, Orchestration and workflow, Learning and compounding, Guardrails and determinism, Agentic system engineering.

**Compliance sub-dimensions** (0–10 each): Regulatory grounding, Traceability, Automated compliance, Controls and enforcement, Human oversight, Responsible AI.

**Project sub-dimensions** (0–10 each): Problem framing, Architectural coherence, Delivery credibility, Enterprise suitability.

Identify sub-dimensions where suppliers diverge most (>3 point spread) and where they cluster (≤1 point spread). High divergence on the same sub-dimension is a strong signal of genuine differentiation. Clustering signals potential scoring calibration issues or genuine similarity — determine which.

### 2. Score Normalization

For each supplier:
- restate the original weighted scores and sub-dimension scores
- assess whether any category score appears inflated or depressed due to evidence posture rather than actual capability
- assess whether the supplier's comparative case rests mainly on `primary` and `implementation` proof or on `supporting` and `reuse-capability` evidence
- check whether sub-dimension scores are internally consistent with the category score (mean of sub-dimensions × 10 should approximately equal the category score; flag discrepancies)
- check whether pattern taxonomy tags are consistent with sub-dimension scores (e.g., a supplier tagged `no-agent` + `ad-hoc` should not score 8+ on orchestration)
- note whether weak or blended harness evidence makes the original score harder to compare on common ground
- compare evidence inventories: if one supplier has 15 operational proof artifacts and another has 4, assess whether score differences reflect this disparity appropriately, and whether those artifacts are mostly `primary` or `implementation` proof versus `supporting` or `reuse-capability`
- if needed, add a comparison note explaining how the score should be interpreted in the cross-supplier view

Do not silently rewrite the original score. If you introduce a normalized comparison view, keep the original score and explain the adjustment logic.
Do not convert Harness Engineering or Agentic System Engineering into a fourth weighted score or a standalone normalized numeric rating.

### 3. Cross-Supplier Comparison

Compare suppliers on:
- strongest evidence-backed AI-native SDLC
- strongest evidence-backed compliance operationalization
- strongest delivered-project credibility relative to time and leverage
- strongest proof posture, meaning the best balance of `project-proof-root` and `implementation-proof-root` depth relative to `supporting-process-root` and `accelerator-root` reliance
- strongest deterministic guardrails (hooks, CI gates, policy-as-code, boundary enforcement)
- strongest LLM-eval guardrails (critical assessment, judge patterns, multi-POV review)
- strongest agentic operating loop / orchestration approach
- strongest evaluation and verification approach
- clearest human gates and policy boundaries
- strongest agentic development system engineering (extensibility, coding agent leverage, compounding, team scalability, adaptability, drift resistance)
- most credible estimated harness effectiveness
- strongest evidence quality for harness claims
- best speed-to-meaningful-capability under the 3-week constraint
- strongest enterprise pattern applicability and maintainability
- strongest meaningful accelerator adaptation without over-relying on reusable roots as current-project proof

Additionally, compare pattern taxonomy profiles to identify fundamentally different architectural approaches:
- which suppliers leverage coding agent extensibility most effectively?
- which suppliers have the most mature feedback loops (including adversarial eval)?
- which suppliers combine deterministic and LLM-eval guardrails most effectively?
- which suppliers' agentic systems are best positioned to compound, adapt, and scale?

### 4. Fairness Checks

Explicitly check for comparison distortions caused by:
- different repo counts or platform-plus-template structures
- variable dependence on external systems not mirrored in repo
- different levels of pre-existing accelerator reuse
- proof-posture imbalance, such as one supplier relying mostly on `reuse-capability` and `supporting` evidence while another shows deeper `primary` and `implementation` proof
- evidence-rich documentation versus evidence-rich automation
- independently authored reports using slightly different emphases
- reports that blend deterministic guardrails, LLM-eval guardrails, evaluation, and human gates instead of separating the canonical harness dimensions
- differences in collaboration-evidence source, such as delivery snapshot versus live GitHub query versus local-only checkout
- evidence inventory asymmetry: significantly different counts of operational proof artifacts across suppliers
- AI role classification mismatch: scoring product AI as SDLC capability, or vice versa
- sub-dimension score drift: two suppliers scoring identically on the category level but with very different sub-dimension profiles
- pattern taxonomy differences that category scores fail to differentiate (e.g., `orchestrated-coding-multi-agent` + `learning-loop` scored same as `coding-agent` + `none-visible`)

### 5. Comparative Verdict

Provide:
- a ranked view or tiered grouping if the evidence supports it
- the reasons for the ordering or grouping
- any unresolved comparability limits
- what additional evidence would most reduce uncertainty

If suppliers are otherwise close, explain explicitly whether meaningful OSS MIT accelerator adaptation changes the ordering. Use it as a positive transferable factor only when the reusable asset was `meaningfully-adapted` and did not substitute for missing project-specific proof.

## Output Requirements

**Read the report template from [`.github/prompts/comparison-report-template.md`](comparison-report-template.md) and follow it exactly when writing the report.** That file defines file naming, structure, all sections, tables, and required fields.

Write the comparison report to the workspace-level `reports/` folder. Create a fresh dated report on every run and refresh the `LATEST` file.

## Final Constraints

- Compare reports on common ground, not on repository aesthetics or stack preference.
- Keep original supplier scores visible even if you add normalized interpretation.
- Normalize harness findings with the same canonical dimension set for every supplier. Do not introduce supplier-specific harness categories.
- Normalize proof posture with the same `accelerator-root`, `project-proof-root`, `implementation-proof-root`, `supporting-process-root`, and `proof-weight` vocabulary used in the evaluation prompt.
- Use sub-dimension score comparisons to surface genuine differentiation hidden by category-level score proximity.
- Use pattern taxonomy comparisons to surface architectural differences that scores alone cannot capture.
- Compare evidence inventories quantitatively when assessing score confidence.
- Credit meaningful accelerator adaptation positively when evidenced, but do not let reusable roots outweigh stronger current-project `primary` or `implementation` proof.
- Be explicit when uncertainty comes from missing proof rather than missing capability.
- Be explicit when one report had stronger access to exported or live GitHub collaboration evidence than another.
- Do not manufacture precision where the evidence is weak.
- Treat agentic system engineering as a comparison dimension but not as a fourth weighted score.