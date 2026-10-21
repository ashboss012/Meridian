# Run-the-Strategy Screener v2

One server-side scan over the 300-name universe (`watchlists/watchlist-300-v2.md`), then a Risk Manager pass. Replaces the old momentum, earnings and watchlist files.

## Step 0 — Fresh data, every time
Each run is a new session. Re-pull everything live; never reuse prior prices. Pull: portfolio + buying power, open orders, SPY quote.

## Step 1 — Regime gate
SPY green and above its 20-day average = long momentum/breakout setups allowed.
SPY flat or red = mean-reversion bases and options income only, or stand down.

## Step 2 — Scan (Robinhood `preview_scan`)
- Scope with `{"expression":"symbol","predicate":"ANY_OF","values":[...]}`. The tool returns max 200 rows per call, so run the universe in 2 chunks of ~150.
- Columns pulled: Last, % Change, RSI (14, 1d), Relative volume, Volume.
- Dead tickers silently drop out of the results, so compare the returned count to 300 on every run and replace anything missing.

## Step 3 — Four screens on the result set
| Screen | Rule | What it is |
|---|---|---|
| **Oversold bounce** | RSI <= 35, up on the day, price turning | Mean-reversion base. Needs a held low, not a falling knife |
| **Pullback in uptrend** | RSI 35-48, up >0.5% today, above 50-day trend | Buy the dip in a name that is already working |
| **Momentum** | RSI 55-70, up >2%, RVOL >= 1.3 (full-day) | Breakout / relative-strength leaders |
| **Extended** | RSI >= 75 | Do not chase. Watch for pullback or covered call |

Note: relative volume reads low intraday because the day is only partly done. Weigh it more after 2 PM ET, and treat it as a hard filter only on full-day data.

## Step 4 — Confirm survivors (top 3-5 only)
Per-symbol `get_equity_technical_indicators` (RSI, MACD, 20/50 SMA, ATR) and recent historicals for support. Pull `get_earnings_calendar` and skip anything reporting inside the hold window.

## Step 5 — Risk Manager gate (nothing executes without it)
- Risk <= 1.5% of account per trade
- <= 3 open swing positions, one per theme
- R:R >= 1.5 to the nearest real target (e.g. 50-day average)
- Liquidity >= $20M/day
- Funded from settled cash
- Stop = real structure (below the base low or support), not a fixed %
- No earnings inside the hold window
- Daily loss limit -3% account
- Valid outcome: STAND DOWN

## Step 6 — Execute
Whole shares. Limit entry. Place the stop-market GTC immediately on fill. Verify with `get_equity_orders(state="confirmed")` after every stop change. Resting limit entries get a fill check at the start of the next session.

## Sizing (dynamic, replaces the old fixed <=$30 cap)
shares = floor((0.015 x account) / (entry - stop)); position cost <= ~40% of settled cash.
At ~$2.5k account / ~$1.5k cash: risk ~ $38, max position ~ $600. A $100+ stock is tradeable only if the stop distance leaves >= 1 share inside that budget.

## Output format
FLOOR REPORT: regime, scan count (X/300 returned), top setups per screen, Risk Manager verdict (EXECUTE / WATCH / STAND DOWN).

*Not investment advice.*
