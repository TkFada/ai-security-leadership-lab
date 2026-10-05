# AI Security Leader Practicum (v3)

> **Operating thesis:** Assume sensible defenses already exist. Test the residual risk that remains when models, agents, tools, data, identities, business authority, and human decision-making interact.

A lab is not complete because an exploit ran. A lab is complete when the practitioner can **explain the architecture, reproduce the behavior, inspect the implementation, support conclusions with evidence, implement or review remediation, regression-test it, explain residual risk, and defend the decision under challenge.**

**What changed from v2:** a starting-point diagnostic; phased sequencing with interview-critical labs first; measurable coding milestones with an authorship log; pass criteria and external assessors for gates; a Leadership Artifacts track; per-lab framework mapping restored (OWASP Agentic, OWASP LLM 2026, OSFI, ACS); a lighter publication standard; version pinning; track naming collision fixed.

---

## 1. Structure at a Glance

| Component | What it is | When |
|---|---|---|
| **Diagnostic** | Measure the real starting point before planning hours | Week 0 |
| **18 Core Labs** | One defended reference system, attacked and remediated | Phases 1 to 4 |
| **Track T: Technical Foundations** | Python, shell, Git, HTTP, identity protocols, policy-as-code, containers | Alongside labs, front-loaded |
| **Track P: Cloud and Platform** | IAM, workload identity, Kubernetes, secrets, network policy | Inside Labs 6, 13, 18 plus one more |
| **Track L: Leadership Artifacts** | Documents a security leader actually produces | After specific labs |
| **Track B: Blind Reviews** | Unfamiliar architectures, no prepared answer | One per phase from Phase 2 |
| **Track I: Interview Gates** | Timed, scored checkpoints with an external assessor where possible | End of each phase |

Lab groupings are called **Blocks** (1 to 5) so they do not collide with track letters.

---

## 2. Week 0: Diagnostic

The plan starts from measured ability, not from zero. Record results in `progress/diagnostic.md`.

| Skill | Test | Pass means |
|---|---|---|
| Python reading | Explain a 40-line unfamiliar function: inputs, outputs, failure modes | Correct without running it |
| Python writing | Write a 20-line function that validates a JSON payment request, plus 3 tests, no AI-generated code | Tests pass; you can explain every line |
| Shell | Find all log lines for one correlation ID across 5 files and count them | Done with `grep`/`jq` in under 10 minutes |
| HTTP / auth | Decode a JWT and state its audience, scopes, expiry, and what it does not authorize | All four correct |
| Git | Branch, commit, resolve a simple conflict, open a PR | Done without lookup |
| Containers | Explain what a given Dockerfile runs as, exposes, and mounts | All three correct |
| Kubernetes | Read a ServiceAccount, Role, and RoleBinding and state the effective permission | Correct |
| Threat modeling | DFD plus STRIDE/ATLAS overlay for a 6-component agent system in 60 minutes | Trust boundaries and top 5 threats defensible |

Any skill that passes is credited. Track T modules for credited skills become optional refreshers.

---

## 3. Reference System

All core labs use one fictional system so complexity compounds instead of resetting.

**Maplewood Trust (fictional)** is a Canadian financial institution operating a **Payments Operations Agent** that helps analysts resolve payment exceptions.

| Component | Purpose |
|---|---|
| Payments Operations Agent | Investigates exceptions; proposes or submits repair actions |
| Policy knowledge base (RAG) | Policies, procedures, limits, operational guidance |
| Persistent memory | Analyst working context across sessions |
| MCP servers (pinned to spec 2026-07-28) | Payments API, customer records, ticketing, email |
| Peer agents | Fraud-screening and reconciliation agents |
| Coding agent | Maintains integration code and pipeline |
| Policy engine | Deterministic authorization outside the model |
| Identity layer | User, agent, workload, and delegated identities |
| Telemetry pipeline | Logs, traces, authorization evidence, SIEM |
| Model provider | Third-party hosted model |

**Controls present before testing:** injection filtering; structured outputs; scoped delegated credentials; MCP gateway with tool allow-list; workload identity; human approval for selected actions; sandboxed code execution; egress restricted to one internal package proxy; activity logging with correlation IDs; memory scoping; policy versioning; synthetic data and credentials only.

Use real, named open components where practical. Anything simulated is labelled `SIMULATED` in the lab README and diagrams.

---

## 4. Sequencing

Labs run in **priority order**, not numeric order. Phase 1 covers what technical AI security architecture and engineering interviews probe most: threat modeling, authorization, identity, MCP, and cloud blast radius.

| Phase | Labs | Track L | Track B | Gate |
|---|---|---|---|---|
| **1. Interview-critical** | 1, 5, 6, 8, 13 | L1, L2 | none | Gate 1 |
| **2. Influence and integrity** | 2, 3, 4, 7 | L3 | Review A | Gate 2 |
| **3. Supply chain and multi-agent** | 9, 10, 11, 12 | L4 | Review B | Gate 3 |
| **4. Containment, evidence, capstone** | 14, 15, 16, 17, 18 | L5 | Review C | Gate 4 (final) |

**Effort is a planning estimate, not a commitment.** For someone building components while learning them, expect roughly 15 to 30 hours per lab, plus track work. After Lab 1, replace this estimate with your actual hours and recompute the phase dates. If Phase 1 alone exceeds your available window, publish Phase 1 before starting Phase 2.

---

## 5. Track T: Technical Foundations

### Coding milestones (measurable)

"Unaided" means you write the code yourself. AI may explain concepts and review your code afterwards, but does not generate the solution.

| By | Milestone |
|---|---|
| Gate 1 | Unaided: modify an existing authorization check to add one deny condition, and write the test proving it |
| Gate 2 | Unaided: write a 50 to 100 line policy-check module (subject, action, resource, context) with at least 8 tests |
| Gate 3 | Unaided: implement a policy enforcement point that intercepts a tool call, queries the policy engine, and logs the decision |
| Gate 4 | Unaided: implement one remediation in the capstone end to end, including regression test and telemetry |

### Authorship log

Every lab keeps `AUTHORSHIP.md`, listing which files or functions you wrote, modified, or only reviewed, and which were AI-generated. It is the portfolio equivalent of a verifiable resume, and the honest answer to "show me the code you wrote."

### Modules

| Module | Covers | Primary labs |
|---|---|---|
| T1 Python | Read, trace, modify, test, debug, then write | All |
| T2 Shell / Linux | Files, logs, env vars, `grep`, `find`, `curl`, `jq` | 1, 17 |
| T3 Git | Branches, diffs, PRs, conflicts, signed commits | 9, 11 |
| T4 HTTP / APIs | Methods, headers, status codes, auth headers, replay, idempotency | 2, 8 |
| T5 Identity protocols | OAuth 2.x, OIDC, scopes vs resource authorization, audience, lifetime, delegation | 6, 12 |
| T6 Policy-as-code | Read, write, and test Rego or Cedar independently of model output | 5, 7 |
| T7 Containers | Images, runtime user, mounts, network exposure, least privilege | 10, 13 |

---

## 6. Track P: Cloud and Platform Security

Platform evidence (real or locally simulated, labelled) is **required** in Labs 6, 13, 14, and 18:

- cloud IAM roles and trust policies
- workload identity
- Kubernetes service accounts and RBAC
- secret access paths
- service-to-service authentication
- network policy and egress restrictions
- tenant and resource scoping
- privilege escalation paths
- blast-radius analysis

---

## 7. Track L: Leadership Artifacts

Labs show technical judgment. These artifacts show how you would run the function. They demonstrate leadership thinking, not a leadership track record; present them honestly as such.

| Artifact | After | Content |
|---|---|---|
| **L1 Risk acceptance memo** | Lab 5 | One residual risk: options (block, constrain, monitor, accept), cost, owner, recommendation |
| **L2 Third-party AI vendor assessment** | Lab 8 | Assess one AI or MCP vendor: evidence requested, gaps, contract clauses, concentration risk |
| **L3 Agent inventory and risk tiering** | Lab 7 | Inventory Maplewood's agents with risk tiers driven by autonomy, data, and impact |
| **L4 Control ownership and metrics** | Lab 11 | RACI for agent controls, plus 5 to 8 measurable KPIs/KRIs |
| **L5 90-day AI security program plan** | Lab 18 | Priorities, sequencing, staffing assumptions, budget drivers, board-level risk summary |

---

## 8. Track B: Blind Architecture Reviews

Each review uses an unfamiliar system with an incomplete architecture. Timebox: 90 minutes, then a 20-minute defense.

| Review | System | Must cover |
|---|---|---|
| **A** | SaaS coding agent: repo access, package installation, CI, issue tracker | Config and dependency supply chain, token scope, CI blast radius |
| **B** | Healthcare / research RAG: sensitive records, decision support | Retrieval authorization, provenance, human decision boundary |
| **C** | Cloud infrastructure agent: cloud APIs, IaC, workload identity, approvals, rollback | IAM escalation paths, approval integrity, recovery |

Output for each: missing evidence list, threat model, top 5 prioritized risks, recommended controls, tradeoffs defended.

---

## 9. Track I: Interview Gates

Each gate is timed, scored pass / not yet, and repeated until passed. **At least two gates use a human assessor** (peer, former colleague, or practitioner community). AI can run practice rounds, but should not be the only grader of work it helped build.

Every gate includes:
- 10 to 20 lines of unfamiliar code, explained without running it
- one architecture diagram critique
- one incident or evidence question
- one control-design question
- one executive-risk question
- one pushback question (for example: "Why is the latency and availability dependency of a policy enforcement point justified?")
- the coding milestone for that gate

| Gate | Phase-specific must-demonstrate |
|---|---|
| **1** | Model judgment vs authorization; trace one decision from input to side effect; inspect a delegated token; explain MCP trust boundaries; IAM blast-radius reasoning |
| **2** | RAG and memory trust; approval design critique; one log chain explained; Blind Review A defended |
| **3** | Diff and CI config review; artifact provenance; multi-agent delegation analysis; Blind Review B defended |
| **4** | Containment plan; incident reconstruction; resilience design; executive briefing; Blind Review C defended; full adversarial defense of the capstone |

---

## 10. Evidence Standard

**Architecture → Existing Controls → Attacker Capability → Attack Path → Control That Held → Control That Failed or Was Missing → Authority Exercised → Business Impact → Detection Evidence → Architectural Remediation → Regression Test → Residual Risk**

A control only "failed" if it failed its intended function. An unsafe outcome with every control working as designed is a design gap, not a control failure.

### Classification

| Layer | Question | Taxonomy |
|---|---|---|
| Root / initial technique | How did influence or compromise begin? | MITRE ATLAS |
| Model-manipulation technique | How was model reasoning or goal selection influenced? | MITRE ATLAS, OWASP LLM 2026 |
| Downstream abuse technique | How was a legitimate capability misused? | MITRE ATLAS, OWASP Agentic |
| Security weakness | What condition enabled the outcome? | CWE |
| Impact | What happened? | Lab-specific |
| Control | What prevented, detected, or contained it? | OSFI bulletin section, ACS hook, ATLAS mitigation |

Do not force a single label onto a multi-stage chain.

### Five-lens review

- **Red team:** How can this fail despite existing controls?
- **Security engineering:** Which control constrains, detects, or contains the failure?
- **Governance and audit:** Who owns the decision, and what evidence proves the control operated?
- **Executive:** What business risk remains, and who can accept it?
- **Regulatory and legal, where relevant:** What obligations or defensibility questions arise?

---

## 11. Design Rules

1. Start from the defended reference system.
2. Guardrails are not authorization.
3. Enforce sensitive side effects at the boundary where they occur.
4. Separate authentication, authorization, business policy, and model judgment.
5. Treat trusted components as potentially compromised.
6. Track authority, not just prompts.
7. Measure blast radius.
8. Capture evidence.
9. Regression-test every remediation.
10. Document residual risk.
11. **Pin versions:** protocol revisions (MCP 2026-07-28), SDKs, models, policies. Label results against older specs.
12. **Treat sanctioned exceptions as attack surface:** every allow-listed egress path, approval bypass, and break-glass credential is tested.

---

## 12. The 18 Core Labs

Mapping legend is at the end of this section. ATLAS IDs are confirmed at atlas.mitre.org at publication, since ATLAS releases monthly.

### Block 1: Influence and Integrity

#### Lab 1: Residual Risk Baseline (Phase 1)
**Question:** What still fails in the defended system with every listed control enabled?
**Build / test:** establish architecture; end-to-end threat model; baseline identity, policy, tooling, data, telemetry; reproduce one legitimate action and one unauthorized action caused by weak authorization design; remediate and regression-test.
**Technical:** Python reading, shell, JSON evidence, tests.
**Output:** one page on why a working guardrail can coexist with an unauthorized business outcome.

#### Lab 2: Injection to Exfiltration (Phase 2)
**Question:** With private data, untrusted content, and an outbound channel present, can filtering and structured outputs stop unauthorized disclosure?
**Build / test:** synthetic private data; untrusted content; permitted outbound tool; trace influence to tool use to attempted disclosure; add data-flow and authorization controls.
**Technical:** request tracing, structured tool calls, log analysis.

#### Lab 3: RAG Integrity and Provenance (Phase 2)
**Question:** Can access-controlled, ingestion-checked retrieval still feed stale, manipulated, or unauthorized knowledge into a decision?
**Build / test:** synthetic vector store; provenance metadata; stale-but-authentic, manipulated, and cross-scope content; retrieval-driven decision.
**Technical:** metadata filters, freshness checks, retrieval authorization tests.

#### Lab 4: Persistent Memory Integrity (Phase 2)
**Question:** Can scoped memory become malicious, stale, cross-user, or over-trusted?
**Build / test:** per-user memory; write provenance; expiry; cross-user isolation; stale and poisoning scenarios.
**Technical:** SQLite or Postgres basics, serialization, access-control tests.

### Block 2: Identity and Authority

#### Lab 5: Least Agency and Business Authorization (Phase 1)
**Question:** Can a valid, allow-listed tool call still produce an unauthorized business outcome?
**Build / test:** scoped identity; allow-listed tool; valid schema and authentication; wrong business authorization; deterministic policy outside the model.
**Technical:** policy-as-code introduction; subject/action/resource/context; allow/deny tests.
**ACS focus:** pre-execution hook and traceable decision inputs and outputs.

#### Lab 6: Agent Identity, Delegated Authorization, and Workload Trust (Phase 1)
**Question:** Can the agent act for a user without inheriting all of the user's authority?
**Build / test:** user, agent, and workload identities; delegated token; audience and resource constraints; service-to-service authorization; over-scope scenario.
**Platform (required):** IAM policy and workload identity evidence; blast-radius analysis.
**Technical:** OAuth/OIDC, JWT inspection, scopes vs business authorization.

#### Lab 7: Human Approval as a Security Control (Phase 2)
**Question:** Does the approver see what will actually execute, and does approval stay meaningful under volume or ambiguity?
**Build / test:** pending approval state; reviewer identity; approval bound to the exact action; amount, resource, and policy version visible; stale or mismatched approval; volume scenario.
**Technical:** approval object, state machine, replay prevention, audit evidence.

### Block 3: Tools, Protocols, and Supply Chain

#### Lab 8: Third-Party MCP Servers (Phase 1)
**Question:** What if an authenticated, allow-listed MCP server changes behavior or behaves unsafely?
**Build / test:** local MCP server on spec 2026-07-28; current authorization pattern; tool discovery; allow-list; metadata/runtime mismatch; behavior change after onboarding; runtime enforcement.
**Technical:** MCP flow, tool metadata, auth boundary, server logs, ACS-style hook (self-implemented; see ACS note).

#### Lab 9: Coding Agent and Configuration Supply Chain (Phase 3)
**Question:** Can configuration, dependency changes, CI automation, and human review still admit unsafe changes?
**Build / test:** local repo; coding agent; PR workflow; dependency change; config-file change; CI checks; review gate.
**Technical:** Git, diff review, CI YAML, dependency scanning, secure code review.

#### Lab 10: Model Artifact Trust (Phase 3)
**Question:** Can a trusted model artifact still create unsafe execution at load time or runtime?
**Build / test:** serialization format comparison; hash-verified artifact; loader configuration; controlled demonstration of unsafe deserialization in an isolated environment.
**Technical:** hashing, signature concepts, artifact provenance.

#### Lab 11: Provenance and Release Promotion (Phase 3)
**Question:** Can you prove which model, prompt, tools, data, policies, and dependencies contributed to a release or action?
**Build / test:** versioned model, config, prompt, and policy; SBOM/AIBOM metadata; CI promotion gate; unproven release denied; rollback evidence.
**Technical:** CI/CD, provenance files, signing concepts, release policy.

#### Lab 12: Multi-Agent Trust and Delegation (Phase 3)
**Question:** Why is authenticated agent-to-agent messaging insufficient for authorization?
**Build / test:** two or more agent identities; authenticated messages; explicit delegation; recommendation vs approval; cross-agent leakage; unauthorized delegated action.
**Technical:** message schemas, identity binding, delegation chains.

### Block 4: Containment and Resilience

#### Lab 13: Sandbox Egress, Cloud IAM, and Permitted Exceptions (Phase 1)
**Question:** Does the sanctioned path out of the sandbox become the path to business impact?
**Build / test:** container sandbox; restricted egress; one permitted service; workload identity; resource policy; secret boundaries; network policy; misuse of the permitted path; blast radius.
**Platform (required):** container isolation, IAM policy, and egress evidence; Kubernetes or equivalent local workload-identity exercise.

#### Lab 14: Rogue Agent Containment (Phase 4)
**Question:** How do you contain an agent misbehaving with valid credentials through permitted interfaces?
**Build / test:** detection signal; narrow or revoke authority; disable tool path; rotate credentials; stop workflow; preserve evidence.
**Platform (required):** revocation and isolation evidence at the workload and IAM layer.

#### Lab 15: Browser and Computer-Use Agents (Phase 4)
**Question:** What goes wrong when browser or desktop actions are permitted but semantically unsafe?
**Build / test:** isolated browser; synthetic sites and accounts; untrusted page content; permitted click/type actions; confirmation boundary; action replay.

#### Lab 16: Cascading Failure and AI Dependency Outage (Phase 4)
**Question:** What breaks when the model provider fails, degrades, changes behavior, or becomes too expensive?
**Build / test:** simulated outage; degraded responses; fallback and manual operation; backpressure; cost and rate-limit condition; recovery.
**Technical:** retries, timeouts, circuit breakers, observability.

### Block 5: Evidence and Leadership

#### Lab 17: Telemetry, Incident Response, and Evidence (Phase 4)
**Question:** Can a bad agent action be reconstructed to root cause, and can telemetry itself create risk?
**Build / test:** correlated logs and traces; policy decision evidence; identity events; data-minimized telemetry; sensitive-log leakage; incident timeline; root cause.
**Technical:** JSONL parsing, correlation IDs, a detection query, evidence retention.

#### Lab 18: Capstone: Defend, Red Team, Explain (Phase 4)
**Question:** Can the system be independently reviewed, blind red-teamed, defended, monitored, and explained to engineering, risk, audit, and executives?
**Required:** all prior components integrated; external blind attack scenarios; cloud/IAM blast radius; incident timeline; engineer brief; board brief (L5); full interview defense.

### Framework Mapping

| Lab | OWASP Agentic | OWASP LLM 2026 | OSFI bulletin | ACS | Anchor evidence |
|---:|---|---|---|---|---|
| 1 | ASI01 to ASI10 | All | G | | Reference system |
| 2 | ASI01 | LLM01, LLM02, LLM10 | A, I | | Lethal trifecta (practitioner model) |
| 3 | ASI06 | LLM01, LLM05, LLM09 | I | | LLM01:2026 scope includes RAG-corpus persistence |
| 4 | ASI06 | LLM01 | I | | LLM01:2026 scope includes memory persistence |
| 5 | ASI02, ASI03 | LLM03 | A | ✓ | ATLAS: Data Destruction via AI Agent Tool Invocation |
| 6 | ASI03 | LLM03 | A | | NIST NCCoE concept paper; MCP 2026-07-28 authorization |
| 7 | ASI09 | LLM03 | A, G | ✓ | Hypothesis-driven |
| 8 | ASI02, ASI04 | LLM04 | R, S | ✓ | MCP 2026-07-28; ATLAS: AI Agent Tool Data Poisoning |
| 9 | ASI04, ASI05 | LLM04 | S | | ATLAS agent configuration tampering; malicious `.git/config` coding-agent flaw (Sept 2026, verify primary) |
| 10 | ASI04, ASI05 | LLM04 | S | | Keras CVE-2025-1550, CVE-2025-8747, CVE-2025-9905 |
| 11 | ASI04 | LLM04 | S | | OWASP AIBOM initiative; ACS Agent Bill of Materials |
| 12 | ASI07, ASI03 | LLM01 | A | ✓ | A2A Agent Card spoofing (research) |
| 13 | ASI05, ASI10 | LLM06 | A, R | | OpenAI / Hugging Face ExploitGym incident, July 2026 |
| 14 | ASI10 | LLM03 | C | ✓ | Same incident: containment side |
| 15 | ASI01, ASI02 | LLM01, LLM10 | A | | ATLAS: AI Agent Clickbait |
| 16 | ASI08 | LLM06 | R | | OSFI: AI outage testing, manual fallbacks |
| 17 | ASI10 | LLM02 | C, I | ✓ | ACS OpenTelemetry/OCSF observability |
| 18 | All | All | All | ✓ | Labs 1 to 17 |

**Legend.** OWASP Agentic: ASI01 goal hijack, ASI02 tool misuse, ASI03 identity and privilege, ASI04 supply chain, ASI05 code execution, ASI06 memory and context, ASI07 inter-agent communication, ASI08 cascading failures, ASI09 human-agent trust, ASI10 rogue agents (short descriptors; use official titles when publishing). OWASP LLM 2026: LLM01 Prompt Injection, LLM02 Sensitive Information Disclosure, LLM03 Excessive Agency, LLM04 Supply Chain, LLM05 Data and Model Poisoning, LLM06 Unbounded Consumption, LLM07 Misinformation, LLM08 Hidden Context Exposure, LLM09 Vector and Embedding Weaknesses, LLM10 Improper Output Handling. OSFI bulletin sections: G governance, I information and decision integrity, S software development and change, A agent autonomy and access, C cyber operations, R resilience and third-party risk.

**OSFI mapping note.** The OSFI Generative and Agentic AI Technology Risk Bulletin is used here as a source of supervisory sound practices and sector-relevant risk themes. A mapping in this catalogue means **alignment to those sound practices**, not a claim that the bulletin itself creates a mandatory compliance requirement or that a lab demonstrates regulatory compliance.

**ACS note.** The OWASP Agent Control Standard is a v0.1 public preview: specifications, JSON schemas, observability definitions, and AgBOM requirements. A reference Guardian implementation and framework instrumentation are planned for v1. Labs implement **ACS-style** hooks themselves and must not claim ACS conformance.

---

## 13. Publication Standard

**Core (required to publish):**
- architecture diagram with controls present; simulated parts labelled
- attack chain with reproducible evidence
- identity, authority, and blast-radius analysis
- held / failed / missing control classification
- remediation with regression test
- residual-risk statement
- framework mapping row
- `AUTHORSHIP.md`
- synthetic data only

**Extended (featured labs and the capstone):**
- detection query or alert logic
- policy-as-code
- cloud/IAM evidence
- engineer brief and executive brief

---

## 14. Source Hierarchy

Use the strongest available source for each claim and describe its authority accurately.

1. **Regulatory / standards / protocol:** OSFI regulatory guidance and supervisory publications, NIST publications, RFCs, and protocol specifications such as MCP.
2. **Authoritative security guidance / frameworks:** OWASP official publications and MITRE ATLAS. These are highly relevant security references, but should not be described as equivalent to regulation.
3. **Authoritative technical / primary evidence:** vendor security documentation, CVE/NVD records, and primary incident disclosures.
4. **Research:** peer-reviewed papers and reputable preprints.
5. **Practitioner models:** respected practitioner frameworks and essays. Useful for reasoning and hypothesis formation, but never presented as equivalent to regulation, standards, or primary evidence.

---

## 15. Reference Baseline

Reviewed October 2026. Re-verify before publication.

**Usage note:** OSFI bulletin mappings in this practicum indicate alignment to published sound practices and risk themes; they do not constitute a compliance claim.

- OWASP Top 10 for Agentic Applications 2026: https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/
- OWASP GenAI LLM Top 10 2026: https://genai.owasp.org/resource/owasp-genai-llm-top-10-2026/
- OWASP Agent Control Standard: https://genai.owasp.org/resource/agent-control-standard-acs/
- OWASP Agentic Security Initiative: https://genai.owasp.org/initiatives/agentic-security-initiative/
- MITRE ATLAS: https://atlas.mitre.org
- MCP specification 2026-07-28 changelog: https://modelcontextprotocol.io/specification/2026-07-28/changelog
- NIST NCCoE concept paper, Software and AI Agent Identity and Authorization: https://csrc.nist.gov/pubs/other/2026/02/05/accelerating-the-adoption-of-software-and-ai-agent/ipd
- NCCoE summary of comments: https://pages.nist.gov/nccoe-ai-identity/summary-of-comments.html
- OSFI, Generative and Agentic AI bulletin: https://www.osfi-bsif.gc.ca/en/risks/technology-cyber-risk-management/technology-risk-bulletin/generative-agentic-artificial-intelligence-implications-technology-cyber-security-operational
- OSFI Guideline E-23: https://www.osfi-bsif.gc.ca/en/guidance/guidance-library/guideline-e-23-model-risk-management-2027
- OSFI Guideline B-10: https://www.osfi-bsif.gc.ca/en/guidance/guidance-library/third-party-risk-management-guideline
- OSFI Guideline B-13: https://www.osfi-bsif.gc.ca/en/guidance/guidance-library/technology-cyber-risk-management
- Simon Willison, The lethal trifecta for AI agents (practitioner model): https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/
- A2A threat analysis (research): https://arxiv.org/pdf/2504.16902

### Verification log

| Item | Status |
|---|---|
| OSFI bulletin and E-23 text, MCP 2026-07-28, OWASP release dates, ACS v0.1 status, NCCoE status, Keras CVEs | Verified against primary or official sources, October 2026 |
| OWASP LLM 2026 entry order | Multiple consistent secondary summaries; confirm in the OWASP PDF |
| ATLAS technique names | Contributor and vendor sources; confirm IDs at atlas.mitre.org |
| OpenAI / Hugging Face incident; `.git/config` coding-agent flaw | Secondary reporting; cite primary disclosures before publishing |

---

## 16. Ethics and Safety

- isolated, local lab environments only
- synthetic identities, tokens, transactions, and data
- never target real organizations, users, or production systems without explicit authorization
- minimal internet egress; Lab 13 egress goes only through a monitored proxy you own
- no real secrets or unsafe deployment defaults published
- dual-use techniques shown only to the depth needed to understand detection, control placement, remediation, and residual risk

---

## 17. Final Readiness Standard

The success criterion is not the number of completed folders. Independently, without AI assistance in the moment, you can:

- read unfamiliar security-relevant Python and write a tested authorization module
- operate the lab from the command line
- trace an OAuth/delegated authorization flow and inspect a token
- review MCP tool trust, cloud IAM, and workload identity
- inspect and modify a policy-as-code decision
- threat-model an unfamiliar agent architecture in 90 minutes
- reconstruct a bad agent action from evidence
- distinguish authentication, authorization, business policy, and model judgment
- explain one risk to an engineer, an auditor, and a CISO
- recommend block, constrain, monitor, or accept, and defend it under technical and executive pushback

No lab programme manufactures years of production ownership or a leadership track record. This one builds verifiable capability and shows how you would lead; present it as exactly that.
