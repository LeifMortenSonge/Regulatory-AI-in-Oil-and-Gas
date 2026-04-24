# Supplier Evaluation Report Template

Mandatory output template for `evaluate-supplier.prompt.md`. The writing agent must use this structure exactly.

## File Naming

Write the report to the workspace-level `reports/` folder as:
- dated report: `reports/SUPPLIER-EVALUATION-<supplier>-YYYY-MM-DD-HH-MM.md`
- rolling latest: `reports/SUPPLIER-EVALUATION-<supplier>-LATEST.md`

Create a fresh dated report on every run and refresh the matching `LATEST` file.

## Report Structure

```markdown
# Supplier Evaluation — <Supplier Name>

**Generated:** <ISO 8601 timestamp>
**Supplier folder:** <path>
**Repositories assessed:** <list>
**Weighted total:** <score>/100

## Summary

<Short evaluation posture: what is strongest, what is weakest, how much confidence the evidence supports>

## Normalization Metadata

| Field | Value |
| --- | --- |
| Supplier | <name> |
| Evaluation confidence | <high/medium/low> |
| Repo shape | <single repo / multi-repo / template + project / platform + project / other> |
| Primary stacks | <languages, frameworks, infra style> |
| AI operating model | <prompt-driven / agent-driven / mixed / unclear> |
| AI role | <process-only / product-only / both-connected / both-disconnected> |
| Dominant evidence posture | <doc-heavy / balanced / proof-heavy / template-heavy / other> |
| Delivery window assumption | <3-week showcase build window applied> |
| Accelerator or prior-asset reuse | <clear / probable / unclear / minimal> |
| Reuse adaptation quality | <strong / moderate / weak / unclear> |
| Speed-to-value assessment | <strong / moderate / weak / unclear> |
| GitHub evidence source | <delivery export / live gh / local git only / mixed / none> |
| Evidence freshness | <delivery snapshot / live query / mixed / unclear> |
| External-proof dependency | <high / medium / low> |

## Evidence Inventory

| Metric | Count |
| --- | --- |
| Distinct operational proof artifacts | <number> |
| Populated vs empty/templated artifacts | <N populated / M empty or templated> |
| Claims with verifiable evidence | <percentage or ratio> |
| Evidence channels available | <list: delivery export, live gh, local git, none> |
| Evidence channels actually used | <list> |

**Confidence-reducing factors** (check all that apply):
- [ ] Heavy reliance on README claims without supporting artifacts
- [ ] Templates or scaffolding not populated with project-specific content
- [ ] External systems referenced but not mirrored in repo
- [ ] Collaboration evidence inaccessible (no export, no live access)
- [ ] Key artifacts appear auto-generated without evidence of review
- [ ] Compliance documentation not connected to implementation
- [ ] CI/CD workflows defined but no run evidence available
- [ ] Significant claims depend on narrative rather than inspectable traces
- [ ] AI logs or decision records absent or minimal
- [ ] Test coverage claims without test execution evidence

## Pattern Profile

Classify the supplier using the Pattern Taxonomy. List all applicable tags per dimension.

| Dimension | Tags |
| --- | --- |
| Agent architecture | <tags from taxonomy> |
| Workflow model | <tags> |
| Orchestration style | <tags> |
| Feedback loops | <tags> |
| Deterministic guardrails | <tags> |
| LLM-eval guardrails | <tags> |
| Agent extensibility | <tags> |
| Determinism level | <tags> |
| Compliance integration | <tags> |
| AI role | <tag> |

## Repo Inventory

| Repo | Role | Notes |
| --- | --- | --- |

## Evidence Posture

### Documented Intent
- <key findings>

### Operational Proof
- <key findings>

### Confidence and Verification Limits
- <what could not be verified locally>
- <what was verified through exported collaboration data or live GitHub access>

## Weighted Assessment

| Category | Score | Weight | Weighted |
| --- | ---: | ---: | ---: |
| AI-native SDLC and workflow quality | <0-100> | 50% | <value> |
| Compliance, regulation, and governance with AI support | <0-100> | 30% | <value> |
| Delivered project and practical credibility | <0-100> | 20% | <value> |
| **Total** |  |  | **<value>/100** |

## Harness Engineering

**Deterministic guardrails:**
- <findings — hooks, CI gates, policy-as-code, boundary enforcement, schema validation>

**LLM-eval guardrails:**
- <findings — critical assessment, multi-POV review, judge patterns, advisory checks>

**Agentic operating loop / orchestration approach:**
- <findings>

**Evaluation and verification approach:**
- <findings>

**Human gates and policy boundaries:**
- <findings>

**Agentic development system engineering:**
- <findings on extensibility, coding agent leverage, compounding, team scalability, eval/regression, drift resistance, adaptability>

**Estimated harness effectiveness:**
<brief judgment on how well the harness likely preserves intent fidelity, proof of correctness, safety, and delivery throughput>

**Evidence quality:**
<brief confidence judgment grounded in concrete repository evidence versus documentation-only claims>

## 1. AI-native SDLC and Workflow Quality

**Score:** <0-100>

**Sub-dimension scores:**

| Sub-dimension | Score (0–10) | Key evidence |
| --- | ---: | --- |
| Planning and decomposition | | |
| Implementation and coding | | |
| Review and quality | | |
| Testing and verification | | |
| Orchestration and workflow | | |
| Learning and compounding | | |
| Guardrails and determinism | | |
| Agentic system engineering | | |

**Documented process:**
- <findings>

**Proven execution:**
- <findings>

**Strengths:**
- <findings>

**Gaps and risks:**
- <findings>

**Assessment:**
<brief synthesis covering quality, maintainability, drift resistance, enterprise applicability, and HITL steering>

## 2. Compliance, Regulation, and Governance with AI Support

**Score:** <0-100>

**Sub-dimension scores:**

| Sub-dimension | Score (0–10) | Key evidence |
| --- | ---: | --- |
| Regulatory grounding | | |
| Traceability | | |
| Automated compliance | | |
| Controls and enforcement | | |
| Human oversight | | |
| Responsible AI | | |

**Documented process:**
- <findings>

**Proven execution:**
- <findings>

**Strengths:**
- <findings>

**Gaps and risks:**
- <findings>

**Assessment:**
<brief synthesis covering traceability, controls, oversight, and evidencing quality>

## 3. Delivered Project and Practical Credibility

**Score:** <0-100>

**Sub-dimension scores:**

| Sub-dimension | Score (0–10) | Key evidence |
| --- | ---: | --- |
| Problem framing | | |
| Architectural coherence | | |
| Delivery credibility | | |
| Enterprise suitability | | |

**Documented scope and claims:**
- <findings>

**Observed implementation evidence:**
- <findings>

**Architectural approach and coherence:**
- <findings>

**Acceleration and speed-to-value:**
- <findings>

**Strengths:**
- <findings>

**Gaps and risks:**
- <findings>

**Assessment:**
<brief synthesis covering problem framing, architectural coherence, delivery credibility under the 3-week window, accelerator reuse, correctness confidence, and whether the project proves the process>

## Strengths

1. <supplier-level strength>
2. <supplier-level strength>
3. <supplier-level strength>

## Gaps and Notable Risks

1. <important gap or risk>
2. <important gap or risk>
3. <important gap or risk>

## Evidence Notes

- Separate template or platform capability from project-specific instantiated evidence.
- Cite concrete repository artifacts when making claims.
- Note where evidence is missing, ambiguous, external, or low confidence.
- Capture enough normalized metadata that another evaluation pass can compare suppliers on common ground without re-reading every repository.
- State which collaboration-evidence source was used: delivery export, live GitHub, local git, or a mix.
```
