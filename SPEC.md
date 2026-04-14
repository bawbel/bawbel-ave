# AVE — Agentic Vulnerability Enumeration

**The open standard for tracking vulnerabilities in AI agent components.**

> Version: 0.1.0 — Draft  
> Status: Active Development  
> Maintainer: [Bawbel](https://bawbel.io) · [github.com/bawbel](https://github.com/bawbel)  
> License: Apache 2.0

---

## Table of Contents

1. [What is AVE?](#1-what-is-ave)
2. [Why AVE and not CVE?](#2-why-ave-and-not-cve)
3. [Scope — What AVE Covers](#3-scope--what-ave-covers)
4. [AVE ID Format](#4-ave-id-format)
5. [Record Schema](#5-record-schema)
6. [CVSS-AI Scoring](#6-cvss-ai-scoring)
7. [OWASP Agentic AI Mapping](#7-owasp-agentic-ai-mapping)
8. [NIST AI RMF Mapping](#8-nist-ai-rmf-mapping)
9. [Example Records](#9-example-records)
10. [How to Submit an AVE Record](#10-how-to-submit-an-ave-record)
11. [Disclosure Policy](#11-disclosure-policy)
12. [Governance](#12-governance)
13. [Contributing](#13-contributing)

---

## 1. What is AVE?

AVE (Agentic Vulnerability Enumeration) is an open numbering system for vulnerabilities found in **agentic AI components** — the files, servers, prompts, and protocols that define what an AI agent can do and how it behaves.

AVE records are the operational intelligence layer for AI agent security. Each record describes:

- **What** the vulnerability is (attack class, behavioral description)
- **Where** it appears (component type, affected registries)
- **How dangerous** it is (CVSS-AI score, agentic impact dimensions)
- **How to find it** (behavioral fingerprint, detection methodology)
- **How it maps** to established frameworks (OWASP, NIST, MITRE ATLAS)

AVE is maintained by [Bawbel](https://bawbel.io) and powered by [PiranhaDB](https://bawbel.io) — the first global behavioral threat intelligence database for agentic AI components. The specification is open. Any tool can implement it. Any researcher can submit records.

---

## 2. Why AVE and not CVE?

CVE (Common Vulnerabilities and Exposures) was designed in 1999 for deterministic software flaws — buffer overflows, SQL injection, use-after-free. It works exceptionally well for that problem. AVE is not a replacement for CVE. It covers a fundamentally different attack surface.

| Dimension | CVE | AVE |
|---|---|---|
| **Vulnerability type** | Deterministic code flaw | Behavioral, probabilistic, natural language |
| **Subject** | Specific software version | Agentic component (any format, any platform) |
| **Reproducibility** | Exact reproduction required | Behavioral pattern matching |
| **Patching model** | Vendor issues patched version | Component removed, replaced, or behavioral policy applied |
| **Mutation tracking** | One CVE per instance | One AVE record covers all behavioral variants |
| **Scoring** | CVSS (network, auth, impact) | CVSS-AI (adds agentic scope, human oversight, tool access) |
| **Disclosure target** | Software vendor | Registry operator, platform maintainer, or community |
| **Processing speed** | Days to months | Near real-time via PiranhaDB |
| **Coverage** | Code vulnerabilities only | Skills, MCP servers, prompts, plugins, A2A protocols, RAG, models |

**If a SKILL.md file contains a traditional RCE in embedded Python code, that gets a CVE.** The natural language prompt injection instruction in the same SKILL.md that hijacks the agent's goals — that gets an AVE. Both systems are necessary. They cover different layers.

---

## 3. Scope — What AVE Covers

AVE covers every type of **agentic component** — any artifact that defines an AI agent's capabilities, behavior, or permissions.

| Component Type | `component_type` value | Examples | Primary Attack Classes |
|---|---|---|---|
| Skill files | `skill` | SKILL.md, .cursorrules, CLAUDE.md, Codex skills | Prompt injection, goal hijack, shadow permissions, metamorphic payloads |
| MCP servers | `mcp` | Any MCP-compatible server manifest | Tool poisoning, unauthorized execution, SQL injection via MCP, MPMA |
| System prompts | `prompt` | LLM deployment instructions | Jailbreaking, safety bypass, PII leakage, instruction injection |
| Agent plugins | `plugin` | Copilot plugins, AgentForce skills, Bedrock agents | Supply chain poisoning, capability escalation, exfiltration |
| A2A protocols | `a2a` | Google A2A handlers, Anthropic multi-agent configs | Transitive trust exploitation, agent impersonation, lateral movement |
| RAG knowledge bases | `rag` | LlamaIndex, LangChain, Bedrock KB sources | Data poisoning, indirect prompt injection, exfiltration via retrieval |
| Fine-tuned models | `model` | Hugging Face models, Azure AI, Vertex AI | Model poisoning, backdoor triggers, capability manipulation |

**Out of scope for AVE:**
- Traditional code vulnerabilities in software that powers agents (use CVE)
- Model alignment failures not caused by deliberate adversarial input (use ML safety frameworks)
- Privacy violations not arising from agentic component behavior (use applicable privacy frameworks)

---

## 4. AVE ID Format

```
AVE-{YEAR}-{SEQUENCE}
```

**Examples:**
```
AVE-2026-00001
AVE-2026-00142
AVE-2026-01000
```

- `YEAR` — four-digit year of first public disclosure
- `SEQUENCE` — five-digit zero-padded sequence number, assigned by PiranhaDB on publication
- IDs are **permanent and immutable** — once assigned, an AVE ID never changes, even if the record is later disputed or marked false positive
- Sequence numbers are assigned in order of publication, not order of discovery

---

## 5. Record Schema

Every AVE record is a JSON document conforming to this schema. All fields marked **required** must be present for a record to be published.

```json
{
  "ave_id": "AVE-2026-00001",
  "schema_version": "0.1.0",
  "component_type": "skill",
  "title": "Prompt injection via deceptive tool description in SKILL.md",
  "attack_class": "Prompt Injection — Goal Hijack",
  "description": "...",
  "affected_platforms": ["claude-code", "cursor", "codex"],
  "affected_registries": ["clawhub.io", "agentskills.io"],
  "cvss_ai_score": 9.1,
  "cvss_ai_vector": "CVSS:4.0/AV:N/AC:L/AT:P/PR:N/UI:N/VC:H/VI:H/VA:N/SC:H/SI:H/SA:N",
  "owasp_mapping": ["ASI01", "ASI04"],
  "nist_ai_rmf_mapping": ["GOVERN-1.1", "MAP-1.5", "MEASURE-2.5"],
  "mitre_atlas_mapping": ["AML.T0054", "AML.T0049"],
  "behavioral_fingerprint": "Natural language instruction that overrides stated agent goals, directing tool use toward attacker-controlled endpoints.",
  "behavioral_vector": [0.82, -0.14, 0.67],
  "mutation_count": 47,
  "detection_methodology": "Semantic analysis of tool description fields for goal-override language. Static scan for hardcoded egress targets in skill instructions.",
  "indicators_of_compromise": [
    "Tool description contains imperative override language ('always', 'regardless of', 'ignore previous')",
    "Egress URL not declared in A-BOM network manifest",
    "Tool description length disproportionate to stated purpose"
  ],
  "remediation": "Remove or sandbox the skill. Audit all skills from the same publisher. Apply A-BOM network policy to block undeclared egress.",
  "status": "active",
  "kill_switch_active": true,
  "researcher": "Researcher Name, Organization",
  "researcher_url": "https://example.com",
  "published": "2026-04-14T08:00:00Z",
  "last_updated": "2026-04-14T08:00:00Z",
  "references": [
    "https://owasp.org/www-project-top-10-for-large-language-model-applications/",
    "https://bawbel.io/ave/AVE-2026-00001"
  ]
}
```

### Field Definitions

| Field | Type | Required | Description |
|---|---|---|---|
| `ave_id` | string | ✓ | Unique identifier in AVE-YYYY-NNNNN format |
| `schema_version` | string | ✓ | AVE schema version used for this record |
| `component_type` | enum | ✓ | One of: `skill`, `mcp`, `prompt`, `plugin`, `a2a`, `rag`, `model` |
| `title` | string | ✓ | Concise human-readable title, max 120 characters |
| `attack_class` | string | ✓ | Primary attack classification (see Attack Class Taxonomy below) |
| `description` | string | ✓ | Full behavioral description. Must be reproducible by a third party |
| `affected_platforms` | array | ✓ | Platforms where vulnerable component can execute |
| `affected_registries` | array | — | Known registries where variants have appeared |
| `cvss_ai_score` | float | ✓ | CVSS-AI numeric score 0.0–10.0 |
| `cvss_ai_vector` | string | ✓ | Full CVSS-AI vector string |
| `owasp_mapping` | array | ✓ | OWASP Agentic AI Top 10 identifiers (ASI01–ASI10) |
| `nist_ai_rmf_mapping` | array | — | NIST AI RMF function and subcategory references |
| `mitre_atlas_mapping` | array | — | MITRE ATLAS technique identifiers |
| `behavioral_fingerprint` | string | ✓ | Plain-language description of the behavioral pattern |
| `behavioral_vector` | array | — | PiranhaDB pgvector embedding (auto-generated on submission) |
| `mutation_count` | integer | — | Number of confirmed variants matching this behavioral fingerprint |
| `detection_methodology` | string | ✓ | How to detect this vulnerability. Must be actionable |
| `indicators_of_compromise` | array | ✓ | Specific observable signals that indicate this vulnerability |
| `remediation` | string | ✓ | What to do when this vulnerability is found |
| `status` | enum | ✓ | One of: `active`, `patched`, `disputed`, `false_positive` |
| `kill_switch_active` | boolean | — | If true, Bawbel Registry blocks downloads of matching components |
| `researcher` | string | ✓ | Full name and organization of discovering researcher — permanent credit |
| `researcher_url` | string | — | Researcher's profile or publication URL |
| `published` | datetime | ✓ | ISO 8601 UTC timestamp of first public disclosure |
| `last_updated` | datetime | ✓ | ISO 8601 UTC timestamp of most recent update |
| `references` | array | — | External references, advisories, related publications |

### Attack Class Taxonomy

| Attack Class | Description |
|---|---|
| `Prompt Injection — Goal Hijack` | Instructions that override the agent's stated goals |
| `Prompt Injection — Data Exfiltration` | Instructions that cause the agent to transmit sensitive data |
| `Prompt Injection — Tool Abuse` | Instructions that misuse available tools for unauthorized purposes |
| `Prompt Injection — Indirect` | Malicious instructions delivered via retrieved content (RAG, web) |
| `Tool Poisoning — Description Manipulation` | Malicious content hidden in MCP tool descriptions |
| `Tool Poisoning — Schema Injection` | Malicious content embedded in tool input schema definitions |
| `Shadow Permission Escalation` | Instructions that cause the agent to claim or exercise undeclared permissions |
| `Metamorphic Payload` | Skills that fetch and execute external instructions at runtime |
| `Supply Chain Substitution` | Malicious component published under a trusted name |
| `Transitive Trust Exploitation` | Abuse of agent-to-agent trust relationships |
| `Agent Impersonation` | Component that causes an agent to misrepresent its identity |
| `Model Backdoor` | Trigger-based behavior modification in fine-tuned model weights |
| `Training Data Poisoning` | Adversarial data injected during model training |
| `RAG Poisoning` | Malicious content injected into retrieval knowledge bases |
| `Safety Bypass` | Instructions designed to circumvent safety guardrails |

---

## 6. CVSS-AI Scoring

AVE uses an extended CVSS 4.0 scoring model with additional agentic dimensions. Standard CVSS 4.0 metrics apply with the following agentic extensions:

### Agentic Scoring Dimensions

| Dimension | Symbol | Values | Description |
|---|---|---|---|
| **Agentic Scope** | `AS` | `Isolated \| Collaborative \| Autonomous` | Degree of agent independence |
| **Human Oversight** | `HO` | `Full \| Partial \| None` | Level of human review before actions execute |
| **Tool Access** | `TA` | `None \| Read \| Write \| Execute \| All` | Highest permission level of available tools |
| **Persistence** | `PE` | `Session \| Persistent \| Propagating` | Whether malicious behavior persists across sessions |
| **Real-World Action** | `RW` | `Logical \| Physical` | Whether agent can affect physical systems |

### Score Interpretation

| Score | Severity | Recommended Action |
|---|---|---|
| 9.0–10.0 | **Critical** | Immediate kill switch. Block all downloads. Emergency disclosure |
| 7.0–8.9 | **High** | Kill switch recommended. Coordinated disclosure within 7 days |
| 4.0–6.9 | **Medium** | Coordinated disclosure within 30 days |
| 0.1–3.9 | **Low** | Standard disclosure timeline |
| 0.0 | **Informational** | No immediate risk. Published for awareness |

---

## 7. OWASP Agentic AI Mapping

Every AVE record must map to one or more entries from the [OWASP Agentic AI Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/).

| ID | Name | Common AVE Attack Classes |
|---|---|---|
| ASI01 | Prompt Injection | Prompt Injection (all variants) |
| ASI02 | Insecure Output Handling | Data Exfiltration, Tool Abuse |
| ASI03 | Training Data Poisoning | Training Data Poisoning, RAG Poisoning |
| ASI04 | Model Denial of Service | Tool Abuse (resource exhaustion) |
| ASI05 | Supply Chain Vulnerabilities | Supply Chain Substitution |
| ASI06 | Sensitive Information Disclosure | Data Exfiltration, Shadow Permission Escalation |
| ASI07 | Insecure Plugin Design | Tool Poisoning (all variants) |
| ASI08 | Excessive Agency | Shadow Permission Escalation, Metamorphic Payload |
| ASI09 | Overreliance | Safety Bypass |
| ASI10 | Model Theft | Model Backdoor |

---

## 8. NIST AI RMF Mapping

AVE records optionally map to the [NIST AI Risk Management Framework](https://www.nist.gov/system/files/documents/2023/01/26/AI%20RMF%201.0.pdf) using the format `FUNCTION-SUBCATEGORY`.

| Function | Relevant AVE Scenarios |
|---|---|
| `GOVERN` | Policies governing agent component sourcing and verification |
| `MAP` | Identifying agentic component attack surfaces in AI system design |
| `MEASURE` | Scanning and scoring agentic components against AVE database |
| `MANAGE` | Responding to AVE findings — kill switch, remediation, monitoring |

**Example mappings:**

```
GOVERN-1.1  — AI risk policies include agentic component security requirements
GOVERN-6.1  — Third-party AI component risks are managed
MAP-1.5     — Likelihood of harm from each AI component is assessed
MAP-5.1     — Practices for detecting emergent behaviors are established
MEASURE-2.5 — AI system behavior is monitored for unexpected outputs
MANAGE-1.3  — Responses to AI risks are prioritized by impact
MANAGE-3.1  — AI risks are tracked in a risk register
```

---

## 9. Example Records

### AVE-2026-00001 — Metamorphic Payload via External Config Fetch

```json
{
  "ave_id": "AVE-2026-00001",
  "schema_version": "0.1.0",
  "component_type": "skill",
  "title": "Metamorphic payload via external configuration fetch in SKILL.md",
  "attack_class": "Metamorphic Payload",
  "description": "A SKILL.md file instructs the agent to fetch its operating instructions from an external URL at runtime (e.g., rentry.co, pastebin.com, or attacker-controlled domains). The skill file itself appears benign on static analysis. The actual malicious instructions are hosted externally and can be changed by the attacker at any time without modifying the skill file. This allows the attacker to deliver prompt injection, data exfiltration, or goal hijack instructions to any agent that has installed the skill, with zero changes to the distributed artifact.",
  "affected_platforms": ["claude-code", "cursor", "codex", "any-skill-compatible-agent"],
  "affected_registries": ["clawhub.io", "agentskills.io", "github.com/topics/agent-skills"],
  "cvss_ai_score": 9.4,
  "cvss_ai_vector": "CVSS:4.0/AV:N/AC:L/AT:P/PR:N/UI:N/VC:H/VI:H/VA:L/SC:H/SI:H/SA:L",
  "owasp_mapping": ["ASI01", "ASI08"],
  "nist_ai_rmf_mapping": ["MAP-1.5", "MEASURE-2.5", "MANAGE-1.3"],
  "mitre_atlas_mapping": ["AML.T0054"],
  "behavioral_fingerprint": "Skill file contains instruction to fetch content from an external URL and treat that content as operating instructions or commands.",
  "mutation_count": 89,
  "detection_methodology": "Static scan for URL fetch instructions in skill files (fetch, curl, wget, http.get patterns). Semantic analysis of instructions that reference external configuration sources. Behavioral sandbox: monitor network egress during skill initialization.",
  "indicators_of_compromise": [
    "Skill contains fetch/curl/wget calls in setup or initialization instructions",
    "Skill references external URL as 'configuration', 'instructions', or 'rules' source",
    "Network egress to non-declared domain during agent startup",
    "Skill behavior changes between sandbox runs without file modification"
  ],
  "remediation": "Remove the skill immediately. Audit all skills from the same publisher. Block all egress to the referenced external domains. Check agent logs for any actions taken while skill was active.",
  "status": "active",
  "kill_switch_active": true,
  "researcher": "Bawbel Security Research Team",
  "researcher_url": "https://bawbel.io",
  "published": "2026-04-14T08:00:00Z",
  "last_updated": "2026-04-14T08:00:00Z",
  "references": [
    "https://owasp.org/www-project-top-10-for-large-language-model-applications/",
    "https://bawbel.io/ave/AVE-2026-00001"
  ]
}
```

---

### AVE-2026-00002 — MCP Tool Description Prompt Injection

```json
{
  "ave_id": "AVE-2026-00002",
  "schema_version": "0.1.0",
  "component_type": "mcp",
  "title": "Prompt injection via malicious MCP tool description field",
  "attack_class": "Tool Poisoning — Description Manipulation",
  "description": "An MCP server exposes tools whose description fields contain hidden prompt injection instructions. When an LLM reads the tool manifest to understand available tools, it also ingests the injected instructions embedded in the description text. These instructions can override the agent's current task, redirect output to attacker-controlled destinations, or cause the agent to invoke other tools with attacker-specified parameters. Because tool descriptions are read automatically during agent initialization, the injection executes without any user interaction.",
  "affected_platforms": ["claude-code", "cursor", "any-mcp-compatible-agent"],
  "affected_registries": ["github.com/topics/mcp-server", "mcp.so"],
  "cvss_ai_score": 8.7,
  "cvss_ai_vector": "CVSS:4.0/AV:N/AC:L/AT:N/PR:N/UI:N/VC:H/VI:H/VA:N/SC:H/SI:H/SA:N",
  "owasp_mapping": ["ASI01", "ASI07"],
  "nist_ai_rmf_mapping": ["MAP-1.5", "MEASURE-2.5", "MANAGE-3.1"],
  "mitre_atlas_mapping": ["AML.T0054", "AML.T0049"],
  "behavioral_fingerprint": "MCP tool description field contains natural language instructions addressed to the LLM rather than — or in addition to — a functional description of the tool's purpose.",
  "mutation_count": 34,
  "detection_methodology": "Parse MCP server manifest and apply semantic analysis to tool description fields. Flag descriptions that contain imperative instructions addressed to an AI model, override language, or references to other tools or external destinations.",
  "indicators_of_compromise": [
    "Tool description contains second-person imperative language ('you should', 'always', 'ignore', 'instead')",
    "Tool description length significantly exceeds functional description needs",
    "Tool description references other tool names or agent behaviors",
    "Tool description contains conditional instructions ('if the user asks X, do Y')"
  ],
  "remediation": "Disconnect and remove the MCP server. Review all tool calls made while the server was active. Audit the MCP server publisher for other affected servers.",
  "status": "active",
  "kill_switch_active": false,
  "researcher": "Bawbel Security Research Team",
  "researcher_url": "https://bawbel.io",
  "published": "2026-04-14T08:00:00Z",
  "last_updated": "2026-04-14T08:00:00Z",
  "references": [
    "https://owasp.org/www-project-top-10-for-large-language-model-applications/",
    "https://bawbel.io/ave/AVE-2026-00002"
  ]
}
```

---

## 10. How to Submit an AVE Record

### Step 1 — Verify it is in scope

Check [Section 3](#3-scope--what-ave-covers). The vulnerability must exist in an agentic component (skill, MCP server, system prompt, plugin, A2A protocol, RAG knowledge base, or model). Traditional code vulnerabilities in the software running agents should be reported to CVE/NVD.

### Step 2 — Responsible disclosure first

If the vulnerability affects a specific named product or publisher:

1. Contact the publisher directly with full details
2. Allow **14 days** for acknowledgment and **90 days** for remediation before public disclosure
3. If the publisher is unresponsive or the component is clearly malicious with no legitimate use, proceed directly to submission

### Step 3 — Prepare your record

Create a JSON file following the [Record Schema](#5-record-schema). Required fields: `component_type`, `title`, `attack_class`, `description`, `affected_platforms`, `cvss_ai_score`, `cvss_ai_vector`, `owasp_mapping`, `behavioral_fingerprint`, `detection_methodology`, `indicators_of_compromise`, `remediation`, `status`, `researcher`.

### Step 4 — Submit

Open a pull request to this repository with your record file:

```
records/
  AVE-2026-XXXXX.json    ← your record (use XXXXX as placeholder, we assign the ID)
```

Or email: **ave-submissions@bawbel.io** with subject line `AVE Submission: [brief title]`

### Step 5 — Review process

| Stage | Timeline | Description |
|---|---|---|
| Acknowledgment | 48 hours | We confirm receipt and assign a provisional ID |
| Technical review | 7 days | We verify reproducibility and scoring |
| Publication | 14 days | Record published to PiranhaDB and this repository |
| Credit | Permanent | Your name appears on the record forever |

### Researcher Recognition

Every accepted AVE record permanently credits the discovering researcher by name. Records submitted through the official portal are eligible for:

- **Cash bounty**: $100–$500 USD per accepted record (severity-dependent)
- **Permanent attribution**: your name on the published record
- **Bawbel Pro account**: free for the lifetime of the product
- **Featured researcher**: monthly spotlight in the Bawbel threat report

---

## 11. Disclosure Policy

Bawbel follows **coordinated disclosure** for all AVE records.

**For component publishers:**
- We notify you before publication when a named publisher is identified
- Standard timeline: 90 days from notification to public disclosure
- Critical severity (9.0+): 14 days — due to active exploitation risk
- Unresponsive publishers after 14 days of notification: disclosure proceeds

**For registry operators:**
- We notify registry operators simultaneously with publishers
- Registry operators are encouraged to quarantine affected components during the disclosure window
- Kill switch activation is coordinated with registries for Critical severity records

**For the community:**
- All published AVE records are freely accessible in this repository and via the PiranhaDB API
- Records are published in full — no redacted or partial disclosures
- Disputed records are marked `disputed` and remain published with the dispute noted

---

## 12. Governance

AVE v0.1 is maintained by [Bawbel](https://bawbel.io).

**Roadmap to neutral governance:**

| Phase | Timeline | Governance state |
|---|---|---|
| Phase 1 — Build | 2026 | Bawbel-owned. Spec on GitHub, open PRs accepted |
| Phase 2 — Coalition | 2027 | AI Skill Security Foundation (ASSF) formed. Spec transferred to ASSF |
| Phase 3 — Standard | 2028 | ASSF governs AVE. Multiple certified AVE scanners. Bawbel is one implementer |
| Phase 4 — Infrastructure | 2029+ | AVE is de facto global standard. ASSF 50+ member organisations |

The ASSF will be a neutral nonprofit with a multi-stakeholder governing board including representatives from academia, enterprise security vendors, AI platform companies, and government or regulatory bodies. No single organization — including Bawbel — will hold a majority on the board.

---

## 13. Contributing

We welcome contributions of all kinds.

**Ways to contribute:**

- Submit an AVE record (see [Section 10](#10-how-to-submit-an-ave-record))
- Improve the schema — open an issue or PR with proposed field changes
- Add detection rules — YARA rules, Semgrep patterns, or behavioral signatures
- Improve documentation — corrections, clarifications, translations
- Review open PRs — security expertise from any background is welcome

**Schema changes:**

Breaking changes to the schema (removing or renaming fields) require a schema version bump and a 30-day comment period before merging. Additive changes (new optional fields) can merge with standard PR review.

**Code of conduct:**

All contributors are expected to treat each other with respect. Security research involves difficult topics — disagree on technical grounds, not personal ones. We are all trying to make AI agents safer.

---

## Contact

| Purpose | Contact |
|---|---|
| AVE record submission | ave-submissions@bawbel.io |
| Urgent / critical disclosure | security@bawbel.io |
| General questions | hello@bawbel.io |
| Schema and governance | github.com/bawbel/bawbel-ave/issues |

---

*AVE — Agentic Vulnerability Enumeration*  
*Maintained by [Bawbel](https://bawbel.io) · [github.com/bawbel](https://github.com/bawbel)*  
*Apache License 2.0*
