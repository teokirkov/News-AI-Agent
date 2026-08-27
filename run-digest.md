# Run Process: Weekly News Digest

This is the exact sequence to follow every time the digest is generated.
Refer to `/CLAUDE.md` for the underlying rules — this file is the actionable
checklist version.

---

## Step 1 — Set the window
- Determine today's date and calculate the 7-day lookback window
  (e.g. "Aug 20–27, 2026").
- This range will be printed at the top of the output file.

## Step 2 — Gather candidate stories
- Search for major news across the window using live search tools
  (never rely on memory/training data).
- Pull from a spread of categories: World, Politics, Business/Markets,
  Science & Tech, Conflict/Security, Health, Climate/Disaster — adjust
  based on `resources/topic-preferences.md` once defined.
- Aim to gather more candidates than needed (~20–25) so there's room to
  filter down to the strongest 10.

## Step 3 — Filter by date
- Drop anything outside the 7-day window unless it's a genuinely ongoing,
  still-developing major story (see CLAUDE.md Rule 1).
- If a date can't be confirmed, drop the story rather than guess.

## Step 4 — Vet sources
- Run each candidate against `workflow/source-checklist.md`.
- Cross-check important/surprising claims against a second source.
- Drop anything that fails the checklist or can't be corroborated.

## Step 5 — Rank by importance
- Score remaining candidates using `workflow/ranking-rubric.md`.
- Select the top 10, keeping topical diversity in mind (don't let one
  event crowd out everything else unless it's genuinely dominating the
  week).

## Step 6 — Write summaries
- For each of the 10, write a 2–4 sentence neutral, factual summary in
  original wording (see CLAUDE.md Rule 4).
- Attach outlet name, link, and publish date.

## Step 7 — Format the output
- Use the standard template (see `output/` template below / CLAUDE.md
  Rule 6).
- Order 1–10 by importance.

## Step 8 — Save to the archive
- Save the digest as a new file:
  `output/[YYYY]/[MM]/[YYYY-MM-DD]_digest.md`
- Update `output/latest.md` with a copy of (or link to) the new digest.
- Add a new row to `output/index.md` with: date, date range covered, and
  the #1 headline.

## Step 9 — Deliver
- Present the digest in chat (and/or wherever delivery is configured —
  see Open Items in CLAUDE.md).

---

## Quick checklist (per run)
- [ ] Date window calculated
- [ ] Candidates gathered from live search
- [ ] Filtered to last 7 days
- [ ] Sources vetted against checklist
- [ ] Ranked using rubric
- [ ] Top 10 selected with topical diversity
- [ ] Summaries written (neutral, paraphrased, 2–4 sentences)
- [ ] Formatted using standard template
- [ ] Saved to dated archive file
- [ ] `latest.md` updated
- [ ] `index.md` row added
