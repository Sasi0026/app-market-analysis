# SwiftFlow: Data-Driven Market Entry Strategy

**Author:** Sasi Kiran | Data Analyst

**Dataset:** Google Play Store Apps (Kaggle)


---

## Executive Summary

This analysis examines Google Play Store data to identify optimal market positioning for SwiftFlow's Version 1.0 launch across three dimensions: app size, user satisfaction, and monetization.

- **App Size:** The data strongly favors a lightweight build under 10 MB. This is where independent productivity apps achieve peak install volumes, while the 20–50 MB mid-range acts as a market dead zone with significantly lower adoption.
- **Quality Standard:** Productivity users set a high bar — the category median sits at 4.2 stars. The 0–10 MB space is volatile and flooded with low-rated clones, making rigorous QA non-negotiable for Version 1.0.
- **Monetization:** Free apps account for over 99.85% of installs in the productivity category. A paid launch would effectively eliminate user adoption. SwiftFlow must launch free and monetize through a freemium model once a user base is established.

---

## Project Objective & Business Problem

SwiftFlow is entering a highly competitive productivity market. To maximize user acquisition and retention while minimizing engineering waste, this project leverages global app market data to define strict engineering constraints, quality standards, and pricing strategies — before a single line of application code is written.

---

## Phase 1: Data Engineering Pipeline — [`01_data_cleaning.ipynb`](notebooks/01_data_cleaning.ipynb)

Before analysis could begin, raw market data was processed through a reproducible data pipeline covering four key steps.

- **Structural Cleanup:** Fixed broken text artifacts and standardized category strings.
- **Type Casting:** Converted object formats into clean numeric data types for `Size`, `Installs`, and `Price`.
- **Deduplication:** Purged duplicate application listings to protect statistical integrity.
- **Null Imputation:** Handled missing values using localized category medians rather than global averages to prevent distributional skew.

---

## Phase 2: Core Insights & Strategic Visualizations — [`02_EDA.ipynb`](notebooks/02_EDA.ipynb)

### 1. Global App Size vs. User Adoption

**Hypothesis:** Smaller apps achieve higher install volumes due to reduced download friction.

**Finding:** The vast majority of viral apps are heavily clustered below 40 MB. A major spike exists in the 50–100 MB range, but this is driven entirely by AAA mobile games — necessitating a category-specific analysis before drawing any engineering conclusions.

---

### 2. The Productivity Market Size Ceiling

**Hypothesis:** Isolating the Productivity category will reveal a more accurate size-to-install relationship, free from game-related data skew.

**Finding:** The 10–50 MB range is a complete market dead zone for productivity tools. Independent apps thrive strictly under 10 MB. The 50–100 MB spike is attributable to enterprise giants — Google Workspace and Microsoft Office — whose brand authority allows users to tolerate large file sizes. This is not a position available to a new market entrant.

---

### 3. User Satisfaction Benchmarks

**Hypothesis:** Productivity users maintain higher rating standards compared to other app categories, setting a more demanding QA benchmark for launch.

**Finding:** The category median sits at 4.2 stars. While median ratings remain stable across all size tiers, the 0–10 MB bucket contains significant rating volatility, with low-quality clones pulling scores down to 1.0. Releasing an unpolished app in this tier results in immediate market rejection.

---

### 4. Monetization Strategy

**Hypothesis:** An upfront paywall significantly damages initial user acquisition compared to a free-to-download model.

**Finding:** Free productivity apps achieve a median of 500,000 installs. Paid alternatives collapse to a median of 750 installs — a 99.85% reduction in market penetration. The data leaves no room for ambiguity on pricing strategy.

---

## Final Launch Blueprint

| Dimension | Constraint | Rationale |
|---|---|---|
| App Size | Under 10 MB | Peak install volume for independent productivity tools |
| Quality Standard | 4.2+ star rating at launch | Lightweight tier punishes buggy releases immediately |
| Pricing Model | Free with freemium tier in V2.0 | Paid model reduces adoption by 99.85% |

---

## Tech Stack

- **Language:** Python 3.10+
- **Libraries:** Pandas, NumPy, Matplotlib, Seaborn
- **Environment:** Jupyter Notebook (Google Colab compatible)

---

## How to Run

```bash
# 1. Clone the repository
git clone https://github.com/Sasi0026/app-market-analysis.git

cd app-market-analysis

# 2. Install dependencies
pip install pandas numpy matplotlib seaborn jupyter

# 3. Add the dataset
# Download googleplaystore.csv from Kaggle and place it in the data/ folder
# Update the file path in the first cell of each notebook to match your local structure
```

Run `notebooks/01_data_cleaning.ipynb` first to generate `clean_playstore.csv`,
then open `notebooks/02_EDA.ipynb` for the full analysis.
---

## Project Structure

```
swiftflow-market-analysis/
│
├── data/
|   ├── Raw/
|        └── googleplaystore.csv
│   ├── Processed/       
│        └── clean_playstore.csv          # Generated by 01_data_cleaning.ipynb
│
├── docs/
│   └── problem_statement.md         # Project scope and business problem definition
│
├── notebooks/
│   ├── 01_data_cleaning.ipynb       # Data pipeline: cleaning, casting, deduplication
│   └── 02_EDA.ipynb                 # Core analysis and strategic visualizations
│
└── README.md
```
