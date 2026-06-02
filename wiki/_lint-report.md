## Lint report — 2026-06-02

First post-ingest lint run. 58 wiki pages audited (24 source/, 10 concepts/, 8 claims/, 6 constructs/, 5 actors/, 2 themes/ index pages, 1 incidents/, plus continuity files).

---

### Failures (7 categories)

**F1. concepts/ pages missing `proponents:` frontmatter field (5 pages)**

The standard schema requires `proponents:` on all pages. Five concept pages omit it.

- [wiki/concepts/social-construction-of-technology.md] Fix: add `proponents: []` (originators Pinch & Bijker not in actors/ yet; leave empty or add as plain text note)
- [wiki/concepts/utaut.md] Fix: add `proponents: []` (Venkatesh et al. not in actors/)
- [wiki/concepts/theory-of-planned-behavior.md] Fix: add `proponents: []` (Ajzen not in actors/)
- [wiki/concepts/explainable-ai.md] Fix: add `proponents: []`
- [wiki/concepts/cognitive-offloading.md] Fix: add `proponents: []`

---

**F2. constructs/ pages have no backlink to any existing claims/ page (6 pages)**

The checklist requires every constructs/ page to have at least one related_claims backlink. All six constructs pages were written before the claims/ pages existed; none link to any of the 8 claims/ pages now in wiki/claims/.

Proposed links to add to each page's `## See also`:

- [wiki/constructs/algorithm-aversion.md] → add `[[Algorithm Preference Does Not Predict Advice Use]]`
- [wiki/constructs/algorithm-appreciation.md] → add `[[Lay Decision-Makers Prefer Algorithmic to Human Advice]]` (see also F5 — the current wikilink text is wrong)
- [wiki/constructs/ai-literacy.md] → add `[[Lower AI Literacy Predicts Greater AI Receptivity]]`
- [wiki/constructs/cognitive-load.md] → add `[[AI Improves Performance But Not Learning]]`
- [wiki/constructs/ai-self-efficacy.md] → no direct claims/ page yet; add to _candidates.md
- [wiki/constructs/algorithmic-anxiety.md] → no direct claims/ page yet; add to _candidates.md

---

**F3. `{{unverified}}` markers in 4 pages not tracked in wiki/_review.md**

Rule: every `{{unverified}}` marker must have a corresponding entry in `_review.md`.

- [wiki/constructs/algorithm-aversion.md] marker: `Dietvorst et al. (2015) coined the term {{unverified — not in raw/}}`
- [wiki/constructs/cognitive-load.md] marker: `Sweller (1988) — foundational {{unverified — not in raw/}}`
- [wiki/concepts/theory-of-planned-behavior.md] marker: `Ajzen (1991) {{unverified — not in raw/}}`
- [wiki/concepts/assistance-dilemma.md] marker: `Koedinger and Aleven (2007) {{unverified — not in raw/}}`

Fix: add four entries to `wiki/_review.md`.

---

**F4. 24 bib keys cited in source/ frontmatter absent from references.bib**

Every source/ page cites a shortened bib key (e.g., `armstrong-2025`, `bassner-2026`) in its `sources:` frontmatter. None of these keys exist in references.bib. This is expected at initial ingest but is a formal checklist failure.

Fix: populate references.bib manually. All 24 entries are peer-reviewed journal articles or a book; standard @article / @incollection / @phdthesis formats apply. The source/ page for each gives the full citation details. references.bib is write-protected — requires manual addition.

Missing keys (24): armstrong-2025, bassner-2026, bearman-2023, cheng-2025, conradty-2026, ehsan-riedl-2024, eynon-young-2021, himmelstein-budescu-2023, huang-2025, jin-2025, jussupow-2024, karamifar-valente-2026, lan-2024, logg-2019, mah-gross-2024, nikolic-2024, shekhar-saurombe-2026, tully-2024, vendrell-johnston-2026, verano-tacoronte-2025, wang-2026, xia-2025, xu-xiong-2026, yuxian-2025.

---

**F5. Broken wikilinks: claim title mismatches (5 links in 4 pages)**

Five wikilinks in constructs/ and actors/ pages use informal short titles for claims/ pages, which do not match the actual frontmatter `title:` of those pages. Obsidian will not resolve these.

| Broken link text | Actual claim title | File(s) containing the broken link |
|---|---|---|
| `[[Algorithm Appreciation Exists in Lay Decision-Making]]` | "Lay Decision-Makers Prefer Algorithmic to Human Advice" | constructs/algorithm-appreciation.md; actors/logg-jennifer.md |
| `[[HE AI Discourse Dominated by Imperative-Change Framing]]` | "HE AI Literature is Dominated by Imperative-Change and Altering-Authority Framings" | actors/bearman-margaret.md |
| `[[Three Stakeholder Frames for AI in Lifelong Learning]]` | "Academia, Industry, and Policy Construct AI for Lifelong Learning Through Three Incompatible Frames" | actors/eynon-rebecca.md |
| `[[XAI Definition Should Remain Plural]]` | "A Singular XAI Definition Is Neither Feasible Nor Desirable" | actors/jussupow-ekaterina.md (XAI link); ehsan-riedl-2024 source |
| `[[Peer Influence Drives GenAI Cheating Behavior]]` | "Peer Influence and Moral Obligation Drive GenAI Cheating Behavior More Than Institutional Policies" | source/huang-2025-academic-cheating.md |

Fix: update each broken link to use the correct full title.

---

**F6. [[Disputed Claims]] page referenced but does not exist**

Two pages link to `[[Disputed Claims]]` (claims/lower-ai-literacy-greater-receptivity.md and constructs/algorithm-aversion.md), but no `wiki/claims/disputed-claims.md` page exists. The checklist requires this page to list contested claims with both positions represented.

Fix: create `wiki/claims/disputed-claims.md` as an index page listing: (1) the AI literacy/receptivity contradiction (Tully et al. vs. Xu & Xiong), and (2) the algorithm aversion/appreciation tension (Logg vs. Himmelstein & Budescu). See `wiki/_review.md` for the existing contested-items tracking.

---

**F7. [[Cognitive Autonomy]] used as wikilink but not in _candidates.md**

`[[Cognitive Autonomy]]` appears as a wikilink in source/conradty-2026-students-conceptions.md but no page exists and it is not in _candidates.md.

Fix: add `- [ ] [[Cognitive Autonomy]] (constructs) — Conradty et al. 2026; capacity for independent thinking distinct from self-regulation; related to [[Learner Agency]]` to _candidates.md.

---

### Warnings (6)

**W1. Actor page for Ekaterina Jussupow has no backlinks as proponent in claims/ or incidents/**

jussupow-ekaterina.md exists but no claims/ page lists her in `proponents:`. Her paper (Jussupow et al. 2024) provides the integrative framework for algorithm aversion/appreciation — a claim page could be created.

Fix: add a claim page for her paper's central argument (the integrative re-conceptualisation of algorithm aversion), or add her as a co-proponent to claims/algorithm-preference-does-not-predict-use.md if appropriate.

---

**W2. themes/perceptions/ and themes/frameworks/ have no linked content pages**

Both subdirectory index pages contain the placeholder "(Populated during /ingest sessions)" — no claims, concepts, or actors pages currently link into these theme clusters.

Fix: update index pages as content is added. Next /ingest session should explicitly populate these theme clusters by linking relevant pages. Not a structural failure at this stage; expected at initial build.

---

**W3. Source citation-style wikilinks do not resolve (16 instances)**

Source/ pages use citation-style wikilinks in `## Cross-source links` sections (e.g., `[[Bassner et al. (2026)]]`, `[[Logg (2019)]]`). These do not match the full title of the source pages (which begin "Bassner et al. (2026) — Less stress, better scores..."). Obsidian may partially resolve via title prefix matching but strict resolution fails.

Fix: either (a) convert to plain text in cross-links sections, or (b) shorten source page titles to match the citation style (e.g., retitle to "Bassner et al. (2026)"). Option (b) is cleaner for wikilink consistency but is a larger change. Flag for next /ingest session.

---

**W4. 43 minor-author wikilinks unresolved**

All co-author names used as wikilinks in source/ page `## Entities extracted` sections are broken (no actors/ pages exist for them). These are expected at first ingest; actor pages for minor authors are not a priority.

Fix: for authors who appear in multiple sources or who are primary proponents of significant claims, add to _candidates.md. For the majority, convert wikilink format to plain text in entities-extracted sections during next /ingest or editing pass.

---

**W5. Four minor concepts referenced but not yet created**

The following concepts are used as wikilinks but have no concepts/ page and are not in _candidates.md:
- `[[ChatGPT]]` — product/actor reference; could be redirect stub to actors/openai.md
- `[[Comfort Trap (AI)]]` — Bassner et al. term for misalignment between student AI preferences and learning outcomes
- `[[Theory of Digital Objects]]` — Faulkner & Runde framework used in Jussupow et al.
- `[[Behavioral Intention]]` — UTAUT construct; often treated as a core construct alongside performance/effort expectancy

Fix: add to _candidates.md.

---

**W6. Candidate claim not in _candidates.md**

`[[Faculty Anxiety About Student Learning Directly Inhibits ChatGPT Adoption]]` is listed as a candidate claim in source/verano-tacoronte-2025-faculty-anxiety.md entities but is not in _candidates.md.

Fix: add to _candidates.md.

---

### Passed (13 checks)

1. All 8 claim/ pages have at least one proponent in `proponents:` ✓
2. All 8 claim/ pages have at least one source in `sources:` ✓
3. All 8 claim/ pages have structured body sections (claim framing, evidence, counter-positions, status) ✓
4. All 24 source/ pages have `## Entities extracted` section ✓
5. All 6 constructs/ pages have: definition, operationalisation, related_instruments, related_actors, domain ✓
6. All 6 constructs/ pages have at least one instrument documented ✓
7. All 6 constructs/ pages have related_actors (even if empty list — no data error) ✓
8. No pages have `draft: true` ✓
9. All pages have title, type, draft, created, updated fields ✓
10. Incident page follows [[YYYY-MM Short Description]] format: "2022-11 ChatGPT-3.5 Release" ✓
11. No verbatim quotes longer than 15 words detected ✓
12. wiki/_review.md is current with 2 tracked items (Bécirović PDF; AI literacy contradiction) ✓
13. wiki/_candidates.md is current with 5 constructs queued ✓

---

### Summary

| Category | Count |
|---|---|
| Failures | 7 (across 5 categories) |
| Warnings | 6 |
| Passed | 13 |

**Priority actions before next /ingest:**
1. F3: Add 4 `{{unverified}}` items to _review.md (this session — see below)
2. F6: Create `wiki/claims/disputed-claims.md`
3. F5: Fix 5 broken claim-title wikilinks in constructs/ and actors/ pages
4. F1: Add `proponents: []` to 5 concepts/ pages
5. F4: Manually populate references.bib (user action — outside Claude Code)
