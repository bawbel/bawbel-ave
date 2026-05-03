<div align="center">

# AVE — Agentic Vulnerability Enumeration

**The open standard for tracking vulnerabilities in AI agent components**

[![License](https://img.shields.io/badge/License-Apache_2.0-teal.svg)](LICENSE)
[![Schema Version](https://img.shields.io/badge/Schema-v0.1.0-green.svg)](SPEC.md)
[![Records](https://img.shields.io/badge/AVE_Records-45-blue.svg)](records/)
[![Contributions Welcome](https://img.shields.io/badge/Contributions-Welcome-brightgreen.svg)](CONTRIBUTING.md)

[Read the Spec](SPEC.md) &nbsp;·&nbsp; [Browse Records](records/) &nbsp;·&nbsp; [Submit an AVE](CONTRIBUTING.md) &nbsp;·&nbsp; [bawbel.io](https://bawbel.io)

</div>

---

## What is AVE?

AVE (Agentic Vulnerability Enumeration) is the open numbering system for vulnerabilities in **agentic AI components** — the skills, MCP servers, system prompts, plugins, and protocols that define what an AI agent can do and how it behaves.

Think of it as **CVE for AI agents** — but purpose-built for the behavioral, probabilistic nature of agentic vulnerabilities that CVE was never designed to handle.

```
AVE-2026-00001   Metamorphic payload via external config fetch in SKILL.md       [CRITICAL 9.4]
AVE-2026-00002   Prompt injection via malicious MCP tool description field        [HIGH 8.7]
AVE-2026-00041   MCP server-card injection before agent makes first call          [CRITICAL 9.3]
AVE-2026-00045   Cross-App-Access escalation via shared agent session             [CRITICAL 9.0]
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

## Published Records

**45 records across 12 attack classes.** All records are in `records/` and queryable via [PiranhaDB](https://api.piranha.bawbel.io).

| Attack Class | Records | Severity | AVE IDs |
|---|---|---|---|
| Prompt Injection — Goal Hijack | 3 | HIGH | 00007, 00009, 00010 |
| Prompt Injection — External Fetch | 1 | CRITICAL | 00001 |
| Prompt Injection — RAG | 1 | HIGH | 00016 |
| Prompt Injection — Server-Card | 1 | CRITICAL | 00041 |
| Prompt Injection — REPL Code Mode | 1 | CRITICAL | 00042 |
| Prompt Injection — UI Payload | 1 | HIGH | 00043 |
| MCP — Tool Poisoning | 2 | HIGH | 00002, 00017 |
| Data Exfiltration | 5 | HIGH–CRITICAL | 00003, 00013, 00026, 00034, 00039 |
| Privilege Escalation | 4 | CRITICAL | 00012, 00030, 00036, 00045 |
| Persistence & Replication | 3 | HIGH–CRITICAL | 00008, 00019, 00027 |
| Async & A2A Injection | 3 | HIGH | 00020, 00044, 00025 |
| Tool Abuse & Destruction | 6 | HIGH–CRITICAL | 00004, 00005, 00011, 00021, 00038, 00040 |

**Severity breakdown:** CRITICAL: 13 · HIGH: 30 · MEDIUM: 2

**New in v1.1.0 — MCP 2026 attack surface (AVE-2026-00041 to 00045):**

| AVE ID | Title | CVSS-AI |
|---|---|---|
| AVE-2026-00041 | MCP Server-Card Injection | CRITICAL 9.3 |
| AVE-2026-00042 | REPL Code Mode Payload Injection | CRITICAL 9.1 |
| AVE-2026-00043 | MCP App UI Payload Injection | HIGH 8.4 |
| AVE-2026-00044 | Async Task Result Poisoning | HIGH 8.6 |
| AVE-2026-00045 | Cross-App-Access Escalation | CRITICAL 9.0 |

---

## Component Types Covered

| `component_type` | Examples | Primary Threats |
|---|---|---|
| `skill` | SKILL.md, .cursorrules, CLAUDE.md | Prompt injection, goal hijack, metamorphic payloads |
| `mcp-server-card` | `.well-known/mcp.json`, server-card manifests | Server-card injection, tool poisoning at discovery |
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
records/AVE-2026-00041.json
```

**Scan your skills with Bawbel:**
```bash
pip install bawbel-scanner
bawbel scan ./my-skill.md

# Scan an MCP server-card before connecting
bawbel scan-server-card https://api.example.com

# Pin skill files and detect rug pulls
bawbel pin ./skills/
bawbel check-pins ./skills/
```

**Query the PiranhaDB API:**
```bash
# Get a record
curl https://api.piranha.bawbel.io/records/AVE-2026-00041

# Get all records
curl https://api.piranha.bawbel.io/records

# Ecosystem stats
curl https://api.piranha.bawbel.io/stats
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
│   ├── AVE-2026-00001.json          # Metamorphic payload — external fetch
│   ├── AVE-2026-00002.json          # MCP tool description injection
│   ├── ...                          # AVE-2026-00003 to AVE-2026-00040
│   ├── AVE-2026-00041.json          # MCP server-card injection      [NEW]
│   ├── AVE-2026-00042.json          # REPL code mode payload         [NEW]
│   ├── AVE-2026-00043.json          # MCP App UI payload injection   [NEW]
│   ├── AVE-2026-00044.json          # Async task result poisoning    [NEW]
│   └── AVE-2026-00045.json          # Cross-App-Access escalation    [NEW]
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