---
name: "Evaluate Supplier"
description: "Evaluate one supplier folder across one or more repos for AI-native SDLC, compliance/governance, and project quality using evidence-backed Ariadne-style analysis."
argument-hint: "Supplier folder under workspace root, plus optional focus areas or comparison notes"

---

# Evaluate Supplier

Evaluate a single supplier submission under this workspace. The supplier may have one repository or multiple repositories inside its folder. Use Ariadne-style orchestration and subagents to discover evidence dynamically based on the supplier's stack, repository structure, and process model.

Treat the user input as:
- the supplier folder under the workspace root, such as `digia`, `futurice`, `hiq-finland`, or `vivicta` etc.
- optional focus areas, constraints, or comparison notes

If the supplier folder is missing or ambiguous, stop and ask for clarification before evaluating.

## Evaluation Process Overview

This prompt is one half of a two-prompt evaluation system:

1. **Independent evaluation** (this prompt): Run once per supplier, in isolation. Each run produces a structured report with normalization metadata, pattern tags, sub-dimension scores, and evidence inventories. No cross-supplier information should influence the evaluation.
2. **Cross-supplier alignment** (`align-supplier-evaluations.prompt.md`): Run once after all suppliers are evaluated. Reads the per-supplier reports, normalizes scores against common anchors, compares pattern profiles, and produces a comparative ranking.
3. **Human review**: The alignment output is reviewed and adjusted by a human evaluator who owns the final verdict.

Each evaluation run must be self-contained and repeatable. The normalization metadata, pattern tags, and sub-dimension scores exist specifically to make the alignment pass mechanical rather than interpretive.

## Primary Goal

Produce a repeatable, evidence-backed supplier evaluation that distinguishes:
- documented or intended process
- operational proof and evidence of actual use
- quality of the approach and the delivered result
- engineering quality of the agentic development system itself

Do not use the OP AI enablement levels as a scoring rubric. Use the underlying concepts and considerations as a discovery lens, and allow valid alternative partner approaches when the repository evidence supports them.

## Evaluation Weights

Use this weighted model:

| Category | Weight | What to assess |
| --- | --- | --- |
| AI-native SDLC and workflow quality | 50% | AI use across planning, implementation, review, testing, release, learning, orchestration, guardrails, harness, and traceability |
| Compliance, regulation, and governance with AI support | 30% | regulatory grounding, obligation handling, traceability, controls, policy-as-code, responsible AI, auditability, and oversight |
| The delivered project and its practical credibility | 20% | what was built, how clearly the problem is framed, architectural coherence, suitability for a regulated enterprise context, delivery credibility under a 3-week build window, and whether the implementation meaningfully exercises the claimed process |

Provide both:
- evidence-backed qualitative findings
- numeric scores per category and a weighted total

## Operating Rules

1. Start from the workspace root evaluation instructions and then inspect supplier-local instructions before drilling into code.
2. Use Ariadne and subagents to explore dynamically. Prefer discovery first, then deeper repo inspection where needed.
3. Adapt search patterns to the supplier's actual approach, language, tooling, and repo shape. Do not assume Python, Java, Node, Azure, or GitHub-specific conventions unless the repo shows them.
4. Evaluate breadth and depth of the working model, not marketing language.
5. Distinguish clearly between:
   - described process and implemented process
   - compliance documentation and operationalized compliance
   - AI in the product and AI used to run an AI-native SDLC
   - reusable framework or template capability and project-specific instantiated evidence
6. Evidence beats claims. Empty templates, placeholder files, generic starter assets, and aspirational README statements are not proof by themselves.
7. Explicitly call out what cannot be verified from a local checkout alone.
8. Do not modify supplier repositories. Write the evaluation report only to the workspace-level `reports/` folder.
9. Keep the 3-week showcase delivery window in mind. Do not penalize limited breadth by default; instead assess speed to meaningful capability, leverage of accelerators, and how credibly the team turned prior assets into a working, governed result.

## Shared Proof-Weight Vocabulary

During discovery, label major roots and evidence with one reusable vocabulary:
- `accelerator-root`: reusable framework, template, starter, skeleton, bootstrap, or factory asset. Default proof-weight: `reuse-capability`.
- `project-proof-root`: the strongest current-submission design, scope, decision, or problem-framing artifacts. Default proof-weight: `primary`.
- `implementation-proof-root`: instantiated source, tests, infra, generated outputs, or other concrete execution artifacts. Default proof-weight: `implementation`.
- `supporting-process-root`: workflow state, logs, exported collaboration data, SDLC metadata, or other supporting evidence that informs confidence but should not outrank direct project proof. Default proof-weight: `supporting`.

Also record accelerator instantiation strength as `template-only`, `lightly-instantiated`, or `meaningfully-adapted`.

Use this calibration heuristic generically: when a submission separates reusable framework roots, project-specific design roots, concrete `src/` or `tests/` or `infra/` roots, and process-state roots, weight them in that order. Meaningful OSS MIT accelerator reuse is a positive transferable capability signal when adaptation is evidenced, but it is not direct current-project proof by itself.

## Evidence Source Resolution

Do not assume that GitHub-native process evidence is unavailable just because the workspace copy is a clone, zip, or repo archive.

## Pattern Taxonomy

**Read the full taxonomy from [`.github/prompts/evaluation-taxonomy.md`](evaluation-taxonomy.md) before classifying.** That file defines all tags and dimensions used in the Pattern Profile section of the report output.

Classify the supplier on every dimension defined in the taxonomy. Use the listed tags where they fit; add `other:<description>` when the supplier's approach does not match any listed tag. Multiple tags per dimension are expected and encouraged for mature submissions.

## Evidence Source Resolution (continued)

For collaboration and delivery-process evidence such as issues, issue comments, pull requests, reviews, timeline events, branches, labels, and repository metadata, use the strongest accessible source in this order:

1. Delivery-exported collaboration data committed with the submission, such as `github_data/`, issue and pull request exports, repo manifests, or other exported platform metadata.
2. Live public GitHub metadata via `gh` CLI when:
   - the repository is hosted on public `github.com`
   - authentication is available
   - the remote or source repository can be identified from the checkout or export metadata
3. Local `.git` checkout metadata and commit history.

When both exported and live GitHub data are available:
- prefer the exported data as the delivery-bound evidence snapshot
- use live GitHub data to fill export omissions or confirm repository state
- note any material drift between the delivery snapshot and the live repository state

If the submission is an archive without `.git`, still inspect exported collaboration data when present.

## Mandatory Discovery Flow

### Phase 1: Supplier Inventory

Identify all repositories and major artifacts under the supplier folder.

For each repo, classify it as one of:
- primary submission repo
- supporting repo
- shared template or starter
- platform or factory repo
- compliance or infrastructure companion repo

For each repo, also inventory the major evidence roots and label them as `accelerator-root`, `project-proof-root`, `implementation-proof-root`, or `supporting-process-root` before scoring.

If a supplier has multiple repos, evaluate them as one supplier submission while keeping repo-specific evidence clearly attributed.

### Phase 2: Two-Pass Evidence Discovery

Run the evaluation in two passes.

#### Pass A: Documented or Intended Process

Search for artifacts that declare how AI, process, compliance, and governance are intended to work. Look for:
- `AGENTS.md`, `.github/copilot-instructions.md`, `CLAUDE.md`, cursor rules,  prompt files, custom agents, skills, instruction files
- README files, architecture docs, ADRs, RFCs, SDLC docs, backlog and planning artifacts
- compliance source registers, obligation extracts, traceability matrices, policy files, evaluation criteria, risk docs, audit or evidence pack docs
- workflow docs, release docs, operating model docs, contribution rules, branching rules, human approval rules

Capture what the repo claims about:
- AI-assisted planning, decomposition, coding, review, testing, release, and learning
- deterministic approach, such as hooks, CI gates, policy checks, required validations, fail-closed rules, typed contracts, or schema checks
- agentic operating loop / orchestration approach, such as prompts, agents, workflows, task decomposition, orchestration boundaries, scoped agents, and execution limits
- evaluation and verification approach, such as tests, evals, acceptance criteria, judge patterns, baselines, thresholds, regression checks, and evidence requirements
- human gates and policy boundaries, such as human-in-the-loop steering, escalation paths, approvals, override boundaries, and environment boundaries
- compliance handling, regulation-to-implementation flow, privacy, security, governance, and responsible AI
- problem framing, target users, product intent, PRD-level thinking, and architectural approach
- whether the submission appears to rely on accelerators, templates, prior platform work, or pre-existing assets, and how that reuse is presented
- which roots appear to hold reusable accelerator evidence versus project proof, implementation proof, or supporting process-state evidence

#### Pass B: Operational Proof and Evidence

Search for evidence that the intended model was actually operationalized. Look for:
- populated traceability artifacts linking source to requirement, implementation, tests, controls, and evidence
- committed AI logs, decision logs, dated work logs, change logs, ADRs with concrete outcomes, generated evidence files, scorecards
- active CI or workflow automation, policy-as-code, scan configs, quality gates, provenance markers, reproducible scripts
- deterministic approach in operation, such as hooks, CI checks, policies, typed contracts, or schema validations that actually enforce fail-closed behavior
- agentic operating loop / orchestration approach in operation, such as prompts, agents, plan files, scoped execution flows, or handoff artifacts that show how work moved through the loop
- evaluation and verification approach in operation, such as test suites, eval datasets, judge prompts, baselines, thresholds, regression checks, acceptance criteria traces, or generated proof artifacts
- human gates and policy boundaries in operation, such as required approvals, explicit review checkpoints, escalation paths, release boundaries, or evidence of who can override what
- evaluation harnesses, test suites, eval datasets, judge prompts, baselines, thresholds, regression checks, smoke tests
- implementation artifacts that demonstrate the claimed workflow in action
- collaboration and delivery-process evidence from exported `github_data/`-style artifacts when present
- live public GitHub evidence via `gh` CLI when accessible, especially for issues, pull requests, reviews, comments, labels, and workflow metadata
- local git history only as supplemental evidence when available and meaningful
- evidence of delivery velocity, such as concentrated build activity, rapid repo setup, scaffold-to-customization traces, or other signs of how quickly the team got to a meaningful working state
- evidence that pre-existing accelerators or shared assets were actually adapted rather than merely copied, including whether they are `template-only`, `lightly-instantiated`, or `meaningfully-adapted`

Do not count accelerator roots that are `template-only` or `lightly-instantiated` as strong operational proof. Only `meaningfully-adapted` accelerator roots can support positive leverage claims, and even then they remain `reuse-capability` evidence unless linked to project-specific proof or implementation evidence.

### Phase 3: Artifact Classification

For each important artifact, classify it with all of the following:
- evidence type: `documented-intent`, `operational-proof`, or `mixed`
- scope: `project-specific`, `shared-template`, `shared-platform`, or `supporting`
- root role: `accelerator-root`, `project-proof-root`, `implementation-proof-root`, or `supporting-process-root`
- accelerator instantiation: `not-applicable`, `template-only`, `lightly-instantiated`, or `meaningfully-adapted`
- proof-weight: `primary`, `implementation`, `supporting`, or `reuse-capability`
- confidence: `high`, `medium`, or `low`
- evaluation relevance: which category or categories it supports

Lower confidence when:
- the artifact is generic or templated
- the artifact is an `accelerator-root` that is only `template-only` or `lightly-instantiated`
- the artifact describes a process but shows no execution evidence
- the evidence depends on external systems not mirrored in the repo
- claims of rapid delivery depend entirely on narrative rather than inspectable traces
- collaboration evidence exists only as an inaccessible external claim even though no export or live GitHub lookup was attempted

## What To Evaluate

### 1. AI-native SDLC and Workflow Quality (50%)

Assess the breadth and depth of AI usage across the software delivery lifecycle.

Treat harness engineering as a required cross-cutting lens. Keep these dimensions distinct in both discovery and reporting rather than folding them into general SDLC prose.

Look for:
- AI-assisted product definition, planning, refinement, issue creation, decomposition, and acceptance criteria
- prompt-driven or agent-driven implementation, review, testing, and release work
- reusable instructions, prompts, agents, and skills that shape engineering behavior
- deterministic approach: guardrails and controls that do not rely on agent obedience alone
- agentic operating loop / orchestration approach: how humans and agents plan, implement, verify, and hand off work
- evaluation and verification approach: tests, evals, quality gates, thresholds, regression controls, and proof artifacts
- human gates and policy boundaries: review checkpoints, approval points, override rules, and escalation boundaries
- learning loops, updated instructions, post-review compounding, or captured lessons
- traceability from idea to plan to implementation to review to release evidence
- maintainability of the operating model, enterprise applicability, and drift resistance

Assess not only whether these elements exist, but whether they appear operational, coherent, maintainable, and likely to remain reliable under real delivery pressure.

#### Agentic Development System Engineering (cross-cutting lens within SDLC)

Assess the engineering quality of the agentic development system itself — not just whether AI is used, but whether the AI tooling is built to compound, adapt to new capabilities, and scale team expertise. This is an engineering maturity assessment, not a tool preference. A well-engineered custom framework scores as well as a well-engineered coding-agent setup, provided both demonstrate these properties.

Evaluate these properties:

| Property | What to assess | Evidence examples |
| --- | --- | --- |
| **Agent extensibility** | Can capabilities be added without restructuring? | Skill/plugin architecture, modular prompt files, composable agents, MCP integration |
| **Coding agent leverage** | Does the setup amplify coding agents and take advantage of their evolving capabilities? | AGENTS.md, instruction files, skills, custom modes, context engineering, conventions that make the repo legible to AI |
| **Compounding and learning** | Does the system get better over time? | Captured lessons, updated instructions, post-session learning, memory, feedback loops that update the system |
| **Team scalability** | Can new developers onboard and be productive via the AI system? | Conventions encoded in agent config, self-documenting workflows, skill-based knowledge distribution |
| **Eval and regression** | Can quality be measured and regressed against? | Eval datasets, baselines, thresholds, automated verification, adversarial testing |
| **Drift resistance** | Will the workflow degrade silently or does it fail visibly? | Schema enforcement, typed contracts, mandatory gates vs advisory checks, boundary enforcement |
| **Adaptability** | Can the system take advantage of model improvements and new agent capabilities without rearchitecting? | Separation of concerns between orchestration and execution, provider-agnostic patterns where they serve, modular rather than monolithic AI integration |

Use these findings to inform the SDLC score and the Harness Engineering section. Do not create a separate numeric score for agentic system engineering — it is a lens that sharpens the SDLC and harness judgments.

### 2. Compliance, Regulation, and Governance with AI Support (30%)

Assess how the submission uses AI and automation to improve regulated delivery.

Look for:
- regulatory source grounding and explicit obligation extraction
- traceability from regulation to requirement to implementation to control to evidence
- AI-assisted compliance review, policy checks, risk analysis, audit generation, or evidence collection
- responsible AI controls if AI is part of the product or process
- security, privacy, and governance controls expressed as workflows, tests, or policy-as-code
- clear human oversight, approval, escalation, and transparency mechanisms
- proof that compliance artifacts are connected to implementation rather than standing alone

Do not over-credit broad compliance language without enforcement mechanisms or proof.

### 3. Delivered Project and Practical Credibility (20%)

Assess the delivered project mainly as proof that the workflow can produce a credible outcome.

Look for:
- clarity of problem framing and delivered scope
- architectural coherence of the built solution, including whether the major parts fit together cleanly
- suitability for a regulated financial-services context
- whether the architecture and implementation choices seem proportionate to the problem and likely maintainable beyond the demo
- speed to meaningful capability under the 3-week constraint
- signs of accelerator, template, platform, or prior asset reuse, including meaningful OSS MIT reuse, and whether that reuse was meaningfully adapted into current-project proof or merely inflated apparent scope
- whether the demo or implementation meaningfully exercises the claimed SDLC and compliance model
- quality risks in the approach, including correctness risk, operational fragility, maintainability risk, and drift potential

Do not let flashy scope or polished language outweigh weak process evidence. Avoid over-penalizing teams for limited breadth within three weeks; focus instead on the credibility, leverage, and coherence of what they delivered in that time.
Credit meaningful accelerator adaptation positively, but do not let `reuse-capability` or `supporting` evidence substitute for `primary` or `implementation` proof.

## Required Distinctions

The evaluation must explicitly separate these dimensions:

1. Documented process
2. Proven execution
3. Quality of the process and controls
4. Quality and credibility of the result
5. Risks to correctness, maintainability, enterprise adoption, and long-term drift
6. Human steering and accountability boundaries
7. Delivery speed and leverage under the showcase time constraint
8. Reuse of accelerators or prior assets versus evidence of meaningful adaptation

Also keep the mandatory harness section separated into these fixed dimensions: `Deterministic guardrails`, `LLM-eval guardrails`, `Agentic operating loop / orchestration approach`, `Evaluation and verification approach`, `Human gates and policy boundaries`, `Agentic development system engineering`, `Estimated harness effectiveness`, and `Evidence quality`.

For each major positive claim, answer:
- what is documented?
- what is proven from the accessible evidence sources?
- what remains uncertain or external?
- how much should that affect confidence in the score?

## External Evidence Access and Limits

Treat these as verifiable when they are available through delivery exports or live public GitHub access, and otherwise mark them as unverified:
- GitHub issues, issue comments, PR discussions, reviews, approvals, labels, branch protections, workflow run history, and repository metadata
- Azure DevOps boards, tickets, comments, approvals, or external audit systems
- cloud runtime state, deployed guardrails, live telemetry, identity configuration, or hosted evaluation results

If the repo references these external systems, record:
- whether evidence was available from exported submission data
- whether live public GitHub was queried successfully
- what still remained inaccessible or unverified

## Scoring Guidance

### Sub-Dimension Scoring

Score each weighted category through its sub-dimensions first, then derive the category score. This forces granular evidence-based judgments instead of a single gestalt impression.

#### AI-native SDLC sub-dimensions (50% category)

Score each sub-dimension from 0 to 10:

| Sub-dimension | What it covers |
| --- | --- |
| Planning and decomposition | AI-assisted planning, issue creation, refinement, acceptance criteria, decomposition into tasks |
| Implementation and coding | Prompt-driven or agent-driven coding, code generation quality, conventions, context engineering |
| Review and quality | AI-assisted code review, PR review, quality checks, architectural review |
| Testing and verification | AI-assisted test creation, eval loops, acceptance verification, regression testing |
| Orchestration and workflow | How work flows through humans and agents, task handoff, coordination patterns |
| Learning and compounding | Updated instructions, captured lessons, post-review improvements, feedback loops that improve the system |
| Guardrails and determinism | Deterministic controls, boundary enforcement, policy-as-code, fail-closed behavior |
| Agentic system engineering | Extensibility, coding agent leverage, adaptability, team scalability, drift resistance (from the cross-cutting lens above) |

Category score = mean of sub-dimension scores × 10, producing a 0–100 value.

#### Compliance sub-dimensions (30% category)

Score each sub-dimension from 0 to 10:

| Sub-dimension | What it covers |
| --- | --- |
| Regulatory grounding | Source regulations identified, obligation extraction, legal basis documented |
| Traceability | Regulation → requirement → implementation → control → evidence chain |
| Automated compliance | AI-assisted or automated policy checks, compliance review, evidence generation |
| Controls and enforcement | Policy-as-code, security controls, privacy controls, governance enforcement |
| Human oversight | Approval gates, escalation paths, transparency, accountability boundaries |
| Responsible AI | AI ethics controls, bias detection, transparency, disclosure, if AI is in the product or process |

Category score = mean of sub-dimension scores × 10.

#### Project sub-dimensions (20% category)

Score each sub-dimension from 0 to 10:

| Sub-dimension | What it covers |
| --- | --- |
| Problem framing | Clarity of the problem, target users, product intent, scope definition |
| Architectural coherence | Whether the major parts fit together, proportionality to the problem, maintainability |
| Delivery credibility | Speed to meaningful capability, accelerator leverage, demo exercises the process |
| Enterprise suitability | Fitness for a regulated financial-services context, operational readiness signals |

Category score = mean of sub-dimension scores × 10.

### Scoring Anchors

Use these archetype descriptions to calibrate scores consistently across independent evaluation runs. These are not supplier-specific — they describe what each score level looks like in general.

**SDLC sub-dimension anchors** (apply similar logic to each sub-dimension):

| Score | Planning and decomposition archetype |
| --- | --- |
| 9–10 | AI-assisted issue creation with acceptance criteria, traceable from requirement to implementation, evidence of refinement loops, operational and maintained |
| 7–8 | AI-assisted planning visible in prompts or agents, some issue/task evidence, partially connected to implementation |
| 5–6 | Planning prompts or templates exist but limited evidence of actual use; or AI planning described in README but not instantiated |
| 3–4 | Generic mention of AI in planning with no supporting artifacts |
| 0–2 | No evidence of AI in planning |

| Score | Implementation and coding archetype |
| --- | --- |
| 9–10 | Rich instruction files, skills, custom agents shaping coding; evidence of agent-generated code with review; conventions make repo highly legible to AI agents |
| 7–8 | Meaningful instruction files or prompt files; evidence of prompt-driven coding; some convention engineering |
| 5–6 | Basic AGENTS.md or copilot-instructions.md; limited evidence of systematic use |
| 3–4 | Generic AI coding setup without customization |
| 0–2 | No evidence of AI-assisted coding workflow |

| Score | Guardrails and determinism archetype |
| --- | --- |
| 9–10 | Multiple deterministic guardrail types (hooks, CI gates, policy-as-code, boundary enforcement) AND LLM-eval guardrails (critical assessment, judge patterns); fail-closed behavior demonstrated; evidence of enforcement |
| 7–8 | Some deterministic guardrails operational, supplemented by LLM-eval checks; mostly enforced |
| 5–6 | Advisory guardrails or partial enforcement; some hooks or CI checks but not fail-closed |
| 3–4 | Guardrails described but not implemented; or only advisory warnings |
| 0–2 | No guardrail evidence |

| Score | Agentic system engineering archetype |
| --- | --- |
| 9–10 | Modular, extensible agent architecture; skill-based or plugin-based extensibility; evidence of compounding (updated instructions from lessons); team onboarding through AI conventions; eval baselines; drift-resistant with hard boundaries; adaptable to new model capabilities without rearchitecting |
| 7–8 | Good extensibility through prompt files and instruction files; some evidence of learning loops; conventions that scale to team; partial eval coverage |
| 5–6 | Standard agent setup with some customization; limited evidence of compounding or adaptability |
| 3–4 | Basic AI tooling without engineering discipline around it |
| 0–2 | No evidence of agentic system engineering |

**Compliance sub-dimension anchors:**

| Score | Traceability archetype |
| --- | --- |
| 9–10 | Complete chain from regulation → obligation → requirement → implementation → control → test → evidence, with artifacts at each stage and cross-references between them |
| 7–8 | Most links in the chain present with concrete artifacts; some gaps in evidence or cross-referencing |
| 5–6 | Partial traceability — regulation identified and some requirements linked, but chain breaks before implementation or evidence |
| 3–4 | Regulation mentioned, obligations listed, but no connection to implementation |
| 0–2 | No traceability chain |

**Project sub-dimension anchors:**

| Score | Delivery credibility archetype |
| --- | --- |
| 9–10 | Credible working result within the 3-week window; accelerators leveraged effectively; demo clearly exercises the claimed SDLC and compliance model; evidence of rapid but governed delivery |
| 7–8 | Functional result with good leverage; meaningful accelerator adaptation is evidenced; demonstrates most of the claimed process; minor gaps in exercising the full workflow |
| 5–6 | Partial implementation that shows the approach but doesn't fully exercise the claimed process |
| 3–4 | Scaffolding, boilerplate, or lightly instantiated accelerator reuse with limited project-specific substance |
| 0–2 | No credible delivery evidence |

### Score Calculation

Score each weighted category from 0 to 100 derived from sub-dimension scores as described above.

Interpret category scores through proof weight:
- `primary` and `implementation` evidence should dominate operational-depth judgments.
- `supporting` evidence can raise or lower confidence, but it should not replace missing direct proof.
- `reuse-capability` evidence can credit transferable leverage and meaningful OSS MIT adaptation, but it must not outweigh weak current-project instantiation.

Do not create a separate numeric score for Harness Engineering or Agentic System Engineering. Use the mandatory `Harness Engineering` section and the agentic system engineering lens to justify and interpret the three weighted category scores only.

For the 20% project category, score against quality and delivery credibility, not raw feature volume. A smaller but coherent and well-leveraged result can score higher than a broader but weakly evidenced one.

Use the full range:
- 90 to 100: strong, operationalized, evidenced, and maintainable
- 75 to 89: clearly capable, with good evidence but some gaps or confidence limits
- 50 to 74: meaningful partial implementation with notable weaknesses or proof gaps
- 25 to 49: mostly aspirational, lightly evidenced, or operationally weak
- 0 to 24: minimal evidence or materially unreliable approach

Then calculate:

`Weighted Total = SDLC score × 0.50 + Compliance score × 0.30 + Project score × 0.20`

Round the final total to the nearest whole number.

## Output Requirements

**Read the report template from [`.github/prompts/evaluation-report-template.md`](evaluation-report-template.md) and follow it exactly when writing the report.** That file defines file naming, structure, all sections, tables, and required fields.

Write the report to the workspace-level `reports/` folder. Create a fresh dated report on every run and refresh the matching `LATEST` file.

## Working Method

1. Inspect the supplier folder and map the repositories.
2. Read workspace-level instructions and supplier-local instructions.
3. Use subagents for discovery when the repo structure is broad or heterogeneous.
4. Search documented intent artifacts first.
5. Search operational proof artifacts second.
6. Compare claims against concrete evidence.
7. Inventory and rank the major evidence roots by `proof-weight` before classifying or scoring so reusable accelerators cannot outrank project-specific proof.
8. Classify the supplier's approach using the Pattern Taxonomy — tag every dimension.
9. Assess the agentic development system engineering properties as a cross-cutting lens.
10. Record the mandatory harness findings using the fixed section headings so deterministic guardrails, LLM-eval guardrails, orchestration, evaluation and verification, human gates, and agentic system engineering remain distinct.
11. Score each sub-dimension individually using the scoring anchors for calibration.
12. Derive category scores from sub-dimension means.
13. Score conservatively when proof is weak, templated, lightly instantiated, or external-only.
14. Fill the evidence inventory with concrete counts, not qualitative labels alone.
15. Add normalization metadata that will support second-pass cross-supplier comparison.
16. Treat delivery speed, accelerator reuse, and meaningful OSS MIT adaptation as evaluation factors, but do not confuse `reuse-capability` with proof of current-team execution quality.
17. Resolve collaboration evidence using exported submission data first, then live public GitHub when accessible, then local git.
18. Write the report files under `reports/`.
19. Return a concise summary in chat with the weighted total, top strengths, top gaps, and the report path.

## Final Constraints

- Be evidence-driven and explicit about uncertainty.
- Prefer direct file-based evidence over high-level claims.
- Do not assume good practice from naming alone.
- Do not invent missing GitHub issue or PR evidence.
- Use accessible GitHub/exported collaboration metadata when available before labeling process evidence as unverifiable.
- Keep the evaluation repeatable across current and future supplier submissions.
