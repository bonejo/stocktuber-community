# StockTuber public JSON API

Free, read-only, no API key. Data is an aggregation of what tracked finance YouTubers say; **not investment advice**. AI-generated summaries may contain errors.

Base URL: `https://stocktuber.com`

## `GET /api/public/stocks`

Today's most-discussed stocks with sentiment scores.

```bash
curl -s "https://stocktuber.com/api/public/stocks"
```

Each item includes `ticker`, `name`, `sentiment_score` (0–100, 50 = neutral), `bullish_pct`, `neutral_pct`, `bearish_pct`, `creators`, `opinions`, and `url`.

## `GET /api/brief?tickers=NVDA,TSLA`

A brief for the tickers you hold: sentiment score, change versus the previous day, buy / hold / sell counts, bull and bear points, and the latest creator views.

```bash
curl -s "https://stocktuber.com/api/brief?tickers=NVDA,TSLA"
```

- `POST /api/brief` also works with body `{"holdings":["NVDA","TSLA"]}`.
- Add `?lang=zh` (or `{"lang":"zh"}`) for Chinese text.
- A ticker with no recent coverage is returned with `covered: false`.

## Sentiment score

`round((bullish% − bearish%) / 2 + 50)`; 100 = all bullish, 0 = all bearish. "Most-discussed" reflects creator attention, not a recommendation.
