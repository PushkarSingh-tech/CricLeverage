# CricLeverage

Ball-by-ball win probability, a Pressure Index, and clutch ratings for T20 cricket.

## Overview

CricLeverage estimates each team's chance of winning after every ball of a T20 match,
then uses those probabilities to measure how much pressure a moment carries and how
players perform when it matters most.

The project has three parts:

1. **Win-probability model**: predicts the winner from the live match state
   (score, wickets, balls left, run rate, required rate, venue, and recent momentum).
   Logistic regression is the baseline, compared against LightGBM. First and second
   innings are modelled separately.
2. **Pressure Index**: a per-ball metric combining how close the match is, how much
   the next ball or over could swing win probability, and the required rate against
   balls remaining. Validated by checking that it spikes in known last-over finishes.
3. **Clutch ratings**: compares each batter's and bowler's performance in high-pressure
   situations against what was expected, using runs above expected and win probability
   added. Bayesian shrinkage and confidence intervals keep low-sample players from
   getting misleading ratings.

## Data

Ball-by-ball data from [Cricsheet](https://cricsheet.org) (IPL, T20Is and more),
parsed into one row per delivery. Rain-affected (DLS) matches are filtered out.

## Evaluation

- Train/test split by season, never by random rows, to avoid leakage between balls
  of the same match
- Metrics: log loss, Brier score, and calibration curves
- Test of whether "clutch" performance persists across seasons, rather than assuming
  it is a stable skill

## Results

- Brier score: _X.XX_ | Log loss: _X.XX_
- Calibration plot: _insert chart_
- Pressure Index across a famous match: _insert chart_
- Top and bottom clutch performers: _insert table_

## Limitations

- Clutch ratings rely on small samples even after shrinkage
- The model does not account for individual matchups (e.g., specific bowler vs batter)
- Results depend on the leagues and years included in the training data

## Tech stack

Python, pandas, scikit-learn, LightGBM, matplotlib

## How to run

_Add setup and run instructions here._
