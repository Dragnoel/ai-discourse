---
name: lint
description: Audit wiki structure and citation integrity; regenerate PROJECT_CONTEXT_BRIEF.md
triggers:
  - /lint
---

# /lint — Audit wiki integrity

## Before starting
Read guides/lint-checklist.md. Read wiki/index.md. Read PROJECT_CONTEXT_BRIEF.md
for current counts.

## What to audit
Run every check in guides/lint-checklist.md. For each failure, record it in
wiki/_lint-report.md with: the file, the rule violated, and the proposed fix.

## ai-discourse-specific checks
1. claim/ pages with no identified proponents (frontmatter `proponents:` empty or missing)
2. actor/ pages with no claim/ or incident/ backlinks
3. theme/ pages with no claims linked under them
4. constructs/ pages missing any of: `definition:`, `operationalisation:`,
   `related_claims`, `related_actors` frontmatter fields
5. [[Disputed Claims]] entries with only one position represented (need both pro and con)
6. source/ pages with no entities listed in `## Entities extracted`
7. Pages with `{{unverified}}` markers not recorded in wiki/_review.md
8. Frontmatter missing required fields (title, type, draft, created)
9. Wikilinks pointing to pages that do not exist (broken links)
10. references.bib keys cited in wiki/ pages but absent from references.bib
11. source/ pages missing `## Abstract` (or `## Author summary` /
      `## Publisher description` for opinion pieces and edited volumes)
12. source/ pages missing `**DOI:**` line after the abstract block

## Output format
Write full report to wiki/_lint-report.md:

```
## Lint report — YYYY-MM-DD

### Failures (N)
- [wiki/claims/foo.md] Rule: "claim/ page has no proponents". Fix: add proponents: field.

### Warnings (N)
- [wiki/actors/bar.md] Rule: "no backlinks from claim/ or incident/". Fix: check claim pages.

### Passed (N checks)
```

## Regenerate PROJECT_CONTEXT_BRIEF.md
After the audit, rewrite with current counts:
- Total pages by type
- _review.md item count
- _candidates.md item count
- Date generated

## Constraints
- Propose fixes only — do not modify entity pages during a lint run
- Do not write to raw/, references.bib, CLAUDE.md, or guides/
- Update PROJECT_STATUS.md at end of session
