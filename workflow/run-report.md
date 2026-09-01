# Run Process: Weekly News Report Page

This is the exact sequence to follow every time the report is generated.
Refer to `/CLAUDE.md` for the underlying rules — this file is the
actionable checklist version.

---

## Step 1 — Set the window
- Determine today's date and calculate the 7-day lookback window
  (e.g. "Aug 20–27, 2026").
- This range will be printed at the top of the report as the masthead.

## Step 2 — Gather candidate stories
- Search for major news across the window using live search tools (never
  rely on memory/training data).
- Pull from a spread of categories: World, Politics, Business/Markets,
  Science & Tech, Conflict/Security, Health, Climate/Disaster — adjust
  based on `resources/topic-preferences.md`.
- Aim to gather more candidate stories than needed (~15–20) so there's
  room to filter down to the strongest 10.

## Step 3 — Filter by date
- Drop anything outside the 7-day window unless it's a genuinely ongoing,
  still-developing major story (see CLAUDE.md Rule 1).
- If a date can't be confirmed, drop the story rather than guess.

## Step 4 — For each candidate story, gather multiple sources
- Search specifically for **additional outlets** covering the same story —
  don't stop at the first result.
- Target 3–5 independent, credible sources per story.
- Run every candidate source through `workflow/source-checklist.md`.
- If a story only turns up 1–2 credible sources after a genuine search
  effort, proceed with what exists — do not force in a weak source to
  hit the target.
- Record for each source: outlet name, link, publish date, and bias/lean
  (from `resources/source-bias-ratings.md`; mark "Unrated" if the outlet
  isn't in the reference file yet).

## Step 5 — Rank by importance
- Score remaining candidates using `workflow/ranking-rubric.md`.
- Select the top 10, keeping topical diversity in mind.

## Step 6 — Synthesize summaries across sources
- For each of the 10 stories, write one synthesized 3–6 sentence summary
  drawing on all gathered sources — not separate summaries per outlet.
- Follow `workflow/bias-synthesis-guide.md` for how to handle framing
  differences and lopsided coverage.
- If source count is below 3, add an explicit coverage note (see CLAUDE.md
  Rule 3).

## Step 7 — Format the Report Page
- Use `output/_report-template.md`.
- Order stories 1–10 by importance.
- Attach the full citation list (outlet, lean, link, date) under each
  story.

## Step 8 — Save to the archive
- Save the report as a new file:
  `output/[YYYY]/[MM]/[YYYY-MM-DD]_report.md`
- Update `output/latest.md` with a copy of (or link to) the new report.
- Add a new row to `output/index.md` with: date, date range covered,
  #1 headline, and total source count used across the report.

## Step 9 — Deliver
- Present the report page in chat (and/or wherever delivery is
  configured — see Open Items in CLAUDE.md).

---

## Quick checklist (per run)
- [ ] Date window calculated
- [ ] Candidates gathered from live search (~15–20)
- [ ] Filtered to last 7 days
- [ ] 3–5 credible sources sought per story (or fewer, explicitly noted)
- [ ] All sources vetted against source checklist
- [ ] Bias/lean recorded per source
- [ ] Ranked using rubric, top 10 selected with topical diversity
- [ ] Summaries synthesized (not per-outlet, one coherent account each)
- [ ] Coverage notes added where source count < 3
- [ ] Formatted using the Report Page template
- [ ] Saved to dated archive file
- [ ] `latest.md` updated
- [ ] `index.md` row added
