# AI Security Lab Catalogue

> **Operating thesis:** Assume sensible guardrails already exist. Test the residual risk that remains when agents, tools, data, identities, and business authority interact.

This catalogue is designed around production-style AI security problems rather than intentionally naive systems. Labs should begin with realistic controls already in place—such as prompt-injection filtering, structured outputs, scoped credentials, tool approvals, sandboxing, logging, and human review—and then test where trust, authorization, provenance, or runtime enforcement can still fail.

Status is marked `published` only after a lab is completed, reviewed, and supported by reproducible evidence.

## Lab Evidence Standard

Every completed lab should answer the same questions:

**Architecture → Existing Controls → Attacker Capability → Attack Path → Control That Held → Control That Failed → Authority Exercised → Business Impact → Detection Evidence → Architectural Remediation → Residual Risk**

The purpose is not merely to prove that an exploit works. The purpose is to explain **why a defended system still allowed an unsafe or unauthorized outcome**.

## Classification Standard

Labs distinguish between different layers of an incident rather than collapsing them into one label:

- **Root / initial technique** — how the attacker first gained influence or compromised a component.
- **Model-manipulation technique** — how model reasoning or agent goals were influenced.
- **Downstream abuse technique** — how a legitimate capability or tool was misused.
- **Security weakness** — the architectural or authorization condition that made the outcome possible.
- **Impact** — what happened to the organization, data, system, or user.
- **Control** — the preventive, detective, or containment mechanism intended to reduce the risk.

If more than one technique occurs in an attack chain, the lab documents each stage explicitly instead of forcing one ambiguous "primary" label.

---

## 30 Advanced AI Security Practicum

| Lab | Name | Enterprise Security Question | Primary Mapping | Status |
|---:|---|---|---|---|
| 1 | [Residual Risk in a Guardrailed Agent](labs/day01/README.md) | What still fails after common AI guardrails are already in place? | OWASP Agentic / NIST |  |
| 2 | [Prompt Injection Beyond Basic Filtering](labs/day02/README.md) | How can untrusted content still influence behavior despite filtering, structured outputs, and instruction hierarchy? | OWASP GenAI |  |
| 3 | [RAG Integrity Under Realistic Controls](labs/day03/README.md) | How can trusted retrieval produce unsafe decisions even when access controls and ingestion checks exist? | OWASP GenAI |  |
| 4 | [Provenance, Freshness, and Knowledge Trust](labs/day04/README.md) | How does an agent distinguish authentic, current, authorized knowledge from stale or manipulated knowledge? | OWASP GenAI / NIST / MAESTRO |  |
| 5 | [AI Supply-Chain Compromise](labs/day05/README.md) | What happens when a trusted package, model, tool, MCP component, or dependency becomes compromised? | OWASP Agentic ASI04 |  |
| 6 | [Applied AI Security Classification Checkpoint](labs/day06/README.md) | Can attack technique, weakness, trust issue, control, and impact be classified precisely in realistic architectures? | OWASP GenAI / NIST |  |
| 7 | [Agent Authority and Least Agency](labs/day07/README.md) | What authority should the agent possess, and what happens when its capability exceeds the task? | OWASP Agentic |  |
| 8 | [Agent Identity and Workload Trust](labs/day08/README.md) | How do systems identify agents and bind an authenticated identity to permitted actions? | NIST Agent Identity |  |
| 9 | [Delegated Authorization and OAuth Scope](labs/day09/README.md) | Can an agent act for a user without inheriting all of that user's authority? | OAuth / NIST |  |
| 10 | [Third-Party MCP Server Security](labs/day10/README.md) | What if an MCP server is authenticated and allowlisted but still behaves unsafely? | MCP / OWASP Agentic |  |
| 11 | [Tool Policy and Business Authorization](labs/day11/README.md) | Can a technically valid, permitted tool call still produce an unauthorized business outcome? | OWASP ASI02 |  |
| 12 | [Tool Poisoning and Runtime Change](labs/day12/README.md) | What if approved tool metadata, behavior, or implementation changes after onboarding? | OWASP Agentic / MCP |  |
| 13 | [Persistent Memory and Context Integrity](labs/day13/README.md) | How can persistent context become malicious, stale, cross-tenant, or over-trusted? | OWASP Agentic ASI06 |  |
| 14 | [Rogue-Agent Containment](labs/day14/README.md) | How do you contain an agent that behaves incorrectly while using valid credentials and permitted interfaces? | OWASP Agentic ASI10 |  |
| 15 | [Runtime Governance Outside the Model](labs/day15/README.md) | Which decisions must be enforced by deterministic policy rather than model judgment? | OWASP Agentic / OpenAI Agent Controls |  |
| 16 | [Sandbox Escape Is Not the Only Problem](labs/day16/README.md) | What harmful outcomes remain when the agent is correctly sandboxed but still has permitted network or API capabilities? | OWASP Agentic |  |
| 17 | [Secure Coding Agents and Pull Requests](labs/day17/README.md) | How can code generation, dependency changes, CI automation, and human review still admit unsafe changes? | Supply Chain / CI/CD |  |
| 18 | [AIBOM, Attestation, and Provenance](labs/day18/README.md) | Can you prove which models, prompts, tools, data sources, and dependencies contributed to an action? | AIBOM / SLSA / Sigstore / OWASP |  |
| 19 | [Multi-Agent Trust Chains](labs/day19/README.md) | Why is authenticated agent-to-agent communication insufficient for authorization? | OWASP Agentic ASI07 |  |
| 20 | [Delegated Approval Between Agents](labs/day20/README.md) | When may one agent legitimately approve or authorize another agent's action? | NIST Agent Authority |  |
| 21 | [Cross-Agent Data and Authority Leakage](labs/day21/README.md) | How do task data, tenant context, credentials, or authority cross agent boundaries unintentionally? | OWASP Agentic |  |
| 22 | [Browser and Computer-Use Agent Security](labs/day22/README.md) | What goes wrong when browser or desktop actions are permitted but semantically unsafe? | Prompt Injection / Sandboxing |  |
| 23 | [Model Artifacts and Unsafe Serialization](labs/day23/README.md) | How can signed or trusted model artifacts still become dangerous at load or runtime? | Model Security / Serialization |  |
| 24 | [Secure AI CI/CD and Promotion](labs/day24/README.md) | How should evaluation, signing, scanning, provenance, approval, and rollback protect AI releases? | MLSecOps |  |
| 25 | [Cloud AI Workload Identity and Blast Radius](labs/day25/README.md) | How do service accounts, cloud identities, network paths, secrets, and workload roles constrain agent impact? | Cloud / Kubernetes |  |
| 26 | [Production AI Threat Modeling](labs/day26/README.md) | Can identity, trust, authorization, data influence, side effects, and blast radius be traced end to end? | MAESTRO / NIST / OWASP |  |
| 27 | [Blind Red Team of a Defended Agent](labs/day27/README.md) | Can realistic defenses be tested without relying on intentionally naive configurations? | AI Red Teaming / OWASP |  |
| 28 | [AI Incident Response and Evidence](labs/day28/README.md) | What telemetry is needed to reconstruct a bad agent action and determine root cause? | Incident Response / MCP / Agent Tracing |  |
| 29 | [AI Security Architecture and Leadership Review](labs/day29/README.md) | Can residual risk be explained clearly to engineering, IAM, cloud, legal, governance, and executives? | NIST / Enterprise Architecture |  |
| 30 | [Capstone — Defend a Production-Style Agentic System](labs/day30/README.md) | Can a realistic agentic system be designed, attacked, defended, monitored, and explained with documented residual risk? | Multi-framework |  |

---

## Lab Design Rules

Each lab should follow these rules:

1. **Start from a defended architecture.** Common controls should already exist unless the lab is explicitly testing why one is absent.
2. **Do not treat guardrails as authorization.** Model safety controls, prompt filters, and structured outputs reduce risk but do not determine whether a business action is authorized.
3. **Put security decisions at the correct boundary.** Sensitive side effects should be validated at the tool, identity, data, network, or policy boundary where they occur.
4. **Separate authentication from authorization.** A valid identity, token, signature, or agent message does not automatically mean the requested action is permitted.
5. **Treat trusted components as potentially compromised.** Approved packages, models, MCP servers, peer agents, knowledge sources, and CI components can become malicious or stale.
6. **Track authority, not just prompts.** Every attack path should identify which identity or capability ultimately caused the business impact.
7. **Measure blast radius.** Document exactly what data, systems, tenants, tools, or actions the compromised path could reach.
8. **Capture evidence.** Logs, traces, tool arguments, authorization decisions, retrieval records, token scopes, file access, and network activity should support the conclusion.
9. **Test remediation.** Every mitigation should have a regression test proving the attack path is blocked or meaningfully constrained.
10. **Document residual risk.** A lab is not complete until it explains what risk still remains after remediation.

---

## Portfolio Standard

A published lab should contain:

- architecture diagram
- threat hypothesis
- controls already present
- attacker assumptions and capabilities
- attack-chain diagram
- reproducible technical evidence
- root-cause analysis
- identity and authorization analysis
- business impact and blast-radius analysis
- detection and telemetry evidence
- remediation design
- regression test
- residual-risk statement
- engineer-facing explanation
- leadership-facing explanation
- references to current primary standards, specifications, and vendor documentation

## Reference Baseline

The catalogue should be periodically reviewed against current primary guidance. Current baseline references include:

- OWASP Top 10 for Agentic Applications 2026: https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/
- OWASP Agentic Security Initiative: https://genai.owasp.org/initiatives/agentic-security-initiative/
- NIST — Identity and Authority of Software Agents: https://www.nist.gov/news-events/news/2026/02/new-concept-paper-identity-and-authority-software-agents
- OpenAI — Safety in building agents: https://developers.openai.com/api/docs/guides/agent-builder-safety
- OpenAI — Guardrails and human review: https://developers.openai.com/api/docs/guides/agents/guardrails-approvals

## Ethics

All offensive exercises must be performed only against intentionally vulnerable lab environments, isolated test systems, or systems for which explicit authorization exists. Use synthetic credentials and data, minimize external connectivity, and never publish live secrets or unsafe deployment defaults.
