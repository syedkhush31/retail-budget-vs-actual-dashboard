# Retail Budget vs Actual Dashboard (Power BI)

![Dashboard](images/dashboard.png)

## Overview

✍️ YOUR TURN: 2–3 sentences. What business question does this dashboard answer?
(Hint: "Did the business hit its sales targets in 2018, and where did it beat or miss?")

## Dataset

- **Source:** [Superstore Sales Dataset](https://www.kaggle.com/datasets/rohitsahoo/sales-forecasting) (Kaggle)
- ~9,800 order lines, US retail, 2015–2018
- The dataset contains **actual sales only**. The **budget was built by me** (see below).

## Tools

- **Excel:** Power Query (data cleaning), PivotTables (exploration), budget calculation
- **Power BI:** Power Query, star-schema data model, DAX measures, report design
- **Git / GitHub:** version control

## Process

1. **Data cleaning:** fixed a date-format issue (dates were dd/mm/yyyy but read as mm/dd/yyyy, silently corrupting about half the dates). Fixed with locale-aware type conversion in Power Query.
2. **Exploration:** year-over-year growth: 2016 −4.3%, 2017 +30.6%, 2018 +20.3%.
3. **Budget creation:** 2018 budget = 2017 actual sales × (1 + 15%), built at Month × Region × Category level (144 rows), so the budget follows seasonality.
4. **Data model:** star schema with shared dimension tables (Date, Region, Category) connected to both the Sales and Budget fact tables.
5. **DAX measures:** Total Actual, Total Budget, Variance, Variance %.
6. **Dashboard:** KPI cards, monthly trend, variance by region and category, slicers.

## Budget Assumption

✍️ YOUR TURN: Why did you choose 15% growth? (1–3 sentences, as if explaining to a manager)

## Data Model

![Data model](images/model.png)

Sales (order level) and Budget (month level) have different granularity, so they can't be joined directly. Both connect to shared dimension tables, so one slicer filters actuals and budget together.

## Key Insights

✍️ YOUR TURN: 3–4 bullet points. Use your homework:

- Overall result (beat budget by how much?)
- Which region and category drove it?
- Which region and category missed?
- Which months were below budget?

## Challenges & What I Learned

✍️ YOUR TURN: 2–3 bullets. Pick from what actually happened to you:

- the date-locale bug
- the circular dependency error when sorting months in Power BI
- the hidden trailing space in a column name ("Month ")

## Repository Structure

retail-budget-vs-actual-dashboard/
├── data/
│ ├── raw/train.csv # original dataset
│ └── processed/budget_2018.csv # budget built from 2017 actuals
├── analysis/exploration.xlsx # pivots, YoY growth, budget logic
├── powerbi/retail_budget_vs_actual.pbix
└── images/ # screenshots

## How to Open

1. Download/clone this repo and open `powerbi/retail_budget_vs_actual.pbix` in Power BI Desktop
2. If data doesn't load: **Transform data → Data source settings → Change Source**, and point to the CSV files in the `data/` folder
