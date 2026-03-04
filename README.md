# FinancialXRecap

A Claude skill that scans X/Twitter financial accounts daily and generates structured Obsidian-compatible trading intelligence reports in French.

## What it does

- Scans configurable X/Twitter accounts for trading ideas, macro commentary, and market signals
- Generates a daily markdown report with per-account summaries and cross-account key takeaways
- Saves to your Obsidian vault with proper YAML frontmatter and tags
- Optionally sends a Telegram notification with a short summary

## Default accounts

- `@NCheron_bourse` — French market analyst (commodities, European equities, macro)
- `@ValueSeeker_` — Value/commodity investor (oil, precious metals, macro charts)
- `@Convertbond` — Lawrence McDonald (macro, stagflation, factor rotation)

## Installation

Copy the skill folder to your Claude skills directory, or install via the `.skill` package.

## Usage

Say things like:
- "Lance le scan X trading"
- "Recap des comptes trading"
- "Qu'est-ce que disent les traders aujourd'hui ?"
- "Scan @NCheron_bourse et @Convertbond"

## Requirements

- Claude with Chrome browser access (for reading X/Twitter)
- Telegram skill (optional, for notifications)
