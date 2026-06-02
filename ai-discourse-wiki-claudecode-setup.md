# AI Discourse Wiki — Claude Code Setup Document

> **Master design reference:** `wiki-design-plan-v2.md` governs all structural and
> schema decisions. If anything here conflicts with that document, the design plan wins.
>
> **Scope:** This document is specific to the `ai-discourse` wiki only. It assumes
> Claude Code is already installed and authenticated (`claude doctor` passes). The
> gaming-language wiki is a sibling vault and can be used as a structural reference —
> from inside `ai-discourse/`, run `cd ../gaming-language` to inspect it.
>
> **GitHub:** This vault is linked to https://github.com/Dragnoel/ai-discourse via SSH.
> All git operations go to that remote.

---

## Key Differences From the Gaming-Language Wiki

The ai-discourse vault is simpler in structure:

- No `entries/` directory, no `entries_index.json`, no `build/` toolchain
- No `guides/furigana.md`, no furigana or JP↔EN skill files
- Four skill files only (the four slash commands: `ingest`, `lint`, `query`, `cleanup`)
- Wiki entity types: `concepts/`, `claims/`, `actors/`, `incidents/`, `themes/`,
  `comparisons/`, `source/`, `constructs/`
- `themes/` supports subdirectories (e.g. `themes/perceptions/`) for domain clusters
  that grow large enough to warrant their own index page
- The initial entity type layout is provisional — the first `/ingest` session reviews
  `raw/` and may propose additions or modifications to the schema before any content
  is committed
- Strictly descriptive voice — never asserts a contested position in its own voice

---

## Working Principle: Plan-Then-Approve

Claude Code will **not** execute freely. At each phase, it must:

1. Read the relevant section of the design plan
2. State its complete plan for that phase (files to create, content summary, commands
   to run)
3. **Wait for your approval before doing anything**

When you respond with approval, it executes. If you request changes first, it revises
the plan and waits again. A phase is not complete until you have explicitly approved
it. This replaces the previous model of approving every individual command.

Claude Code is permitted to ask clarifying questions before presenting a plan if
something is genuinely ambiguous. It should not ask questions it can resolve by reading
the design plan.

---

## Setup Overview

| Phase | What happens | Approval gate |
|---|---|---|
| 0 | Confirm starting directory and git remote | — |
| 1 | Scaffold all directories and placeholder files | Plan → your approval → execute |
| 2 | Write `CLAUDE.md` | Plan → your approval → execute |
| 3 | Write `.claude/settings.json` and hook | Plan → your approval → execute |
| 4 | Write four skill files | Plan → your approval → execute |
| 5 | Write four guide files | Plan → your approval → execute |
| 6 | Seed continuity files and `references.bib` | Plan → your approval → execute |
| 7 | Initialise git, set remote, push initial commit | Plan → your approval → execute |
| 8 | OS-level locks (`chmod`, optional `chattr`) | **You only — outside Claude Code** |
| 9 | Smoke tests | Plan → your approval → execute |
| 10 | Generate knowledge graph with graphify | Plan → your approval → execute |
| 11 | Schema-review ingest: read `raw/`, propose schema amendments | Plan → your approval → execute |

---

## Phase 0 — Orientation (no approval gate)

Paste this as your opening prompt:

```
You are setting up the ai-discourse wiki. Before doing anything else:

1. Confirm your current working directory is .../ai-discourse/ and that this
   is the correct project root. If it is not, stop and tell me.

2. Read wiki-design-plan-v2.md from wherever it is accessible (try
   ~/Documents/wiki-project/wiki-design-plan-v2.md first). Confirm you have
   read it by summarising §1 and §2 (ai-discourse sections only) in two
   sentences each.

3. Note that the gaming-language wiki exists at ../gaming-language/ relative
   to this directory. You may cd there to inspect its structure as a reference,
   but return to this directory before any writes.

4. Note that this vault is linked to https://github.com/Dragnoel/ai-discourse
   via SSH. Do not push to the remote until Phase 7.

5. Confirm the SSH remote is reachable:
   git ls-remote git@github.com:Dragnoel/ai-discourse.git
   Report the result. If authentication fails, stop and tell me.

Do not scaffold any files yet.
```

---

## Phase 1 — Directory Scaffold

Paste this prompt:

```
Read §2 of wiki-design-plan-v2.md (the ai-discourse vault tree). Then:

Present your complete plan for Phase 1:
- Full list of directories to create (mkdir -p commands)
- Full list of placeholder files to create (touch commands)
- Confirm: no entries/, no entries_index.json, no build/ directory

Wait for my approval before executing anything.
```

**Expected directory tree (for your reference when reviewing the plan):**

```
ai-discourse/
├── .claude/
│   ├── hooks/
│   │   └── protect_raw.py
│   ├── skills/
│   │   ├── ingest/
│   │   │   └── SKILL.md
│   │   ├── lint/
│   │   │   └── SKILL.md
│   │   ├── query/
│   │   │   └── SKILL.md
│   │   └── cleanup/
│   │       └── SKILL.md
│   └── settings.json
├── raw/
│   ├── papers/
│   ├── articles/
│   └── notes/
├── wiki/
│   ├── index.md
│   ├── _review.md
│   ├── _candidates.md
│   ├── concepts/
│   ├── claims/
│   ├── actors/
│   ├── incidents/
│   ├── themes/             ← subdirectories allowed: e.g. themes/perceptions/
│   ├── comparisons/
│   ├── constructs/         ← psychological/theoretical constructs (trust, self-efficacy, etc.)
│   └── source/
├── queries/
│   └── _cleanup.sh
├── guides/
│   ├── style.md
│   ├── research.md
│   └── lint-checklist.md
├── CLAUDE.md
├── PROJECT_STATUS.md
├── PROJECT_CONTEXT_BRIEF.md
└── references.bib
```

**Notes on provisional structure:**
- `constructs/` holds psychological and theoretical constructs distinct from
  discourse terms. Each page should include frontmatter for `definition:`,
  `operationalisation:`, `related_instruments:`, `related_actors:`, `domain:`.
- `themes/` subdirectories (e.g. `themes/perceptions/`) are created only when
  a cluster grows large enough. Each subdirectory gets an `index.md`.
- Both `constructs/` and any `themes/` subdirectories are provisional until the
  first schema-review ingest (Phase 11) confirms they are needed.

**Note on skills format:** `.claude/skills/` uses the directory-per-skill format
(`skills/<name>/SKILL.md`), not flat files. This is required for auto-loading to work.

---

## Phase 2 — `CLAUDE.md`

```
Read §10.2 of wiki-design-plan-v2.md (the ai-discourse CLAUDE.md specification).
Also inspect ../gaming-language/CLAUDE.md as a structural reference if it exists.

Present your complete plan for CLAUDE.md:
- Section headings you will include
- One-sentence description of each section's content
- Any deviations from the design plan's spec and your reason for them
- Confirm the file will be under ~300 lines (design plan §11 constraint)

Wait for my approval before writing.
```

**Key requirements to verify in the plan:**

- Project identity and purpose section
- Vault structure summary (entity types: concepts, claims, actors, incidents,
  themes, comparisons, source, constructs — with a note that constructs and
  theme subdirectories are provisional pending Phase 11 schema review)
- Session contract (what the agent reads first, what it does not open unprompted)
- Slash command descriptions (four commands)
- Hard prohibitions including the core constraint: never assert a contested
  position in the wiki's own voice
- Deny list: `raw/`, `references.bib`, `CLAUDE.md`, `guides/` — no writes
- Forbidden commands: `chmod`, `chflags`, `rm`, `mv`, `git push`, `sudo`,
  `curl`, `wget`
- A note that `constructs/` pages use extended frontmatter (`definition:`,
  `operationalisation:`, `related_instruments:`, `related_actors:`, `domain:`)
- A note that `themes/` subdirectories get their own `index.md` when created

---

## Phase 3 — `.claude/settings.json` and Hook

```
Read §4 of wiki-design-plan-v2.md (the four security layers). Focus on
the ai-discourse variant (no entries/, no build/ references).
Also inspect ../gaming-language/.claude/settings.json and
../gaming-language/.claude/hooks/protect_raw.py as structural references
if they exist.

Present your complete plan for Phase 3:

Part A — settings.json:
- The three top-level keys you will include (permissions, sandbox, hooks)
- List of all denyWrite paths
- List of all denyRead paths
- Confirm: no entries/**, no build/** references
- The sandbox configuration you will use
- How the hook will be registered

Part B — protect_raw.py:
- What the hook does (block writes to raw/ and other protected paths)
- The exit codes it returns
- Confirm it is identical in logic to the gaming-language hook (if that
  exists), or describe any differences

Wait for my approval before writing either file.

After approval and execution, validate settings.json with:
python3 -m json.tool .claude/settings.json
Report the validation result.
```

---

## Phase 4 — Skill Files

```
Read §5.1 of wiki-design-plan-v2.md (skill files). The ai-discourse wiki uses
only the four slash command skills (ingest, lint, query, cleanup). There are
no auto-loaded guide skills for this vault.

Also read the ai-discourse-specific slash command content in §10.1 of the
design plan.

Present your complete plan for all four skill files:
- For each skill: the file path, the frontmatter fields, and a paragraph
  describing what the skill instructs the agent to do
- Confirm the entity types referenced in /ingest and /lint include all
  ai-discourse types: concepts, claims, actors, incidents, themes,
  comparisons, source, constructs — not the gaming wiki types
- Confirm /ingest handles constructs/ pages with extended frontmatter
  (definition:, operationalisation:, related_instruments:, related_actors:,
  domain:) and themes/ subdirectory index pages
- Confirm /ingest links related pages when similarities exist across sources
  — at minimum: same actor, same claim, same construct, or overlapping themes
- Confirm /lint includes the ai-discourse-specific checks:
    * claim/ pages without identified proponents
    * actor/ pages with no claim/ or incident/ backlinks
    * theme/ pages with no claims
    * constructs/ pages with no related_claims or related_actors backlinks
    * [[Disputed claims]] entries with only one position represented

Wait for my approval before writing any skill files.
```

---

## Phase 5 — Guide Files

```
Read §5.2 of wiki-design-plan-v2.md (guide files) and §5.3 (style.md skeleton).

The ai-discourse wiki needs three guide files:
- guides/style.md
- guides/research.md
- guides/lint-checklist.md

There is no guides/furigana.md for this vault.

Present your complete plan for all three guide files:
- For each: the major sections and their purpose
- Confirm style.md includes the ai-discourse-specific prohibition on
  asserting contested positions in the wiki's own voice
- Confirm research.md includes guidance on source evaluation for contested
  AI discourse claims (hype, environmental cost, labour impact, safety,
  regulation)
- Confirm lint-checklist.md sections match the /lint skill's checklist
  (they must stay in sync), including:
    * constructs/ pages with no related_claims or related_actors backlinks
    * the existing claim/actor/theme/disputed-claims checks

Wait for my approval before writing any guide files.
```

---

## Phase 6 — Continuity Files and `references.bib`

```
Seed the continuity files and bibliography stub for this vault.

Present your complete plan:
- Content for PROJECT_STATUS.md (today's date, "Setup complete", what the
  next session should do)
- Content for PROJECT_CONTEXT_BRIEF.md (entity counts all at 0, generated
  by: setup)
- Two-line content for references.bib
- Stub content for wiki/index.md (one paragraph describing the wiki's
  purpose and a placeholder section list)
- Empty state for wiki/_review.md and wiki/_candidates.md (header only)
- Empty state for queries/_cleanup.sh (shebang + comment header only)

Wait for my approval before writing.
```

---

## Phase 7 — Git Initialisation and Remote Setup

```
This vault will be version-controlled at:
git@github.com:Dragnoel/ai-discourse.git

Present your complete plan for Phase 7:
- Whether to run git init or whether a .git/ directory already exists
  (check first, report what you find)
- The .gitignore entries you recommend (raw/, .obsidian/workspace*.json,
  any OS files)
- The initial commit strategy (what gets committed, what gets excluded)
- The remote add and push commands you will run

Do NOT run git push or any remote-touching command until I explicitly
approve this phase.

Wait for my approval.
```

**Review before approving:** Confirm `raw/` is in `.gitignore` before any push.
Source material in `raw/` should never be committed to the public remote.

---

## Phase 8 — OS-Level Locks (you, outside Claude Code)

**Exit Claude Code before running these commands.** The agent cannot run `chmod`
or `chattr` — those are in the deny list by design. Apply locks yourself:

```bash
# Exit Claude Code first
# cd into the vault root
cd ~/ai-discourse

# Lock raw source material and static config
chmod -R a-w raw/ references.bib

# Lock CLAUDE.md and guides/ (agent must not edit these)
chmod a-w CLAUDE.md
chmod -R a-w guides/

# Optional: use chattr for stronger immutability (ext4 filesystems only)
# sudo chattr +i CLAUDE.md references.bib
# sudo chattr -R +i raw/ guides/

# Verify
ls -la raw/
ls -la guides/
```

**Note:** Unlike the gaming-language wiki, there is no `build/` directory to lock here.

To unlock for hand-editing (e.g. to add a source to `raw/` or update a guide):
```bash
chmod -R u+w raw/          # unlock
cp ~/Downloads/my-paper.pdf raw/articles/
chmod -R a-w raw/          # re-lock
```

---

## Phase 9 — Smoke Tests

```
Run the following verification checks and report results for each.

1. Hook blocks write to raw/:
   echo '{"tool_name":"Edit","tool_input":{"file_path":"./raw/articles/x.pdf"}}' \
     | .claude/hooks/protect_raw.py ; echo "exit: $?"
   Expected: BLOCKED + exit 2

2. Hook allows write to wiki/:
   echo '{"tool_name":"Edit","tool_input":{"file_path":"./wiki/concepts/test.md"}}' \
     | .claude/hooks/protect_raw.py ; echo "exit: $?"
   Expected: exit 0 (silent)

3. settings.json is valid JSON:
   python3 -m json.tool .claude/settings.json
   Expected: no errors

4. All four skill files exist and are non-empty:
   for d in ingest lint query cleanup; do
     wc -l .claude/skills/$d/SKILL.md
   done

5. Sandbox is configured:
   grep -A3 '"sandbox"' .claude/settings.json
   Expected: "enabled": true, "allowUnsandboxedCommands": false

6. Git remote is set correctly:
   git remote -v
   Expected: origin git@github.com:Dragnoel/ai-discourse.git

7. raw/ is locked:
   ls -la raw/
   Expected: no write bits

Present all results. Flag any failures before proceeding to Phase 10.
```

---

## Phase 10 — Knowledge Graph (graphify)

This phase runs after all setup is complete and the vault is in a working state.
The `graphify` program is installed and available on PATH.

```
All prior phases are complete and the vault is verified. Now generate a
knowledge graph of the ai-discourse vault using graphify.

Present your complete plan for Phase 10:
- The graphify command you will run and its arguments
- What the output will be (file format, location, what it represents)
- Whether graphify needs to be pointed at specific directories or the
  vault root
- Where the output graph file(s) will be saved (recommend: inside the
  vault, outside raw/ and wiki/ so it is not mistaken for content)

Do not run graphify until I approve the plan.

After approval and execution, confirm the graph file was created and
report its location and size.
```

**Recommended output location:** `~/ai-discourse/graph/` (create if needed).
The graph is for Claude Code's reference in future sessions and need not be
committed to git unless you want it version-controlled.

---

## Phase 11 — Schema-Review Ingest

This is the first real `/ingest` session. Its purpose is not to produce polished wiki
pages but to let the actual source material in `raw/` shape the final schema before
content accumulates. Run this after Phase 10 (graphify) is complete and you have
placed at least a handful of sources in `raw/`.

```
Phase 11: Schema-review ingest.

This is a read-and-propose session, not a content-creation session. Do not
create entity pages yet. The goal is to survey raw/ and return a schema
amendment proposal for my approval before any wiki/ content is written.

Step 1 — Survey raw/.
List every file in raw/ (papers/, articles/, notes/). For each file, read
enough to identify:
- The broad topic domain (e.g. EdTech, AI safety, environmental cost,
  human-AI interaction, perceptions, regulation)
- Whether it involves measurable psychological or theoretical constructs
  (e.g. trust, self-efficacy, anxiety, adoption intent, autonomy)
- The actor group(s) discussed or studied (e.g. teachers, students,
  policymakers, researchers, general public)
- Any cross-source similarities: shared actors, shared claims, shared
  constructs, or overlapping themes

Step 2 — Propose schema amendments.
Based on what you find, propose:

A. New or modified entity types, if any. For each proposal state:
   - What the new type is and what problem it solves
   - What entity type it replaces or supplements
   - Example pages it would hold from the current raw/ files

B. New theme subdirectories, if any. For each proposal state:
   - The subdirectory name and what cluster it organises
   - Which raw/ sources would seed it
   - Whether it warrants an index.md now or should wait

C. Constructs identified. List every psychological or theoretical construct
   you found across raw/, even if only mentioned briefly. For each:
   - Construct name and the source(s) it appears in
   - Whether a constructs/ page is warranted now or should go in
     _candidates.md for later

D. Cross-source links. List any pairs or groups of sources that share
   enough subject matter that their eventual wiki pages should be linked.
   State what the link relationship would be (same actor, same construct,
   contradictory claims, complementary claims, same incident).

E. Anything that does not fit the current entity types and needs a home.

Step 3 — Wait.
Do not create any wiki/ pages, modify CLAUDE.md, or alter any guide files.
Present the full proposal and wait for my approval before doing anything.

After I approve (with any modifications), execute only the approved changes:
- Create any new wiki/ subdirectories
- Add approved constructs to _candidates.md or create their stub pages
- Create any approved theme subdirectory index pages
- Update PROJECT_STATUS.md to reflect Phase 11 complete
- Do not begin full ingest until the next session
```

**What to expect from this phase:** The proposal may be short (the schema fits the
sources well) or it may surface meaningful gaps. Common findings on a first pass:

- Sources cluster around a construct (e.g. "trust in AI" appears across four papers)
  that has no dedicated page — warrants a `constructs/trust.md` stub
- A theme subdirectory (`themes/perceptions/`) is clearly needed from day one
  rather than as a future migration
- Two sources make contradictory claims about the same actor or incident, which
  should be flagged in `_review.md` before either page is written
- An entity type is missing (e.g. "policy document" doesn't fit cleanly into
  any existing type)

After you approve the schema amendments, the next session is the first full
`/ingest` run against the confirmed schema.

---

## Ongoing Session Workflow

Once setup and the Phase 11 schema review are complete, every future session
follows this pattern:

```bash
cd ~/ai-discourse
claude
```

Claude Code loads `CLAUDE.md` automatically. Start each session with the relevant
slash command:

- `/ingest` — process new source material from `raw/` into wiki pages (run
  against the confirmed schema after Phase 11 is approved)
- `/lint` — audit wiki for structural and citation issues; regenerates
  `PROJECT_CONTEXT_BRIEF.md`
- `/query [topic]` — research and surface connections across wiki pages
- `/cleanup` — after a lint run, review `queries/_cleanup.sh` and execute
  removals you approve

**Pro-plan rhythm** (one session per day, manual trigger):
- Weekly: `/lint` — highest-value cheap session
- After lint: `/cleanup` if removals are proposed
- As needed: `/ingest` after adding sources to `raw/`
- As needed: `/query` for synthesis or research

**Never mix jobs in one session.** One command per session keeps token use
predictable.

---

## Continuity: Starting a New Session Mid-Setup

If setup spans multiple sessions, hand the new session:

1. `wiki-design-plan-v2.md`
2. This document (`ai-discourse-wiki-claudecode-setup.md`)
3. A note on which phase you completed last (e.g. "Phase 5 done, Phase 6
   not yet started")
4. Output of `tree ~/ai-discourse -L 4 -a` so it can see what exists

That is sufficient context for any session to resume cleanly.

---

## Constraints Reference

These apply in every session, not just setup. Claude Code must never:

- Write to `raw/`, `references.bib`, `CLAUDE.md`, or `guides/`
- Run `chmod`, `chflags`, `rm`, `mv`, `git push`, `sudo`, `curl`, or `wget`
- Assert a position on a contested AI discourse claim in the wiki's own voice
- Aggregate claims across actors without explicit per-actor attribution
- Use emojis, "TL;DR", bolded "key takeaways", or rhetorical flourish in wiki content
- Open entity pages it was not asked to open (read `wiki/index.md` first; open
  specific pages on demand only)

---

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| Hook not firing | `protect_raw.py` not executable or `settings.json` invalid JSON | `chmod +x .claude/hooks/protect_raw.py`; validate JSON |
| Agent reads/writes outside vault | Sandbox not active | Verify `"sandbox": {"enabled": true}` in `settings.json` |
| `/ingest` does nothing | `SKILL.md` empty or not found | Check `.claude/skills/ingest/SKILL.md` is non-empty |
| `settings.json` silently ignored | Malformed JSON | `python3 -m json.tool .claude/settings.json` |
| SSH push fails | Key not added to GitHub | `ssh -T git@github.com` to test; add key at github.com/settings/keys |
| Agent proposes writing to `raw/` | Hook not registered in settings | Confirm `"hooks"` block in `settings.json` points to the correct path |
| Phase plan is too vague | Agent skipped design plan | Instruct it to re-read the relevant section before presenting plan |
| `graphify` command not found | Not on PATH in current shell | `which graphify`; if missing, check install location and add to PATH |
| Phase 11 proposal is too vague | Agent read file names but not contents | Instruct it to read each file in `raw/` before proposing; confirm it reports construct names and cross-source links |
| Constructs found but not listed | Agent conflated constructs with concepts | Remind it: concepts are discourse terms (AGI, stochastic parrots); constructs are measured/operationalised (trust, self-efficacy) |
| Phase 11 proposes creating pages immediately | Agent skipped the read-and-propose constraint | Remind it: Phase 11 is proposal-only; no wiki/ pages until schema is approved and a new `/ingest` session begins |
