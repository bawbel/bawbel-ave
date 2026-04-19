<div align="center">

# AVE — Agentic Vulnerability Enumeration

**The open standard for tracking vulnerabilities in AI agent components**

[![License](https://img.shields.io/badge/License-Apache_2.0-teal.svg)](LICENSE)
[![Schema Version](https://img.shields.io/badge/Schema-v0.1.0-green.svg)](SPEC.md)
[![Records](https://img.shields.io/badge/AVE_Records-8-blue.svg)](records/)
[![Contributions Welcome](https://img.shields.io/badge/Contributions-Welcome-brightgreen.svg)](CONTRIBUTING.md)

[Read the Spec](SPEC.md) · [Browse Records](records/) · [Submit an AVE](CONTRIBUTING.md) · [bawbel.io](https://bawbel.io)

</div>

---

## What is AVE?

AVE (Agentic Vulnerability Enumeration) is the open numbering system for vulnerabilities in **agentic AI components** — the skills, MCP servers, system prompts, plugins, and protocols that define what an AI agent can do and how it behaves.

Think of it as **CVE for AI agents** — but purpose-built for the behavioral, probabilistic nature of agentic vulnerabilities that CVE was never designed to handle.

```
AVE-2026-00001   Metamorphic payload via external config fetch in SKILL.md       [CRITICAL 9.4]
AVE-2026-00002   Prompt injection via malicious MCP tool description field        [HIGH 8.7]
```

---

## Why AVE, not CVE?

| | CVE | AVE |
|---|---|---|
| **Designed for** | Deterministic code flaws | Behavioral AI vulnerabilities |
| **Covers** | Specific software versions | Skills, MCP, prompts, plugins, A2A, RAG, models |
| **Mutation tracking** | One record per instance | One record covers all behavioral variants |
| **Scoring** | CVSS | CVSS-AI (adds agentic scope, human oversight, tool access) |
| **Processing** | Days to months | Near real-time via PiranhaDB |
| **Disclosure target** | Software vendor | Registry operator or community |

> If a SKILL.md file contains a traditional RCE in embedded Python — that gets a CVE. The natural language prompt injection in the same file that hijacks the agent's goals — that gets an AVE. Both systems are necessary.

[→ Full comparison in SPEC.md](SPEC.md#2-why-ave-and-not-cve)

---

## Component Types Covered

| `component_type` | Examples | Primary Threats |
|---|---|---|
| `skill` | SKILL.md, .cursorrules, CLAUDE.md | Prompt injection, goal hijack, metamorphic payloads |
| `mcp` | MCP server manifests | Tool poisoning, schema injection |
| `prompt` | System prompts, deployment configs | Safety bypass, instruction injection |
| `plugin` | Copilot plugins, AgentForce skills | Supply chain substitution, capability escalation |
| `a2a` | Agent-to-agent protocol handlers | Transitive trust exploitation, agent impersonation |
| `rag` | Knowledge base sources | RAG poisoning, indirect prompt injection |
| `model` | Fine-tuned weights | Model backdoors, training data poisoning |

---

## Quick Start

**Browse published records:**
```
records/AVE-2026-00001.json
records/AVE-2026-00002.json
```

**Scan your skills with Bawbel:**
```bash
pip install bawbel-scanner
bawbel scan ./my-skill.md
```

**Query the PiranhaDB API:**
```bash
curl https://api.piranha.bawbel.io/ave/AVE-2026-00001
```

---

## Contributing

We welcome AVE record submissions, schema improvements, detection rules, and documentation.

| What | How |
|---|---|
| Submit an AVE record | [Open a PR](CONTRIBUTING.md) or email bawbel.io@gmail.com |
| Report a false positive | [Open an issue](https://github.com/bawbel/bawbel-ave/issues/new?template=false_positive.md) |
| Propose a schema change | [Open an issue](https://github.com/bawbel/bawbel-ave/issues/new?template=schema_change.md) |
| Ask a question | [GitHub Discussions](https://github.com/bawbel/bawbel-ave/discussions) |

**Researcher recognition:** Every accepted AVE record permanently credits the discovering researcher. A $10 thank-you bounty is paid per accepted submission.

---

## Governance

AVE v0.1 is maintained by [Bawbel](https://bawbel.io). The roadmap transfers governance to the neutral **AI Skill Security Foundation (ASSF)** in 2027, ensuring no single organisation controls the standard.

[→ Full governance roadmap](SPEC.md#12-governance)

---

## Repository Structure

```
bawbel-ave/
├── SPEC.md                          # The AVE specification
├── CONTRIBUTING.md                  # How to contribute
├── SECURITY.md                      # Security policy
├── records/
│   ├── TEMPLATE.json                # Copy this to submit a record
│   ├── AVE-2026-00001.json
│   └── AVE-2026-00002.json
└── rules/
    ├── yara/                        # YARA detection rules
    └── semgrep/                     # Semgrep detection rules
```

---

## License

Apache License 2.0 — see [LICENSE](LICENSE)

---

<div align="center">
Maintained by <a href="https://bawbel.io">Bawbel</a> &nbsp;·&nbsp;
<a href="https://twitter.com/bawbel_io">@bawbel_io</a> &nbsp;·&nbsp;
<a href="https://linkedin.com/company/bawbel">LinkedIn</a>
</div>
