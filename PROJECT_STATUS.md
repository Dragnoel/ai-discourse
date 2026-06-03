# AI Discourse Wiki — Session Status

## Session: 2026-06-03

### Completed this session
- **Abstract + DOI additions** (completed in previous session, uncommitted): All 24 `wiki/source/` pages have word-for-word abstracts (or equivalent: Author Summary / Publisher Description for opinion pieces and edited volumes) and DOI lines inserted between the lead paragraph and the `## Summary` section. These 24 files were modified in the prior session and remain as uncommitted working-tree changes.
- **Actor stub pages**: Created 70 new `wiki/actors/` pages (5 previously existed; 75 total now). Every actor linked via `[[Name]]` in source page frontmatter `proponents:` fields now has a corresponding page. Pages follow the logg-jennifer.md / eynon-rebecca.md template: frontmatter + brief bio with affiliation where available + `## Key contributions to the discourse` + `## See also`.
- Actors whose affiliations were not visible in source page text carry the note: *affiliation not stated in this collection's source material.*

### Counts by type
- Source pages modified (abstract+DOI): 24
- Actor pages created: 70

### Known open items
- **Cross-source short-title links**: Source pages use short-form wikilinks like `[[Armstrong (2025)]]` in `## Cross-source links` sections. These do not resolve to the verbose source page titles (`"Armstrong (2025) — AI Integration..."`). Resolution requires either alias fields in source page frontmatter or a separate source index with short-title redirects. Flagged for a future session.
- **Unverified affiliations**: ~30 minor co-authors have `affiliation not stated in this collection's source material`. These can be updated by checking the raw PDFs or searching institutional databases.
- **DOI verification**: Several source pages carry `{{doi unverified}}` flags. These should be verified against live DOI resolvers before publishing.
- **Phase 8** (user action required): `chmod -R a-w raw/ references.bib CLAUDE.md guides/` — still pending from original setup.

### Next session should
1. Commit the 24 modified source pages and 70 new actor pages together (one commit: "Add abstracts, DOIs, and actor stub pages").
2. Optionally resolve cross-source short-title wikilinks by adding `aliases:` frontmatter to source pages or creating a short-title index.
3. Verify flagged `{{doi unverified}}` DOIs.
4. Begin creating entity pages (concepts, claims, constructs, themes) extracted in source pages' `## Entities extracted` sections — many of these are also dead wikilinks.
