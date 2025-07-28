# Estimating the Causal Impact of a Growth Mindset Intervention

This project evaluates the **causal effect** of a “growth mindset” intervention on student academic achievement using synthetic data modeled after the National Study of Learning Mindsets (NSLM). The intervention aimed to instill the belief that intelligence can grow with effort. We estimate the **Average Treatment Effect (ATE)** using a diverse set of statistical and causal inference methods, including both frequentist and Bayesian approaches.

---

## Background

A **growth mindset**—the belief that intelligence and abilities can improve with effort—has been shown to enhance student motivation and performance. In this project, we study the impact of such an intervention (a "nudge") on standardized academic achievement scores using a rich dataset containing both student-level and school-level covariates. The data are structured to mirror a real-world randomized trial with observable confounding and treatment imbalance.

---

## Dataset Overview

- **Total Students**: 10,391  
- **Schools**: 76 across the U.S.  
- **Outcome Variable**: `y` – Academic achievement score  
- **Treatment Indicator**: `z` – Growth mindset intervention  
- **Covariates**:
  - *Student-level*: `race`, `gender`, `fgen` (first-generation status), `selfrpt` (self-report motivation score)
  - *School-level*: `urban`, `mindset`, `test`, `sch_race`, `pov` (poverty rate), `size`

The dataset is unbalanced: the treated and control groups differ in both size and covariate distribution, necessitating proper causal adjustment.

---

## Objective

Estimate the **Average Treatment Effect (ATE)** of the mindset intervention on academic achievement, accounting for covariate imbalance and potential confounding.

---

## Methods Used

### 1. **Exploratory Data Analysis (EDA)**
- Visualized differences in outcomes and covariates between treatment groups.
- Identified potential confounders (e.g., `fgen`, `selfrpt`, `pov`).

### 2. **Linear Regression (OLS)**
- Used baseline regression to estimate ATE, adjusting for covariates.
- Provided interpretability and initial benchmark estimate.

### 3. **Bootstrap**
- Estimated the uncertainty of ATE via resampling.
- Built confidence intervals for both naïve and adjusted models.

### 4. **LASSO Regression**
- Identified key predictive variables for outcome and treatment.
- Prevented overfitting and improved robustness of causal estimates.

### 5. **Propensity Score Matching (PSM)**
- Estimated propensity scores using logistic regression.
- Matched treated and control units using nearest-neighbor matching.
- Achieved balance in covariates, improving comparability.

### 6. **Inverse Probability Weighting (IPW)**
- Applied weights to correct for treatment assignment bias.
- Improved covariate balance while preserving sample size.

### 7. **Augmented IPW (AIPW)**
- Combined outcome modeling and weighting (doubly robust).
- Consistent and efficient estimator under model misspecification.

### 8. **Bayesian Estimation**
- Used posterior sampling to estimate ATE and quantify uncertainty.
- Generated distribution of likely ATE values using priors and observed data.

---

## Results Summary

| Method          | ATE Estimate | Notes                                |
|-----------------|--------------|--------------------------------------|
| Naive Difference | 0.62         | Inflated due to covariate imbalance  |
| OLS             | 0.41         | Adjusted for all covariates          |
| Bootstrap       | 0.41 ± 0.02  | 95% CI: [0.38, 0.44]                 |
| LASSO           | 0.41         | Selected key predictors              |
| PSM             | 0.39         | Improved covariate balance           |
| IPW             | 0.41         | Weighted estimate                    |
| AIPW            | 0.41         | Most reliable, doubly robust         |
| Bayesian        | ~0.41        | Posterior mean, aligned with others  |

All models consistently estimate the ATE to be approximately **0.41** — indicating a significant and positive effect of the growth mindset intervention.

---

## Key Insights

- The mindset intervention significantly increased academic performance by ~0.41 standard deviations.
- Subgroup analysis revealed **higher gains among non-first-generation students** and those with **higher self-motivation**.
- Covariate balance was critical to obtaining valid causal estimates.
- Bayesian inference validated frequentist conclusions and offered rich uncertainty quantification.

---

## Limitations

- The dataset is **simulated** and may not fully reflect real-world behavior.
- **Unobserved confounding** (e.g., teacher influence, classroom dynamics) is not addressed.
- Results assume **correct model specification** in IPW and regression.

---

## Technologies Used

- **R**, **R Markdown**, **HTML**
- Causal packages: `MatchIt`, `boot`, `glmnet`, `survey`, `rstanarm`
- Visualization: `ggplot2`, `patchwork`, `cowplot`

---

## Author

- **Aditya Shah**  
Course: *Statistical Modeling and Computing*  
Rutgers University, Spring 2024

---

## Files Included

- `project.Rmd` – Full analysis code  
- `Project-Stat-Mod-Comp.html` – Final rendered report  
- `Final Poster.pdf` – Condensed summary for presentation  
