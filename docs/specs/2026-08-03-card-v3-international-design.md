# GitHub profile card v3 — international audience

Date: 2026-08-03. Supersedes 2026-07-30 design (instrument panel, 1200×340).

## Goal

Profile readable by an English-speaking recruiter / EU-US hiring engineer.
5-second scan must yield: Senior DE, production scale (TB/day, pipelines, consumers), proof of method (csv_to_click). Then they click into csv_to_click.

## Why v2 failed (measured live on github.com/Odarink)

- Card authored at 1200px; GitHub README column is 581–846px → scale 0.48–0.70.
  10px caps rendered 4.8–7.0px, org labels 5.6–8.1px — unreadable at every viewport.
- Career timeline duplicated the markdown list directly below it, at 8px.
- Timeline x-scale inconsistent: 326px/yr vs 141px/yr (2.3× spread), 2024 silently missing, 174px dead line after last dot.
- Headline sold a pet project (5.30× on CSV loader) while resume holds 5 yrs of prod at TB scale.
- Profile bio said "Student of BMSTU" — read before any card.

## Decisions

1. **SVG carries only what markdown cannot**: identity + stat row. Chart and company timeline leave the SVG. Career list lives in markdown (native font, always readable). csv_to_click story lives in its README section.
2. **Design at the narrow end**: viewBox 600×225. Rendered scale 0.968× (581px col) to 1.41× (846px col). Card never shrinks below ~1:1.
3. **Type floor is arithmetic**: min font in viewBox units 11.5px → 11.1px rendered worst-case. Acceptance-tested, not eyeballed.
4. **Headline = production scale**, not pet-project speedup. Numbers from user, honesty markers kept:
   - `≤2 TB` / INGESTED PER DAY — user said "up to 1–2 TB/day possible"; `≤` encodes "up to", covers capacity-vs-actual ambiguity.
   - `20–30` / PIPELINES IN PROD — user's own range for owned Airflow DAGs; range kept as-is, no rounding up.
   - `≈100` / USERS · 20+ TEAMS — user said "20+ teams, ~100 people".
5. **Mobile (~360px) degrades by design**: labels ~7px there. Accepted because every card fact is duplicated in README text below — markdown is the baseline, SVG is enhancement.

## Card spec

### Geometry (viewBox 600×225)

- Frame: rect 0.5,0.5 599×224, rx 12.
- Name x=32 y=50; role line x=32 y=74.
- Divider y=96, x 32→568.
- Stat cells left-aligned at x = 32, 220, 408 (3 × ~178px). Number baseline y=136, label baseline y=158.
- Divider y=182.
- Footer flow line x=32 y=207: `sources → warehouse → flows → marts → BI`.

### Type scale (viewBox units / worst-case rendered @581px)

| Class  | Size | Weight | Rendered min |
|--------|------|--------|--------------|
| name   | 27   | 600    | 26.1 |
| role   | 14   | 500    | 13.6 |
| num    | 26   | 600    | 25.2 |
| cap    | 11.5 | 600, ls 1px | 11.1 |
| foot   | 12   | 400    | 11.6 |

Font stack unchanged: `ui-sans-serif, -apple-system, "Segoe UI", Roboto, Helvetica, Arial, sans-serif`.

### Content

- Name: `Artem Kholdzhgonov`
- Role: `Senior Data Engineer · Moscow`
- Stats: `≤2 TB` / `INGESTED PER DAY` · `20–30` / `PIPELINES IN PROD` · `≈100` / `USERS · 20+ TEAMS`
- Footer: `sources → warehouse → flows → marts → BI`

### Colors

| Token   | Dark    | Light   |
|---------|---------|---------|
| bg      | #0D1117 | #FFFFFF |
| border  | #30363D | #D0D7DE |
| divider | #21262D | #D8DEE4 |
| name    | #E6EDF3 | #1F2328 |
| role    | #C9D1D9 | #424A53 |
| num     | #58A6FF | #0969DA |
| cap     | #8B949E | #57606A |
| foot    | #8B949E | #57606A |

Dark and light SVGs identical except color values (verified by diff after color-normalization).

### Accessibility

`role="img"` + aria-label:
`Artem Kholdzhgonov, Senior Data Engineer, Moscow. Up to 2 terabytes ingested per day, 20 to 30 pipelines in production, about 100 users across 20 plus teams. Data flow: sources to warehouse to flows to marts to BI.`

README `<img alt>` carries the same text.

## README structure

Order: card → one-liner → Where I've worked → Selected work → Contact.
(Production scale first, per approved design; csv_to_click second as proof of method.)

Company scale context added for non-RU readers (public common knowledge only, no invented figures):

- **Wildberries** — largest e-commerce marketplace in the CIS · Senior Data Engineer / Analyst · 2025 → now — up to 2 TB/day into ClickHouse, 20–30 Airflow DAGs in production, data serving 20+ teams (~100 analysts); Kafka, S3, PySpark
- **Sber** — largest bank in Eastern Europe · Data Engineer, Middle+ · 2023–2025 — consumer-credit risk marts on Greenplum and Hive/HDFS; data-quality tooling
- **Promsvyazbank** — top-10 Russian bank · Lead Database Analyst · 2022–2023 — RAW → STG → DDS → CDM on MS SQL; Power BI and a Flask service
- **LANIT** — one of the largest IT groups in Russia · Junior Data Engineer · 2021–2022 — Airflow ETL on PostgreSQL; API, FTP, HTTP and WFM sources

csv_to_click block kept (profiling story, 427 tests, stop-by-arithmetic) — second position, proof of method.

Contact line gains `Open to remote & relocation`.
Assumption, stated to user: hh.ru resume currently says the opposite ("не готов к переезду"); GitHub is written for the stated goal, hh is user's to fix.

BMSTU/rockets sentence kept, one line.

## Profile settings (user applies in GitHub UI; exact strings provided)

- **Bio** (replaces `Student of BMSTU`):
  `Senior Data Engineer · 5 yrs · Python, SQL, ClickHouse, Airflow, Kafka, Spark · retail & banking` (95 chars, limit 160)
- **Pins**: keep 4 — `csv_to_click` (first), `de-project-final`, `de-project-sprint-9`, `ozon_task_test`. Unpin `de-project-sprint-2` (fork of yandex-praktikum template) and `Odarink` (profile repo pinned to itself).
- **Repo descriptions**:
  - csv_to_click: `CSV → ClickHouse loader over plain HTTP. 500M rows / 5.5 GB in 369.6 s, 5.3× vs baseline. 427 tests + mutation testing.`
  - de-project-final, de-project-sprint-9, ozon_task_test: drafted at implementation time from actual repo contents, pattern `<what it does> — <stack>`, English, one line, no invented facts.

## Acceptance criteria

1. At 581px column width, no rendered text below 11.0px (arithmetic check on every font size × 0.968).
2. Dark/light SVGs differ only in color values.
3. aria-label and img alt match the numbers shown on the card.
4. Every fact on the card also appears in README text (mobile fallback).
5. Each SVG ≤ 6 KB, no external references, no scripts.
6. Visual check in browser at 581 / 846 / 390px, dark and light, before commit.

## Out of scope

- hh.ru resume edits (flagged to user separately).
- csv_to_click README rewrite.
- git push — requires separate explicit permission.
- GitHub UI clicks (bio, pins, descriptions) — user performs; strings come from this spec.
