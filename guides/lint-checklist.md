# Lint checklist — AI Discourse Wiki

Run this checklist during every /lint session. Each item maps to a check in
the /lint skill. Record all failures in wiki/_lint-report.md.

## Frontmatter completeness
- [ ] Every page has: title, type, draft, created, updated, sources
- [ ] No page has `draft: true` that should be published
- [ ] constructs/ pages have: definition, operationalisation, related_instruments,
      related_actors, domain

## claim/ checks
- [ ] Every claim/ page has at least one identified proponent in `proponents:`
- [ ] Every claim/ page has at least one source in `sources:`
- [ ] Conflicting claims are linked from [[Disputed Claims]]
- [ ] [[Disputed Claims]] entries each have at least two positions represented

## actor/ checks
- [ ] Every actor/ page has at least one backlink from a claim/ or incident/ page
- [ ] Actor names are consistent across all wikilinks (no alternate spellings
      without redirect stubs)

## theme/ checks
- [ ] Every theme/ page has at least one claim/ page linked under it
- [ ] themes/ subdirectory index pages list all pages in the subdirectory

## constructs/ checks
- [ ] Every constructs/ page has at least one related_claims backlink
- [ ] Every constructs/ page has at least one related_actors backlink
- [ ] Every constructs/ page documents at least one instrument or measurement approach

## source/ checks
- [ ] Every file in raw/ has a corresponding source/ page
- [ ] Every source/ page lists entities extracted from it

## Citation checks
- [ ] No `{{unverified}}` markers exist outside wiki/_review.md tracking
- [ ] Every footnote key cited in wiki/ pages exists in references.bib
- [ ] No verbatim quotes longer than 15 words

## Wikilink integrity
- [ ] No broken wikilinks (target page does not exist)
- [ ] Incident page titles follow format: [[YYYY-MM Short Description]]

## Structural
- [ ] wiki/_review.md is up to date with all unresolved items
- [ ] wiki/_candidates.md checkbox items are not stale (> 3 months old)

## After checklist
Regenerate PROJECT_CONTEXT_BRIEF.md with current counts.
