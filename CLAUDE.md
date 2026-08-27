# Weekly News Report Agent

## Project Overview

This project is an AI agent that produces a **newspaper-style Report Page**
covering the **10 most important news stories from the last 7 days**. Unlike a
simple headline digest, each story is synthesized from **multiple sources
(3–5 where available)** so the reader can see not just what happened, but how
different outlets are covering it — including their editorial lean/bias.

The goal is a report that reads like a well-edited front page: authoritative,
multi-sourced, transparent about bias, and skimmable in a few minutes.

**Core output, every run: the Report Page**
- Exactly 10 stories, ranked by importance
- Each story is summarized by pulling from **3–5 credible sources** when
  available
- Each story shows: headline, synthesized summary, and a **citation list**
  with outlet name, link, publish date, and known bias/lean for each source
  used
- If fewer than 3 credible sources exist for a story, that is **explicitly
  stated** in the story's summary (e.g. "Limited coverage — only 2
  independent credible sources found") rather than silently reported as if
  fully corroborated
- No non-credible source is ever included, regardless of how many sources
  are needed to hit the 3–5 target

---

## Project Structure

```
news-digest-agent/
├── CLAUDE.md                      # This file — context & rules
│
├── workflow/
│   ├── run-report.md              # Step-by-step process for each run
│   ├── source-checklist.md        # Criteria for vetting a source
│   ├── ranking-rubric.md          # How stories are scored/ranked
│   └── bias-synthesis-guide.md    # How to summarize across sources w/ bias
│
├── output/
│   ├── latest.md                  # Copy of the most recent report page
│   ├── index.md                   # Log of every report ever generated
│   ├── _report-template.md        # Template each saved report follows
│   └── [YYYY]/[MM]/[YYYY-MM-DD]_report.md   # Archived reports by date
│
└── resources/
    ├── preferred-sources.md       # Trusted outlet whitelist
    ├── excluded-sources.md        # Outlet blacklist
    ├── source-bias-ratings.md     # Bias/lean reference per outlet
    ├── topic-preferences.md       # Categories to prioritize/exclude
    └── glossary.md                # Continuity tracker for ongoing stories
```

**How to use this structure:**
- Before each run, read `workflow/run-report.md` for the process, and check
  `resources/` for preferences and bias reference data.
- After each run, save the output into `output/[year]/[month]/`, update
  `output/latest.md`, and add a row to `output/index.md`.
- `resources/` files should be treated as living documents — update them
  directly as preferences or bias assessments change.

---

## Rules

### 1. Recency
- Only include stories with a confirmed publish/update date within the last
  7 days (relative to the moment the agent runs).
- If a major story broke slightly outside the window but is still actively
  developing and highly relevant, it may be included — flag it explicitly as
  "ongoing story, originally broke on [date]."
- Never include evergreen, undated, or stale content to fill out the count
  of 10.

### 2. Source quality (unchanged — non-negotiable)
- Only credible, established outlets may be cited: major wire services,
  national/international newspapers, established broadcasters, official
  statements/press releases.
- Never include low-quality aggregators, unverified social media posts,
  content-farm sites, satire, or anonymous/unattributed sources.
- Every citation must include the real outlet name, a working direct link,
  and the publish date.
- **Credibility is never sacrificed to hit the 3–5 source target.** If only
  1–2 credible sources exist, use only those and say so explicitly.

### 3. Multi-source requirement (new)
- Each story should be synthesized from **3–5 credible sources** when that
  many independent, credible reports exist.
- Sources must be genuinely independent reporting, not the same wire copy
  republished — e.g. don't count both "Reuters" and a local paper's verbatim
  Reuters reprint as two separate sources.
- If fewer than 3 credible independent sources exist, state this plainly in
  the story summary, e.g.:
  > "Limited coverage: only 2 credible sources reporting as of publish time."
- Never pad the source list with weak/borderline sources just to reach the
  3–5 target.

### 4. Bias transparency (new)
- For each source cited, note its general editorial lean using
  `resources/source-bias-ratings.md` as the reference (e.g. Left-leaning,
  Center, Right-leaning, or "Wire/Neutral" for wire services).
- The goal is not to editorialize about which outlet is "right," but to let
  the reader see the spread of coverage — e.g. "Reported by Reuters
  (Neutral), NYT (Left-leaning), and WSJ (Right-leaning), with consistent
  core facts across all three."
- If coverage is lopsided (e.g. only left-leaning or only right-leaning
  outlets are reporting a story), note that explicitly — it's relevant
  context, not something to hide.
- If sources disagree on facts (not just framing), note the discrepancy
  rather than picking a side.

### 5. Selection / importance ranking
- Prioritize stories with broad impact: global or national significance,
  large numbers of people affected, financial markets, major political or
  policy events, significant conflict/security developments, major
  disasters, and landmark scientific/technological developments.
- Avoid celebrity gossip, routine sports results, and purely local
  human-interest stories unless they have outsized national/global
  relevance.
- Aim for topical diversity across the 10 stories, unless one event is
  genuinely dominating the week's news cycle.
- If fewer than 10 stories meet the importance bar, say so rather than
  padding the list with filler.

### 6. Summaries (now synthesized across sources)
- Each story's summary should synthesize the 3–5 sources into one coherent,
  neutral account — not a list of separate mini-summaries per outlet.
- Roughly 3–6 sentences (slightly longer than a single-source digest, since
  it's now representing multiple reports).
- State what happened, who's involved, why it matters, and note any
  meaningful differences in how outlets are framing it.
- Do not copy sentences verbatim from any source; always paraphrase in
  original wording.
- No speculation presented as fact. If something is unconfirmed/developing
  across all sources, say so.

### 7. Objectivity & tone
- The synthesized summary itself stays neutral — bias context belongs in
  the citation list/framing note, not in Claude's own narrative voice.
- Where sources have significant factual disputes (not just tone), note
  that briefly rather than picking a side.
- Consistent, professional, newspaper-editorial tone across all 10 stories.

### 8. Output format — the Report Page
- Formatted like a newspaper front page: a top masthead (date range,
  generation date), followed by 10 stories ranked by importance.
- Each story block includes:
  1. Headline
  2. Synthesized summary (3–6 sentences)
  3. Coverage note if source count < 3
  4. Citation list: outlet, lean/bias, link, date — one line per source
- See `output/_report-template.md` for the exact structure.
- Optionally group by section (World, Politics, Business, Science/Tech,
  etc.) like a real paper's sections — but importance ranking takes
  priority over section grouping.
- Keep the whole report readable in under 5–7 minutes (it's longer than
  the old single-source digest, given multi-source synthesis).

### 9. Process / tool use
- Always fetch fresh, live information for each run — never answer from
  memory.
- For each story, actively search for multiple outlets covering it, not
  just the first result — target 3–5 credible, independent sources before
  settling for fewer.
- If search/fetch tools return conflicting or unclear dates, err on the
  side of excluding the story rather than guessing.
- Note the exact date range covered at the top of the report.

### 10. Things to avoid
- No duplicate stories or near-duplicate stories covering the same event
  from different angles counted as separate items.
- No fabricated sources, links, quotes, or bias ratings — if a source or
  its lean can't be verified, either omit that source or mark the lean as
  "Unrated."
- No reproducing full article text or long verbatim passages (copyright).
- No filler items just to reach exactly 10 stories, and no filler sources
  just to reach 3–5 citations.
- No editorializing about which outlet's framing is "correct."

---

## Open Items (to be refined by the user)

- [ ] Preferred news categories / topics to prioritize or exclude
- [ ] Preferred geographic focus (global, US-only, specific region?)
- [ ] Preferred output delivery format (chat, HTML file, PDF, Markdown?)
- [ ] Preferred run cadence (daily trailing 7 days? weekly on a fixed day?)
- [ ] List of preferred/excluded specific sources
- [ ] Bias rating system to use (simple L/C/R, or a numeric scale?)
- [ ] Desired summary length/style adjustments
