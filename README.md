# A/B test analysis framework

## Problem statement

Data-driven organizations run dozens of A/B tests simultaneously, but without rigorous statistical methodology the results are prone to false positives, peeking bias, and multiple comparison errors. This project provides a reusable framework that analyzes controlled experiments using frequentist, Bayesian, and sequential methods, giving decision-makers clear, defensible recommendations on which changes to ship.

## Approach

- **Frequentist testing**: z-test for proportions and Welch's t-test for continuous metrics, with effect sizes (Cohen's h / d) and confidence intervals
- **Bayesian A/B testing**: Beta-Binomial model with uninformative priors, posterior sampling, P(B>A), and credible intervals for relative lift
- **Sequential monitoring**: O'Brien-Fleming spending function for valid early stopping without inflating the false positive rate
- **Multiple comparison correction**: Bonferroni, Holm, and Benjamini-Hochberg FDR methods applied across simultaneous experiments
- **Power analysis**: sample size calculator for planning future experiments given baseline rate, MDE, alpha, and power

## Key results

| Experiment | p-value | Significant? | Bayesian P(B>A) |
|-----------|---------|-------------|-----------------|
| Website redesign | 0.008 | Yes | 0.996 |
| Pricing change | 0.260 | No | 0.869 |
| Email subject | <0.001 | Yes | 1.000 |

## How to run

```bash
pip install -r requirements.txt
python data/generate_data.py
streamlit run app.py
```

## Project structure

```
project_16_ab_test_framework/
  data/
    ab_test_results.csv
    generate_data.py
  src/
    __init__.py
    experiment.py
    visualizations.py
  notebooks/
    01_analysis.ipynb
  figures/
    conversion_exp_001.png
    posterior_exp_001.png
    sequential_exp_001.png
    ...
    sample_size_mde.png
    forest_plot.png
  app.py
  requirements.txt
  README.md
```

## Technical stack

Python, SciPy, scikit-learn, pandas, matplotlib, Streamlit
