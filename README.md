# Urban Transit Dynamics and Extreme Weather (Group 7)

How extreme heat, cold, snow and heavy rain relate to transit ridership in New York City (MTA subway) and Chicago (CTA 'L' rail and bus), 2017–2025, comparing 2017–19 with 2022–25.

## Files

| File | What it is |
|---|---|
| `Group7_Step2.ipynb` | **The final notebook.** Cleaning, cleaning log, spot-checks, briefing pack (P1–P7), Round 2 follow-up requests and Round 3 challenges. This is the one to print for submission. |
| `Group7_Step0_Clean_Join_Explore.ipynb`, `..._v2.ipynb` | Earlier Step 0 versions, kept for history. |
| `Alex_Shirley_Rebecca_LLM_Conversations.pdf` | The three stakeholder conversations (Rounds 1–3). |
| `figures/` | Charts written by the notebook: P1–P6 (briefing pack) and P7 (Round 2). |
| `data/raw/` | Cached downloads (NOAA, MTA, CTA). Not in git. |
| `data/clean/` | Cleaned and joined tables, result tables, and `cleaning_log_all_sources.csv`. Not in git. |

## Data sources

- **NYC MTA Subway Hourly Ridership:** NY Open Data `t69i-h2me` (2017–19), `wujg-7c2s` (2020–24), `5wq4-mkjj` (2025+), plus the station list `39hk-dx4f`
- **CTA:** Daily Boarding Totals `6iiy-9s97`, 'L' Station Entries `5neh-572f`, 'L' stops `8pix-ypme`, community areas `igwz-8jzy` (Chicago Data Portal)
- **NOAA GHCN-Daily:** NCEI Data Service API; Central Park, LaGuardia, JFK, O'Hare and Midway

## Running the notebook

1. Use Python 3 with `pandas`, `numpy`, `matplotlib` and `requests` (last run with Python 3.13, pandas 2.2, numpy 2.4, matplotlib 3.10, via Anaconda).
2. Open `Group7_Step2.ipynb` from the project folder (paths are relative to it) and run all cells top to bottom.
3. **First run:** the notebook downloads everything into `data/raw/`. The MTA part is slow: 108 monthly files at about 35 seconds each, roughly an hour. To skip that, copy a teammate's `data/raw/` folder into the project first. With the cache in place, a full run takes about 2 minutes. It still needs internet for a few small calls: the MTA spot-check's 20 hourly lookups and the CTA stops and community-area lists.
4. Optional: a free Socrata app token reduces throttling on the NY and Chicago open-data APIs. Set it before starting Jupyter:
   ```
   export SOCRATA_APP_TOKEN=your_token_here
   ```

The notebook stops with `CHECK FAILED: …` if anything is wrong: a missing cached month, a join that doesn't match, a spot-check difference no cleaning step explains, and so on. A run that finishes means every check passed.

## Outputs

- **Cleaning log:** every decision (issue, rows affected, action, rejected alternative) in `data/clean/cleaning_log_all_sources.csv`, also printed in full in Part 10 of the notebook.
- **Results:** `data/clean/result_*.csv`, % change on extreme-weather weekdays vs. a normal weekday, by system, area and station, with sensitivity views.
- **Charts:** `figures/P1`–`P7`.
