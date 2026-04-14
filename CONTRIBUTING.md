# Contributing to AVE

Thank you for helping make AI agents safer. Every AVE record you submit protects developers who install agentic components without knowing what they contain.

## Ways to Contribute

| Type | How |
|---|---|
| 🛡️ Submit an AVE record | [Pull request](#submitting-an-ave-record) or email |
| 🐛 Report a false positive | [Open an issue](https://github.com/bawbel/bawbel-ave/issues/new?template=false_positive.md) |
| 📐 Propose a schema change | [Open an issue](https://github.com/bawbel/bawbel-ave/issues/new?template=schema_change.md) |
| 🔍 Add a detection rule | Pull request to `rules/` |
| 📝 Fix documentation | Pull request to any `.md` file |
| 💬 Ask a question | [GitHub Discussions](https://github.com/bawbel/bawbel-ave/discussions) |

---

## Submitting an AVE Record

### Step 1 — Verify scope

The vulnerability must be in an **agentic component** — skill, MCP server, system prompt, plugin, A2A protocol, RAG knowledge base, or model. Traditional code vulnerabilities in the software that powers agents belong in CVE/NVD.

### Step 2 — Responsible disclosure

If the vulnerability affects a specific named publisher or product:

1. Contact the publisher privately with full technical details
2. Allow **14 days** for acknowledgment
3. Allow **90 days** for remediation before public disclosure
4. If the publisher is unresponsive after 14 days, or the component is clearly malicious with no legitimate use, proceed to submission

For **Critical severity** (CVSS-AI 9.0+) with active exploitation: 14-day total disclosure timeline.

### Step 3 — Prepare your record

```bash
# Fork this repo, then:
git checkout -b ave/brief-description-of-vulnerability
cp records/TEMPLATE.json records/AVE-PENDING.json
# Fill in all required fields
```

**Required fields:** `component_type`, `title`, `attack_class`, `description`,
`affected_platforms`, `cvss_ai_score`, `cvss_ai_vector`, `owasp_mapping`,
`behavioral_fingerprint`, `detection_methodology`, `indicators_of_compromise`,
`remediation`, `status`, `researcher`

See [SPEC.md Section 5](SPEC.md#5-record-schema) for field definitions and the attack class taxonomy.

### Step 4 — Open a pull request

- **Branch:** `ave/brief-description` → target `main`
- **Title:** `[AVE Submission] Brief description of vulnerability`
- Fill in the PR template — it appears automatically

### Step 5 — Review timeline

| Stage | Timeline |
|---|---|
| Acknowledgment | 48 hours |
| Technical review | 7 days |
| Publication | 14 days |
| Researcher credit | Permanent |

### Researcher recognition

Every accepted submission earns:
- 💰 **Cash bounty** — $10 USD per accepted record (paid via PayPal)
- 📛 **Permanent credit** — your name on the published record forever
- 🎁 **Bawbel Pro** — free account for the lifetime of the product
- 📢 **Featured spotlight** — monthly researcher highlight in the Bawbel threat report

---

## Schema Changes

**Additive changes** (new optional fields): standard PR review, no waiting period.

**Breaking changes** (removing or renaming fields):
1. Open an issue with the `schema-change` label
2. 30-day community comment period
3. Maintainer approval required
4. Schema version bump required
5. Existing records updated if needed

---

## Detection Rules

YARA rules → `rules/yara/`
Semgrep rules → `rules/semgrep/`

Each rule file must include:
- The AVE record(s) it detects (or `AVE-PENDING` if new)
- A brief description comment at the top
- At least one test case in `rules/tests/`

---

## Branching Convention

| Branch prefix | Use case |
|---|---|
| `ave/` | New AVE record submission |
| `fix/` | Correction to existing record |
| `schema/` | Schema change |
| `docs/` | Documentation only |
| `rule/` | New YARA or Semgrep rule |

---

## Code of Conduct

- Be respectful — disagree on technical grounds, not personal ones
- Credit others accurately — do not claim discoveries that are not yours
- Act in good faith — this standard exists to protect developers and users
- Security research involves difficult topics — approach them professionally

---

## Contact

| Purpose | Contact |
|---|---|
| AVE submission | bawbel.io@gmail.com — subject: `AVE Submission: [title]` |
| Critical disclosure | bawbel.io@gmail.com — subject: `AVE CRITICAL: [title]` |
| General questions | [GitHub Discussions](https://github.com/bawbel/bawbel-ave/discussions) |
