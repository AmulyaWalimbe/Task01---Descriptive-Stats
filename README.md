# Task 1: Descriptive Statistics with and without Pandas

Analysis of the 2024 U.S. Presidential election Facebook political ads
dataset, computed two independent ways: pure Python (standard library
only) and Pandas. The goal is to verify both approaches agree, and to
reflect on where they differ.

## Project description

This repo contains two scripts that each load the same dataset and
compute descriptive statistics for every column: count, mean, min, max,
standard deviation, median for numeric columns; count, unique values,
mode, and top-5 frequencies for categorical columns; plus overall
shape, missing-value counts, and inferred data types.

- `pure_python_stats.py` — uses only `csv`, `re`, `math`, `statistics`,
  `collections` from the standard library.
- `pandas_stats.py` — uses Pandas (`read_csv`, `describe`,
  `value_counts`, `isna`, etc.) to do the same analysis.

## Dataset

**Source:** 2024 Facebook Political Ads dataset (Presidential election),
provided by course instructor.
Not included in this repo per instructions — download it separately and
place `fb_ads_president_scored_anon.csv` in the project root (or pass its
path as a command-line argument to either script).

- 246,745 rows
- 40 columns
- Each row = one ad purchase by a page/organization, where the ad
  mentions one or more presidential candidates.

### A data quirk worth knowing before you run anything

Three columns — `spend`, `impressions`, and `estimated_audience_size` —
are **not** plain numbers. Meta/Facebook obscures exact figures by
storing them as string-encoded ranges, e.g.:

```
{'lower_bound': '200', 'upper_bound': '299'}
```

Both scripts parse this and convert it to the midpoint of the range
(`249.5` in the example above) before computing statistics. This
decision is documented further in `COMPARISON.md`.

## How to run

```bash
# 1. Clone the repo
git clone <your-repo-url>
cd Task_01_Descriptive_Stats

# 2. Download the dataset separately and place it here as:
#    fb_ads_president_scored_anon.csv

# 3. Run the pure Python script (no install needed)
python pure_python_stats.py fb_ads_president_scored_anon.csv

# 4. Install Pandas and run the second script
pip install -r requirements.txt
python pandas_stats.py fb_ads_president_scored_anon.csv
```

Both scripts also default to looking for
`fb_ads_president_scored_anon.csv` in the current directory if no path
argument is given.

## Summary of findings

See `FINDINGS.md` for the full write-up. Headline points:

- Total ad spend across the dataset is about **$262 million** (using
  range midpoints). The top 10 spending pages account for about
  **63%** of that, led by the Kamala Harris campaign page (~$82.8M),
  Joe Biden (~$26.4M), and Donald J. Trump (~$19.6M).
- Spend rises sharply in the final two weeks before the election
  (week of Oct 27, 2024 alone: ~$36.4M).
- "Donald Trump" is the single most frequent named mention (53,182
  ads), ahead of "Kamala Harris." Candidate names aren't always
  formatted consistently in the data (e.g. "Donald Trump" vs.
  "President Trump" are counted separately).

## Comparing the two approaches

See `COMPARISON.md` for the full reflection. In short: the numeric
results **match exactly** between the two scripts once the range-dict
columns are handled the same way in both. The differences that showed
up were in *how much work it took to get there*, not in the final
numbers.

## Repo contents

```
Without_Pandas.ipynb   - stdlib-only descriptive stats
With_Pandas.ipynb         - Pandas descriptive stats
Findings of Task 01.pdf             - narrative analysis of the data
Comparison between With Pd& Without Pd.pdf           - reflection on the two approaches
requirements.txt        - dependencies for pandas_stats.py
README.md               - this file
```
