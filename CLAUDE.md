# AI Discourse Wiki — agent schema

## Session start (read in this order)
1. `PROJECT_STATUS.md` — what happened last session; what to do first
2. `CLAUDE.md` (this file)
3. `guides/style.md` and `guides/research.md`
4. The relevant `.claude/skills/` file for the task type

## Session end
Update `PROJECT_STATUS.md` with:
- Pages created/edited (counts by type)
- Items added to `_review.md` and `_candidates.md`
- Unresolved questions
- What the next session should start with

## Purpose
This wiki maps contemporary AI discourse — hype, mysterianism, environmental cost,
EdTech, labour, safety, regulation, sociocultural effects — documenting concepts,
claims, actors, incidents, and themes with sources. It is not a position paper.
The agent records who said what, when, and with what evidence; it never asserts a side.

## Folder rules
- `raw/`                — read allowed, writes blocked
- `references.bib`      — read-only
- `wiki/`               — agent writes entity pages here
- `queries/`            — saved Q&A and `_cleanup.sh`
- `PROJECT_STATUS.md` and `PROJECT_CONTEXT_BRIEF.md` — agent updates these
- `CLAUDE.md`, `guides/`, `.claude/`                 — read-only; never write

## Entity types (wiki/ subdirectories)
| Directory      | What goes here |
|---|---|
| `concepts/`    | A term in the discourse (e.g. [[AGI]], [[Stochastic Parrots]]) |
| `claims/`      | A specific argued position attributable to one or more actors |
| `actors/`      | A person, lab, journal, advocacy org, or commercial vendor |
| `incidents/`   | A discrete event: release, lawsuit, statement, retracted paper |
| `themes/`      | A recurring framing: hype cycle, mysterianism, environmental cost, etc. |
| `comparisons/` | Side-by-side of two claims, actors, or positions |
| `constructs/`  | Psychological or theoretical constructs (trust, self-efficacy, adoption intent) |
| `source/`      | One page per `raw/` file, summarising it |

**Provisional note:** `constructs/` and any `themes/` subdirectories (e.g.
`themes/perceptions/`) are provisional until Phase 11 schema-review ingest confirms
they are needed. Do not create them unless source material warrants it.

## Standard frontmatter
```yaml
---
title: <Title Case>
type: concept | claim | actor | incident | theme | comparison | constructs | source
themes:
  - hype | mysterianism | environmental | edtech | sociocultural | labour | safety | regulation
position: pro | against | descriptive | n/a
proponents:
  - [[Actor Name]]
status: active | superseded | retracted | contested
draft: false
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources:
  - <bib-key-or-filename>
---
```

## Extended frontmatter for constructs/ pages
```yaml
---
title: <Construct Name>
type: constructs
definition: <one-sentence definition>
operationalisation: <how it is measured or operationalised in the literature>
related_instruments:
  - <scale or instrument name>
related_actors:
  - [[Actor Name]]
domain: edtech | human-ai-interaction | safety | regulation | other
draft: false
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources:
  - <bib-key-or-filename>
---
```

## themes/ subdirectories
When a theme cluster grows large enough, create a subdirectory (e.g.
`themes/perceptions/`). Each subdirectory gets its own `index.md` listing its pages.
Do not create subdirectories speculatively — wait for source material to warrant it.

## Claim-page structure
One claim per page. Conflicting positions: separate pages, linked from [[Disputed Claims]].

1. Lead (≤ 80 words): claim in neutral wording, primary proponent(s), earliest source
2. `## The claim, in their own framing` — paraphrase; ≤ 15-word verbatim quotes, one per source
3. `## Evidence the proponents offer` — bullet list, footnoted
4. `## Counter-positions` — wikilinks to opposing `claim/` pages
5. `## Status`
6. `## See also`
7. `## References`

## Sourcing rules
- "X said Y" is a fact. "Y is true" needs evidence.
- Verbatim quotes ≤ 15 words; one per source per page.
- Unlocatable source: `{{unverified}}` + add to `wiki/_review.md`.

## Wikilink conventions
- Title Case always.
- Actor pages: preferred public name; redirect stubs for alternates.
- Incident pages: `[[YYYY-MM Short Description]]`.

## What the slash commands do
- `/ingest` — create `source/` pages from `raw/` files; extract claims, actors,
  incidents, constructs; create/update entity pages; link related pages (same actor,
  same claim, same construct, overlapping themes); update `PROJECT_STATUS.md`
- `/query` — answer using `wiki/` + `references.bib` only; offer to file back
- `/lint` — run `guides/lint-checklist.md`; regenerate `PROJECT_CONTEXT_BRIEF.md`;
  output to `wiki/_lint-report.md`; propose only, do not execute
- `/cleanup` — write proposed deletions to `queries/_cleanup.sh`; do not run it

## Hard prohibitions
- Never assert a position on a contested AI discourse claim in the wiki's own voice
- Never write to `raw/`, `references.bib`, `CLAUDE.md`, or `guides/`
- Never run `chmod`, `chflags`, `rm`, `mv`, `git push`, `sudo`, `curl`, or `wget`
- Never delete files — use `/cleanup` to produce a reviewed shell script
- No emojis, no "TL;DR", no bolded "key takeaways", no rhetorical flourish
- No aggregated claims across actors without explicit per-actor attribution
- Do not open entity pages unprompted — read `wiki/index.md` first; open specific pages on demand

## _review.md vs _candidates.md
- `wiki/_review.md` — unverified claims, source conflicts, contested attributions; human resolves
- `wiki/_candidates.md` — entity pages to create in a future session. Format:
  - `[ ] [[2025-03 EU AI Act Enforcement Begins]]` — see `raw/articles/eu-ai-act.pdf`
  - `[ ] [[Yann LeCun]]` (actor) — prominent counter-voice to safety discourse
