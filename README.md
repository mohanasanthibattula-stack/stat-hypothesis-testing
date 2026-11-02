# Advanced Statistical Analysis & Hypothesis Testing: Palmer Penguins

[![CI](https://github.com/mohanasanthibattula-stack/stat-hypothesis-testing/actions/workflows/ci.yml/badge.svg)](https://github.com/mohanasanthibattula-stack/stat-hypothesis-testing/actions/workflows/ci.yml)
[![Python 3.12](https://img.shields.io/badge/Python-3.12-3776AB.svg?logo=python&logoColor=white)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A rigorous inferential statistics and hypothesis testing framework analyzing morphological sexual dimorphism and interspecies body mass variation across the Palmer Archipelago penguin population (*Pygoscelis adeliae*, *Pygoscelis antarcticus*, and *Pygoscelis papua*).

---

## Executive Summary & Headline Results

| Research Question | Analytical Method | Key Statistical Metric | Decision ($\alpha = 0.05$) | Headline Biological Insight |
| :--- | :--- | :--- | :--- | :--- |
| **Q1: Normality Distribution** | Shapiro-Wilk & Lilliefors | All 6 cells $p > 0.19$ (SW), $p > 0.28$ (Lilliefors) | **Fail to Reject $H_0$** | Subpopulation body masses adhere to Gaussian distributions, validating parametric modeling. |
| **Q2: Adelie Sexual Dimorphism** | Welch Two-Sample $t$-test & Mann-Whitney $U$ | Mean Diff $= +674.66$ g (95% CI: $[573.01, 776.30]$), $t = 13.13$, $d = 2.17$, $p = 6.40 \times 10^{-26}$ | **Reject $H_0$** | Huge sexual dimorphism; males systematically outweigh females by $\sim 20\%$. |
| **Q3: Adelie vs. Chinstrap** | Welch Two-Sample $t$-test & Mann-Whitney $U$ | Mean Diff $= -26.92$ g (95% CI: $[-145.66, 91.82]$), $t = -0.45$, $p = 0.6548$, $d = -0.06$ | **Fail to Reject $H_0$** | No statistically significant difference in body mass between Adelie and Chinstrap penguins. |
| **Q4: Species Variation (One-Way)** | One-Way ANOVA & Welch ANOVA | $F(2, 330) = 341.89$, $p = 3.74 \times 10^{-81}$, $\eta^2 = 0.6745$, Welch $F = 316.50$ | **Reject $H_0$** | Species accounts for $67.45\%$ of total body mass variance. Gentoo is vastly larger than both. |
| **Q5: Species $\times$ Sex Interaction** | Two-Way Factorial ANOVA (Type II) | Species $F = 748.86$ ($p < 10^{-120}$), Sex $F = 387.58$ ($p < 10^{-50}$), Interaction $F = 8.75$ ($p = 1.97 \times 10^{-4}$) | **Reject $H_0$** | Sexual dimorphism gap is non-uniform: largest in Gentoo (+805.1 g), Adelie (+674.7 g), lowest in Chinstrap (+411.8 g). |

---

## Platform Requirements Traceability

| Platform Requirement | Implementation Location in Repository | Verifiable Artifacts |
| :--- | :--- | :--- |
| **1. Shapiro-Wilk & K-S Normality Tests** | `notebooks/statistical_analysis.ipynb` (Section 2) | Table in Cell 4, `reports/figures/01_normality_histograms.png`, `02_normality_qqplots.png` |
| **2. Two-Sample Tests ($t$-test & Mann-Whitney $U$)** | `notebooks/statistical_analysis.ipynb` (Section 3a & 3b) | Welch $t$, manual vs automated 95% CI assertions, Cohen's $d$, Levene test, Rank-biserial $r$, `reports/figures/03_two_sample_adelie_sex.png`, `04_two_sample_adelie_chinstrap.png` |
| **3. One-Way & Two-Way ANOVA with Tukey HSD** | `notebooks/statistical_analysis.ipynb` (Section 4 & 5) | OLS ANOVA ($F=341.89$), Welch ANOVA, Kruskal-Wallis, Type II Two-Way ANOVA, 6-cell Tukey HSD (13/15 sig pairs), `reports/figures/05_oneway_tukey_ci.png`, `06_oneway_residuals.png`, `07_twoway_interaction.png` |
| **4. Hypotheses & Confidence Intervals in Markdown** | `notebooks/statistical_analysis.ipynb` (Cells 0, 3, 7, 10, 13, 16, 19, 21) | Null & alternative mathematical hypothesis pairs documented before every code execution block |
| **Expected Proof: Executable Notebook** | `notebooks/statistical_analysis.ipynb` | Fully executed in-place with persisted graphical outputs and HTML export (`reports/statistical_analysis.html`) |

---

## Repository Structure

```text
stat-hypothesis-testing/
├── .github/
│   └── workflows/
│       └── ci.yml               # Automated CI workflow on Python 3.12 (nbconvert execution)
├── data/
│   ├── penguins.csv             # Unchanged raw Palmer Penguins dataset (344 observations)
│   └── README.md                # Data provenance, research citations, and variable codebook
├── notebooks/
│   └── statistical_analysis.ipynb# Primary executable research notebook (alpha = 0.05)
├── reports/
│   ├── figures/                 # High-resolution figures (150 DPI)
│   │   ├── 01_normality_histograms.png
│   │   ├── 02_normality_qqplots.png
│   │   ├── 03_two_sample_adelie_sex.png
│   │   ├── 04_two_sample_adelie_chinstrap.png
│   │   ├── 05_oneway_tukey_ci.png
│   │   ├── 06_oneway_residuals.png
│   │   └── 07_twoway_interaction.png
│   ├── proof/
│   │   ├── environment.txt      # Reproducible environment specifications (pip freeze)
│   │   └── PROOF.md             # Verification deliverables catalog and validation status
│   ├── results_summary.csv      # Consolidated tabular summary of all hypothesis tests
│   └── statistical_analysis.html# Standalone rendered HTML report
├── .gitignore
├── LICENSE                      # MIT License (Mohan Asanthibattula)
├── README.md                    # Project documentation and reproduction instructions
└── requirements.txt             # Pinned package dependencies
```

---

## Reproduction & Execution Guide

### Prerequisites
- Python 3.12 (or virtual environment)
- Git

### Local Setup
```bash
# Clone the repository
git clone https://github.com/mohanasanthibattula-stack/stat-hypothesis-testing.git
cd stat-hypothesis-testing

# Create and activate virtual environment
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# Install exact pinned dependencies
pip install --upgrade pip
pip install -r requirements.txt
```

### Executing the Analysis
```bash
# Run the notebook in-place to regenerate all outputs and figures
jupyter nbconvert --to notebook --execute --inplace notebooks/statistical_analysis.ipynb

# Export standalone HTML report
jupyter nbconvert --to html notebooks/statistical_analysis.ipynb --output-dir=reports --output=statistical_analysis.html
```

---

## Dataset Provenance & Citation

The dataset originates from the long-term ecological research at Palmer Station, Antarctica:
1. **Primary Study**: Gorman KB, Williams TD, Fraser WR (2014) Ecological Sexual Dimorphism and Environmental Variability within a Community of Antarctic Penguins (Genus *Pygoscelis*). *PLoS ONE* 9(3): e90081. [doi:10.1371/journal.pone.0090081](https://doi.org/10.1371/journal.pone.0090081)
2. **Package**: Horst AM, Hill AP, Gorman KB (2020). palmerpenguins: Palmer Archipelago (Antarctica) penguin data. [doi:10.5281/zenodo.3960218](https://doi.org/10.5281/zenodo.3960218) (CC0 Public Domain).

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
