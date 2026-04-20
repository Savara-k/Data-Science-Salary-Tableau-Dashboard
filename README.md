# Data Science Salary Intelligence Dashboard

> An interactive Tableau dashboard exploring data science compensation, remote work trends, and US cost of living — built to answer the question every tech worker is asking: *where should I work, and can I actually afford to live there?*

---

## Live Dashboard

**[View on Tableau Public](https://public.tableau.com/app/profile/savara.khan/viz/DataScienceSalaryIntelligenceDashboard/Dashboard1#1)**


---


## Executive Summary

Most salary analysis projects stop at "which job pays the most." This dashboard goes further.

**Data Science Salary Intelligence Dashboard** is a multi-sheet Tableau project that combines two independent datasets — global data science compensation records and US county-level cost of living data — into a unified visual story. The result is a decision-support tool for anyone navigating career choices in the data science field.

The dashboard surfaces three findings that are consistently surprising to viewers:

- Fully remote data scientists earn measurably more on average than in-office counterparts
- The highest-paying roles are not always in the most expensive states
- Housing cost as a share of income varies dramatically across US states — making "high salary" mean very different things depending on location

---

## The Problem This Addresses

Salary data in isolation is misleading. A $150K data science role in San Francisco and a $110K role in Austin represent very different lived realities once housing, food, transportation, and taxes are accounted for.

Existing salary dashboards answer: *what does this role pay?*

This dashboard answers: *what does this role pay, relative to where you would realistically live?*

---

## Dashboard Structure

The dashboard contains five interactive sheets assembled into a single canvas:

### Sheet 1 — Average salary by job title
Horizontal bar chart showing average USD salary per data science role, broken down by experience level (Entry, Mid, Senior, Executive). Sortable, color-coded, and filterable.

### Sheet 2 — Salary by remote work type
Compares average salary across three work arrangements: fully in-office (0), hybrid (50), and fully remote (100). Reveals the remote work salary premium in the data science field.

### Sheet 3 — US cost of living map
Choropleth map of the continental United States shaded by average total cost of living per state. Sourced from county-level expenditure data aggregated to state level.

### Sheet 4 — Median family income vs housing cost by state
Horizontal bar chart showing average median family income per state, with housing cost encoded as color. Identifies states where income-to-housing ratios are most and least favorable.

### Sheet 5 — Total cost of living treemap
Treemap where each state's box is sized by average total living cost. Provides an immediate visual hierarchy of affordability across the US.

---

## Key Insights

- **Principal Data Engineer** and **Machine Learning Scientist** rank among the highest-compensated roles in the dataset
- **Fully remote workers** earn a higher average salary than hybrid or in-office workers across most experience levels
- **DC, Hawaii, and California** have the highest cost of living — significantly outpacing median family income relative to other states
- **Midwest and Southern states** offer the most favorable income-to-housing ratios for remote data science workers

---

## Data Sources

| Dataset | Source | Description |
|---|---|---|
| `ds_salaries.csv` | Kaggle | 607 data science salary records across roles, experience levels, company sizes, and locations (2020–2022) |
| `cost_of_living_us.csv` | Kaggle / EPI Family Budget Calculator | 31,430 county-level records covering housing, food, transportation, healthcare, childcare, taxes, and total cost |

Both datasets are included in this repository for full reproducibility.

---

## Technical Decisions

**Separate data sources instead of a forced join**

The salary dataset uses ISO 2-letter country codes (`US`, `GB`, `DE`) while the cost of living dataset uses US state abbreviations (`CA`, `TX`, `NY`). These columns look similar but represent incompatible geographic granularities. Rather than engineering a lossy join, both datasets are maintained as independent Tableau data sources and presented as complementary views — which more accurately reflects the analytical question being asked.

**Average over sum for geographic aggregation**

The cost of living dataset contains multiple county-level rows per state. All geographic aggregations use `AVG()` rather than `SUM()` to prevent inflation from county count differences across states.

**Remote ratio treated as a dimension**

The `remote_ratio` field contains three discrete values (0, 50, 100) representing work arrangement categories, not a continuous numeric scale. Converting it to a Tableau dimension enables categorical color encoding and meaningful axis labeling (In-Office / Hybrid / Fully Remote).

---

## Tools Used

- Tableau Public (dashboard design, data connection, visualization)
- Tableau Data Source tab (data inspection, aggregation logic)
- GitHub (version control, portfolio documentation)

---

## Limitations

- Salary dataset contains 607 records — sufficient for exploratory analysis, not for statistical inference
- Cost of living data is US-only; salary data is global. Cross-dataset comparison is limited to US-based roles
- No time-series analysis — salary trends across years are not modeled
- Remote ratio is self-reported and may not reflect actual work arrangements

---

## Future Roadmap

- Filter dashboard by US-only salaries to enable direct salary vs. cost-of-living comparison
- Add a calculated "purchasing power" field: `avg_salary / avg_total_cost` per state
- Incorporate 2023–2024 salary data to capture post-pandemic remote work shifts
- Add experience level parameter filter that updates all five sheets simultaneously
- Build a second dashboard focused on entry-level roles only for new graduates

---

## Repository Structure

```
data-science-salary-dashboard/
│
├── ds_salaries.csv              # Salary dataset
├── cost_of_living_us.csv        # Cost of living dataset
├── dashboard.twbx               # Tableau packaged workbook
├── dashboard_screenshot.png     # Dashboard preview image
└── README.md                    # This file
```

---

## What This Project Demonstrates

Through this dashboard I demonstrate:

- Multi-source data connection and management in Tableau
- Deliberate aggregation decisions aligned with data structure
- Five chart types: horizontal bar, choropleth map, treemap, stacked bar, color-encoded bar
- Dashboard layout and cross-sheet filter interactivity
- Translating a real-world analytical question into a visual narrative
- Portfolio documentation at a professional standard
