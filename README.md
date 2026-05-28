# aso-audit

A Claude Code skill for a comprehensive ASO health audit of an App Store listing. Scores ten factors, produces an overall ASO score, and outputs a prioritized action plan (quick wins / this week / strategic).

## What it does

Scores each factor 0-10, weighted into an overall score:

| Factor              | Weight |
|---------------------|--------|
| Title               | 20%    |
| Subtitle (iOS)      | 15%    |
| Keyword field (iOS) | 15%    |
| Description         | 5% iOS / 15% Android |
| Screenshots         | 15%    |
| App preview video   | 5%     |
| Ratings & reviews   | 15%    |
| Icon                | 5%     |
| Keyword rankings    | 10%    |
| Conversion signals  | 5%     |

### Plus: Promise-Delivery Thread Check

A cross-cutting section that traces each primary keyword through:

```
keyword → title/subtitle → screenshot 1-3 → description hook
       → first-launch screen → onboarding → aha moment → core feature
```

…to catch the single biggest leak between a high-ranking keyword and actual retained users. A keyword that ranks #3 but has a broken thread is worth less than a #8 keyword with a clean one.

For the full end-to-end version of this check (extending into the running app), see [`funnel-consistency`](https://github.com/hyojinmo/funnel-consistency).

## Install

```bash
git clone https://github.com/hyojinmo/aso-audit.git ~/.claude/skills/aso-audit
```

## Usage

Triggers:

- "ASO audit", "ASO score"
- "review my listing", "listing review"
- "why am I not ranking"
- "optimize my App Store page"

The skill will ask for App ID, target country, and platform (iOS / Android / both).

## Output

```
Overall ASO Score: [X]/100

Title:              [X]/10  ████████░░
Subtitle:           [X]/10  ██████░░░░
...

Quick wins (today):           [3-5 items]
High-impact (this week):      [3-5 items]
Strategic (this month):       [3-5 items]
Competitor comparison:        [table]
Promise-Delivery threads:     [score per primary keyword + weakest hop]
```

## Structure

```
SKILL.md   # Full audit framework, scoring rubrics, output format
```

## How it pairs

- [`keyword-research`](https://github.com/hyojinmo/keyword-research) — deep dive into opportunities surfaced during audit
- [`metadata-optimization`](https://github.com/hyojinmo/metadata-optimization) — implements metadata changes identified
- [`funnel-consistency`](https://github.com/hyojinmo/funnel-consistency) — end-to-end version of the Promise-Delivery Thread Check
- [`product-operations`](https://github.com/hyojinmo/product-operations) — quarterly review uses this skill

## Status

Private, used by [@hyojinmo](https://github.com/hyojinmo). Preparing for open source.
