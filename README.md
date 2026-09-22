# The AI Trading Floor

A structured, multi-lens trading system: six specialist "agents," each scanning one domain, every setup routed through one Risk Manager before anything executes. You invoke it with **"run the floor."**

**The honest principle:** six agents don't create six edges — they create six *lenses* and one *gate*. The Risk Manager is the star. Its most common output should be "stand down." This is a discipline machine, not a trade-manufacturing machine.

---

## The workflow
```
        SCAN                ANALYZE            RISK CHECK           MANAGE
  [6 agents scan their  →  each reports a  →  Risk Manager    →  execute survivors,
   own domain]             setup OR passes     scores all          stop on entry,
                                               against rules       monitor/trail
```

---

## The 6 agents (and what each can actually do in this account)

| Agent | Job | Execution status |
|---|---|---|
| **1. Momentum** | Breakouts, volume spikes, relative-strength leaders on a green tape | ✅ Full — trades live |
| **2. Swing** | Multi-day structure, support/resistance, pullback-to-support, base breakouts | ✅ Full — trades live |
| **3. News/Earnings** | Earnings reactions (PEAD), macro catalysts, gap-and-go vs fade | ✅ Full — trades live |
| **4. Options (income)** | Covered calls + cash-secured puts (Level 2). Reads IV/premium/OI | ⚠️ Income only — no spreads/flow trading |
| **5. Quant** | Designs/reasons through backtests, probabilities, position math, expectancy | ⚠️ Analysis only — no live backtest engine |
| **6. Crypto** | Monitors crypto price/volume/funding | ❌ Analysis only — account can't trade crypto |

**Be honest about 4-6:** Options trades only what Level 2 allows, Quant *informs* rather than executes, Crypto can *comment* but cannot place a trade in this equities/options account. They earn their seat as *analysts*, not executors.

---

## Each agent's scan checklist

**Momentum** — SPY green + near highs? Name up more than market, breaking out on RVOL >1.3, price whole-share-friendly, not extended >15-20%? → propose entry + real stop 4-7% below breakout.

**Swing** — Beaten-down name that *based* and is reclaiming support on volume (not a falling knife)? Or a pullback to a rising level in an uptrend? → propose entry + stop below structure.

**News/Earnings** — Any holding/watchlist name reporting? >5% reaction on 2x volume? Beat+gap = long the drift on retest; miss/cut = avoid/fade. Never chase the spike. → propose retest entry + stop beyond reaction low.

**Options (income)** — A holding stalled → covered call above cost. A name I'd own dropping → cash-secured put at a strike I'd accept. Check OI >500, spread <15%. → propose strike/expiry + collateral.

**Quant** — For any proposed setup: what's the historical base rate of this pattern? Is size correct for 1.5%? Is expectancy positive after costs? → stamps each setup PASS/FAIL on math.

**Crypto** — Directional read on BTC/ETH as a *risk-on/off signal* for the equity book (crypto leads risk sentiment). → informs regime, does not trade.

---

## The Risk Manager (the gate — nothing executes without it)

Every proposed setup is scored against these HARD limits. Any red = rejected.

| Check | Limit |
|---|---|
| **Risk per trade** | ≤ 1.5% of account (sized via stop distance) |
| **Concurrent positions** | ≤ 3 open trades |
| **Correlation** | No more than 1 position per theme/sector cluster |
| **R:R** | ≥ 1.5:1 |
| **Regime gate** | Long momentum/swing only when SPY green + near highs |
| **Liquidity** | ≥ $20M/day dollar volume |
| **Cash** | Must have settled buying power to fund it |
| **Daily loss limit** | Stop all new trades after −3% account day |
| **The stand-down rule** | If nothing clears, the verdict is "no trades." That is a valid, common, correct output. |

**Risk Manager output format:**
```
FLOOR REPORT — [date/time] — Regime: [green/flat/red]
  Momentum:  [setup or PASS]
  Swing:     [setup or PASS]
  News:      [setup or PASS]
  Options:   [setup or PASS]
  Quant:     [PASS/FAIL stamp on each]
  Crypto:    [risk-on / risk-off read]

RISK MANAGER VERDICT:
  ✅ EXECUTE: [ticker, entry, stop, size, R:R]  — or —
  👁  WATCH:   [ticker, trigger level]           — or —
  ⛔ STAND DOWN: nothing clears the gate today
```

---

## How to run it
- **You say "run the floor"** → I run all 6 scans, the Risk Manager scores everything, and you get one ranked verdict.
- I execute **only** what the Risk Manager clears, and place the stop on the same fill.
- On flat/red tape or thin cash, expect "stand down" often — that's the system protecting you, not failing.

## What this is NOT
- **Not autonomous** — it runs when you prompt, not in the background. No 3 AM crypto trades.
- **Not six edges** — it's six lenses + one disciplined gate. The edge is process and risk control.
- **Not a reason to overtrade** — more agents scanning must never mean more trades forced. The gate holds.

*Not investment advice. Educational tool for a self-directed account.*
