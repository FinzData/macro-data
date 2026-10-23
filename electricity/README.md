# Electricity (244 series)

Free package: the last 12 months of the latest values for every series in this category, refreshed weekly.

| File | What it holds |
|---|---|
| `long.csv` | `series_id, date, value`: one row per observation (latest revised values) |
| `series.csv` | every series: id, title, units, frequency, seasonal adjustment, where its full history starts, last update |
| `top_series.csv` | the most-watched series in this category |
| `sample.csv` | the first 10 rows, for a quick look |

```python
import pandas as pd
df = pd.read_csv("https://raw.githubusercontent.com/FinzData/macro-data/main/electricity/long.csv", parse_dates=["date"])
wide = df.pivot(index="date", columns="series_id", values="value")
```

Same data as Parquet on Hugging Face: [FinzData/macro-electricity](https://huggingface.co/datasets/FinzData/macro-electricity).

Need more than 12 months? The FinzData API has the full history of each series, **every vintage** (what the number was on any past date, before revisions) and same-day updates when a release lands:

```python
import finzdata as fz   # pip install finzdata
c = fz.Client()                    # free key: https://api.finzdata.com/
c.macro("<series_id>", as_of="2020-03-01")   # exactly what was published by that date
```

[All categories](../README.md) · [Pricing](https://finzdata.com/pricing) · Source: U.S. government agencies via FRED/ALFRED (Federal Reserve Bank of St. Louis). Research data, not investment advice.
