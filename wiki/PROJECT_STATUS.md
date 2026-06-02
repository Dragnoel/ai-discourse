# AI Discourse Wiki — Session Status

## Citation and reference-linking pass: 2026-06-03

### Completed this session
- **24 source pages**: each now ends with a `## Citation` section containing a full APA-format reference. Three DOIs are confirmed (Logg 2019, Bearman 2023, Eynon & Young 2021, Ehsan & Riedl 2024, Mah & Groß 2024); all 2025–2026 papers are marked `{{doi unverified}}` and should be verified against the PDFs.
- **6 construct pages**: `sources:` frontmatter updated from long PDF-filename strings to proper short bib keys; `## References` entries converted to wikilinks → `[[source/<slug>|Author (Year)]]`.
- **10 concept pages**: `## References` entries converted to wikilinks.
- **8 claim pages**: `## References` entries converted to wikilinks.
- **Bug fix**: removed stale `</content>` / `</invoke>` XML artifacts from `source/cheng-2025-asking-genai.md`.

### Notes
- Tully et al. bib key is `tully-2024` but the article appeared in *Journal of Marketing* 2025 (vol. 89). Citation section notes the discrepancy.
- Volume/article numbers for 2026 Elsevier *C&E:AI* papers are unverified; marked accordingly.

### Next session should
1. Verify the 19 `{{doi unverified}}` citations against the raw PDFs and add confirmed DOIs.
2. Manually populate `references.bib` (24 bib keys needed; see _lint-report.md F4).
3. Add new sources to `raw/` and run `/ingest`.

---

## /cleanup session: 2026-06-02

### Completed this session
/cleanup run following /lint. No pages were deleted (no stubs, duplicates, or superseded drafts found). All agent-fixable lint failures were applied as direct edits.

### Changes made
- **queries/_cleanup.sh**: updated — notes no deletions proposed; documents manual actions outstanding
- **F1 fixed**: added `proponents: []` to 5 concepts/ pages (social-construction-of-technology, utaut, theory-of-planned-behavior, explainable-ai, cognitive-offloading)
- **F2 fixed**: added claims/ backlinks to 4 constructs/ pages (algorithm-aversion → algorithm-preference-does-not-predict-use; algorithm-appreciation → lay-decision-makers-prefer-algorithmic; ai-literacy → lower-ai-literacy; cognitive-load → ai-improves-performance-not-learning)
- **F5 fixed**: corrected 5 broken claim-title wikilinks across actors/ and source/ pages
- **F6 fixed**: created `wiki/claims/disputed-claims.md` — index of two active disputes

### Outstanding (not agent-fixable)
- **F4**: references.bib requires manual population — 24 bib keys needed; see _lint-report.md for key list
- **W3**: source citation-style wikilinks — decision deferred (shorten titles vs. convert to plain text)
- **W4**: 43 minor-author wikilinks — expected; address in next /ingest or editing pass

### Next session should
1. Manually populate references.bib (outside Claude Code; see lint report F4 for key list)
2. Add new sources to raw/ and run /ingest
3. Run /lint after next ingest to track improvements
