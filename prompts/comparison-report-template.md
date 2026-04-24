# Supplier Comparison Report Template

Mandatory output template for `align-supplier-evaluations.prompt.md`. The writing agent must use this structure exactly.

## File Naming

Write the comparison report to:
- dated report: `reports/SUPPLIER-COMPARISON-YYYY-MM-DD-HH-MM.md`
- rolling latest: `reports/SUPPLIER-COMPARISON-LATEST.md`

Create a fresh dated report on every run and refresh the `LATEST` file.

## Report Structure

```markdown
# Supplier Comparison

**Generated:** <ISO 8601 timestamp>
**Reports compared:** <list>

## Comparison Basis

<what reports were used, what was normalized, what limits applied>

## Supplier Metadata Snapshot

| Supplier | Confidence | Repo shape | AI model | AI role | Evidence posture | Reuse | Adaptation | Speed to value | GitHub evidence | Freshness | External dependency |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

## Evidence Inventory Comparison

| Supplier | Proof artifacts | Populated/templated | Verifiable claims | Channels used | Confidence-reducing factors |
| --- | ---: | --- | --- | --- | ---: |

## Pattern Taxonomy Comparison

| Dimension | <Supplier 1> | <Supplier 2> | <Supplier N> |
| --- | --- | --- | --- |
| Agent architecture | | | |
| Workflow model | | | |
| Orchestration style | | | |
| Feedback loops | | | |
| Deterministic guardrails | | | |
| LLM-eval guardrails | | | |
| Agent extensibility | | | |
| Determinism level | | | |
| Compliance integration | | | |
| AI role | | | |

### Pattern Taxonomy Analysis
- <which architectural approaches differ most and why it matters>
- <which suppliers leverage coding agent extensibility most effectively>
- <which suppliers have the strongest feedback loops>
- <which suppliers combine deterministic and LLM-eval guardrails most effectively>

## Original Supplier Scores

| Supplier | SDLC | Compliance | Project | Weighted total |
| --- | ---: | ---: | ---: | ---: |

## Sub-Dimension Score Comparison

### SDLC Sub-Dimensions

| Sub-dimension | <Supplier 1> | <Supplier 2> | <Supplier N> | Spread | Analysis |
| --- | ---: | ---: | ---: | ---: | --- |
| Planning and decomposition | | | | | |
| Implementation and coding | | | | | |
| Review and quality | | | | | |
| Testing and verification | | | | | |
| Orchestration and workflow | | | | | |
| Learning and compounding | | | | | |
| Guardrails and determinism | | | | | |
| Agentic system engineering | | | | | |

### Compliance Sub-Dimensions

| Sub-dimension | <Supplier 1> | <Supplier 2> | <Supplier N> | Spread | Analysis |
| --- | ---: | ---: | ---: | ---: | --- |
| Regulatory grounding | | | | | |
| Traceability | | | | | |
| Automated compliance | | | | | |
| Controls and enforcement | | | | | |
| Human oversight | | | | | |
| Responsible AI | | | | | |

### Project Sub-Dimensions

| Sub-dimension | <Supplier 1> | <Supplier 2> | <Supplier N> | Spread | Analysis |
| --- | ---: | ---: | ---: | ---: | --- |
| Problem framing | | | | | |
| Architectural coherence | | | | | |
| Delivery credibility | | | | | |
| Enterprise suitability | | | | | |

### Sub-Dimension Divergence Analysis
- <sub-dimensions with highest spread — where differentiation is genuine>
- <sub-dimensions with lowest spread — where scoring may have drifted or capability is genuinely similar>
- <suppliers whose category scores mask significant sub-dimension variation>

## Harness Engineering Comparison

| Supplier | Deterministic guardrails | LLM-eval guardrails | Agentic operating loop / orchestration | Evaluation and verification | Human gates and policy boundaries | Agentic system engineering | Estimated harness effectiveness | Evidence quality |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

### Deterministic guardrails
- <comparison — hooks, CI gates, policy-as-code, boundary enforcement, schema validation>

### LLM-eval guardrails
- <comparison — critical assessment, multi-POV review, judge patterns, advisory checks>

### Agentic operating loop / orchestration approach
- <comparison>

### Evaluation and verification approach
- <comparison>

### Human gates and policy boundaries
- <comparison>

### Agentic development system engineering
- <comparison — extensibility, coding agent leverage, compounding, team scalability, adaptability, drift resistance>
- <which suppliers' agentic systems are best positioned to improve with model and agent capability evolution>

### Estimated harness effectiveness
- <comparison>

### Evidence quality
- <comparison>

## Normalized Comparison Notes

### <Supplier>
- <how to interpret the report on common ground>

## Comparative Findings

### AI-native SDLC
- <comparison — cite sub-dimension scores to support claims>

### Compliance and Governance
- <comparison — cite sub-dimension scores to support claims>

### Delivered Project Credibility
- <comparison — cite sub-dimension scores to support claims>

### Speed, Leverage, and Accelerator Use
- <comparison>

### Agentic Development System Engineering
- <comparison — extensibility, compounding, coding agent leverage, team scalability, adaptability>
- <which suppliers are best positioned to improve their AI-native SDLC as models and agents evolve>

### Enterprise Applicability and Maintainability
- <comparison>

## Ranking or Tiering

1. <supplier or tier>
2. <supplier or tier>
3. <supplier or tier>

## Confidence and Comparability Limits

- <limits>

## What Would Change the Verdict

1. <missing evidence>
2. <missing evidence>
3. <missing evidence>
```
