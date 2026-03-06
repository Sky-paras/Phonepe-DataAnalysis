# 📱 PhonePe Pulse — Data Analysis Project
### Python | Pandas | NumPy | Matplotlib | Seaborn | Jupyter Notebook

> An end-to-end exploratory data analysis of PhonePe's transaction pulse data spanning Q1 2018 to Q2 2021 — covering 36 states, 700+ districts, and 14 quarters of India's digital payment revolution.

---

## 📌 What This Project Is About

India's shift to digital payments didn't happen overnight. There were years of steady organic growth, a sudden pandemic-driven dip, and then an acceleration that changed consumer behaviour permanently. This project uses PhonePe's real pulse data to trace that journey — state by state, quarter by quarter — and understand what actually drove adoption, where the gaps still exist, and what the numbers suggest about where growth goes next.

Every analysis here was built from scratch. Raw Excel sheets with inconsistent formatting, columns that needed reconstruction, missing values that had to be reasoned through rather than simply dropped, and datasets verified at multiple levels before being trusted. The outcome is a structured, honest analysis that tells a coherent story about one of the most significant economic shifts in modern India.

---

## 📂 Datasets Used

| Dataset | What It Contains |
|---|---|
| `State_Txn and Users` | State-level transaction counts, amounts, ATV, app opens, registered users — by quarter |
| `State_TxnSplit` | Transaction type breakdown (P2P, P2M, etc.) per state and quarter |
| `State_DeviceData` | Device brand distribution and registered users per brand per state |
| `District_Txn and Users` | District-level transaction and user metrics |
| `District Demographics` | Population, density, and district codes from Census data |

> **Source:** PhonePe Pulse Open Dataset
> **Format:** Multi-sheet Excel workbook with wide-format date structures and inconsistent numeric formatting

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| **Python 3.x** | Core language |
| **Pandas** | Data loading, cleaning, reshaping, merging, aggregation |
| **NumPy** | Numerical operations and edge case handling |
| **Matplotlib** | Line plots, bar charts, scatter plots, pie charts |
| **Seaborn** | Color palettes and subplot aesthetics |
| **openpyxl** | Reading multi-sheet Excel workbooks |
| **Jupyter Notebook** | Interactive analysis and inline documentation |

---

## 🔍 What Was Analysed — Task by Task

### Task 1 — Data Loading and Understanding

Each dataset lived in a separate sheet of a single Excel workbook. None of them were analysis-ready straight out of the box. Date columns had to be rebuilt from separate Year and Quarter fields. Amount columns had embedded Indian-format commas that broke numeric parsing. One dataset had missing ATV values that couldn't simply be dropped — they were recalculated from Amount divided by Transactions to preserve every row.

After loading, each dataset was inspected using `.info()` to check column types and null counts before any cleaning. Summary statistics and missing value percentages were then computed across all five datasets to understand the data landscape before touching it.

### Task 2 — Exploratory Data Analysis

**2.1 — Transaction Trends Over Time**
Transactions and amounts were aggregated by state and year. Maharashtra, Karnataka, Telangana, Andhra Pradesh, and Rajasthan led consistently. The bottom 5 pointed to infrastructure and access gaps in smaller states and union territories that haven't closed yet.

**2.2 — Most Common Transaction Types**
The dominant transaction type per state and quarter was identified. Peer-to-peer transfers topped the list almost universally — the entry-point use case for most users. Merchant payments showed steady quarter-on-quarter growth in commercially active states, which is the more meaningful long-term signal.

**2.3 — Device Brand Analysis**
Xiaomi led by registered user count across most states — consistent with its dominance in the affordable smartphone segment. Samsung and Vivo followed as strong runners-up. Premium brands appeared more frequently in wealthier states, aligning with higher average transaction values in those same geographies.

**2.4 — District Population Analysis**
The most populous district per state was identified and visualised on a column chart. State capitals and primary commercial hubs dominated predictably — Bengaluru Urban, Mumbai, Hyderabad. The chart makes it easy to see just how concentrated population is within each state's single leading district.

**2.5 — Average Transaction Value (ATV) by State**
ATV was computed using `.mean()` across districts per state — giving a truer average than summing would. The top 5 and bottom 5 states were placed side by side on a single bar chart with edge labels. High volume and high value don't always go together, and this chart makes that distinction visible.

**2.6 — App Usage Trends**
App opens were tracked quarterly for every state. A line plot was built for Maharashtra as a representative high-engagement state. The interesting observation: app opens don't scale proportionally with transactions. Users open the platform for balance checks, UPI ID lookups, and browsing — not only to transact.

**2.7 — Transaction Type Distribution (Most Recent Quarter)**
A dynamic subplot grid shows the transaction type breakdown for every state in the most recent available quarter — one colour-coded bar chart per state. The grid resizes automatically based on the number of states in the data, with unused panels hidden cleanly after the loop completes.

**2.8 — District Code Mapping**
A verified one-to-one mapping between district names and official census codes was extracted, deduplicated, and exported as a standalone CSV file — ready for future joins with external datasets.

### Task 3 — Data Quality Checks

District-level aggregates for transactions, amounts, and registered users were computed independently and compared against state-level totals. A tolerance of 1 was applied to account for rounding differences. Zero meaningful discrepancies were found across all 36 states — confirming the dataset is internally consistent before any cross-level merging began.

### Task 4 — Merging and Advanced Analysis

**4.1 — User-to-Population Ratio**
Peak registered users per state (using `.max()` across quarters — capturing the highest adoption point rather than double-counting users across periods) were merged with census population data. The resulting percentage shows what share of each state's population has registered on PhonePe. Maharashtra, Karnataka, and Telangana lead. UP, Bihar, and MP show significantly lower ratios despite their enormous populations — pointing clearly to the largest untapped opportunity in the dataset.

**4.2 — Population Density vs Transaction Volume**
District-level density figures were merged with total transaction counts and a correlation matrix was computed. The relationship came out weak — density alone has limited predictive power over transaction volume. A scatter plot confirmed this visually with widely scattered data points. Economic activity, banking infrastructure, and smartphone access are stronger predictors than raw density.

**4.3 — Average Transaction Amount Per User**
Total transaction amounts were divided by total registered users at the state level to derive a per-user spend figure. States with strong industrial and commercial economies led this metric. Top 5 and bottom 5 were placed on a single chart with bar labels for direct comparison.

**4.4 — Device Brand Usage Ratio**
Each brand's share of total registered users was computed per state and quarter — using `.max()` on the state side to avoid inflating the denominator with cumulative sums across quarters. Results were visualised as a subplot grid, one bar chart per state.

### Task 5 — Interactive Visualisations

Three user-input driven charts were built — state, year, or quarter can be changed at runtime:

- **Dual-axis line plot** — transactions and amount over time for any selected state, with independent Y-axes so neither metric's scale overwhelms the other
- **Pie chart** — transaction type distribution for any chosen state, year, and quarter, with percentage labels
- **Bar chart** — population density across all districts of a selected state, sorted descending so the densest districts appear first

### Task 6 — Insights and Conclusions

- Transaction trend analysis covering the gradual 2018–2019 growth, the 2020 Q2 COVID dip, and the sharp post-pandemic acceleration — all readable directly from the data
- Demographic correlation analysis examining population density against transaction volume, with scatter plot and honest interpretation of the weak relationship found
- Full project summary with findings from every section and six actionable business recommendations, written as a connected analytical narrative

---

## ⚠️ Data Challenges and How They Were Handled

### Challenge 1 — Embedded Commas in Amount Columns
`Amount (INR)` and `ATV (INR)` had Indian-format commas inside numeric values (e.g. `"1,23,456"`), causing Pandas to load them as strings and making any arithmetic fail immediately.

**Fix:** `.str.replace(",", "")` stripped the formatting, `pd.to_numeric()` with `errors='coerce'` converted safely, and `.astype('Int64')` preserved nullable integer behaviour. Forward fill handled genuinely missing values.

---

### Challenge 2 — Date Column Reconstruction
Every dataset stored time across two separate columns — `Year` and `Quarter` — with no combined field ready for time-series operations.

**Fix:** Both fields were concatenated as strings and parsed via `pd.to_datetime()`, then converted to quarter period labels using `.dt.to_period('Q').astype(str)` — producing clean sortable strings like `2020Q1` consistently across all datasets.

---

### Challenge 3 — Missing ATV Values in District Data
Certain districts in `District_Txn and Users` had null ATV values — Arunachal Pradesh was one visible example — that couldn't be dropped without losing valid transaction rows.

**Fix:** Missing ATV values were recalculated in-place using `Amount (INR) / Transactions` via `.loc` targeting only null rows. `.fillna(0)` handled cases where Transactions was also zero to prevent division errors.

---

### Challenge 4 — Missing District Codes
Some districts had no corresponding census code, likely due to unmatched entries at the data source.

**Fix:** Missing codes were filled with `"Unknown"` — keeping all rows in the dataset without introducing NaN-related failures in downstream joins or groupby operations.

---

### Challenge 5 — Avoiding Double-Counting Users Across Quarters
Summing registered users across all quarters for a state inflates the count — the same user appears in multiple quarters. For penetration ratios and brand usage calculations, this distorts every result.

**Fix:** Used `.max()` instead of `.sum()` when aggregating registered users per state — capturing the peak adoption figure at any point in time, which honestly represents how many people have registered without counting them multiple times.

---

### Challenge 6 — ATV Aggregation Accuracy
Summing ATV values across districts doesn't produce a meaningful average — it produces a total of averages, which is a different and less useful number.

**Fix:** Used `.mean()` when aggregating `ATV (INR)` at the state level, giving a genuine average transaction value that reflects actual spending behaviour across districts.

---

### Challenge 7 — Cross-Level Consistency Verification
Before running any merged analysis, district and state level figures needed to match. An undetected inconsistency would silently corrupt every downstream result.

**Fix:** Both levels were aggregated independently and merged with suffixed column names. Absolute differences were computed for transactions, amounts, and users. A tolerance of 1 was applied for rounding. Result: zero discrepancies across all 36 states.

---

### Challenge 8 — Dynamic Subplot Grid for Variable State Count
Building one chart per state requires a grid that adjusts automatically — hardcoding rows or columns breaks whenever the dataset changes.

**Fix:** `(len(states) + 2) // 3` computes the required row count for a 3-column layout dynamically. Empty panels after the main loop are hidden via `axes[j].set_visible(False)`, with `j` starting from the last value of `i` retained in memory after the loop.

---

### Challenge 9 — Wrong Import Alias Breaking Pandas (Fixed)
An earlier version had `import matplotlib.pyplot as pd` — which silently overwrote the Pandas alias, breaking all Pandas operations from that cell onwards.

**Fix:** Corrected to `import matplotlib.pyplot as plt` — consistent with every other cell in the notebook.

---

### Challenge 10 — Wrong Chart Title in District Density Plot (Fixed)
Task 5.3 had the title `"Transaction Type Distribution"` on a chart that was actually showing population density by district — a copy-paste error from the previous cell.

**Fix:** Updated to `"Population Density by District\n{state_name}"` — accurately reflecting what the chart displays. Districts are also sorted descending by density so the highest-density areas appear first.

---

## 📊 Key Findings at a Glance

| What We Looked At | What We Found |
|---|---|
| Overall transaction growth | Low Lakhs in Q1 2018 → nearly 4 Arabs by Q2 2021 |
| COVID-19 impact | Clear dip in 2020 Q2, followed by the steepest growth phase in the dataset |
| Top transaction states | Maharashtra, Karnataka, Telangana, Andhra Pradesh, Rajasthan |
| Dominant transaction type | Peer-to-Peer (P2P) across virtually all states and quarters |
| Leading device brand | Xiaomi — dominant in most states by registered user count |
| Highest user penetration | Maharashtra, Karnataka, Telangana |
| Biggest untapped markets | Uttar Pradesh, Bihar, Madhya Pradesh |
| Density vs transaction volume | Weak correlation — economic infrastructure is the stronger predictor |
| ATV aggregation | Corrected to mean — gives accurate average spend per state |
| Data consistency check | District and state level fully consistent — zero discrepancies |

---

## 📁 Project Structure

```
PhonePe-Pulse-Analysis/
│
├── Phonepe_Project.ipynb              # Main analysis notebook
├── phonepe-pulse_raw-data.xlsx        # Source data (5 sheets)
├── unique_district_mapping.csv        # Exported district-code mapping
└── README.md                          # Project documentation
```

---

## ▶️ How to Run

**Step 1 — Clone the repository:**
```bash
git clone https://github.com/Sky-paras/PhonePe-Pulse-Analysis.git
cd PhonePe-Pulse-Analysis
```

**Step 2 — Install dependencies:**
```bash
pip install pandas numpy matplotlib seaborn openpyxl jupyter
```

**Step 3 — Update the file path:**
```python
# Replace this:
filepath = r"D:\Paras\My Document\...\phonepe-pulse_raw-data.xlsx"

# With this:
filepath = "phonepe-pulse_raw-data.xlsx"
```

**Step 4 — Run the notebook:**
```bash
jupyter notebook Phonepe_Project.ipynb
```

---

## 💡 Recommendations Based on the Analysis

**1. Go after high-population, low-penetration states.**
UP, Bihar, and MP have enormous populations but comparatively low digital payment adoption. Regional language support, simpler onboarding, and offline UPI features are practical levers that can move these markets.

**2. The post-COVID shift is permanent — capitalise on it.**
The acceleration from 2020 Q3 is not a temporary spike. The window to convert app-active users into regular P2M transactors — especially in Tier-2 and Tier-3 cities — is open right now.

**3. Optimise for Xiaomi's ecosystem.**
Xiaomi users are the single largest cohort across most states. MIUI-specific optimisations and pre-load partnerships reach the widest audience at minimal marginal cost.

**4. Build features for high-ATV states.**
States with high average transaction values have a meaningful commercial user base. Instant settlement, GST-linked invoicing, and business dashboards create genuine platform dependency for these users.

**5. Don't chase density — chase infrastructure.**
Population density is a weak predictor of transaction volume. Expansion decisions should follow internet connectivity growth, banking coverage improvements, and developing merchant ecosystems.

**6. Close the gap in north-eastern states and smaller territories.**
Low transaction volumes here are an infrastructure story, not a demand story. Targeted inclusion programs and streamlined KYC can shift this picture over time.

---

## 🙌 Acknowledgements

- Data sourced from the **PhonePe Pulse open dataset**
- Project completed as part of a Python Data Analysis curriculum at **Coding Ninjas**

---

## 📬 Connect

Feel free to reach out to discuss the analysis, suggest improvements, or collaborate.

> ⭐ If this project was useful, a star on GitHub helps others find it too.
