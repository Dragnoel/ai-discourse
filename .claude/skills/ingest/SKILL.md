---
name: ingest
description: Process new source material from raw/ into wiki pages
triggers:
  - /ingest
---

# /ingest — Ingest new source material

## Before starting
Read PROJECT_STATUS.md. Read wiki/index.md. Do not open individual entity pages
unless directly relevant to a source being ingested.

## Step 1 — Identify unprocessed sources
List all files in raw/papers/, raw/articles/, raw/notes/. For each, check whether
a corresponding source/ page exists. Process only files without a source/ page,
unless explicitly asked to re-process.

## Step 2 — For each unprocessed source

**Create a source/ page** at wiki/source/<filename-without-ext>.md:
- Lead paragraph (≤ 80 words): document type, author(s), date, main topic
  - `## Abstract`: if the document contains an abstract, copy it **verbatim** as a
    blockquote immediately after the lead paragraph. Do not paraphrase or summarise.
    For documents without a standard abstract, use an equivalent heading and note
    the difference inline:
    - Opinion/commentary pieces → `## Author summary`
    - Edited volumes → `## Publisher description`
    - Documents with no abstract → omit the section; note the absence in the lead paragraph
    Follow the blockquote immediately with `**DOI:** <url>`, or if no DOI is assigned
    (e.g. dissertations), note that explicitly. The abstract and DOI must appear
    before `## Summary`.
- `## Summary` (2–4 paragraphs): key claims, actors mentioned, evidence offered
- `## Entities extracted`: bullet list of claims, actors, incidents, constructs identified
- `## Cross-source links`: other wiki pages this source connects to, and why
- Standard frontmatter (type: source)
- For the `## Summary` section and any extended prose, consult
  `guides/academic-writing-style-guide.md` for sentence architecture,
  paragraph structure (claim → context → evidence → implication), and
  hedging calibration

**Create or update entity pages** for each entity identified:
- `concepts/` — discourse terms introduced or discussed
- `claims/` — specific argued positions; one claim per page; note proponent(s)
- `actors/` — persons, labs, orgs; link claims and incidents back to them
- `incidents/` — discrete events (releases, lawsuits, statements, retractions)
- `themes/` — recurring framings; add to existing theme page or create new
- `constructs/` — psychological/theoretical constructs (trust, self-efficacy, etc.);
  use extended frontmatter: definition:, operationalisation:, related_instruments:,
  related_actors:, domain:
- `comparisons/` — only when a source explicitly contrasts two claims or positions

**Link related pages** — at minimum:
- Same actor appears in multiple sources → link actor page to all relevant claim/incident pages
- Same construct appears across sources → backlink from each claim/ page that relies on it
- Contradictory claims → link both from [[Disputed Claims]]
- Complementary claims on the same topic → link via See also

## Step 3 — Candidates and review
- Entity mentioned but not yet warranting a full page → `wiki/_candidates.md`
- Claim that cannot be verified from the raw/ source → `{{unverified}}` + `wiki/_review.md`

## Step 4 — End of session
Update PROJECT_STATUS.md: source pages created, entity pages created/updated,
items added to _review.md and _candidates.md, unresolved questions, what to do next.

## Constraints
- Never assert a position on a contested claim in the wiki's own voice
- Never write to raw/, references.bib, CLAUDE.md, or guides/
- One claim per claim/ page; split conflicting positions into separate pages
- No emojis, no "key takeaways", no rhetorical flourish
- constructs/ pages require extended frontmatter — see CLAUDE.md
- themes/ subdirectories (e.g. themes/perceptions/) only when a cluster is large
  enough; each subdirectory gets an index.md
