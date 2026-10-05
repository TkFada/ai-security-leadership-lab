# AI Security Lab Catalogue

> **Operating thesis:** Assume sensible defenses already exist. Test the residual risk that remains when models, agents, tools, data, identities, business authority, and human decision-making interact.

## Lab Catalogue

| # | Lab | Security focus | Framework alignment |
|---:|---|---|---|
| **1** | [**Residual Risk in a Defended Agent**](labs/lab01/README.md) | Establish a defended agentic system and test how an unauthorized business outcome can still occur even when several security controls operate correctly. | OWASP Agentic ASI01–ASI10 · OWASP LLM 2026 · OSFI G |
| **2** | [**Injection to Exfiltration**](labs/lab02/README.md) | Examine whether untrusted content can influence an agent into disclosing synthetic private data through an otherwise permitted tool or communication channel. | ASI01 · LLM01/02/10 · OSFI A/I |
| **3** | [**RAG Integrity and Provenance**](labs/lab03/README.md) | Test whether retrieval systems can still produce unsafe decisions when information is stale, manipulated, incorrectly scoped, or lacking reliable provenance. | ASI06 · LLM01/05/09 · OSFI I |
| **4** | [**Persistent Memory Integrity**](labs/lab04/README.md) | Explore how persistent agent memory can become stale, poisoned, over-trusted, or improperly shared across users or sessions. | ASI06 · LLM01 · OSFI I |
| **5** | [**Least Agency and Business Authorization**](labs/lab05/README.md) | Test whether a technically valid and permitted tool action can still violate business policy, and place independent authorization at the business-action boundary. | ASI02/03 · LLM03 · OSFI A · ACS-style runtime control |
| **6** | [**Agent Identity and Delegated Authorization**](labs/lab06/README.md) | Explore how users, agents, and workloads are identified and how delegated authority is constrained without transferring all of a user's privileges. | ASI03 · LLM03 · OSFI A · NIST agent identity/authorization |
| **7** | [**Human Approval as a Security Control**](labs/lab07/README.md) | Test whether approval remains meaningful when context is incomplete, approvals become stale or mismatched, or review volume increases. | ASI09 · LLM03 · OSFI A/G · ACS-style approval control |
| **8** | [**Third-Party MCP Server Security**](labs/lab08/README.md) | Examine the risks of authenticated and allow-listed MCP servers whose metadata, capabilities, or runtime behavior change after onboarding. | ASI02/04 · LLM04 · OSFI R/S · MCP 2026-07-28 · ACS-style runtime control |
| **9** | [**Coding Agent and Configuration Supply Chain**](labs/lab09/README.md) | Test how code, dependencies, configuration, CI automation, and human review can still introduce unsafe changes into AI-enabled development workflows. | ASI04/05 · LLM04 · OSFI S |
| **10** | [**Model Artifact Trust**](labs/lab10/README.md) | Explore why trusted, signed, or hash-verified model artifacts can still introduce risk when loading or serialization mechanisms are unsafe. | ASI04/05 · LLM04 · OSFI S |
| **11** | [**Provenance and Secure Release Promotion**](labs/lab11/README.md) | Track the models, prompts, policies, tools, data sources, and dependencies that contribute to a release and block promotion when provenance cannot be demonstrated. | ASI04 · LLM04 · OSFI S · AIBOM/AgBOM concepts |
| **12** | [**Multi-Agent Trust and Delegation**](labs/lab12/README.md) | Examine why authenticated communication between agents does not automatically imply authorization, including delegation, approval, and cross-agent data boundaries. | ASI03/07 · LLM01 · OSFI A · ACS-style runtime control |
| **13** | [**Sandbox Egress, Cloud IAM, and Permitted Exceptions**](labs/lab13/README.md) | Test whether sanctioned network paths, workload identities, cloud permissions, or other permitted exceptions can still become routes to business impact. | ASI05/10 · LLM06 · OSFI A/R |
| **14** | [**Rogue Agent Containment**](labs/lab14/README.md) | Explore how to contain an agent that is behaving incorrectly while still using valid credentials and approved interfaces. | ASI10 · LLM03 · OSFI C · ACS-style runtime control |
| **15** | [**Browser and Computer-Use Agent Security**](labs/lab15/README.md) | Test how browser and desktop agents can create unsafe outcomes even when individual clicks, typing, and navigation actions are technically permitted. | ASI01/02 · LLM01/10 · OSFI A |
| **16** | [**Cascading Failure and AI Dependency Resilience**](labs/lab16/README.md) | Examine what happens when an AI provider becomes unavailable, slow, degraded, changes behavior, or creates unexpected cost and capacity pressure. | ASI08 · LLM06 · OSFI R |
| **17** | [**Telemetry, Incident Response, and Evidence**](labs/lab17/README.md) | Determine whether a harmful agent action can be reconstructed from logs, traces, identities, policy decisions, and execution evidence without creating excessive telemetry risk. | ASI10 · LLM02 · OSFI C/I · ACS observability concepts |
| **18** | [**Capstone — Defend a Production-Style Agentic System**](labs/lab18/README.md) | Integrate the full system, test realistic failure scenarios, strengthen the architecture, investigate incidents, and document residual risk. | OWASP Agentic · OWASP LLM 2026 · OSFI · ACS-style controls |

## Security Architecture Coverage

The catalogue is structured around five security domains that recur in production agentic systems:

- **Influence and information integrity — Labs 1–4:** model influence, prompt injection, retrieval integrity, provenance, freshness, and persistent memory.
- **Identity, authority, and decision control — Labs 5–7:** least agency, delegated authorization, workload identity, business-policy enforcement, and human approval.
- **Tools, protocols, and supply chain — Labs 8–12:** MCP trust, coding agents, dependencies, model artifacts, release provenance, and inter-agent delegation.
- **Containment and resilience — Labs 13–16:** cloud IAM, workload isolation, sanctioned egress, rogue-agent containment, computer-use agents, and dependency failure.
- **Detection, investigation, and assurance — Labs 17–18:** telemetry, incident reconstruction, remediation validation, residual-risk analysis, and end-to-end architecture assurance.

## Reference System

All labs build on the same fictional environment so controls, evidence, identities, and trust relationships become more realistic over time rather than resetting for every exercise.

**Maplewood Trust (fictional)** operates a **Payments Operations Agent** that assists analysts with payment exceptions.

| Component | Purpose |
|---|---|
| Payments Operations Agent | Investigates exceptions and proposes or submits repair actions |
| Policy knowledge base (RAG) | Policies, procedures, limits, and operational guidance |
| Persistent memory | Analyst working context across sessions |
| MCP servers (spec pinned to 2026-07-28) | Payments API, customer records, ticketing, and email |
| Peer agents | Fraud-screening and reconciliation agents |
| Coding agent | Maintains integration code and pipeline |
| Policy engine | Deterministic authorization outside the model |
| Identity layer | User, agent, workload, and delegated identities |
| Telemetry pipeline | Logs, traces, authorization evidence, and SIEM integration |
| Model provider | Third-party hosted model |

**Baseline controls:** injection filtering, structured outputs, scoped delegated credentials, an MCP gateway with a tool allow-list, workload identity, selected human approval, sandboxed execution, restricted egress, correlated activity logging, memory scoping, and policy versioning.

Anything simulated in a lab is explicitly labelled `SIMULATED`.

## Security Analysis Model

Each lab follows the same evidence-driven analysis:

**Architecture → Existing Controls → Attacker Capability → Attack Path → Controls That Held → Control Gap or Failure → Authority Exercised → Business Impact → Detection Evidence → Architectural Remediation → Regression Test → Residual Risk**

A control is classified against its intended purpose. If an unsafe outcome occurs while a control performs exactly as designed, the finding is recorded as an architectural or control-design gap rather than incorrectly labelling that control as failed.

For multi-stage incidents, the analysis records each layer separately: **initial influence or compromise, model manipulation, downstream capability abuse, architectural weakness, and business impact.** This prevents different parts of an attack chain from being collapsed into one misleading label.

### Review lenses

- **Adversarial:** How can the system fail despite its existing controls?
- **Security engineering:** Which control prevents, constrains, detects, or contains the failure?
- **Governance and audit:** Who owns the decision and what evidence proves the control operated?
- **Executive risk:** What business exposure remains and who has authority to accept it?
- **Regulatory and legal:** Where relevant, what obligations, supervisory expectations, or defensibility questions arise?

## Architecture Principles

1. Start from a defended system rather than a deliberately naive one.
2. Do not treat guardrails as business authorization.
3. Enforce sensitive side effects at the boundary where they occur.
4. Separate authentication, authorization, business policy, and model judgment.
5. Treat trusted components as potentially compromised, stale, or changed.
6. Track the authority that caused an outcome, not only the prompt that influenced it.
7. Measure blast radius.
8. Capture sufficient evidence to reconstruct material decisions and actions.
9. Regression-test every remediation.
10. Document residual risk after controls are applied.
11. Pin relevant protocol, SDK, model, and policy versions.
12. Treat sanctioned exceptions—allow-listed egress, approval bypasses, and break-glass access—as attack surface.

## Frameworks

The lab mappings use current security and regulatory references to make the control reasoning explicit:

- **OWASP Top 10 for Agentic Applications 2026** — agentic security risks and control themes.
- **OWASP GenAI LLM Top 10 2026** — model and application-layer risk categories.
- **MITRE ATLAS** — adversarial techniques and mitigations; technique identifiers are re-verified when individual labs are published.
- **OWASP Agent Control Standard (ACS)** — used for runtime-control and observability concepts; labs describe these as **ACS-style** where conformance has not been established.
- **MCP specification 2026-07-28** — protocol baseline for MCP-focused exercises.
- **NIST NCCoE Software and AI Agent Identity and Authorization work** — identity and delegated-authorization reference material.
- **OSFI Generative and Agentic AI Technology Risk Bulletin** — used to map relevant financial-sector sound practices and risk themes; mapping does not imply regulatory compliance.

## Lab Safety

All exercises use isolated test environments, fictional organizations, synthetic identities, synthetic transactions, and synthetic data. Offensive techniques are used only to demonstrate security failure modes, detection, containment, remediation, and residual risk.
