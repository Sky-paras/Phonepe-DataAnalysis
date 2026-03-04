# 📱 PhonePe Pulse — Data Analysis Project
### Python | Pandas | NumPy | Matplotlib | Seaborn | Jupyter Notebook

> An end-to-end exploratory data analysis of PhonePe's transaction pulse data spanning Q1 2018 to Q2 2021 — covering 36 states, 700+ districts, and 14 quarters of India's digital payment revolution.

---

## 📌 What This Project Is About

India's shift to digital payments didn't happen in a straight line. There were periods of steady organic growth, a sudden pandemic-driven dip, and then an acceleration that changed the landscape permanently. This project uses PhonePe's real pulse data to trace that journey — state by state, quarter by quarter — and understand what actually drove adoption, where the gaps still exist, and what the numbers say about where growth is heading next.

This isn't just a collection of charts. Every analysis here was built from scratch — raw Excel sheets with messy formatting, columns that needed reconstruction, missing values that had to be reasoned through rather than just dropped, and datasets that were cross-verified at multiple levels before being trusted. The outcome is a structured, honest analysis that tells a coherent story about one of the most significant economic behavioural shifts in modern India.

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
> **Format:** Multi-sheet Excel workbook with wide-format structures and inconsistent numeric formatting across columns

---

## 🛠️ Tech Stack

| Tool | What It Was Used For |
|---|---|
| **Python 3.x** | Core language |
| **Pandas** | Data loading, cleaning, reshaping, merging, aggregation |
| **NumPy** | Numerical operations and edge case handling |
| **Matplotlib** | All visualisations — line plots, bar charts, scatter plots, pie charts |
| **Seaborn** | Color palettes and subplot aesthetics |
| **openpyxl** | Reading multi-sheet Excel workbooks |
| **Jupyter Notebook** | Interactive analysis and inline documentation |

---

## 🔍 What Was Analysed — Task by Task

### Task 1 — Data Loading and Understanding

Getting the data into a workable shape was the first real challenge. Each dataset lived as a separate sheet in a single Excel file, and none of them were immediately ready for analysis. Date columns had to be reconstructed by combining separate Year and Quarter fields. Amount columns had embedded commas that broke numeric parsing entirely. One dataset had missing ATV values that couldn't simply be dropped — they were recalculated from Amount and Transactions columns to preserve row integrity.

Beyond loading, each dataset was profiled individually — data types, summary statistics, and a detailed missing value audit with percentage breakdowns. This groundwork made every downstream analysis more trustworthy.

### Task 2 — Exploratory Data Analysis

**2.1 — Transaction Trends Over Time**
Total transactions and amounts were aggregated by state and year to understand how volumes evolved across the full 14-quarter window. The top 5 states by transaction volume — Maharashtra, Karnataka, Telangana, Andhra Pradesh, and Rajasthan — emerged consistently across years. The bottom 5 told a different story, pointing to infrastructure and access gaps that haven't been closed yet.

**2.2 — Most Common Transaction Types**
For each state and quarter, the single most frequent transaction type was identified and displayed. Peer-to-peer (P2P) transfers dominated almost universally — which makes sense as the primary use case that brings most users onto any digital payments platform. Merchant payments showed steady growth particularly in commercially active states, which is a more meaningful long-term signal than raw P2P volume.

**2.3 — Device Brand Analysis**
Xiaomi emerged as the leading brand by registered user count across most Indian states — consistent with its dominance in the affordable smartphone segment that powered much of India's digital payment adoption. Samsung and Vivo followed as strong runners-up across multiple geographies.

**2.4 — District Population Analysis**
For each state, the most populous district was identified and plotted on a column chart. State capitals and primary commercial hubs — Bengaluru Urban, Mumbai, Hyderabad — topped these lists predictably, but the chart makes it easy to see just how concentrated population is within each state's leading district relative to others.

**2.5 — Average Transaction Value (ATV) by State**
ATV was computed at the state level and the top 5 and bottom 5 states were compared side by side on a single bar chart. One of the more useful findings here is that transaction frequency and transaction value don't always move together — high volume states aren't always high value states, and that distinction matters for understanding how different economies engage with digital payments.

**2.6 — App Usage Trends**
Total app opens were tracked across all states and quarters. A line plot was built for Maharashtra as a representative high-engagement state. The interesting pattern here is that app opens don't scale proportionally with transaction counts — users open the platform for balance checks, UPI ID lookups, and browsing features, not just to transact. Engagement and transaction activity are related but distinct metrics.

**2.7 — Transaction Type Distribution (Most Recent Quarter)**
A dynamic subplot grid was built showing the transaction type breakdown for every state in the most recent available quarter. Each state gets its own bar chart. The grid adjusts automatically based on the number of states in the data, with unused panels hidden cleanly.

**2.8 — District Code Mapping**
A verified one-to-one mapping between district names and their official census codes was extracted, deduplicated, and exported as a standalone CSV file for future use or joining with external datasets.

### Task 3 — Data Quality Checks

District-level aggregates for transactions, amounts, and registered users were independently computed and compared directly against state-level totals. A tolerance threshold of 1 was applied to account for rounding. The result was clean — zero meaningful discrepancies found across all 36 states. This verification step was done before any merging or advanced analysis to ensure the foundation was solid.

### Task 4 — Merging and Advanced Analysis

**4.1 — User-to-Population Ratio**
State-level registered users were merged with census population data to compute what share of each state's population is registered on PhonePe. The results confirmed that economically developed, digitally mature states like Maharashtra, Karnataka, and Telangana lead in penetration ratios — while high-population states like UP, Bihar, and MP show significantly lower figures, pointing to the largest untapped markets in the dataset.

**4.2 — Population Density vs Transaction Volume**
District-level density figures were merged with transaction counts and a correlation matrix was computed. The correlation came out weak — density alone has very limited predictive power over transaction volume. A scatter plot confirmed this visually, with data points scattered widely rather than forming any discernible trend. What actually drives transaction volume appears to be a combination of economic activity, banking infrastructure, and smartphone access — not simply how many people live per square kilometre.

**4.3 — Average Transaction Amount Per User**
Total transaction amounts were divided by registered users at the state level to derive a per-user spend metric. States with strong industrial and commercial economies led this metric. The top 5 and bottom 5 were visualised together on a single bar chart with value labels for direct comparison.

**4.4 — Device Brand Usage Ratio**
The proportion of each device brand's users relative to total registered users was calculated for every state and visualised as individual bar charts in a subplot grid — one chart per state.

### Task 5 — Interactive Visualisations

Three user-driven charts were built where the state, year, or quarter can be changed by input at runtime:

- **Dual-axis line plot** showing total transactions and transaction amount over time for any selected state — both metrics on the same chart with independent Y-axes so neither scale overwhelms the other
- **Pie chart** showing transaction type distribution for any chosen state, year, and quarter combination
- **Bar chart** showing population density across all districts of any selected state

### Task 6 — Insights and Conclusions

- A full transaction trend analysis covering the gradual growth phase (2018–2019), the COVID-19 dip at 2020 Q2, and the sharp post-pandemic acceleration that followed
- A demographic correlation analysis examining population density against transaction volume, with scatter plot and written interpretation
- A comprehensive project summary covering key findings from every section, patterns observed across the data, and six actionable recommendations — written as a connected analytical narrative rather than a list of disconnected bullets

---

## ⚠️ Data Challenges and How They Were Handled

### Challenge 1 — Embedded Commas in Numeric Columns
`Amount (INR)` and `ATV (INR)` columns contained values formatted with commas (e.g., `"1,23,456"`) which caused Pandas to load them as strings, making any arithmetic operation fail immediately.

**Fix:** `.str.replace(",", "")` stripped the formatting, `pd.to_numeric()` with `errors='coerce'` safely converted the values, and `.astype('Int64')` preserved nullable integer behaviour. Forward fill was applied selectively where values were genuinely missing rather than just unformatted.

---

### Challenge 2 — No Ready-to-Use Date Column
Every dataset stored time information across two separate columns — `Year` and `Quarter` — with no combined date field available for time-series operations.

**Fix:** Combined the two fields as strings and parsed them using `pd.to_datetime()`, then converted to quarter period strings via `.dt.to_period('Q').astype(str)` — producing clean labels like `2020Q1` that sort, filter, and group correctly.

---

### Challenge 3 — Missing ATV Values in District Data
The `District_Txn and Users` dataset had missing ATV values for certain districts — Arunachal Pradesh being one visible example — that couldn't be simply dropped without losing valid rows.

**Fix:** Where ATV was null, it was recalculated directly from the available data using `Amount (INR) / Transactions`, with `.fillna(0)` handling any cases where Transactions was also zero to avoid division errors.

---

### Challenge 4 — Missing District Codes
Some districts in the dataset had no corresponding census code — likely due to unmatched entries at the data collection stage.

**Fix:** Missing codes were filled with the string `"Unknown"` to keep all rows available for aggregation without introducing NaN-related join failures downstream.

---

### Challenge 5 — Cross-Level Consistency Verification
Before running any merged analysis between district and state datasets, it was necessary to verify that both levels of data told the same story. An undetected inconsistency here would silently corrupt every downstream result.

**Fix:** Both levels were aggregated independently and merged with suffixed column names. Absolute differences were computed for transactions, amounts, and users, and any row exceeding a tolerance of 1 was flagged. Result: fully consistent across all 36 states — zero discrepancies found.

---

### Challenge 6 — Dynamic Subplot Grid for All States
Plotting one chart per state required a grid that adjusts automatically based on how many states exist in the data — hardcoding rows or columns would break the moment a different dataset was used.

**Fix:** `(len(states) + 2) // 3` computes the required number of rows for a 3-column layout dynamically. After the main plotting loop, any remaining empty subplot panels are hidden using `axes[j].set_visible(False)` — with `j` picking up from the last value of `i` retained in memory after the loop completes.

---

### Challenge 7 — Weak Correlation Between Density and Transactions
The assumption going in was that higher population density would predict higher transaction volume. The data pushed back on that. Rather than force-fitting a narrative, the finding was investigated properly and reported honestly.

**Fix:** District density was merged with district transaction totals, `.corr()` was run on the numeric columns, and the result was validated visually with a scatter plot. The weak correlation was confirmed on both fronts and documented as a genuine analytical finding — not explained away.

---

## 📊 Key Findings at a Glance

| What We Looked At | What We Found |
|---|---|
| Overall transaction growth | Low Lakhs in Q1 2018 → nearly 4 Arabs by Q2 2021 |
| COVID-19 impact | Visible dip in 2020 Q2, followed by the fastest growth phase in the entire dataset |
| Top transaction states | Maharashtra, Karnataka, Telangana, Andhra Pradesh, Rajasthan |
| Dominant transaction type | Peer-to-Peer (P2P) across virtually all states and quarters |
| Leading device brand | Xiaomi — dominant in most states by registered user count |
| Highest user penetration | Maharashtra, Karnataka, Telangana |
| Biggest untapped markets | Uttar Pradesh, Bihar, Madhya Pradesh |
| Density vs transaction volume | Weak correlation — economic infrastructure matters far more |
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
UP, Bihar, and MP collectively hold a massive share of India's population but remain significantly underpenetrated. Regional language support, simpler onboarding flows, and offline UPI features like UPI Lite are practical levers that could move these markets meaningfully.

**2. The post-COVID behavioural shift is permanent — build on it.**
The acceleration from 2020 Q3 onwards wasn't a temporary spike driven by circumstance. It was a structural change in how people approach everyday payments. The opportunity now is converting that momentum into deeper merchant payment adoption across Tier-2 and Tier-3 cities.

**3. Optimise for Xiaomi's ecosystem.**
Xiaomi users form the single largest user cohort across most states in the dataset. Making the app experience seamless on MIUI — and exploring pre-load partnerships — would reach the widest possible audience with minimal additional acquisition cost.

**4. Build differently for high-ATV states.**
States with high average transaction values have a meaningful commercial and business user base. Features like instant settlement, GST-linked invoicing, and business analytics dashboards would create genuine platform dependency among these users rather than just transactional utility.

**5. Don't plan expansion purely around population density.**
The data makes this point clearly — density is a weak predictor of transaction volume. Expansion strategy should prioritise areas where internet connectivity is growing, banking infrastructure is improving, and local merchant ecosystems are forming — regardless of how densely populated a region is.

**6. Close the gap in north-eastern states and smaller territories.**
Transaction volumes from these regions sit at the bottom of the dataset — but the gap is largely about infrastructure, not about willingness or need. Targeted inclusion programs and streamlined KYC processes tailored to these geographies could shift that picture over time.

---

## 🙌 Acknowledgements

- Data sourced from the **PhonePe Pulse open dataset** — one of the most comprehensive publicly available records of India's digital payment ecosystem
- Project completed as part of a Python Data Analysis curriculum at **Coding Ninjas**

---

## 📬 Connect

If you'd like to discuss the analysis, suggest improvements, or collaborate on something — feel free to reach out.

> ⭐ If this project was useful or interesting to you, a star on GitHub goes a long way — it helps others find it too.
