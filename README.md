# econ5200-lab07-bootstrapping

# Diagnosing Broken Confidence Intervals

## Objective
I tested when bootstrap and parametric confidence intervals fail, and how to fix them, using real census-style ages, simulated skewed data, and clustered wage data.

## Methodology
- Bootstrapped the median of 32,561 integer ages and checked the standard error and the BCa interval.
- Simulated skewed data (n = 50) across 400 experiments and counted how often nominal 95% intervals contained the true value, for both the mean and the median, using parametric and bootstrap methods.
- Bootstrapped wages from 25 firms two ways: treating workers as independent, and resampling whole firms (cluster bootstrap). I compared interval width and coverage between the two.
- Put the percentile, i.i.d. and cluster bootstrap functions in a `bootstrap_utils.py` module.
- Had an AI write a coverage function, revised my prompt once, and checked its output against my own coverage numbers.

## Key Findings
- **Degenerate median bootstrap:** The bootstrap SE of the median of the 32,561 ages was 37. BCa returned nan with a warning instead of an interval. The ages are integers, so the bootstrap medians take very few distinct values.
- **Coverage on skewed data (nominal 95%):**
  - Mean: parametric 92.5%, bootstrap 92%.
  - Median: parametric 66.8%, bootstrap 92.8%.
- **Clustered data:** Bootstrapping the 25 firms' wages as independent workers gave an interval [$59,092, $60,121]x too narrow, with 91% coverage. Resampling whole firms brought coverage to 95%.
- **AI-written coverage function:** After one prompt revision, I checked it against my own coverage numbers: 92.8%.
