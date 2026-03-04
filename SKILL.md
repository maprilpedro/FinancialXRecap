---
name: financial-x-recap
description: |
  Scan X/Twitter accounts for trading ideas, market analysis, and financial insights, then generate a structured Obsidian-compatible markdown report in French. Use this skill whenever the user asks to scan X/Twitter for trading ideas, recap financial accounts, check what traders are posting, get a daily market scan, or generate a trading intelligence report from social media. Also trigger when the user mentions "x scan", "trading scan", "recap X", "what are [trader names] saying", "daily scan", "market recap from X", or any variation of monitoring financial X/Twitter accounts for investment signals.
---

# Financial X Recap

Scan a configurable list of X/Twitter accounts for recent trading ideas and market commentary, then produce a structured daily report saved as an Obsidian note. Optionally notify the user via Telegram with a short summary.

## Why this skill exists

Financial Twitter/X is one of the richest sources of real-time market intelligence, but it's scattered across accounts and mixed with noise. This skill automates the daily ritual of checking multiple accounts, extracting what matters, and organizing it into a single actionable report — so the user starts their trading day with a clear picture instead of scrolling for 30 minutes.

## Default accounts

If the user doesn't specify accounts, use these defaults:

- `@NCheron_bourse` — Nicolas Chéron, French market analyst (commodities, European equities, macro)
- `@ValueSeeker_` — Value/commodity investor (oil, precious metals, macro charts)
- `@Convertbond` — Lawrence McDonald (macro, stagflation thesis, factor rotation)

The user can override this list by specifying different accounts in their prompt. If they say something like "scan @X and @Y", use those accounts instead of the defaults.

## Workflow

### Step 1: Scan each account

For each account, use the Chrome browser tools to:

1. Navigate to `https://x.com/<account_handle>`
2. Wait for the page to load (3 seconds)
3. Extract the page text with `get_page_text`
4. Scroll down and capture more posts (at least 2-3 scroll passes)
5. Take screenshots if charts or images seem important for context

Focus on posts from the last 24-48 hours. Skip pinned posts unless they're recent. Include reposted content if it's market-relevant — the user cares about what the account is signal-boosting, not just original posts.

### Step 2: Extract trading signals

For each account, identify and categorize:

- **Specific trade ideas** — long/short calls with tickers, price levels, targets
- **Macro commentary** — inflation data, geopolitical events, central bank signals
- **Technical analysis** — chart patterns, support/resistance levels, moving averages
- **Sector/factor rotation signals** — what's leading, what's lagging, why

Ignore promotional content (course sales, book promos, subscriber pitches) unless it contains substantive analysis alongside the promotion.

### Step 2b: Translate to French

All content in the report must be written in French, regardless of the original language of the posts. Several default accounts post in English (e.g., @ValueSeeker_, @Convertbond). When summarizing their posts:

- Translate all key points, analysis, and commentary into natural, fluent French
- Keep financial tickers, symbols, and proper nouns as-is (e.g., $EURCHF, WTI, S&P 500, ISM, MACD, Novo Nordisk)
- Keep numbers and price levels as-is (e.g., "$69.8", "70.5", "0.905")
- Use commonly accepted French financial terms when they exist (e.g., "overbought" → "suracheté", "breakout" → "cassure", "bullish" → "haussier", "bearish" → "baissier", "stagflation" remains "stagflation")
- If a quote from the original post is particularly impactful, you can include a short excerpt in the original language in parentheses, but the surrounding summary must be in French

This applies to everything: the .md report file, the Key Takeaways section, and the Telegram notification. The user should never have to mentally translate English when reading the output.

### Step 3: Generate the report

Write the report entirely in French. Use this structure:

```markdown
---
date: YYYY-MM-DD
tags: [trading, x-scan]
---

# X Trading Scan — [Date in French format, e.g. "4 Mars 2026"]

## Contexte du jour
[1-2 phrases sur le thème dominant du marché s'il y en a un — événement géopolitique, publication macro, etc. Sinon, sauter cette section.]

---

## @handle (Nom)
[Répéter pour chaque compte]

**[Sujet] ([timeframe, ex. "il y a 6h"])**
- Point clé 1
- Point clé 2
- Niveaux/tickers mentionnés

---

## Points Clés

1. **[Thème]** — [Synthèse inter-comptes, insight actionnable]
2. **[Thème]** — [...]
[3-5 points max. Focus sur la convergence entre comptes — quand plusieurs comptes pointent vers le même trade ou thème, c'est le signal le plus fort.]
```

The Key Takeaways section is the most important part. It should synthesize across accounts, not just repeat what each one said. If two accounts are both bullish on the same asset for different reasons, say so. If they disagree, flag the divergence.

### Step 4: Save the report

Save to the user's Obsidian vault. The default path is:

```
/Users/maprilpedroferreira/MPFEVault/X-Trading-Scan-YYYY-MM-DD.md
```

If the user specifies a different path, use that instead. If you don't have write access to the vault, save to the workspace folder and tell the user where to find it.

If a report for today's date already exists, append a suffix (e.g., `-v2`) rather than overwriting.

### Step 5: Telegram notification (optional but default)

After saving the report, send a concise summary via Telegram using the `telegram` skill. The message must be in French. Format:

```
📊 X Trading Scan — [Date]

[Point clé 1 en français]
[Point clé 2 en français]
[Point clé 3 en français]

📄 Rapport complet dans Obsidian
```

If the Telegram skill is not available or fails, don't block on it — just inform the user that the report is ready without the notification.

## Edge cases

- **Account suspended or unavailable**: Note it in the report and move on to the next account
- **No recent posts (>48h)**: Write "[Account] — Pas de posts récents" and move on
- **Login wall / rate limiting**: If X shows a login wall, try scrolling past it. If blocked, note it and try the next account
- **Weekend/holiday**: Markets are closed but accounts might still post macro analysis. Run normally but note that markets were closed if relevant
