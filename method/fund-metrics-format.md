# Fund-metrics file format

This is the column layout for each published fund-metrics file. The file is a comma-separated values (CSV) table: one header row, then one row per fund that has a usable Net Asset Value (NAV) series.

The figures are calculated by code from the data sources in the [method manual](method-manual.md). They are not typed by hand. Every file carries an as-of date (the Association of Mutual Funds in India (AMFI) `NAVAll.txt` date used for that run).

This is not investment advice. An example row is included only to show the layout. It is clearly labelled **EXAMPLE** and uses fictional values, not a real fund.

## File naming

Published files should be named with the as-of date, for example `fund-metrics-2026-11-16.csv`, so a new run never overwrites an old one.

## Flags and verdicts

- Pass flags, `unverified` and `recovery_open` use `Y` or `N`.
- If a metric cannot be computed (for example, too little history), its value is left blank and the matching pass flag is `N`.
- `passes` is the count of the four proposed marks that the fund clears (0 to 4). A blank metric counts as a fail.
- `verdict` is one of:
  - `fat-tail` — at least 36 months, and at least 3 of 4 marks passed
  - `not` — at least 36 months, and fewer than 3 marks passed
  - `provisional` — 12 to 35 months (emerging-star-candidate track only; never labelled fat-tail)
  - `insufficient` — fewer than 12 months

The pass marks themselves are proposals under review. See the [method manual](method-manual.md). The Nifty 50 is India's 50-share large-cap index; the proxy used for it is described there.

## Columns

| Column | Type | Unit | Meaning |
| --- | --- | --- | --- |
| `scheme_code` | integer | AMFI scheme code | Official scheme identifier |
| `scheme_name` | text | — | Scheme name as listed by AMFI |
| `category` | text | — | Current AMFI equity category (applied to the whole history; see the caveats in the method manual) |
| `fund_house` | text | — | Fund house as listed by AMFI |
| `months` | integer | count of monthly returns | Number of adjacent-month returns in the series |
| `first_month` | date (`YYYY-MM-01`) | — | First month in the month-end series |
| `last_month` | date (`YYYY-MM-01`) | — | Last month in the month-end series |
| `first_nav_date` | date (`YYYY-MM-DD`) | — | First usable NAV date |
| `last_nav_date` | date (`YYYY-MM-DD`) | — | Last usable NAV date |
| `skew` | decimal | dimensionless | Bias-corrected Fisher–Pearson skew of monthly returns |
| `skew_pass` | `Y` / `N` | — | `Y` if skew is above 0 |
| `upside_capture_nifty` | decimal | ratio (1.0 = matched the benchmark's upside) | Upside capture versus the Nifty 50 proxy |
| `downside_capture_nifty` | decimal | ratio (1.0 = matched the benchmark's downside) | Downside capture versus the Nifty 50 proxy |
| `capture_nifty_pass` | `Y` / `N` | — | `Y` if upside capture is above downside capture versus the Nifty 50 proxy |
| `upside_capture_category` | decimal | ratio | Upside capture versus the category-median monthly return |
| `downside_capture_category` | decimal | ratio | Downside capture versus the category-median monthly return |
| `capture_category_pass` | `Y` / `N` | — | `Y` if upside capture is above downside capture versus the category median |
| `capture_pass` | `Y` / `N` | — | `Y` only if **both** capture comparisons pass |
| `best_worst_ratio` | decimal | dimensionless | Average of the best 10% of months, divided by the size of the average of the worst 10% of months |
| `best_worst_k` | integer | count of months | Number of months in each tail (`max(1, round(10% of months))`) |
| `best_worst_pass` | `Y` / `N` | — | `Y` if the ratio is above 1.0 |
| `ulcer_index` | decimal | percent, Peter Martin's Ulcer Index | Depth and length of drawdowns on month-end NAVs |
| `category_ulcer_median` | decimal | same as `ulcer_index` | Median Ulcer Index of same-category funds that have at least 36 months |
| `category_ulcer_median_n` | integer | count of funds | Number of same-category funds used for that median |
| `ulcer_pass` | `Y` / `N` | — | `Y` if the fund's Ulcer Index is strictly below the category median |
| `recovery_time_months` | integer | months | Longest spell from a peak to a new high, or to the last month if the spell is still open. For information only; not a pass mark |
| `recovery_open` | `Y` / `N` | — | `Y` if that longest spell has not yet made a new high |
| `passes` | integer | count, 0 to 4 | Number of the four proposed marks passed |
| `verdict` | text | — | `fat-tail`, `not`, `provisional`, or `insufficient` |
| `unverified` | `Y` / `N` | — | `Y` if any category comparison uses a monthly return from before April 2018 |
| `pre_april_2018_months` | integer | count of months | Number of monthly returns from before April 2018 |
| `nifty_up_months` | integer | count of months | Months in which the Nifty 50 proxy return was positive, over the fund's own window |
| `nifty_down_months` | integer | count of months | Months in which the Nifty 50 proxy return was negative or zero, over the fund's own window |
| `category_up_months` | integer | count of months | Months in which the category-median return was positive, over the fund's own window |
| `category_down_months` | integer | count of months | Months in which the category-median return was negative or zero, over the fund's own window |

Decimals in published files are written at six decimal places. Dates use the year-month-day form (YYYY-MM-DD).

## Example row (fictional)

The row below is an **EXAMPLE**. The scheme code, name and fund house are fictional. The figures are illustrative only and do not describe a real scheme.

```csv
scheme_code,scheme_name,category,fund_house,months,first_month,last_month,first_nav_date,last_nav_date,skew,skew_pass,upside_capture_nifty,downside_capture_nifty,capture_nifty_pass,upside_capture_category,downside_capture_category,capture_category_pass,capture_pass,best_worst_ratio,best_worst_k,best_worst_pass,ulcer_index,category_ulcer_median,category_ulcer_median_n,ulcer_pass,recovery_time_months,recovery_open,passes,verdict,unverified,pre_april_2018_months,nifty_up_months,nifty_down_months,category_up_months,category_down_months
999999,EXAMPLE Equity Fund (fictional),Flexi Cap Fund,Example Mutual Fund,72,2020-12-01,2026-11-01,2020-11-16,2026-11-16,-0.210000,N,1.080000,0.860000,Y,1.020000,0.980000,Y,Y,1.250000,7,Y,5.500000,6.200000,20,Y,18,N,3,fat-tail,N,0,42,30,45,27
```

Read as: this fictional fund has 72 months of returns, fails the proposed skew mark, passes the other three proposed marks, has a verdict of `fat-tail`, and is not flagged unverified.
