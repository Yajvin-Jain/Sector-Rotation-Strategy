# Sector Rotation Strategy

A momentum-based sector rotation strategy built to test a simple economic
idea: **different sectors of the market tend to lead at different points in
the business cycle**, and that relative strength tends to persist in the
short-to-medium term.

## The idea, in plain terms

The S&P 500 is made up of 11 sectors (Technology, Energy, Health Care,
Financials, etc.). At any given time, some sectors are outperforming the
broader market and some are lagging — often for macro reasons (interest
rates, growth expectations, commodity prices).

This strategy:
1. Looks back 6 months and ranks all 11 sectors by their return
2. Picks the **top 3 strongest** sectors
3. Holds them, equally weighted, for the next month
4. Repeats every month (re-ranking and rotating as needed)

The bet: sectors that have been strong recently tend to keep being
relatively strong in the near term (a well-documented effect known as
momentum / relative strength), so riding the current leaders should
outperform just holding the whole market.

## Data

- 11 SPDR sector ETFs (XLK, XLE, XLV, XLF, XLY, XLP, XLI, XLU, XLB, XLRE, XLC)
- Benchmark: SPY (S&P 500)
- Source: Yahoo Finance via the `yfinance` Python library
- Backtest period: 2015–present

## Methodology

- Monthly rebalancing
- 6-month trailing momentum as the ranking signal
- Top 3 sectors held equally weighted
- No transaction costs modeled (a simplification — noted as a limitation)

## Results

*(Run `sector_rotation.py` to generate current results — CAGR, volatility,
Sharpe ratio, and max drawdown for both the strategy and the S&P 500
benchmark, plus a chart comparing the two.)*

## How to run it

```bash
pip install -r requirements.txt
python sector_rotation.py
```

This will print performance metrics to the console and save a chart
(`backtest_results.png`) comparing the strategy against a simple S&P 500
buy-and-hold.

## Limitations & next steps

- No transaction costs or slippage modeled
- Momentum lookback (6 months) and portfolio size (top 3) were chosen for
  simplicity, not optimized — a natural next step would be testing
  sensitivity to these parameters
- Could be extended with macro signals (yield curve, ISM data) to more
  directly model business-cycle timing rather than relying on price
  momentum alone
