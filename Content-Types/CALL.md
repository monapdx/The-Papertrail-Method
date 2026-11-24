---
CATEGORY: ARTIFACT
MEDIUM: TEXT
CONTAINS:
  - DATE/TIME
  - INCOMING NUMBER
  - OUTGOING NUMBER
  - STATUS
  - DURATION
---

**CALL**

A log entry for an incoming or outgoing phone call.

- DATE/TIME
- INCOMING NUMBER
- OUTGOING NUMBER
- STATUS (`received` or `missed`)
- DURATION (required for `received` calls only)

DATE/TIME and STATUS are required. Include exactly one of INCOMING NUMBER or OUTGOING NUMBER. STATUS must be `received` or `missed`. Include DURATION for `received` calls only.
