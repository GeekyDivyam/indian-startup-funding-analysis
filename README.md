# Indian Startup Funding Analysis (2015-2020)
### Where does startup money go in India, and where does "number of deals" tell a different story from "money raised"?

**Python | Pandas | NumPy | Matplotlib | Seaborn | Jupyter** · 3,044 funding records · 6 data-quality problems solved · 4 business insights

An exploratory data analysis of Indian startup funding deals. The project cleans a messy real-world dataset (Indian lakh/crore number formatting, hidden Unicode characters, renamed cities, duplicate industry spellings, a $3.9B outlier) and then shows where funding is concentrated, how it evolved from 2015 to 2019, and why deal count and total funding often point in different directions.

---

## TL;DR

- **Funding is highly concentrated.** Bengaluru leads on both deal count (≈850) and total funding (≈$14.6B), more than 2x the second-ranked city on both measures.
- **Activity is not the same as money.** Gurugram outranks New Delhi in total funding despite fewer deals, and Consumer Internet leads by deal count while E-Commerce leads by total money raised. In both cases, average deal size is the deciding factor.
- **The market matured between 2015 and 2019.** Deal count fell every year (647 → 104) while average deal size grew about 4x (≈$13M → ≈$56M), a sign of capital consolidating into fewer, larger bets.
- **2017's funding peak ($10.4B) came from bigger deals, not more startups.** Deal count that year was lower than in 2016.

## Business Problem

Analysed 3,000+ Indian startup funding records to uncover where funding activity is concentrated, how it has evolved over time, and where the "number of deals" story diverges from the "total money raised" story. These insights are relevant to investors, founders and market researchers.

## Business Questions

1. **Where do startup deals happen?** Which cities attract the most deals and the most funding?
2. **How has funding changed over time?** What is the yearly trend from 2015 to 2019?
3. **Which industries attract capital?** Which sectors get the most deals, and which get the most money?
4. **Who is funding Indian startups?** Which investors appear most often?

## Dataset

[Indian Startup Funding, Kaggle](https://www.kaggle.com/datasets/sudalairajkumar/indian-startup-funding): **3,044 rows and 10 columns**, covering 2015 to early 2020, sourced from public funding announcements.

| Column | Description |
|---|---|
| Sr No | Row number |
| Date dd/mm/yyyy | Date of the funding deal |
| Startup Name | Name of the funded startup |
| Industry Vertical | Sector (for example E-Tech, FinTech) |
| SubVertical | More specific business area |
| City Location | City where the startup is based |
| Investors Name | Investor(s) in the deal |
| InvestmentnType | Round type (Seed, Series A, Private Equity, and so on) |
| Amount in USD | Funding amount |
| Remarks | Free-text notes (mostly empty) |

**Missing values in the raw data:** Industry Vertical is missing in 171 rows, SubVertical in 936, City Location in 180, Investors Name in 24 and InvestmentnType in 4. Remarks is mostly empty.

## Tools Used

- **Python 3** in **Jupyter Notebook** (Anaconda)
- **Pandas** and **NumPy**: loading, cleaning and aggregating the data
- **Matplotlib** and **Seaborn**: charts

## Key Data Quality Challenges Solved

Cleaning took as much care as the analysis, because every insight below depends on it.

- **Indian number formatting:** funding amounts written in lakh/crore style (for example `20,00,00,000`) were converted into proper numeric values.
- **Hidden characters:** non-breaking spaces and other Unicode characters from web-scraped text were stripped from text fields, including the date column.
- **Broken dates:** 8 rows with unreadable dates were corrected manually by Sr No, and all dates were converted to datetime using the `dd/mm/yyyy` format.
- **City renamings:** inconsistent names caused by official renamings (Bangalore → Bengaluru, Gurgaon → Gurugram) were standardised.
- **Industry spelling variants:** multiple spellings of the same industry (5 versions of "E-Commerce" alone) were merged.
- **A $3.9B outlier:** an extreme funding amount was traced and corrected after cross-checking it against real comparable deals.
- **Multi-city and placeholder entries:** values such as "undisclosed" or "India" used as a city, and rows listing several cities, were handled with explicit judgment-based cleaning rules.

## Project Workflow

1. **Data overview:** inspected shape, column types, missing values and sample rows to understand what needed fixing.
2. **Data cleaning:** resolved the challenges listed above.
3. **Exploratory analysis:** city-wise deals and funding, yearly funding trend, industry-wise deals and funding, and investor frequency. Each has a chart and a written insight.
4. **Packaging:** documented the insights in the notebook and this README.

## Key Insights

### 1. Geographic concentration
Bengaluru leads both deal count (≈850) and total funding (≈$14.6B), more than 2x the second-ranked city on both metrics. Startup funding in India is concentrated in a small number of hubs.

### 2. Activity does not equal money
- **Gurugram vs New Delhi:** Gurugram outranks New Delhi in total funding despite having fewer deals.
- **Consumer Internet vs E-Commerce:** Consumer Internet leads by deal count, but E-Commerce leads by total money raised.

In both cases, **average deal size** is the deciding factor. Ranking by deal count alone would give a misleading picture of where capital actually flows.

### 3. Market maturation (2015-2019)
Deal count fell every year, from 647 to 104, while average deal size grew about 4x, from roughly $13M to roughly $56M. Capital is consolidating into fewer, larger bets.

### 4. The 2017 peak was about deal size, not deal volume
The funding peak of $10.4B in 2017 was driven by bigger deals, not more startups getting funded. Deal count that year was actually *lower* than in 2016.

### Key numbers at a glance

| Metric | Value |
|---|---|
| Records analysed | 3,044 |
| Bengaluru deals / total funding | ≈850 / ≈$14.6B |
| Deal count, 2015 → 2019 | 647 → 104 |
| Average deal size, 2015 → 2019 | ≈$13M → ≈$56M |
| Peak funding year | 2017 (≈$10.4B) |

## What This Means

- **For investors:** deal count and total funding rank cities and sectors differently. Looking at both, plus average deal size, avoids reading activity as capital.
- **For founders:** funding is heavily concentrated in a few hubs and the market moved towards larger rounds, which raises the bar for early-stage deals.
- **For market researchers:** trend analysis needs a complete-year filter, and deal-count and money-raised views should always be reported side by side.

## Notebook

The full analysis, with code, charts and written insights after each stage, is in [`Indian_Startup_Funding_Analysis.ipynb`](Indian_Startup_Funding_Analysis.ipynb). GitHub displays it directly in the browser.

**To run it yourself:** download `startup_funding.csv` from `data/Raw/`, then update the file path in the cell that calls `pd.read_csv(...)` so it points to the file on your computer.

## Limitations

- **Investor counts reflect appearance frequency.** The Investors Name column lists co-investors together without splitting them into individual rows, so investor activity shows how often a name appears, not exclusive deal leadership.
- **2020 is excluded from the time-trend analysis.** It contains only 7 deals, covering January 2 to 13, so it is an incomplete year.
- **The dataset only contains publicly reported deals,** so totals describe disclosed funding and not the whole ecosystem.
- **Some fields are incomplete** (industry, sub-vertical, city, investor), so analysis that needs a missing field leaves those rows out.
- **Funding amounts are skewed.** A few very large deals can dominate totals, which is why the analysis reports deal counts and totals side by side.

## Skills Demonstrated

- Cleaning messy real-world data: number-format conversion, hidden-character removal, date repair, category standardisation and outlier verification
- Making and documenting judgment calls on missing, placeholder and conflicting values
- Aggregation, ranking and trend analysis with Pandas (`groupby`, sorting, filtering)
- Data visualisation with Matplotlib and Seaborn, with a written insight after each chart
- Turning analysis into plain-language findings for non-technical readers

## Repository Contents

```
├── data/
│   └── Raw/                                  # Original Kaggle dataset (startup_funding.csv)
├── Indian_Startup_Funding_Analysis.ipynb     # Full analysis notebook, charts embedded inline
└── README.md                                 # This file
```

## Author

**Divyam Upadhyay**
