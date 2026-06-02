---
name: cleanup
description: Generate a reviewed deletion script from lint findings
triggers:
  - /cleanup
---

# /cleanup — Generate deletion script

## Usage
Run after a /lint session that has produced wiki/_lint-report.md.

## Steps
1. Read wiki/_lint-report.md.
2. Identify pages proposed for deletion: stubs with no content, duplicates,
   superseded drafts, broken-link targets that should not exist.
3. For each proposed deletion, state the reason clearly.
4. Write the deletion script to queries/_cleanup.sh:

```bash
#!/usr/bin/env bash
set -euo pipefail

# Review each rm command carefully before running.
# Run from vault root: bash queries/_cleanup.sh

rm "wiki/concepts/stub-no-content.md"   # empty stub, no sources, no backlinks
rm "wiki/claims/duplicate-claim.md"     # duplicate of claims/original-claim.md
```

## Constraints
- Do not run the script — write it only
- Never include raw/, guides/, references.bib, CLAUDE.md, or .claude/ in deletions
- Update PROJECT_STATUS.md after writing the script
