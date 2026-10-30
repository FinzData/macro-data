# FinzData macro data

[![Series](https://img.shields.io/badge/series-7615-0B1B3F)](https://finzdata.com/datasets)
[![Point in time](https://img.shields.io/badge/vintages-every%20revision-9DB0CC)](https://finzdata.com/docs)
[![PyPI](https://img.shields.io/pypi/v/finzdata?label=pip%20install%20finzdata)](https://pypi.org/project/finzdata/)

Free, ready-to-use US and international macroeconomic data: **7,615 series in 23 categories**,
one folder per category, each loading in one line of pandas. No API key, no sign-up, no scraping.

```python
import pandas as pd
df = pd.read_csv("https://raw.githubusercontent.com/FinzData/macro-data/main/inflation/long.csv", parse_dates=["date"])
```

## Categories

| Category | Series | Folder | Parquet on Hugging Face |
|---|---|---|---|
| Consumption | 1,602 | [consumption/](consumption/) | [FinzData/macro-consumption](https://huggingface.co/datasets/FinzData/macro-consumption) |
| Trade | 1,432 | [trade/](trade/) | [FinzData/macro-trade](https://huggingface.co/datasets/FinzData/macro-trade) |
| Inflation | 960 | [inflation/](inflation/) | [FinzData/macro-inflation](https://huggingface.co/datasets/FinzData/macro-inflation) |
| Labor | 595 | [labor/](labor/) | [FinzData/macro-labor](https://huggingface.co/datasets/FinzData/macro-labor) |
| Other Indicators | 363 | [other-indicators/](other-indicators/) | [FinzData/macro-other-indicators](https://huggingface.co/datasets/FinzData/macro-other-indicators) |
| Liquidity | 340 | [liquidity/](liquidity/) | [FinzData/macro-liquidity](https://huggingface.co/datasets/FinzData/macro-liquidity) |
| Consumption, International | 326 | [consumption-international/](consumption-international/) | [FinzData/macro-consumption-international](https://huggingface.co/datasets/FinzData/macro-consumption-international) |
| Housing | 273 | [housing/](housing/) | [FinzData/macro-housing](https://huggingface.co/datasets/FinzData/macro-housing) |
| Rates | 271 | [rates/](rates/) | [FinzData/macro-rates](https://huggingface.co/datasets/FinzData/macro-rates) |
| Electricity | 244 | [electricity/](electricity/) | [FinzData/macro-electricity](https://huggingface.co/datasets/FinzData/macro-electricity) |
| Consumer Credit | 184 | [consumer-credit/](consumer-credit/) | [FinzData/macro-consumer-credit](https://huggingface.co/datasets/FinzData/macro-consumer-credit) |
| Money and Credit | 182 | [money-credit/](money-credit/) | [FinzData/macro-money-credit](https://huggingface.co/datasets/FinzData/macro-money-credit) |
| Income and Spending | 166 | [income-spending/](income-spending/) | [FinzData/macro-income-spending](https://huggingface.co/datasets/FinzData/macro-income-spending) |
| Productivity | 137 | [productivity/](productivity/) | [FinzData/macro-productivity](https://huggingface.co/datasets/FinzData/macro-productivity) |
| Production | 120 | [production/](production/) | [FinzData/macro-production](https://huggingface.co/datasets/FinzData/macro-production) |
| Growth | 105 | [growth/](growth/) | [FinzData/macro-growth](https://huggingface.co/datasets/FinzData/macro-growth) |
| FX | 81 | [fx/](fx/) | [FinzData/macro-fx](https://huggingface.co/datasets/FinzData/macro-fx) |
| Other | 60 | [other/](other/) | [FinzData/macro-other](https://huggingface.co/datasets/FinzData/macro-other) |
| Commodities | 59 | [commodities/](commodities/) | [FinzData/macro-commodities](https://huggingface.co/datasets/FinzData/macro-commodities) |
| Orders and Trade | 50 | [orders-trade/](orders-trade/) | [FinzData/macro-orders-trade](https://huggingface.co/datasets/FinzData/macro-orders-trade) |
| Financial Conditions | 39 | [financial-conditions/](financial-conditions/) | [FinzData/macro-financial-conditions](https://huggingface.co/datasets/FinzData/macro-financial-conditions) |
| Population | 13 | [population/](population/) | [FinzData/macro-population](https://huggingface.co/datasets/FinzData/macro-population) |
| Recession | 13 | [recession/](recession/) | [FinzData/macro-recession](https://huggingface.co/datasets/FinzData/macro-recession) |

Each folder holds `long.csv` (series_id, date, value), `series.csv` (titles, units, frequency, seasonal adjustment,
start of full history, last update), `top_series.csv` and a 10-row `sample.csv`.

## What is free here, and what the API adds

| | This repository (free) | FinzData API |
|---|---|---|
| Values | latest revised values | latest values **and every vintage** |
| History | last 12 months | full history of every series |
| Updates | weekly | same day, as each release lands |
| Point in time (`as_of`) | no | yes: what was known on any past date |
| Release calendar | no | yes |
| Formats | CSV, Parquet | JSON, CSV, Parquet, pandas, MCP for AI agents |

## Why vintages matter

Macro numbers are revised, often a lot. A backtest that uses today's revised payrolls or GDP for a 2020 decision
uses numbers nobody had in 2020. FinzData keeps every vintage, so you can ask for a series as it stood on any date:

```python
import finzdata as fz          # pip install finzdata ; free key: https://api.finzdata.com/
c = fz.Client()
as_known = c.macro("CPIAUCSL", as_of="2020-05-01")   # CPI as published by that date
latest   = c.macro("CPIAUCSL")                       # after every revision since
```

AI agents get the same data through the MCP server at `https://api.finzdata.com/mcp` (tool `get_macro_vintage`).

## Update schedule

Refreshed weekly from the source agencies. The API updates each series the day it is released; see data freshness at
https://finzdata.com/status.

## Source and license

U.S. government agencies via FRED and ALFRED (Federal Reserve Bank of St. Louis). Only public-domain series are
included; series with third-party copyright are excluded. Packaging and documentation: CC BY 4.0, attribution
"FinzData". Research data, not investment advice.

**Links:** [Pricing](https://finzdata.com/pricing) · [Python client](https://github.com/FinzData/finzdata-python) ·
[Strategies built on this data](https://github.com/FinzData/hub-strategies) · [Docs](https://finzdata.com/docs)
