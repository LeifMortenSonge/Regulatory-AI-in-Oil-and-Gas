# Evaluation Pattern Taxonomy

Shared classification dimensions for supplier evaluation. Used by `evaluate-supplier.prompt.md` to tag each supplier and by `align-supplier-evaluations.prompt.md` to compare suppliers on common ground.

Classify the supplier's approach on every dimension below. Use the listed tags where they fit; add `other:<description>` when the supplier's approach does not match any listed tag. Multiple tags per dimension are expected and encouraged for mature submissions.

## Agent Architecture

| Tag | Meaning |
| --- | --- |
| `coding-agent` | Default coding agent (e.g., Copilot chat, Claude chat) used as-is, without significant extension or customization |
| `coding-agent-extended` | Coding agent extended with custom instructions, prompt files, AGENTS.md, or similar repo-level configuration |
| `coding-agent-specialists` | Coding agent with specialized modes, skills, or agent definitions for different roles (e.g., review agent, test agent, compliance agent) |
| `orchestrated-coding-multi-agent` | Multiple coding agents or agent modes coordinated through an orchestration layer (e.g., Ariadne, plan-execute patterns, delegated sub-agents) |
| `cloud-orchestrated-custom` | Custom agents orchestrated through cloud services (e.g., Azure AI Agent Service, LangGraph Cloud, custom API orchestration) |
| `workflow-agents` | Cloud workflow-style agents (e.g., Azure Logic Apps, Step Functions, Durable Functions) that coordinate AI steps as workflow nodes |
| `no-agent` | No evidence of agent-based development |

## Workflow Model

| Tag | Meaning |
| --- | --- |
| `sequential` | Linear step-by-step execution |
| `parallel` | Concurrent independent tasks |
| `event-driven` | Triggered by events (commits, PR actions, CI signals) |
| `human-gated` | Workflow proceeds only after explicit human approval at defined checkpoints |
| `fully-autonomous` | End-to-end execution without human intervention |
| `hybrid` | Mix of autonomous and human-gated phases |

## Orchestration Style

| Tag | Meaning |
| --- | --- |
| `prompt-chaining` | Sequential prompts where output feeds next input |
| `plan-execute` | Structured plan created first, then executed task-by-task |
| `tool-use` | Agent selects and invokes tools dynamically |
| `state-machine` | Explicit state transitions governing workflow progression |
| `repo-convention-driven` | Orchestration emerges from repo conventions (AGENTS.md, instruction files, prompt files) rather than runtime coordination |
| `ad-hoc` | No discernible orchestration pattern |

## Feedback Loops

| Tag | Meaning |
| --- | --- |
| `learning-loop` | Captured lessons, updated instructions, or compounding knowledge from session to session |
| `eval-loop` | Automated evaluation against baselines, thresholds, or acceptance criteria |
| `adversarial-eval` | Red-teaming, adversarial testing, or deliberately challenging AI outputs to find failure modes |
| `human-review-loop` | Human review feeds back into process improvement, not just approval |
| `ci-feedback` | CI results feed back into development decisions or agent behavior |
| `none-visible` | No evidence of feedback loops |

## Guardrail Mechanisms

Classify guardrails into two distinct types. The strongest submissions combine both.

**Deterministic guardrails** — enforced mechanically, not dependent on LLM judgment:

| Tag | Meaning |
| --- | --- |
| `policy-as-code` | OPA/Rego, Sentinel, or similar policy engines that enforce rules programmatically |
| `schema-validation` | Typed contracts, JSON schema, API schema validation, or structured output enforcement |
| `ci-gate` | CI checks that block merge or deployment on failure |
| `hook-based` | Pre-commit, pre-push, or lifecycle hooks that enforce rules before code enters the pipeline |
| `boundary-enforcement` | Hard boundaries on agent scope, file access, environment access, or action permissions |
| `fail-closed` | System defaults to denial when validation cannot complete |

**LLM-eval guardrails** — rely on language model judgment to assess quality or compliance:

| Tag | Meaning |
| --- | --- |
| `critical-assessment` | LLM-based review or critique of outputs before acceptance |
| `critical-assessment-multi-pov` | Multiple LLM perspectives or roles reviewing the same output (e.g., security reviewer + compliance reviewer + architecture reviewer) |
| `judge-pattern` | Dedicated judge/evaluator model scoring outputs against criteria |
| `advisory-only` | Warnings or suggestions generated but not enforced |

## Agent Extensibility

| Tag | Meaning |
| --- | --- |
| `skill-based` | Modular skills or plugins that can be added without restructuring the agent |
| `prompt-file` | `.prompt.md` files that can be added, edited, or composed |
| `instruction-file` | `.instructions.md`, `AGENTS.md`, or `copilot-instructions.md` that shape agent behavior at repo level |
| `custom-agent-modes` | Named agent modes or personas with distinct tool access and behavioral rules |
| `mcp-integrated` | Model Context Protocol servers extending agent capabilities |
| `hardcoded` | Agent behavior is hardcoded and not easily extensible |
| `not-applicable` | No agent extensibility applicable |

## Determinism Level

| Tag | Meaning |
| --- | --- |
| `fail-closed` | System blocks progression when checks fail or cannot complete |
| `fail-open-with-warning` | System warns but allows progression |
| `advisory` | Checks produce recommendations without enforcement |
| `aspirational` | Controls are described but not implemented |

## Compliance Integration

| Tag | Meaning |
| --- | --- |
| `inline-policy-check` | Compliance checked within the development flow (agent-invoked or tool-invoked) |
| `pre-commit-gate` | Compliance enforced before code enters the repository |
| `ci-gate` | Compliance enforced during CI pipeline |
| `manual-review` | Compliance checked through human review |
| `documentation-only` | Compliance exists as documentation without enforcement |

## AI Role Classification

| Tag | Meaning |
| --- | --- |
| `process-only` | AI used in the SDLC but not in the delivered product |
| `product-only` | AI used in the delivered product but not meaningfully in the SDLC |
| `both-connected` | AI in both process and product, with the SDLC AI workflow meaningfully supporting the product AI |
| `both-disconnected` | AI in both process and product, but the two are independent |

Capture the AI role classification in normalization metadata. When AI is in the product but not in the process, the SDLC score must reflect process maturity only. Product AI quality contributes to the project score.
