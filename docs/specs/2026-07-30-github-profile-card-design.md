# GitHub profile card — design

Date: 2026-07-30. Target: the profile README rendered at https://github.com/Odarink,
which requires a public repository named `Odarink/Odarink` (it does not exist yet).

## Goal

An engineering showcase, not a job pitch. The reader is a tech lead or an engineer who has
already seen the CV on hh.ru. The CV says *where* Artem worked; this page says *how he works*.

Decisions taken during brainstorming:

- **Purpose:** long-lived showcase. Not tuned for a specific vacancy, not ATS-driven.
- **Language:** English, single version. No `README.ru.md` — a second text would drift.
- **Visuals:** own SVG banner committed to the repo, plus static shields.io badges for the
  stack. Rejected `github-readme-stats` and streak/trophy cards: they depend on a third-party
  Vercel service that rate-limits into broken images, and the underlying numbers (0 stars,
  0 followers, 5 repos) argue against their owner.
- **Flagship:** `csv_to_click`, cited with numbers but **no infrastructure names**. The repo is
  public and its README contains an internal host; cleaning that repo is a separate task and is
  not in this scope.

## Structure

1. **Banner** — `<picture>` with dark/light sources, so it works in both GitHub themes.
   Content: name, role, one stack line, and three anchor numbers (1.36M rows/s, 500M rows,
   5.3×). Top right carries a sparkline of the four measured run times (1949 → 369.6 s) —
   the chart is the actual result, not decoration.
2. **What I do** — full data lifecycle in two short paragraphs; badges grouped by function
   (Core / Storage / Processing / Flow & BI) rather than dumped in one row.
3. **Selected work** — the run table, then the part that carries the page: measured before
   cutting (row loop was 90% of insert time), stopped on arithmetic (producer 291 s vs wire
   368 s converged), what was rejected and why, and an honest note that 427 green tests caught
   none of six defects while mutation testing and adversarial review caught all six.
4. **Track record** — one table row per employer, one sentence each. No duty lists; those are
   in the CV. Followed by the path from a rocket-systems degree to senior data engineer.
5. **Contact** — Telegram, email, languages. VK dropped as noise for this audience.

## Revision, same day — the first version read as a 2000s web page

The owner rejected v1 on design: too many colored badges, too much prose about one project.
Diagnosis and what changed:

- **20 shields.io badges in four rows** were the strongest period tell. Badges dropped entirely;
  the stack now lives as plain type inside the card.
- **Three markdown tables with full sentences in cells** became four one-line list items.
- **The flagship section ran ~450 words.** Cut to four bullets, ~70 words.
- **Four `---` rules** removed; headings do the dividing.
- Per `dataviz`: v1 had **no hero** — three equal 29px figures instead of one dominant number —
  and its area fill sat at 28% opacity instead of a ~10% wash.

Three directions were rendered with headless Chrome and compared: editorial (quiet, no chart),
instrument panel (chart + career timeline), hero number (`5.3×` at 108px). The owner chose the
instrument panel, the only one where the card itself carries information rather than just
introducing its owner. Its timeline also replaces the experience table that used to be text.

## Files

- `README.md`
- `assets/card-dark.svg`, `assets/card-light.svg` — 1200×340, system font stack (SVG served
  through GitHub's image proxy cannot load web fonts), no scripts, no external references.
  Layout: identity block left, ingest-time line chart right, career timeline across the bottom.
- `docs/specs/2026-07-30-github-profile-card-design.md` — this file.

## Out of scope, owner action required

1. Create the public `Odarink/Odarink` repository and push. Not done automatically.
2. Profile settings: bio still reads "Student of BMSTU" (four years stale); social link is VK.
   Account settings are the owner's to change.
3. The CV links `github.com/Odarink/test`, which 404s. Correct target: `github.com/Odarink`.
4. Repository hygiene: `csv_to_click` has no description and no topics; pin `csv_to_click` and
   `de-project-final`.
5. `csv_to_click` still exposes an internal hostname and environment defaults in its README.
