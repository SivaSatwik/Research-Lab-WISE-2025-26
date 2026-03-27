# Trust, Ethical Concerns, and Usage Patterns of ChatGPT Among Higher Education Students

Research Lab Project — LLMs in Higher Education (WISE 2025–26)

**Team 5** | Supervisor: Dr.-Ing. Stefania Zourlidou

**Team Members:** Siva Satwik Nanduri · Vivekananda Reddy Godala · Rahul Vardhan Talam · Shashank Garehatti Sridhara · Pranav Chengappa Devanira Bopanna

---

## Overview

This study examines trust in ChatGPT among 22,836 higher education students across 120 countries, drawing on a large-scale international survey. The analysis covers four research questions using hierarchical regression, ANOVA, Pearson correlations, and cross-group comparison methods.

**Sample:** N = 22,836 (after removing 127 duplicate responses from raw N = 22,963)
**Countries:** 120 | **Languages/Regions:** 7 (English, Spanish, Arabic, Turkish, Italian, Japanese, Hebrew)
**Study levels:** 77% Undergraduate, 18% Postgraduate/Masters, 3% Doctoral

---

## Research Questions

| # | Question | Primary Method |
|---|----------|----------------|
| RQ1 | What factors predict student trust in and recommendation of ChatGPT? | 4-block hierarchical OLS regression |
| RQ2 | How do ethical concerns about ChatGPT vary across demographic and usage groups? | Welch's ANOVA + Games-Howell post-hoc |
| RQ3 | What is the relationship between usage patterns, perceived capabilities, and trust? | Pearson correlation matrix |
| RQ4 | Do trust-related relationships differ significantly across academic disciplines? | Fisher's Z + discipline-specific regressions |

---

## Key Findings

**RQ1 — Predictors of Trust:**
- Usage intensity is the dominant predictor (β* = +0.568, ΔR² = .340 over demographics alone)
- Demographics collectively explain only R² = .018; adding usage jumps R² to .358
- Ethical concerns positively predict trust (β* = +0.134), possibly because engaged users think more about AI ethics
- Capabilities score negatively predicts trust (β* = −0.059), suggesting critical awareness reduces uncritical trust
- Satisfaction (Q16) follows a similar pattern (total R² = .177) but attitudes are not significant

**RQ2 — Ethical Concerns:**
- Large effect of usage group: high users report substantially more ethical concern (M = 3.68) than low users (M = 2.99), F = 609.8, p < .001, η² = .0688
- Significant regional variation: Turkish speakers highest (M = 3.71), Japanese lowest (M = 2.87)
- Discipline and gender effects are statistically significant but negligibly small (η² < .003)

**RQ3 — Correlations:**
- Strongest association: Usage Intensity ↔ Trust (r = +0.590, p < .001) — the largest bivariate predictor
- Moderate: Trust ↔ Recommendation (r = +0.426), Usage ↔ Ethical Concerns (r = +0.445)
- Capabilities and Attitudes show weak, negative associations with trust

**RQ4 — Discipline Differences:**
- Usage↔Trust correlation differs between Social Sciences and Natural & Life Sciences (Fisher's Z, Bonferroni-corrected)
- Coefficient difference Z-tests: 0 of 24 predictor–discipline pairs survive Bonferroni correction
- Conclusion: regression relationships are largely consistent across disciplines, with minor variation in correlation magnitudes

---

## Repository Structure

```
.
├── data/
│   ├── raw.xlsx                        # Original survey data (22,963 × 180)
│   └── cleaned/
│       └── cleaned_data.csv            # Cleaned data (22,836 × 191)
│
├── code/
│   └── analysis/
│       ├── 01_data_cleaning.ipynb      # Deduplication, composite scores, reliability
│       ├── 02_descriptive_statistics.ipynb   # Distributions, group summaries
│       ├── 03_correlation_analysis.ipynb     # RQ3: Pearson correlation matrix
│       ├── 04_regression_analysis.ipynb      # RQ1: 4-block hierarchical regression
│       ├── 05_group_comparisons.ipynb        # RQ2 & RQ4: ANOVA, Fisher's Z, discipline regressions
│       └── results/
│           ├── figures/                # 9 publication-ready figures (fig1–fig9.png)
│           └── tables/                 # CSV outputs from all analyses
│
├── results/                            # (legacy output folder)
├── requirements.txt                    # Pinned Python dependencies
└── README.md
```

---

## Variables

### Outcome Variables
| Variable | Column | Description |
|----------|--------|-------------|
| Trust | Q15 | "I trust ChatGPT" (1–5 Likert, N = 19,587) |
| Recommendation | Q16 | Satisfaction / likelihood to recommend (1–5 Likert, N = 19,594) |

### Composite Scales (all mean of constituent items)
| Scale | Items | α | N | M (SD) |
|-------|-------|---|---|--------|
| Usage Intensity | Q18a–l (12 items) | .872 | 19,623 | 2.59 (0.80) |
| Perceived Capabilities | Q22a–j (10 items) | .909 | 18,032 | 2.98 (0.86) |
| Ethical Concerns | Q28a–i (9 items) | .910 | 16,313 | 3.34 (0.74) |
| Attitudes | Q21a–d (4 items) | .843 | 18,033 | 3.35 (0.85) |

All scales have Cronbach's α ≥ .84, meeting the conventional reliability threshold (α > .70).

> **Note on scale direction:** No codebook is available in this repository. Q22 and Q28 scale directions were inferred empirically: all Q22 items correlate negatively with trust (suggesting the scale measures perceived limitations or risks), and all Q28 items correlate positively with trust. Interpret findings accordingly.

### Demographics
| Variable | Column | Categories |
|----------|--------|------------|
| Gender | Q2 | Male (ref), Female, Other, Prefer not to say |
| Age | Q3 | Continuous; grouped into 18–21, 22–25, 26–30, 31+ |
| Study Level | Q8 | Undergraduate (ref), Postgraduate/Masters, Doctoral |
| Discipline | Q10 | Social Sciences (ref), Arts & Humanities, Applied Sciences, Natural & Life Sciences |
| Region | source | English (ref), Spanish, Arabic, Turkish, Italian, Japanese, Hebrew |

---

## Analysis Notebooks

### `01_data_cleaning.ipynb`
- Loads `raw.xlsx`, removes 127 exact duplicate rows
- Creates composite scores for all 4 scales
- Computes Cronbach's α for each scale
- Verifies demographic variable coding (age cross-checked against study level)
- Saves `cleaned_data.csv`

### `02_descriptive_statistics.ipynb`
- Summary statistics (N, M, SD, median, missing %) for all key variables
- Breakdowns by usage group, study level, discipline, and region
- **Figures:** Fig 1 (mean trust by usage group), Fig 2 (trust distribution), Fig 3 (ethical concerns by region)

### `03_correlation_analysis.ipynb` — RQ3
- Pearson correlation matrix (pairwise deletion) for all 6 key variables
- Correlation-with-trust table with effect size labels
- Full inter-scale correlation table sorted by |r|
- **Figures:** Fig 4 (correlation heatmap), Fig 5 (usage vs trust scatter with OLS fit)

### `04_regression_analysis.ipynb` — RQ1
- Demographic dummy coding (reference: Male / Undergraduate / Social Sciences)
- VIF check (max VIF = 1.32; no multicollinearity)
- 4-block hierarchical OLS for Trust (Q15): demographics → usage → capabilities+ethics → attitudes
- HC3 robust standard errors; standardized β computed from z-scored variables
- F-change test for each block
- Repeated for Satisfaction (Q16)
- **Figures:** Fig 6 (R² by block), Fig 7 (standardized β forest plot)

### `05_group_comparisons.ipynb` — RQ2 & RQ4
- Welch's ANOVA with automatic Levene's test (switches to Welch's if p < .05)
- Games-Howell post-hoc for all significant ANOVAs
- **RQ4:** Discipline-specific regressions (4 separate OLS models)
- Coefficient difference Z-tests with Bonferroni correction (6 comparisons/predictor, threshold p < .0083)
- Fisher's Z transformation for 3 key correlations × 6 discipline pairs, Bonferroni corrected
- **Figures:** Fig 8 (ethics by usage group boxplot), Fig 9 (usage–trust correlation by discipline)

---

## Setup and Reproduction

### Step 0 — Check your Python version

Open a terminal (Mac: **Terminal** app, Windows: **Command Prompt** or **PowerShell**) and run:

```bash
python --version
```

You need **Python 3.10 or higher**. If you see `Python 2.x` or nothing, try:

```bash
python3 --version
```

If Python is not installed, download it from [python.org](https://www.python.org/downloads/).

---

### Step 1 — Clone or download the repository

**Option A — using Git:**
```bash
git clone https://github.com/VivekanandaReddy3/Research-Lab-WISE-2025-26.git
cd Research-Lab-WISE-2025-26
```

**Option B — without Git:**
Click **Code → Download ZIP** on the GitHub page, unzip it, and open a terminal inside the unzipped folder.

---

### Step 2 — Install dependencies

Try this first:
```bash
pip install -r requirements.txt
```

If that gives an error like `pip: command not found`, try:
```bash
pip3 install -r requirements.txt
```

If you want to keep your system Python clean, you can use a virtual environment first (optional but recommended):
```bash
python3 -m venv venv          # create a virtual environment called "venv"
source venv/bin/activate       # activate it  (Mac/Linux)
venv\Scripts\activate          # activate it  (Windows)
pip install -r requirements.txt
```

---

### Step 3 — Launch Jupyter and run the notebooks

From the **repo root folder**, run:

```bash
jupyter notebook
```

This opens a browser window. Navigate to `code/analysis/` and run the notebooks **in order**, from top to bottom:

| Order | Notebook | What it does |
|-------|----------|--------------|
| 1st | `01_data_cleaning.ipynb` | Loads raw data, removes duplicates, creates all composite scores → saves `cleaned_data.csv` |
| 2nd | `02_descriptive_statistics.ipynb` | Summary statistics and figures |
| 3rd | `03_correlation_analysis.ipynb` | Pearson correlation matrix (RQ3) |
| 4th | `04_regression_analysis.ipynb` | Hierarchical regression (RQ1) |
| 5th | `05_group_comparisons.ipynb` | ANOVA, Fisher's Z, discipline analysis (RQ2 & RQ4) |

> **Important:** You must run `01_data_cleaning.ipynb` first. All other notebooks read `cleaned_data.csv` which it generates.

Inside each notebook, click **Cell → Run All** (or press `Shift+Enter` on each cell) to execute it.

---

### Output files generated

After running all notebooks, the following are created automatically:

- `code/analysis/results/figures/` — 9 figures (fig1–fig9.png, dpi=150)
- `code/analysis/results/tables/` — 7 CSV files (correlation matrix, ANOVA summary, model comparison, Fisher's Z, discipline regressions, coefficient differences)

---

## Statistical Methods

| Method | Where used | Why |
|--------|-----------|-----|
| Hierarchical OLS, 4 blocks | RQ1 | Partitions variance attributable to each predictor set; F-change tests block significance |
| HC3 robust SEs | RQ1 | Corrects for heteroscedasticity without assuming constant error variance |
| Standardized β | RQ1 | Enables direct coefficient comparison across predictors on different scales |
| Welch's ANOVA (auto) | RQ2 | Robust to unequal variances (Levene's test guides selection) |
| Games-Howell post-hoc | RQ2 | Does not assume equal variances or equal n across groups |
| Pearson r (pairwise) | RQ3 | Standard bivariate correlation; pairwise deletion preserves maximum N per pair |
| Fisher's Z transformation | RQ4 | Formally tests whether two independent Pearson correlations differ |
| Bonferroni correction | RQ4 | Controls family-wise error rate across 6 pairwise discipline comparisons |
| Coefficient difference Z-test | RQ4 | Tests β equality across independent regression models |

---

## Limitations

1. **No codebook available.** Variable interpretations (especially Q15 vs Q16 assignment and Q22/Q28 scale direction) are based on empirical distributions and inter-item correlations, not the original survey instrument.
2. **Cross-sectional design.** Correlations between usage and trust cannot establish causality.
3. **Missing data.** Up to 28.6% missingness on ethical concerns (Q28); listwise deletion reduces regression samples to ~16,000.
4. **Self-report bias.** All measures are student self-reports; social desirability effects cannot be ruled out.
5. **Discipline category breadth.** Four broad discipline categories may mask within-category heterogeneity.
