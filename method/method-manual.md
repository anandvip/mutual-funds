# Method Manual — fat-tail test v1.1

This manual records how the fat-tail research decides whether an Indian direct-plan mutual fund has a fat upside tail. We will simplify on the go, keep the method easy to check, and add new strategies as new versioned entries — never by overwriting an old one. The current test is v1.1. The v1 marks are kept below as a superseded entry.

This is not investment advice. Nothing here is an offer, a recommendation, or a decision to buy or sell any fund.

## Purpose

The goal is capital growth: to find funds whose big up months come more often, and are larger, than their big down months, to spot emerging stars early, and to drop the rest.

Vipul Anand decides. Agents research, check, record and propose. No agent buys, sells, or tells Vipul to act. After a fund has survived the research cadence below, only Vipul decides whether any real money is used.

## What is public and what is private

This public repository holds the method, the fund-level metrics and the weekly reports.

A private Google Sheet holds blind calls, state of mind and the near-miss ledger. Those records are never published here.

## Fat-tail test v1.1

A fund is treated as fat-tail when it passes at least 3 of the 4 marks below. All four marks are measured on monthly returns over the fund's full direct-plan history.

Direct plans (the share class with no distributor commission) began in January 2013, so "full history" is at most about 13 to 14 years, and is shorter for newer funds.

Vipul set these marks on 17 November 2026 (India Standard Time). The timing of the 90-day lock is still to be confirmed. This manual does not claim that the lock has started.

### The four marks (v1.1)

| Mark | What it measures | v1.1 pass mark |
| --- | --- | --- |
| 1. Skew of monthly returns | Whether the fund's big moves lean upward, relative to its category | Skew strictly above the category-median skew |
| 2. Upside / downside capture versus the Nifty 50 and versus the category median | Gains the fund catches versus losses it takes, both against India's 50-share large-cap index and against its own category | Upside capture above downside capture on **both** comparisons (unchanged from v1) |
| 3. Best 10% / worst 10% month ratio | The average of the best tenth of months, divided by the size of the average of the worst tenth of months, relative to the Nifty 50 proxy | Ratio strictly above the Nifty 50 proxy's own ratio (1.249 on data as of 16 November 2026) |
| 4. Ulcer Index, with recovery time for information | How deep and how long the drawdowns are | Ulcer Index strictly below the category median (unchanged from v1) |

**Skew** is the bias-corrected Fisher–Pearson sample skewness (the same figure as a spreadsheet `SKEW` function). A positive value means the right-hand tail is heavier than the left. The category-median skew is the median skew of other funds in the same current category that themselves have at least 36 months of returns. The fund passes if its skew is strictly above that median.

**Capture** uses the Morningstar annualised compounded definition. The fund is compared with two benchmarks: a Nifty 50 proxy (see [Data sources](#data-sources)) and the median monthly return of other direct-plan Growth funds in the same current category. The mark passes only if upside capture is above downside capture on both comparisons. If either comparison cannot be computed, the mark fails.

**Best / worst ratio.** If a fund has *n* monthly returns, *k* is the larger of 1 and *n* rounded to the nearest 10%. The ratio is the average of the best *k* monthly returns, divided by the absolute average of the worst *k* monthly returns. The hurdle is the Nifty 50 proxy's own ratio, computed the same way. On data as of 16 November 2026 that hurdle was 1.249 (exact value 1.248543, from 17 of 166 monthly returns). The fund passes if its ratio is strictly above that hurdle.

**Ulcer Index** follows Peter Martin's definition: the square root of the mean of squared percentage drawdowns from the running peak, measured on month-end Net Asset Values (NAVs). The category median is taken only from funds in the same current category that themselves have at least 36 months of returns. The fund passes if its Ulcer Index is strictly below that median.

**Recovery time** is reported for information. It is not a pass or fail mark. It is the longest spell, in months, from a peak to a new high — or to the last month, if that spell is still open.

A mark that cannot be computed is treated as a fail for the 3-of-4 count.

### History rules

- A full verdict needs at least **36 months** of direct-plan monthly returns.
- Funds with **12 to 35 months** go on a provisional track. They may only be labelled "emerging-star candidate". They are never labelled "fat-tail".
- Funds with fewer than 12 months are insufficient for this test.

### Backtest note (v1.1)

A historical test of the v1.1 marks was run on 17 November 2026 at 9:42 PM India Standard Time (UTC+05:30), on Association of Mutual Funds in India (AMFI) direct-plan NAV history from 2013, with 16 November 2026 as the as-of date. The universe and the four metric values were the same as in the v1 backtest; only the pass marks for skew and the best / worst ratio changed.

Among the 408 funds with at least 36 months:

- Mark 1 (skew above the category median) passed 49%.
- Mark 2 (upside capture above downside capture on both comparisons) passed 56%.
- Mark 3 (best / worst ratio above the Nifty 50 proxy's 1.249) passed 40%.
- Mark 4 (Ulcer Index below the category median) passed 49%.
- 150 of 408 passed at least 3 of 4.

This note is not a ranking, a shortlist, or advice.

## Superseded: fat-tail test v1

v1 is superseded by v1.1. It is kept here so the change is visible. It is not overwritten.

**What changed, from what to what, and why.** On 17 November 2026 Vipul set relative marks for two of the four tests. Mark 1 changed from "skew above 0" to "skew strictly above the category-median skew". Mark 3 changed from "best / worst ratio above 1.0" to "best / worst ratio strictly above the Nifty 50 proxy's own ratio" (1.249 on data as of 16 November 2026). Marks 2 and 4 were unchanged. The reason: in the v1 backtest, on the same 408 funds, skew above 0 passed only 8%, and the best / worst ratio above 1.0 passed 97%. Those two absolute marks did not tell funds apart, so they were replaced with relative hurdles.

### The four marks (v1, superseded)

These were recorded as proposals. They were not locked.

| Mark | What it measures | v1 proposed pass mark |
| --- | --- | --- |
| 1. Skew of monthly returns | Whether the fund's big moves lean upward | Skew above 0 |
| 2. Upside / downside capture versus the Nifty 50 and versus the category median | Gains the fund catches versus losses it takes, both against India's 50-share large-cap index and against its own category | Upside capture above downside capture on **both** comparisons |
| 3. Best 10% / worst 10% month ratio | The average of the best tenth of months, divided by the size of the average of the worst tenth of months | Ratio above 1.0 |
| 4. Ulcer Index, with recovery time for information | How deep and how long the drawdowns are | Ulcer Index strictly below the category median |

### Backtest note (v1)

A historical test of the v1 proposed marks was run on 17 November 2026 (India Standard Time), on the same AMFI direct-plan NAV history, with 16 November 2026 as the as-of date.

- 408 funds had at least 36 months and were tested for a full verdict.
- Proposed mark 1 (skew above 0) passed 8% of those funds.
- Proposed mark 3 (best / worst ratio above 1.0) passed 97% of those funds.

## Cadence: from first look to a decision

No real money is used until a fund has survived 4 weeks of research and 90 days on paper.

1. **Daily check.** A short look at NAV moves, fund news and interrupt triggers. No status or verdict changes on a daily run.
2. **Weekly review (Sunday).** Vipul first writes a private blind one-line call on each fund. Those calls live only in the private Google Sheet and are never published here. Then the data is run, verdicts are drafted and checked, and any status change is recorded. Status changes happen only at this weekly review.
3. **Week 3 triage.** Each fund moves to watching or cold storage. A fund is dropped only if it fails the long-history tail test.
4. **Week 4 report.** Findings go into the published weekly report, using the public [weekly-report template](../templates/weekly-report.md).
5. **90-day paper sandbox.** Shortlisted funds and emerging-star candidates are tracked on paper for 12 weekly runs. Pass and fail rules for the sandbox are written down before day 1.
6. **Real money (Vipul only).** After a pass, Vipul alone decides whether to enter. Agents may record that decision in the private sheet. They never suggest an amount.

## Data sources

Every published number carries its as-of date. Anything recalled but not checked is labelled "unverified".

- **AMFI `NAVAll.txt`.** The official daily list of scheme codes, names, categories and latest NAVs, published by the Association of Mutual Funds in India.
- **NAV history from mfapi.in.** The dated NAV series for each scheme code, used to build month-end NAVs and monthly returns.
- **Nifty 50 proxy.** Official Nifty 50 Total Return Index (TRI) data was not available from the usual public index sites at the time of the backtest. The proxy is the NAV of UTI Nifty 50 Index Fund, Direct Plan, Growth (AMFI scheme code 120716). This series is a total-return proxy minus the fund's expense ratio and tracking difference.

Index funds, exchange-traded funds, funds of funds, hybrid schemes, regular plans, and income-distribution (dividend) options are excluded from the test universe. Only open-ended equity direct-plan Growth schemes are tested.

## Caveats

- **Survivorship bias.** Only schemes still listed on today's AMFI file are tested. Closed or merged funds are absent, which typically flatters average results.
- **Current category applied to all history.** Each fund is compared with its category as it stands today, for the whole of its history. The Securities and Exchange Board of India (SEBI) reclassified fund categories in 2017–18. This method does not reconstruct the pre-2018 classification.
- **Pre-April 2018 comparisons are flagged "unverified".** If a category comparison uses any monthly return from before April 2018, that fund is marked `unverified`.
- **Sectoral / Thematic is a mixed category.** It is a single official category covering very different themes (for example infrastructure, pharma and technology). A category median for that group is a mixed benchmark.
- **Vintages are not strictly comparable.** A fund launched after 2020 will not have lived through earlier years, so its Ulcer Index and skew are not directly comparable with a 2013-vintage peer, even though each fund is measured on its own full history.
- **Month-end rule.** The month-end NAV is the last available NAV of each calendar month. Monthly returns are computed only between adjacent calendar months. A missing calendar month is skipped rather than filled in.

## How numbers are produced

Every metric is calculated by code from shared, dated data files. No one calculates skew, capture, the best / worst ratio, the Ulcer Index or recovery time in chat. The published fund-metrics file follows [`fund-metrics-format.md`](fund-metrics-format.md).

## Change process

Never overwrite. A changed conclusion, a changed rule, or a revised mark is a new versioned entry that points to the old one and says what changed, from what to what, and why.

Anyone can propose a change; only Vipul approves one. Vipul set the v1.1 pass marks on 17 November 2026. The timing of the 90-day lock is still to be confirmed. Once the lock starts, those test rules stay locked for 90-day periods, except to fix a data bug.

Every proposal records: what it changes (for example v1 → v1.1), why it should work, the backtest result, the pass/fail rule set in advance, Vipul's decision, and the date.

## Abbreviations

- AMFI: Association of Mutual Funds in India
- NAV: Net Asset Value
- SEBI: Securities and Exchange Board of India
- TRI: Total Return Index
