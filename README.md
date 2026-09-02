# Startup Investment Analysis

Exploratory analysis of a Crunchbase-derived startup funding dataset (54,294 companies, 40,907 after cleaning), ranking market segments for a hypothetical 2015 venture allocation using a composite score built from funding volume, company count, and returned capital.

**No live demo** — this is a single Jupyter notebook. Read it rendered on GitHub: [`startup_investment_analysis.ipynb`](startup_investment_analysis.ipynb)

---

## Status

Complete and not under development. This is a **data-analysis course capstone**, submitted as part of a Yandex Practicum data science program. The notebook, its narrative, and its section headings are **written in Russian**; this README is the English summary. The brief, the datasets, and the "advise a VC firm on 2015 allocations" framing came from the course, not from me — what is mine is the cleaning strategy, the feature engineering, the outlier treatment, and the scoring model.

Stating that plainly because the analysis is worth showing and its provenance shouldn't be guessed at.

## Data

Both files are fetched over HTTPS at the top of the notebook, so it is reproducible with no local data setup and nothing large is committed to this repo.

| Dataset | Shape | Source |
|---|---|---|
| `cb_investments` | 54,294 × 40 | `https://code.s3.yandex.net/datasets/cb_investments.zip` (`;`-separated) |
| `cb_returns` | 15 × 14 | `https://code.s3.yandex.net/datasets/cb_returns.csv` |

These are course-hosted snapshots. They are Crunchbase-derived and may have been trimmed or modified for teaching purposes; do not treat them as an authoritative Crunchbase extract. If the Yandex URLs go away, the notebook is no longer runnable as written.

## Method

1. **Cleaning** — drop rows with no funding data and no usable dates; normalize currency and date columns. Total data loss 34.5% (54,294 → 40,907 rows).
2. **Feature engineering** — derive a funding-duration group per company (single-round vs. extended cycle), then classify each of the 395 unique market segments into mass / mid / niche by company count (49 / 57 / 289).
3. **Outlier handling** — IQR fences computed *per segment* rather than globally, so a normal-sized round in a capital-heavy segment isn't discarded as an outlier. Flagged rather than deleted, then excluded from the ranking.
4. **Period trimming** — bound the analysis window and drop the Nov–Dec 2014 tail, which is under-reported in the snapshot and would depress the most recent trend.
5. **Dynamics** — year-over-year funding volume overall, by mass segment, and share of returned capital by financing type.
6. **Scoring** — composite 0–100 score per segment, normalized across volume, company count, and returned capital, to produce the ranking.

## Findings

Market structure:

- 395 unique market segments; 49 mass, 57 mid, 289 niche
- 59% of companies raise a single round
- companies with funding cycles longer than a year attract 60%+ of total investment

Financing types by volume:

| Type | Volume | Companies | Returned |
|---|---|---|---|
| Venture | $129.1B | 18,821 (52.9%) | $40.6B |
| Seed | $9.4B | 13,376 (37.6%) | $2.4B |
| Debt financing | $8.2B | 3,265 | $4.7B |

Top-ranked segments for a 2015 allocation:

| Rank | Segment | Score |
|---|---|---|
| 1 | Technology | 56.9 |
| 2 | Apps | 39.0 |
| 3 | Medical | 36.8 |

**Caveat on what this can support.** The composite score is a descriptive ranking of historical funding activity, not a return forecast. The weights were chosen by me and were not validated against out-of-sample outcomes; there is no train/test split and no uncertainty estimate on any of the three scores. A 56.9 versus a 39.0 says Technology had more funding activity and more returned capital in this snapshot — it does not establish that it was the better 2015 investment.

## Stack

Python 3.9 · pandas · NumPy · SciPy · Matplotlib · Seaborn

## Setup

```bash
git clone https://github.com/dudailia/startup-investment-analysis.git
cd startup-investment-analysis
python3 -m venv .venv && source .venv/bin/activate
pip install pandas numpy scipy matplotlib seaborn jupyter
jupyter notebook
```

Run the notebook top to bottom. The data-loading cell downloads both datasets, so no local files are required. No API keys, no `.env`, no credentials of any kind are needed.

## License

No license file. All rights reserved. The underlying datasets belong to their original publishers.
