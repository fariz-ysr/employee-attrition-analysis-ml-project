# Employee Attrition Analysis & Prediction

An end-to-end data science project that analyses and predicts employee attrition using a fictional HR dataset of 1,470 employees across 31 features. The project covers exploratory data analysis (EDA), machine learning modelling, and a management-ready presentation deck.

---

## Project Structure

```
Employee-Attrition-Analysis/
├── Data/
│   └── Employee_Attrition_Data.xlsx          # Fictional HR dataset (1,470 employees, 31 features)
├── Attrition_EDA.ipynb                    # Exploratory Data Analysis
├── Attrition_Modelling.ipynb           # Predictive Modelling
└── README.md
```

---

## Objectives

- Identify the key drivers of employee attrition through exploratory data analysis
- Build and compare machine learning models to predict which employees are at risk of leaving
- Translate analytical findings into actionable retention strategies for HR leadership

---

## Dataset Overview

| Metric | Value |
|---|---|
| Total Employees | 1,470 |
| Employees Stayed | 1,233 |
| Employees Left | 237 |
| Overall Attrition Rate | 16.1% |

The dataset covers four feature categories: Demographics, Job Details, Compensation, and Work Environment.

---

## Notebooks

| Notebook | Description |
|---|---|
| `Attrition_EDA.ipynb` | Data cleaning, attrition rates by department, feature-by-feature analysis vs attrition |
| `Attrition_Modelling.ipynb` | Feature selection, SMOTE for class imbalance, model training, evaluation & comparison |

> Read the notebooks in order — `Attrition_EDA.ipynb` first, then `Attrition_Modelling.ipynb`.

---

## Key Findings

### Attrition by Department
| Department | Total | Left | Attrition Rate |
|---|---|---|---|
| Sales | 446 | 92 | 20.6% |
| Human Resources | 63 | 12 | 19.0% |
| Research & Development | 961 | 133 | 13.8% |

### Top Attrition Drivers

- **Monthly Income** — Employees who left earned a median of $3,202/month vs $5,204 for those who stayed — a $2,000/month gap. Lower pay is the single strongest predictor of departure.
- **Overtime** — Employees working overtime leave at 31%, nearly 3× the rate of those who don't (10%). OT is a strong signal of burnout and disengagement.
- **Job Level** — Entry-level employees have ~26% attrition, well above the overall 16.1% average.
- **Age & Tenure** — The 18–25 age group sees ~36% attrition. Employees with under 2 years at the company are the highest-risk group (avg. tenure of those who left: ~5 years vs ~7 years for those who stayed).
- **Job Involvement** — Low-involvement employees leave at 35%, while highly involved employees leave at only 9%.
- **Stock Options** — Employees with no stock options show significantly higher attrition rates.

---

## Modelling Approach

- **Data Preparation:** Label-encoded categorical features, dropped zero-variance and ID columns, 80/20 stratified train-test split
- **Class Imbalance:** Applied SMOTE on training data only (84:16 imbalance) to prevent model bias
- **Models Trained:** Logistic Regression, Random Forest, Gradient Boosting — each wrapped in an imlearn pipeline to prevent data leakage
- **Evaluation Metrics:** PR-AUC, Recall, F1 (Attrition class), ROC-AUC — accuracy was excluded due to class imbalance (a model predicting "No" for everyone would score 84%)

---

## Model Results

| Model | ROC-AUC | PR-AUC | F1 (Attrition) | Recall | 5-Fold CV AUC |
|---|---|---|---|---|---|
| **Logistic Regression** | 0.737 | **0.459** | 0.429 | **0.511** | 0.726 ± 0.030 |
| Random Forest | 0.734 | 0.345 | 0.423 | 0.447 | 0.790 ± 0.024 |
| Gradient Boosting | 0.757 | 0.429 | 0.440 | 0.404 | 0.811 ± 0.024 |

**Chosen Model: Logistic Regression** — selected for its highest PR-AUC (0.459) and Recall (51.1%), which are the most important metrics when the primary goal is catching at-risk employees before they leave. It also offers high interpretability, with coefficients that directly show which factors increase or decrease attrition risk.

---

## Risk Tier System

The model outputs a probability score that can be used to tier employees for HR intervention:

| Risk Tier | Probability of Leaving | % of Workforce | Recommended Action |
|---|---|---|---|
| 🟢 Low Risk | < 30% | ~62% | Routine check-ins, standard engagement practices |
| 🟡 Medium Risk | 30–60% | ~25% | Flag for manager conversations, review workload and job satisfaction |
| 🔴 High Risk | > 60% | ~13% | Immediate HR intervention, compensation review, retention package |

---

## Recommendations

1. **Compensation Review** — Benchmark entry-level and Sales salaries against market rates. Closing pay gaps has the highest estimated retention ROI.
2. **Onboarding Program** — Invest heavily in employees during their first 0–2 years. Assign dedicated mentors, set milestone check-ins, and track engagement scores monthly.
3. **Overtime Management** — Audit overtime distribution (especially in Sales), implement maximum workload capacity, and monitor OT frequency as an early-warning HR signal.
4. **Sales Retention Focus** — Create a department-specific retention plan addressing commission structure, OT culture, and career upskilling.
5. **Equity Participation** — Extend stock option access to Level 0 (entry-level) employees.
6. **Engagement Monitoring** — Run regular surveys to track job involvement and satisfaction. Integrate survey data with the risk tier model to build a live retention risk index.

---

## Tools & Libraries

- Python 3
- pandas, NumPy
- scikit-learn, imbalanced-learn (SMOTE)
- Matplotlib, Seaborn
- Jupyter Notebook

---

## License

This project uses a fictional dataset for demonstration purposes. MIT License.
