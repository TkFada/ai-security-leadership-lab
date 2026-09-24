# AI Security Lab

> Hands-on research and engineering across agentic AI, MCP, RAG, AI red teaming, platform security, MLSecOps, architecture, and governance.

This repository is a public evidence trail for practical AI security work.

**Build it → attack it → defend it → test it → explain it.**

## Focus Areas

- Agentic AI security
- MCP and tool security
- Prompt injection and indirect prompt injection
- RAG, retrieval, and memory security
- Identity, authorization, delegation, and least agency
- AI red teaming and adversarial evaluations
- Sandboxing and containment
- AI/ML supply-chain security
- MLSecOps and secure deployment pipelines
- Cloud AI platform security
- Threat modeling and security architecture
- Incident response and telemetry
- AI security governance and leadership

## Lab Catalogue

The public lab catalogue is maintained in [`LABS.md`](LABS.md).

Each published lab contains:

- objective and architecture
- threat hypothesis
- attack path
- reproducible evidence
- root-cause analysis
- defensive control
- regression test
- engineer explanation
- leadership explanation
- references to primary standards/specifications where appropriate

## Repository Structure

```text
.
├── LABS.md            # Public lab catalogue and status
├── labs/              # Hands-on attack/defense labs
├── threat-models/     # Architecture and threat-model artifacts
├── writeups/          # Technical write-ups and research notes
├── evidence/          # Screenshots, traces, reports, and demos
├── docs/              # GitHub Pages portfolio
└── .github/workflows/ # CI and security automation
```

## Evidence Standard

A completed lab should show more than a successful exploit. The minimum evidence standard is:

**Architecture → attack path → impact → root cause → mitigation → regression test → explanation**

## Ethics

All offensive exercises are performed only against intentionally vulnerable lab environments or systems where explicit authorization exists.
