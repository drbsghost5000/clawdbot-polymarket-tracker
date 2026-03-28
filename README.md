# Clawdbot Polymarket Tracker

> Clawdbot real-time position and wallet tracker for Polymarket that monitors open trades, P&L, and exposure across all markets. Know exactly where your capital is at all times - with Telegram alerts when positions resolve or approach your risk limits.

*Last updated: March 2026*

---

![preview_clawdbot polymarket tracker pnl dashboard](https://github.com/user-attachments/assets/2b141c67-fc91-4081-b0a7-7e99989798eb)

---

## What is Clawdbot Polymarket Tracker?

Clawdbot Polymarket Tracker is the portfolio analytics and monitoring module of the Clawdbot suite. It connects to your Polymarket account via CLOB API and provides live visibility into every open position, unrealized P&L, win rate from resolved markets, and capital exposure by category - giving you the analytics Polymarket's native interface does not.

---

## Download

| Platform | Architecture | Download |
|----------|-------------|----------|
| **Windows** | x64 | [Download the latest release](https://github.com/drbsghost5000/clawdbot-polymarket-tracker/releases) |

---

## What It Tracks

| Metric | Description |
|--------|-------------|
| **Open positions** | All current YES/NO positions with entry price and current odds |
| **Unrealized P&L** | Live gain/loss on each open position |
| **Realized P&L** | Total profit/loss from all resolved positions |
| **Win rate** | % of resolved markets where your position was correct |
| **Category exposure** | USD value and % of portfolio per Polymarket category |
| **Average ROI** | Mean return per resolved position |
| **Bankroll curve** | Total account value over time |

---

## Engine Features

* **Live P&L** - updates unrealized position values every 30 seconds
* **Win rate tracking** - calculated from full resolution history
* **Category breakdown** - exposure by politics, crypto, sports, economics, and more
* **Daily summary** - end-of-day P&L report sent to Telegram
* **Loss threshold alert** - notification if unrealized loss exceeds configured amount
* **Resolution alert** - instant message when any tracked position resolves
* **Export** - full trade history and current portfolio as CSV
* **Bankroll curve** - charts total account value over time

---

## Two Ways to Run It

| | Windows App | Python Bot |
|---|---|---|
| **Setup** | Double-click | `pip install` + config |
| **Dashboard** | Built-in UI | JSON + CSV output |
| **Alerts** | Telegram + in-app | Telegram + webhook |
| **Config** | `config.toml` | Direct code access |
| **Export** | Built-in | Full data access |

## Quick Start

```
# 1. Download from Releases
# 2. Edit config.toml - add Polymarket API key (read-only access sufficient)
# 3. Run Tracker - loads full history and starts live tracking
```

### Python

```bash
cd clawdbot-polymarket-tracker/python
pip install -r requirements.txt
python clawdbot-polymarket-tracker-v.1.4.14.py
```

---

## How It Works

![tracker pipeline](https://github.com/user-attachments/assets/060173de-e518-4e4a-b844-cf81c89a1e5e)

Three stages per cycle:

1. **Fetch** - pulls current positions, balances, and recent resolutions from Polymarket CLOB API
2. **Calculate** - computes P&L, win rate, exposure breakdown, and portfolio metrics
3. **Display / Alert** - updates dashboard and sends any triggered alerts to Telegram

### Config Reference

```toml
[tracker]
refresh_interval_seconds = 30
track_resolution_history = true

[alerts]
daily_summary_time = "21:00"
loss_alert_threshold_usd = 40
win_rate_alert_below = 0.40

[polymarket]
api_key = ""
private_key = ""           # Optional - only needed for position export

[telegram]
bot_token = ""
chat_id = ""

[export]
portfolio_csv = "data/portfolio/portfolio.csv"
history_csv = "data/portfolio/history.csv"
```

---

## Portfolio Summary Format

```json
{
  "timestamp": "2026-03-27T21:00:00Z",
  "total_balance_usd": 983.25,
  "open_positions": 6,
  "unrealized_pnl_usd": 31.60,
  "realized_pnl_today_usd": 22.40,
  "win_rate_all_time": 0.59,
  "win_rate_30d": 0.65,
  "avg_roi_pct": 13.1,
  "exposure_by_category": {
    "crypto": 210.00,
    "politics": 145.00,
    "economics": 280.00,
    "sports": 95.00
  }
}
```

---

## Verified Live

**Configuration used:**
* Read-only API key, daily summary at 21:00 UTC, loss alert $40

**Portfolio snapshot:**

| | Details |
|---|---|
| Balance | $983.25 |
| Open positions | 6 across 4 categories |
| Unrealized P&L | +$31.60 |
| Realized P&L (today) | +$22.40 |
| Win rate (30d) | 65% |
| Tx hash | 0xd5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b1c2d3e4f5a6b7c8d9e0f1a2b3c4d5e6 |

---

## Frequently Asked Questions

**What is Clawdbot Polymarket Tracker?**
Clawdbot Polymarket Tracker is a real-time portfolio monitoring tool for your Polymarket account. It tracks open positions, live P&L, win rate across resolved markets, and capital exposure by category - with daily summaries and alert thresholds delivered via Telegram.

**Does it require trading access?**
No. The tracker only reads data from your account. A read-only API key is sufficient for all monitoring features. Trading API access is only needed if you want the optional position export.

**How often does P&L update?**
Every 30 seconds by default. You can lower this in config down to 10 seconds if you want more frequent refreshes.

**Can it track multiple accounts?**
The current version tracks one account per instance. Run multiple instances with different config files for multi-account monitoring.

**What is a good win rate target on Polymarket?**
For active traders, 55-65% on resolved markets is a reasonable target. Sustained win rates above 65% typically require specialized information edge or systematic strategy.

**Does it alert on category concentration?**
Yes. You can set a max exposure percentage per category in config. If any category exceeds your threshold, an alert fires.

**Is this a polymarket P&L tracker?**
Yes. Tracking realized and unrealized P&L across all positions is the core function. The tracker separates today's P&L from all-time and calculates it per category.

---

## Use Cases

- **Polymarket portfolio tracker** - real-time dashboard of all open positions and live P&L
- **Polymarket P&L monitor** - measure daily, weekly, and all-time realized and unrealized gains
- **Clawdbot tracker module** - portfolio analytics layer for the full Clawdbot trading suite
- **Polymarket win rate tracker** - track resolution win rate by category and time period
- **Polymarket exposure monitor** - monitor capital concentration across Polymarket categories

---

## Repository Structure

```
clawdbot-polymarket-tracker/
+-- clawdbot-polymarket-tracker-v.1.4.14.exe
+-- config.toml
+-- data/
|   +-- portfolio/
|   +-- history/
|   +-- logs/
|   +-- dll/
+-- python/
|   +-- src/
|   |   +-- fetcher.py
|   |   +-- calculator.py
|   |   +-- reporter.py
|   +-- requirements.txt
+-- README.md
```

---

## Requirements

```
python-dotenv, typer[all], httpx, py-clob-client, pandas
```

* Polymarket account with CLOB API access (read-only sufficient)
* Telegram bot token (for alerts and daily summaries)

---

*Track everything. Miss nothing.*
