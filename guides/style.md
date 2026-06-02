# Style guide — AI Discourse Wiki

## Voice and register
Third person, present tense. Encyclopedic. No metaphor, rhetorical questions,
or second person. Strictly descriptive: the wiki records who said what with what
evidence. It does not argue, editorialize, or summarise toward a conclusion.

**Core constraint:** Never assert a position on a contested AI discourse claim
in the wiki's own voice. "X argues that Y" is acceptable. "Y is true" is not.

## Length norms
- Entity pages: 200–800 words.
- Lead paragraph: ≤ 80 words.
- Source pages: 100–400 words.

## Formatting
- ATX headers only (`#`, `##`). No bold headers inside paragraphs.
- Wikilinks in Title Case: `[[AGI]]`, `[[Sam Altman]]`, `[[Stochastic Parrots]]`.
- Footnote citations: `[^smith-2024]` for every non-trivial claim.
- Lists: hyphens. No nesting beyond one level.

## Frontmatter
Required on every page. See CLAUDE.md for field definitions. `draft: false`
only when the page has at least one sourced claim.

## Prohibited
- Emojis
- "TL;DR"
- Bolded "Key takeaways" or "Summary" callouts
- Rhetorical flourish, dramatic framing, loaded adjectives
- "Recent studies show" without naming the study
- Aggregated claims without per-actor attribution ("researchers believe…")
- First person or essay style
- Verbatim quotes longer than 15 words
- More than one verbatim quote per source per page

## Incident pages
Title format: `[[YYYY-MM Short Description]]`. Lead states: what happened, who
was involved, when, with what consequences. No editorialising about significance.

## constructs/ pages
Use the extended frontmatter from CLAUDE.md. Body defines the construct,
describes how it is operationalised in the literature, and lists instruments
used to measure it. Link to claim/ pages that rely on it; link to actor/ pages
that study or challenge it.

## themes/ index pages
When a themes/ subdirectory is created, its index.md lists: the theme name,
a one-paragraph neutral description, and wikilinks to all pages under it.
