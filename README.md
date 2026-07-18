# FinancialXRecap

A Claude skill that scans X/Twitter financial accounts daily and generates
structured Obsidian-compatible trading intelligence reports in French. It can
use the Xquik API for structured, read-only data or a browser when no API key
is configured.

## What it does

- Scans configurable X/Twitter accounts for trading ideas, macro commentary, and market signals
- Preserves post URLs, timestamps, and source method for review
- Generates a daily markdown report with per-account summaries and cross-account key takeaways
- Saves to your Obsidian vault with proper YAML frontmatter and tags
- Optionally sends a Telegram notification with a short summary

## Default accounts

- `@NCheron_bourse` - French market analyst (commodities, European equities, macro)
- `@ValueSeeker_` - Value/commodity investor (oil, precious metals, macro charts)
- `@Convertbond` - Lawrence McDonald (macro, stagflation, factor rotation)

## Installation

Copy the skill folder to your Claude skills directory, or install via the `.skill` package.

## Usage

Say things like:
- "Lance le scan X trading"
- "Recap des comptes trading"
- "Qu'est-ce que disent les traders aujourd'hui ?"
- "Scan @NCheron_bourse et @Convertbond"

## Requirements

- One X source:
  - `XQUIK_API_KEY` for structured, read-only access through
    [Xquik](https://xquik.com)
  - Claude with Chrome browser access as a fallback
- `curl` and `jq` when using Xquik
- Telegram skill (optional, for notifications)

## Configuration

- `FINANCIAL_X_RECAP_DIR` sets the report directory. If it is unset, the skill
  asks for a location or uses `./reports` in the current workspace.
- `XQUIK_API_KEY` enables Xquik. Keep it in the environment and never place it
  in prompts, reports, or committed files.

Reports are research summaries, not investment advice. Verify material claims
against primary market or issuer sources before acting.

Xquik is an independent third-party service. Not affiliated with X Corp. "Twitter" and "X" are trademarks of X Corp.
