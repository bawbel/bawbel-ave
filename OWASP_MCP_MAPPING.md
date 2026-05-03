# AVE — OWASP MCP Top 10 Mapping

**Version:** 1.0  
**AVE Records:** 45  
**OWASP MCP Top 10:** Beta (MCP01:2025–MCP10:2025)  
**Reference:** https://owasp.org/www-project-mcp-top-10/

This document maps all 45 published AVE records to the OWASP MCP Top 10
risk categories. Use this mapping for:

- Enterprise security procurement and compliance sign-off
- Risk prioritisation by OWASP category
- Gap analysis against existing OWASP-aligned controls
- Audit reporting for regulated industries

---

## OWASP MCP Top 10 Categories

| ID | Category | Description |
|---|---|---|
| MCP01 | Token Mismanagement & Secret Exposure | Hard-coded credentials, long-lived tokens, secrets in model memory or logs |
| MCP02 | Privilege Escalation via Scope Creep | Excessive permissions, weak scope enforcement, expanded capabilities over time |
| MCP03 | Tool Poisoning | Malicious instructions injected into tool descriptions, results, or context |
| MCP04 | Software Supply Chain Attacks | Compromised dependencies, tampered packages, rug pull attacks |
| MCP05 | Command Injection & Execution | Untrusted input used to construct shell, SQL, or code execution calls |
| MCP06 | Intent Flow Subversion | Hijacking the agent's goals, overriding instructions, jailbreaking |
| MCP07 | Insufficient Authentication & Authorization | Missing or weak auth on MCP servers, unverified tool calls |
| MCP08 | Lack of Audit & Telemetry | Unlogged tool invocations, missing observability, no alerting |
| MCP09 | Shadow MCP Servers | Unauthorised servers, server impersonation, unverified discovery |
| MCP10 | Context Injection & Over-sharing | Prompt injection via context, cross-session data leakage, RAG poisoning |

---

## Full AVE → OWASP MCP Mapping

| AVE ID | Title | Severity | CVSS-AI | Primary MCP | Secondary MCP |
|---|---|---|---|---|---|
| AVE-2026-00001 | External instruction fetch (metamorphic payload) | CRITICAL | 9.4 | MCP04 | MCP06 |
| AVE-2026-00002 | MCP tool description injection | HIGH | 8.7 | MCP03 | MCP10 |
| AVE-2026-00003 | Credential exfiltration via agent instruction | HIGH | 8.5 | MCP01 | MCP05 |
| AVE-2026-00004 | Shell pipe injection pattern | HIGH | 8.8 | MCP05 | MCP06 |
| AVE-2026-00005 | Destructive command execution | CRITICAL | 9.1 | MCP05 | — |
| AVE-2026-00006 | Cryptocurrency drain attack | CRITICAL | 9.6 | MCP05 | MCP02 |
| AVE-2026-00007 | Goal override instruction | HIGH | 8.1 | MCP06 | — |
| AVE-2026-00008 | Persistence and self-replication | HIGH | 8.4 | MCP05 | MCP04 |
| AVE-2026-00009 | Jailbreak instruction | HIGH | 8.3 | MCP06 | — |
| AVE-2026-00010 | Hidden instruction concealment | HIGH | 7.9 | MCP06 | MCP08 |
| AVE-2026-00011 | Dynamic tool call injection | HIGH | 8.2 | MCP03 | MCP05 |
| AVE-2026-00012 | Permission escalation via false claim | HIGH | 7.8 | MCP02 | MCP07 |
| AVE-2026-00013 | PII exfiltration pattern | HIGH | 8.0 | MCP01 | MCP05 |
| AVE-2026-00014 | Trust escalation — false authority claim | MEDIUM | 6.5 | MCP07 | MCP09 |
| AVE-2026-00015 | System prompt extraction | MEDIUM | 6.2 | MCP10 | MCP08 |
| AVE-2026-00016 | Indirect RAG prompt injection | HIGH | 8.2 | MCP10 | MCP03 |
| AVE-2026-00017 | MCP server impersonation | HIGH | 8.6 | MCP09 | MCP07 |
| AVE-2026-00018 | Tool result manipulation | HIGH | 8.1 | MCP03 | MCP08 |
| AVE-2026-00019 | Agent memory poisoning | CRITICAL | 9.2 | MCP10 | MCP06 |
| AVE-2026-00020 | Cross-agent A2A injection | HIGH | 8.7 | MCP10 | MCP06 |
| AVE-2026-00021 | Autonomous action without confirmation | HIGH | 8.3 | MCP02 | MCP08 |
| AVE-2026-00022 | Scope creep — undeclared resource access | MEDIUM | 6.8 | MCP02 | — |
| AVE-2026-00023 | Context window manipulation | HIGH | 8.0 | MCP10 | MCP06 |
| AVE-2026-00024 | Content type mismatch — supply chain | HIGH | 8.5 | MCP04 | — |
| AVE-2026-00025 | Conversation history injection | HIGH | 8.5 | MCP10 | MCP06 |
| AVE-2026-00026 | Tool output exfiltration encoding | CRITICAL | 9.1 | MCP01 | MCP08 |
| AVE-2026-00027 | Multi-turn attack persistence | HIGH | 8.4 | MCP06 | MCP10 |
| AVE-2026-00028 | File prompt injection | HIGH | 8.3 | MCP10 | MCP03 |
| AVE-2026-00029 | Homoglyph / Unicode obfuscation | HIGH | 8.0 | MCP03 | MCP04 |
| AVE-2026-00030 | Role claim privilege escalation | CRITICAL | 9.0 | MCP07 | MCP02 |
| AVE-2026-00031 | Feedback / training loop poisoning | HIGH | 8.6 | MCP06 | MCP04 |
| AVE-2026-00032 | Network reconnaissance instruction | HIGH | 8.2 | MCP05 | MCP02 |
| AVE-2026-00033 | Unsafe deserialization / eval | CRITICAL | 9.3 | MCP05 | MCP04 |
| AVE-2026-00034 | Supply chain skill import | CRITICAL | 9.2 | MCP04 | MCP03 |
| AVE-2026-00035 | Environment / sensor data manipulation | HIGH | 7.9 | MCP03 | MCP08 |
| AVE-2026-00036 | Lateral movement — pivot to other systems | CRITICAL | 9.4 | MCP05 | MCP02 |
| AVE-2026-00037 | Vision prompt injection via image | HIGH | 8.5 | MCP10 | MCP03 |
| AVE-2026-00038 | Excessive agency — unbounded tool use | HIGH | 8.1 | MCP02 | MCP08 |
| AVE-2026-00039 | Covert channel — steganographic exfil | HIGH | 8.3 | MCP01 | MCP08 |
| AVE-2026-00040 | Insecure output injection (SQLi/XSS/shell) | HIGH | 8.2 | MCP05 | MCP10 |
| AVE-2026-00041 | MCP server-card injection | CRITICAL | 9.3 | MCP03 | MCP09 |
| AVE-2026-00042 | REPL code mode payload injection | CRITICAL | 9.1 | MCP05 | MCP10 |
| AVE-2026-00043 | MCP App UI payload injection | HIGH | 8.4 | MCP10 | MCP03 |
| AVE-2026-00044 | Async task result poisoning | HIGH | 8.6 | MCP10 | MCP06 |
| AVE-2026-00045 | Cross-App-Access escalation | CRITICAL | 9.0 | MCP02 | MCP09 |

---

## AVE Records by OWASP MCP Category

### MCP01 — Token Mismanagement & Secret Exposure (4 records)

| AVE ID | Title | Severity |
|---|---|---|
| AVE-2026-00003 | Credential exfiltration via agent instruction | HIGH 8.5 |
| AVE-2026-00013 | PII exfiltration pattern | HIGH 8.0 |
| AVE-2026-00026 | Tool output exfiltration encoding | CRITICAL 9.1 |
| AVE-2026-00039 | Covert channel — steganographic exfiltration | HIGH 8.3 |

### MCP02 — Privilege Escalation via Scope Creep (7 records)

| AVE ID | Title | Severity |
|---|---|---|
| AVE-2026-00006 | Cryptocurrency drain attack | CRITICAL 9.6 |
| AVE-2026-00012 | Permission escalation via false claim | HIGH 7.8 |
| AVE-2026-00021 | Autonomous action without confirmation | HIGH 8.3 |
| AVE-2026-00022 | Scope creep — undeclared resource access | MEDIUM 6.8 |
| AVE-2026-00030 | Role claim privilege escalation | CRITICAL 9.0 |
| AVE-2026-00038 | Excessive agency — unbounded tool use | HIGH 8.1 |
| AVE-2026-00045 | Cross-App-Access escalation | CRITICAL 9.0 |

### MCP03 — Tool Poisoning (6 records)

| AVE ID | Title | Severity |
|---|---|---|
| AVE-2026-00002 | MCP tool description injection | HIGH 8.7 |
| AVE-2026-00011 | Dynamic tool call injection | HIGH 8.2 |
| AVE-2026-00018 | Tool result manipulation | HIGH 8.1 |
| AVE-2026-00029 | Homoglyph / Unicode obfuscation | HIGH 8.0 |
| AVE-2026-00035 | Environment / sensor data manipulation | HIGH 7.9 |
| AVE-2026-00041 | MCP server-card injection | CRITICAL 9.3 |

### MCP04 — Software Supply Chain Attacks (5 records)

| AVE ID | Title | Severity |
|---|---|---|
| AVE-2026-00001 | External instruction fetch (metamorphic payload) | CRITICAL 9.4 |
| AVE-2026-00008 | Persistence and self-replication | HIGH 8.4 |
| AVE-2026-00024 | Content type mismatch — supply chain | HIGH 8.5 |
| AVE-2026-00033 | Unsafe deserialization / eval | CRITICAL 9.3 |
| AVE-2026-00034 | Supply chain skill import | CRITICAL 9.2 |

### MCP05 — Command Injection & Execution (8 records)

| AVE ID | Title | Severity |
|---|---|---|
| AVE-2026-00004 | Shell pipe injection pattern | HIGH 8.8 |
| AVE-2026-00005 | Destructive command execution | CRITICAL 9.1 |
| AVE-2026-00006 | Cryptocurrency drain attack | CRITICAL 9.6 |
| AVE-2026-00032 | Network reconnaissance instruction | HIGH 8.2 |
| AVE-2026-00033 | Unsafe deserialization / eval | CRITICAL 9.3 |
| AVE-2026-00036 | Lateral movement — pivot to other systems | CRITICAL 9.4 |
| AVE-2026-00040 | Insecure output injection (SQLi/XSS/shell) | HIGH 8.2 |
| AVE-2026-00042 | REPL code mode payload injection | CRITICAL 9.1 |

### MCP06 — Intent Flow Subversion (8 records)

| AVE ID | Title | Severity |
|---|---|---|
| AVE-2026-00007 | Goal override instruction | HIGH 8.1 |
| AVE-2026-00009 | Jailbreak instruction | HIGH 8.3 |
| AVE-2026-00010 | Hidden instruction concealment | HIGH 7.9 |
| AVE-2026-00019 | Agent memory poisoning | CRITICAL 9.2 |
| AVE-2026-00020 | Cross-agent A2A injection | HIGH 8.7 |
| AVE-2026-00023 | Context window manipulation | HIGH 8.0 |
| AVE-2026-00027 | Multi-turn attack persistence | HIGH 8.4 |
| AVE-2026-00031 | Feedback / training loop poisoning | HIGH 8.6 |

### MCP07 — Insufficient Authentication & Authorization (3 records)

| AVE ID | Title | Severity |
|---|---|---|
| AVE-2026-00014 | Trust escalation — false authority claim | MEDIUM 6.5 |
| AVE-2026-00017 | MCP server impersonation | HIGH 8.6 |
| AVE-2026-00030 | Role claim privilege escalation | CRITICAL 9.0 |

### MCP08 — Lack of Audit & Telemetry (4 records)

| AVE ID | Title | Severity |
|---|---|---|
| AVE-2026-00010 | Hidden instruction concealment | HIGH 7.9 |
| AVE-2026-00018 | Tool result manipulation | HIGH 8.1 |
| AVE-2026-00026 | Tool output exfiltration encoding | CRITICAL 9.1 |
| AVE-2026-00039 | Covert channel — steganographic exfiltration | HIGH 8.3 |

### MCP09 — Shadow MCP Servers (3 records)

| AVE ID | Title | Severity |
|---|---|---|
| AVE-2026-00014 | Trust escalation — false authority claim | MEDIUM 6.5 |
| AVE-2026-00017 | MCP server impersonation | HIGH 8.6 |
| AVE-2026-00041 | MCP server-card injection | CRITICAL 9.3 |
| AVE-2026-00045 | Cross-App-Access escalation | CRITICAL 9.0 |

### MCP10 — Context Injection & Over-sharing (9 records)

| AVE ID | Title | Severity |
|---|---|---|
| AVE-2026-00015 | System prompt extraction | MEDIUM 6.2 |
| AVE-2026-00016 | Indirect RAG prompt injection | HIGH 8.2 |
| AVE-2026-00019 | Agent memory poisoning | CRITICAL 9.2 |
| AVE-2026-00020 | Cross-agent A2A injection | HIGH 8.7 |
| AVE-2026-00023 | Context window manipulation | HIGH 8.0 |
| AVE-2026-00025 | Conversation history injection | HIGH 8.5 |
| AVE-2026-00028 | File prompt injection | HIGH 8.3 |
| AVE-2026-00037 | Vision prompt injection via image | HIGH 8.5 |
| AVE-2026-00043 | MCP App UI payload injection | HIGH 8.4 |
| AVE-2026-00044 | Async task result poisoning | HIGH 8.6 |

---

## Coverage by Category

| OWASP MCP | Records | CRITICAL | HIGH | MEDIUM |
|---|---|---|---|---|
| MCP01 — Token & Secret Exposure | 4 | 1 | 3 | 0 |
| MCP02 — Privilege Escalation | 7 | 3 | 3 | 1 |
| MCP03 — Tool Poisoning | 6 | 1 | 5 | 0 |
| MCP04 — Supply Chain | 5 | 3 | 2 | 0 |
| MCP05 — Command Injection | 8 | 5 | 3 | 0 |
| MCP06 — Intent Subversion | 8 | 1 | 7 | 0 |
| MCP07 — Auth & Authorization | 3 | 1 | 1 | 1 |
| MCP08 — Audit & Telemetry | 4 | 1 | 3 | 0 |
| MCP09 — Shadow MCP Servers | 4 | 2 | 1 | 1 |
| MCP10 — Context Injection | 10 | 1 | 8 | 1 |
| **Total** | **45** | **13** | **30** | **2** |

Note: Records with two OWASP mappings appear in both category tables.
The coverage count above uses the primary mapping only.

---

## Bawbel Scanner — OWASP MCP Output

Every `bawbel scan` finding includes an `owasp_mcp` field mapping the
finding to this taxonomy alongside the existing `owasp` (ASI) field:

```json
{
  "rule_id": "bawbel-mcp-tool-poisoning",
  "ave_id": "AVE-2026-00002",
  "severity": "HIGH",
  "cvss_ai": 8.7,
  "owasp": ["ASI01", "ASI03"],
  "owasp_mcp": ["MCP03", "MCP10"]
}
```

Use this for compliance reporting, audit trails, and OWASP-aligned
risk dashboards.

---

## References

- OWASP MCP Top 10: https://owasp.org/www-project-mcp-top-10/
- OWASP MCP Top 10 GitHub: https://github.com/OWASP/www-project-mcp-top-10
- AVE Standard: https://github.com/bawbel/bawbel-ave
- PiranhaDB API: https://api.piranha.bawbel.io
- Bawbel Scanner: https://github.com/bawbel/bawbel-scanner