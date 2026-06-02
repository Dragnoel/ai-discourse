# Research and citation discipline — AI Discourse Wiki

## Source hierarchy
1. Peer-reviewed publications (`raw/papers/`)
2. Primary sources: official statements, policy documents, legal filings,
   transcripts of named speakers (`raw/articles/`, `raw/notes/`)
3. Reputable secondary writing: named author, dated, attributable to a specific
   outlet (`raw/articles/`)
4. Blog posts, forum threads, social media — pointer to primary source only;
   never the citation itself

## Citation form
```
[^smith-2024-p12]: Smith, J. (2024). *Title*. Publisher, p. 12. raw/papers/smith-2024.pdf.
```
If the source is not in raw/, mark `{{unverified}}` and add to `wiki/_review.md`.

## Contested AI discourse claims
Several topics in this wiki involve actively disputed claims. Handle with care:

- **AI hype / capabilities claims** — Separate what a company or researcher claims
  from what independent studies show. Never merge the two.
- **Environmental cost** — Numbers vary by methodology. Cite the specific study,
  the methodology used, and the date. Note when newer data supersedes older estimates.
- **Labour impact** — Distinguish between projections, surveys, and observed outcomes.
  Attribute projections to their author.
- **Safety discourse** — "Existential risk" claims and counter-claims are attributed
  to named actors. The wiki does not adjudicate them.
- **EdTech outcomes** — Distinguish between self-reported outcomes (vendor or user)
  and independent evaluations. Note study design limitations if documented in raw/.
- **Regulation** — Policy texts are facts; their predicted effects are claims
  attributed to named actors.

## Conflicting sources
Do not silently pick a winner. State both positions, note the conflict, and add
an entry to `[[Disputed Claims]]`. If one source retracts or supersedes another,
note this in the status field of the claim/ page (`status: superseded`).

## Never in a wiki page
- The agent's own assessment of which claim is more credible
- Speculation not grounded in a raw/ source
- Training-data knowledge used as evidence (cite a raw/ source or mark `{{unverified}}`)
- Paraphrases that drift from the source's actual meaning
