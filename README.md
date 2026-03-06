# 📱 PhonePe Pulse — Data Analysis Project
### Python | Pandas | NumPy | Matplotlib | Seaborn | Jupyter Notebook

> An end-to-end exploratory data analysis of PhonePe's transaction pulse data spanning Q1 2018 to Q2 2021 — covering 36 states, 700+ districts, and 14 quarters of India's digital payment revolution.

---

## 📌 What This Project Is About

India's shift to digital payments didn't happen in a straight line. There were periods of steady organic growth, a sudden pandemic-driven dip, and then an acceleration that changed the landscape permanently. This project uses PhonePe's real pulse data to trace that journey — state by state, quarter by quarter — and understand what actually drove adoption, where the gaps still exist, and what the numbers suggest about where growth is heading next.

This isn't just a collection of charts. Every analysis here was built from scratch — raw Excel sheets with inconsistent formatting, columns that needed reconstruction, missing values that had to be reasoned through, and datasets that were cross-verified at multiple levels before being trusted. The outcome is a structured, honest analysis that tells a coherent story about one of the most significant economic behavioural shifts in modern India.

---

## 📂 Datasets Used

| Dataset | What It Contains |
|---|---|
| `State_Txn and Users` | State-level transaction counts, amounts, ATV, app opens, and registered users by quarter |
| `State_TxnSplit` | Transaction type breakdown (P2P, P2M, etc.) per state and quarter |
| `State_DeviceData` | Device brand distribution and registered users per brand per state |
| `District_Txn and Users` | District-level transaction and user metrics |
| `District Demographics` | Population, density, and district codes from Census data |

> **Source:** PhonePe Pulse Open Dataset
> **Format:** Multi-sheet Excel workbook with wide-format structures and inconsistent numeric formatting

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

Getting the data into a workable shape was the first real challenge. Each dataset came as a separate sheet in a single Excel file and none of them were immediately ready for analysis. Date columns had to be reconstructed by combining separate Year and Quarter fields. Amount columns had embedded commas that broke numeric parsing entirely. One dataset had missing ATV values that couldn't simply be dropped — they were recalculated from the Amount and Transactions columns to preserve row integrity.

Each dataset was also inspected using `.info()` after loading — checking column types, null counts, and memory usage before any cleaning began. Beyond that, each dataset was profiled individually with summary statistics and a detailed missing value audit showing column-level percentages. This groundwork made everything downstream more trustworthy.

**Key datasets loaded:**
- `State_Txn_Users` — first 5 rows displayed after cleaning
- `State_TxnSplit` — last 10 rows displayed
- `State_DeviceData` — 10 rows from the middle using a custom `show_middle()` function
- `District_Txn_Users` — first and last 10 rows combined
- `District_Demographics` — every 10th row displayed for a spread-out sample

### Task 2 — Exploratory Data Analysis

**2.1 — Transaction Trends Over Time**
Transactions and amounts were aggregated by state and year. Maharashtra, Karnataka, Telangana, Andhra Pradesh, and Rajasthan led consistently across years. The bottom 5 told a different story — pointing to infrastructure and access gaps in smaller states and union territories that haven't been addressed yet.

**2.2 — Most Common Transaction Types**
For each state and quarter, the most frequent transaction type was identified. Peer-to-peer transfers dominated almost universally — the primary use case that brings most users onto any digital payments platform. Merchant payments showed steady growth in commercially active states, which is a more meaningful long-term signal.

**2.3 — Device Brand Analysis**
Xiaomi led by registered user count across most states — a direct reflection of its dominance in the affordable smartphone segment. Samsung and Vivo followed as strong runners-up across multiple geographies. The brand landscape shifts noticeably in wealthier states where premium devices appear more frequently.

**2.4 — District Population Analysis**
The most populous district per state was identified and plotted on a column chart across all states. State capitals and primary commercial hubs — Bengaluru Urban, Mumbai, Hyderabad — topped these lists, confirming how concentrated economic activity is within a state's leading district.

**2.5 — Average Transaction Value (ATV) by State**
ATV was computed at the state level using district-level data and the top 5 and bottom 5 states were placed on a single bar chart with edge labels. High transaction count doesn't always mean high transaction value — the two metrics paint different pictures, and understanding both matters.

**2.6 — App Usage Trends**
App opens were tracked quarterly for all states. A line plot was built for Maharashtra as a high-engagement representative. Notably, app opens don't scale proportionally with transaction counts — users open the app for balance checks, UPI ID lookups, and exploring features, not just to make payments.

**2.7 — Transaction Type Distribution (Most Recent Quarter)**
A dynamic subplot grid shows transaction type breakdown for every state in the latest available quarter. Each state gets its own colour-coded bar chart. The grid resizes automatically based on how many states are in the data, with unused panels hidden cleanly.

**2.8 — District Code Mapping**
A verified one-to-one mapping between district names and official census codes was extracted from the Demographics dataset, deduplicated, and exported as a standalone CSV — useful for future joins with external datasets.

### Task 3 — Data Quality Checks

Before running any cross-dataset analysis, district-level aggregates for transactions, amounts, and registered users were computed independently and compared against state-level totals. A tolerance of 1 was applied to account for rounding. Zero meaningful discrepancies were found across all 36 states — confirming the dataset is internally consistent at both levels.

### Task 4 — Merging and Advanced Analysis

**4.1 — User-to-Population Ratio**
The peak registered users per state (using `.max()` across quarters — capturing the highest adoption point rather than summing across time) were merged with census population figures. The resulting ratio shows what share of each state's population has ever registered on PhonePe. Maharashtra, Karnataka, and Telangana lead. UP, Bihar, and MP — despite their enormous populations — show significantly lower ratios, pointing clearly to where the next wave of growth needs to happen.

**4.2 — Population Density vs Transaction Volume**
District-level density was merged with total transaction counts and a correlation matrix was computed. The relationship came out weak — density alone has limited predictive power over transaction volume. A scatter plot confirmed this visually. What actually drives transactions appears to be economic activity, banking coverage, and smartphone access rather than simply how many people live per square kilometre.

**4.3 — Average Transaction Amount Per User**
Total amounts were divided by total registered users at the state level to derive a per-user spend figure. States with strong industrial economies led this metric. Top 5 and bottom 5 were visualised side by side with value labels on the bars for easy comparison.

**4.4 — Device Brand Usage Ratio**
Each brand's share of total registered users was computed per state and quarter, then visualised as a subplot grid — one bar chart per state — showing how brand preferences vary across geographies.

### Task 5 — Interactive Visualisations

Three charts were built where inputs drive what gets displayed — users can change state, year, or quarter at runtime:

- **Dual-axis line plot** — transactions and transaction amount on the same chart for any selected state, with independent Y-axes so neither metric's scale dominates the other
- **Pie chart** — transaction type distribution for any chosen state, year, and quarter combination, with percentage labels
- **Bar chart** — population density across all districts of any selected state, with a 90-degree label rotation for readability

### Task 6 — Insights and Conclusions

- A transaction trend analysis covering the 2018–2019 gradual growth phase, the 2020 Q2 COVID-19 dip, and the steep post-pandemic acceleration — all identified from the data without needing labels
- A demographic correlation analysis examining whether population density predicts transaction volume, with a scatter plot and written interpretation of the weak relationship found
- A comprehensive project summary covering key findings from every section and six actionable business recommendations written as a connected narrative

---

## ⚠️ Data Challenges and How They Were Handled

### Challenge 1 — Embedded Commas in Amount Columns
`Amount (INR)` and `ATV (INR)` columns stored numbers with Indian formatting commas (e.g., `"1,23,456"`), which caused Pandas to read them as strings. Any arithmetic on these columns failed immediately until cleaned.

**Fix:** `.str.replace(",", "")` stripped the formatting, `pd.to_numeric()` with `errors='coerce'` handled any remaining non-numeric values safely, and `.astype('Int64')` preserved nullable integer behaviour. Forward fill was applied selectively where values were genuinely missing.

---

### Challenge 2 — No Ready-to-Use Date Column
Every dataset stored time information across two separate columns — `Year` and `Quarter` — with no combined date field for time-series operations.

**Fix:** Combined both fields as strings and parsed them using `pd.to_datetime()`, then converted to quarter period strings via `.dt.to_period('Q').astype(str)` — producing clean labels like `2020Q1` that sort, filter, and group correctly across all datasets.

---

### Challenge 3 — Missing ATV Values in District Data
The `District_Txn and Users` dataset had null ATV values for certain districts — Arunachal Pradesh being one clear example — that couldn't be dropped without losing valid transaction rows.

**Fix:** Where ATV was null, it was recalculated directly from `Amount (INR) / Transactions` using `.loc` to update only the affected rows. `.fillna(0)` handled edge cases where Transactions was also zero, preventing division errors.

---

### Challenge 4 — Missing District Codes
Some districts had no corresponding census code — likely due to unmatched entries at the source.

**Fix:** Missing codes were filled with the string `"Unknown"` to keep all rows available for aggregation without introducing NaN-related join failures downstream.

---

### Challenge 5 — Choosing the Right Aggregation for User Penetration
When calculating how many users each state had relative to its population, summing registered users across all quarters would have inflated the count — the same user appears in multiple quarters. A cumulative sum doesn't represent unique users.

**Fix:** Used `.max()` instead of `.sum()` when aggregating registered users per state — capturing the peak adoption figure at any point in time, which is a more honest representation of how many people have registered on the platform.

---

### Challenge 6 — Cross-Level Data Consistency Verification
Before running any merged analysis, it was necessary to confirm that district-level data and state-level data told the same story. An undetected inconsistency would silently corrupt every downstream result.

**Fix:** Both levels were aggregated independently and merged with suffixed column names. Absolute differences were computed for transactions, amounts, and registered users. Any row exceeding a tolerance of 1 was flagged. Result: fully consistent — zero discrepancies found across all 36 states.

---

### Challenge 7 — Dynamic Subplot Grid for Variable State Count
Building one chart per state requires a grid that resizes automatically — hardcoding row or column counts would break the moment a different dataset was used.

**Fix:** `(len(states) + 2) // 3` dynamically computes the required number of rows for a 3-column layout. After the main loop, leftover empty panels are hidden using `axes[j].set_visible(False)`, with `j` starting from the last value of `i` that remained in memory after the loop completed.

---

### Challenge 8 — Weak Correlation Between Density and Transactions
The working assumption was that higher population density would predict higher transaction volume. The data disagreed — and rather than force a narrative, the finding was investigated properly and reported as is.

**Fix:** District density was merged with district transaction totals, `.corr()` was computed on the numeric columns, and the result was validated with a scatter plot. The weak correlation was confirmed on both fronts and documented honestly as a finding rather than explained away.

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
| Data consistency check | District and state level figures fully consistent — zero discrepancies |

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
Open the notebook and replace the hardcoded local filepath at the top:
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
UP, Bihar, and MP have enormous populations but low digital payment adoption ratios. Regional language support, simpler onboarding, and offline-capable UPI features are practical levers that could move these markets meaningfully.

**2. The post-COVID behavioural shift is permanent — build on it.**
The acceleration from 2020 Q3 onwards wasn't a temporary spike. It was a structural change in how people approach everyday payments. The opportunity now is converting that momentum into deeper merchant payment adoption across Tier-2 and Tier-3 cities.

**3. Optimise for Xiaomi's ecosystem.**
Xiaomi users form the single largest user cohort across most states. Making the app experience seamless on MIUI — and exploring pre-load partnerships — would reach the widest audience at the lowest marginal cost.

**4. Build differently for high-ATV states.**
States with high average transaction values have a meaningful commercial user base. Features like instant settlement, GST-linked invoicing, and business dashboards would create genuine platform dependency for these users rather than just transactional utility.

**5. Don't plan expansion around population density alone.**
The data makes this point clearly — density is a weak predictor. Expansion strategy should prioritise areas where internet connectivity is improving, banking infrastructure is growing, and local merchant ecosystems are forming — regardless of how densely populated a region is.

**6. Close the gap in north-eastern states and smaller territories.**
Transaction volumes from these regions sit at the bottom of the dataset — but the gap is largely an infrastructure story, not a demand one. Targeted inclusion programs and streamlined KYC tailored to these geographies could shift that over time.

---

## 🙌 Acknowledgements

- Data sourced from the **PhonePe Pulse open dataset** — one of the most comprehensive publicly available records of India's digital payment ecosystem
- Project completed as part of a Python Data Analysis curriculum at **Coding Ninjas**

---

## 📬 Connect

If you'd like to discuss the analysis, suggest improvements, or collaborate — feel free to reach out.

> ⭐ If this project was useful or interesting to you, a star on GitHub goes a long way — it helps others find it too.
