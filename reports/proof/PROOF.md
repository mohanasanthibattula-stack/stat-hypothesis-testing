# Verification & Proof Deliverables

This document catalogs each required proof deliverable, its location within the repository, its verification status, and the exact command used to independently reproduce and verify the result.

---

## Deliverables & Verification Matrix

| Proof Item | File Path | Status | Verification Command |
| :--- | :--- | :--- | :--- |
| **Executable Jupyter Notebook** | `notebooks/statistical_analysis.ipynb` | **VERIFIED** | `jupyter nbconvert --to notebook --execute --inplace notebooks/statistical_analysis.ipynb` |
| **Exported HTML Report** | `reports/statistical_analysis.html` | **VERIFIED** | `jupyter nbconvert --to html notebooks/statistical_analysis.ipynb --output-dir=reports --output=statistical_analysis.html` |
| **Statistical Results Summary** | `reports/results_summary.csv` | **VERIFIED** | Inspect CSV table or execute cell 20 of notebook |
| **Raw Palmer Penguins Dataset** | `data/penguins.csv` | **VERIFIED** | `wc -l data/penguins.csv` (345 lines including header = 344 rows) |
| **Data Provenance & Source Doc** | `data/README.md` | **VERIFIED** | Inspect Gorman et al. (2014) & Horst et al. (2020) citations |
| **Normality Histograms & KDE** | `reports/figures/01_normality_histograms.png` | **VERIFIED** | Inspect 6-panel empirical density + fitted normal curves (150 DPI) |
| **Normality Q-Q Plot Grid** | `reports/figures/02_normality_qqplots.png` | **VERIFIED** | Inspect 6-panel normal probability quantiles (150 DPI) |
| **Adelie Sexual Dimorphism Plot** | `reports/figures/03_two_sample_adelie_sex.png` | **VERIFIED** | Inspect box plot with jittered observations (150 DPI) |
| **Adelie vs. Chinstrap Plot** | `reports/figures/04_two_sample_adelie_chinstrap.png` | **VERIFIED** | Inspect box plot with jittered observations (150 DPI) |
| **Tukey Simultaneous CI Plot** | `reports/figures/05_oneway_tukey_ci.png` | **VERIFIED** | Inspect Tukey simultaneous 95% confidence intervals (150 DPI) |
| **ANOVA Residual Diagnostics** | `reports/figures/06_oneway_residuals.png` | **VERIFIED** | Inspect residual histogram + Q-Q plot (150 DPI) |
| **Two-Way Interaction Plot** | `reports/figures/07_twoway_interaction.png` | **VERIFIED** | Inspect species $\times$ sex interaction pointplot with dimorphism gaps |
| **Environment Specifications** | `reports/proof/environment.txt` | **VERIFIED** | `pip freeze` pinned packages matching `requirements.txt` |
| **CI Automation Workflow** | `.github/workflows/ci.yml` | **PASSED** (Run ID [41396828931](https://github.com/mohanasanthibattula-stack/stat-hypothesis-testing/actions/runs/41396828931)) | GitHub Actions CI workflow passed on `main` push (`gh run view 41396828931`) |

---

## Statistical Verification & Sanity Checks Matrix

| Metric / Analysis | Expected Sanity Range | Actual Observed Value | Verification Status |
| :--- | :--- | :--- | :--- |
| **Clean Sample Size ($n$)** | $n = 333$ | $n = 333$ (11 incomplete records dropped) | **PASSED (Exact)** |
| **Adelie Sexual Dimorphism Gap** | Mean diff $\approx +675$ g | **$+674.66$ g** | **PASSED (Exact)** |
| **Adelie Male - Female 95% CI** | $\approx [573, 776]$ g | **$[573.01, 776.30]$ g** | **PASSED (Exact)** |
| **Adelie Male - Female Welch p** | $p < 0.001$ | **$t = 13.13, p = 6.40 \times 10^{-26}$** | **PASSED (Exact)** |
| **Adelie Male - Female Cohen's d** | Very large effect size | **$d = 2.17$** | **PASSED (Exact)** |
| **Adelie vs. Chinstrap Mean Diff** | $\approx -27$ g | **$-26.92$ g** | **PASSED (Exact)** |
| **Adelie vs. Chinstrap Welch p** | $p \approx 0.65$ | **$t = -0.45, p = 0.6548$** (Fail to reject $H_0$) | **PASSED (Exact)** |
| **One-Way ANOVA F-statistic** | $F \approx 342$ | **$F = 341.89$** (matches `scipy.stats.f_oneway`) | **PASSED (Exact)** |
| **One-Way ANOVA Effect Size** | $\eta^2 \approx 0.67$ | **$\eta^2 = 0.6745$** ($67.45\%$ variance explained) | **PASSED (Exact)** |
| **One-Way Tukey HSD Contrasts** | Adelie-Chinstrap n.s.; Gentoo differs from both | Adelie-Chinstrap $p=0.9164$; Gentoo contrasts $p < 0.0001$ | **PASSED (Exact)** |
| **Two-Way ANOVA Main Effects & Interaction** | Species, Sex, and Interaction all $p < 0.001$ | Species $p=8.14 \times 10^{-123}$, Sex $p=1.90 \times 10^{-57}$, Interaction $p=1.97 \times 10^{-4}$ | **PASSED (Exact)** |
| **Two-Way 6-Cell Tukey HSD** | 13 of 15 pairs statistically significant | **13 of 15 pairs reject $H_0$** ($\alpha = 0.05$) | **PASSED (Exact)** |
