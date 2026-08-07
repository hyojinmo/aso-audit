# aso-audit

A Claude Code skill for a comprehensive ASO health audit of an App Store listing. Scores ten factors, produces an overall ASO score, and outputs a prioritized action plan (quick wins / this week / strategic).

## Why use this one

Several open-source ASO audit skills exist with similar 10-factor scoring (Eronred/aso-skills, alirezarezvani/claude-code-aso-skill, others). The ten-factor rubric below follows the standard ASO industry framing — broadly shared across Phiture's ASO Stack, AppTweak, App Radar, and most open-source audits. **That's not where this skill differentiates.**

What's distinctive here:

1. **Promise-Delivery Thread Check (Hops A-D)** — a cross-cutting audit on top of the 10-factor scoring that traces each primary keyword through the storefront. Catches the single biggest leak between a high-ranking keyword and the user tapping Install with the right expectation. Most ASO audits score the title and the screenshot separately; this one asks "does the title's promise match what screenshot 1 shows, in the user's own word?"
2. **Clean hand-off to in-app** — the storefront-side thread (Hops A-D) lives here; the in-app continuation (Hops E-I: install → first launch → onboarding → aha → core feature) is delegated explicitly to [`funnel-consistency`](https://github.com/hyojinmo/funnel-consistency). Compose both audits for the full 9-hop funnel.
3. **Pairs with the Korean-first [`keyword-research`](https://github.com/hyojinmo/keyword-research)** that models user-search-intent (pain vs solution language, locale-specific patterns) before audit. Most ASO audits assume the keyword set is correct — this stack questions that upstream.

If you only need a basic 10-factor score with no thread-checking and no Korean/locale work, the simpler audits are fine. Use this one when promise-delivery consistency is the actual problem you're solving.

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
- `metadata-optimization` (not yet public) — implements metadata changes identified
- [`funnel-consistency`](https://github.com/hyojinmo/funnel-consistency) — end-to-end version of the Promise-Delivery Thread Check
- [`product-operations`](https://github.com/hyojinmo/product-operations) — quarterly review uses this skill

## Status

Used by [@hyojinmo](https://github.com/hyojinmo) for shipping indie iOS apps. Released as open source — issues and PRs welcome (see [CONTRIBUTING](CONTRIBUTING.md)).
