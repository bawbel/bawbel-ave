---
name: "📐 Schema Change Proposal"
about: Propose a change to the AVE record schema
title: "[Schema] "
labels: schema-change
assignees: ''
---

## Change Type

- [ ] **Breaking change** — removing or renaming a field (requires 30-day comment period)
- [ ] **Additive change** — new optional field (standard PR review)

---

## Proposed Change

**Field name:**
**Current definition (if existing):**
**Proposed definition:**
**Type:** <!-- string / integer / float / boolean / enum / array -->
**Required:** <!-- yes / no -->
**Allowed values (if enum):**

---

## Rationale

<!-- Why is this change needed? What vulnerability class does it enable better coverage of? -->

---

## Impact on Existing Records

<!-- How many existing records are affected? Would they need updating? -->

---

## Example

```json
{
  "ave_id": "AVE-2026-00001",
  "new_field_name": "example value"
}
```
