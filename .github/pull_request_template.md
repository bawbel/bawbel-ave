## Type of Change

- [ ] 🛡️ New AVE record submission
- [ ] 🔧 Update to existing AVE record
- [ ] 📐 Schema change
- [ ] 🔍 New detection rule (YARA / Semgrep)
- [ ] 📝 Documentation improvement
- [ ] 🐛 Bug fix
- [ ] Other:

---

## Description

<!-- What does this PR do? For AVE submissions, summarise the vulnerability in 2–3 sentences. -->

---

## AVE Record(s)

<!-- List AVE IDs. Use AVE-PENDING for new submissions — we assign the ID on merge. -->

---

## Checklist

### For AVE record submissions
- [ ] Record file is in `records/AVE-PENDING.json`
- [ ] All required fields are present (see SPEC.md Section 5)
- [ ] `behavioral_fingerprint` is clear and actionable
- [ ] `detection_methodology` is specific and reproducible
- [ ] `indicators_of_compromise` has at least 2 entries
- [ ] `owasp_mapping` references valid ASI identifiers (ASI01–ASI10)
- [ ] `cvss_ai_score` is justified in the PR description
- [ ] Responsible disclosure process followed (see CONTRIBUTING.md)
- [ ] `researcher` field contains my correct name and attribution

### For schema changes
- [ ] Issue opened with `schema-change` label
- [ ] 30-day comment period completed (breaking changes only)
- [ ] `SPEC.md` updated
- [ ] `records/TEMPLATE.json` updated
- [ ] Existing records updated where required

### For all PRs
- [ ] I have read [CONTRIBUTING.md](CONTRIBUTING.md)
- [ ] My changes follow the existing style and format
- [ ] I agree to license my contribution under Apache 2.0
