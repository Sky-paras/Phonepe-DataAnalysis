# 📱 PhonePe Pulse — Data Analysis Project
### Python | Pandas | NumPy | Matplotlib | Seaborn | Jupyter Notebook

> An end-to-end exploratory data analysis of PhonePe's transaction pulse data spanning Q1 2018 to Q2 2021 — covering 36 states, 700+ districts, and 14 quarters of India's digital payment revolution.

---

## 📌 What This Project Is About

India's shift to digital payments didn't happen in a straight line. There were periods of steady growth, a sudden pandemic-driven dip, and then an acceleration that caught everyone off guard. This project uses PhonePe's real pulse data to trace that journey — state by state, quarter by quarter — and understand what actually drove adoption, where the gaps still exist, and what the numbers suggest about where growth is headed.

This isn't just a collection of charts. Every analysis here was built from scratch — raw Excel sheets with messy formatting, columns that needed reconstruction, and datasets that had to be cross-verified before being trusted. The outcome is a clean, structured analysis that tells a coherent story about one of the most significant economic shifts in modern India.

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
> **Format:** Excel workbook with multiple sheets, wide-format date structures, inconsistent numeric formatting

---

## 🛠️ Tech Stack

| Tool | What It Was Used For |
|---|---|
| **Python 3.x** | Core language |
| **Pandas** | Data loading, cleaning, reshaping, merging, aggregation |
| **NumPy** | Numerical operations and edge case handling |
| **Matplotlib** | All visualisations — line plots, bar charts, scatter plots, pie charts |
| **Seaborn** | Color palettes and enhanced chart aesthetics |
| **Jupyter Notebook** | Interactive analysis and documentation |

---

## 🔍 What Was Analysed — Task by Task

### Task 1 — Data Loading and Understanding
Getting the data into a workable shape was the first real challenge. Each dataset came as a separate sheet inside an Excel workbook, and none of them were immediately ready for analysis. Date columns had to be reconstructed from separate Year and Quarter fields. Amount columns had embedded commas that broke numeric parsing. Some sheets had their actual header row buried inside the data rather than at the top.

Once cleaned, basic profiling was done across all five datasets — summary statistics, data type verification, and a thorough missing value audit. The data was then cross-verified between district and state levels to check internal consistency before any analysis began.

### Task 2 — Exploratory Data Analysis

**Transaction Trends Over Time**
Total transactions and amounts were aggregated by state and year to understand how volumes evolved over the 14-quarter period. The top 5 and bottom 5 states by transaction volume were identified — Maharashtra, Karnataka, Telangana, Andhra Pradesh, and Rajasthan led consistently, while smaller union territories and north-eastern states sat at the lower end.

**Most Common Transaction Types**
For each state and quarter, the dominant transaction type was identified. Peer-to-peer (P2P) transfers topped the list almost universally — which reflects how most people first engage with any digital payment platform. Merchant payments (P2M) showed consistent growth over time, particularly in commercially active states.

**Device Brand Analysis**
Xiaomi emerged as the dominant brand in terms of registered users across most Indian states — a direct reflection of its market share in the affordable smartphone segment. Samsung and Vivo were strong runners-up in multiple states, while premium brands appeared more prominently in wealthier geographies.

**District-Level Population Analysis**
For each state, the district with the highest population was identified. As expected, state capitals and primary commercial cities — Bengaluru Urban, Mumbai, Hyderabad — topped these lists. A column chart was built to visualise this distribution across all states.

**Average Transaction Value (ATV) by State**
ATV was computed for each state and the top 5 highest and bottom 5 lowest states were compared side by side. High transaction count doesn't always mean high transaction value — the two metrics paint different pictures of how a state's economy engages with digital payments.

**App Usage Trends**
App opens were tracked over time for each state. Maharashtra showed one of the steepest engagement curves. More interestingly, app opens didn't always scale proportionally with transactions — indicating users engage with the platform for balance checks, history viewing, and exploration beyond just transacting.

**Transaction Type Distribution (Most Recent Quarter)**
A subplot grid was built showing the distribution of transaction types for every state for the most recent quarter. Each state gets its own bar chart, making state-level comparisons easy at a glance.

**District Code Mapping**
A unique mapping between district names and their official census codes was extracted, verified, and exported as a clean CSV file for future reference or joining with external datasets.

### Task 3 — Data Quality Checks
District-level aggregates for transactions, amounts, and registered users were computed and directly compared against state-level figures. After applying a reasonable tolerance threshold, zero discrepancies were found — confirming the dataset is internally consistent and reliable for analysis.

### Task 4 — Merging and Advanced Analysis

**User-to-Population Ratio**
State-level registered users were merged with district demographics to calculate what percentage of each state's population is registered on PhonePe. High-population states like UP and Bihar showed significantly lower penetration ratios — pointing to the largest untapped opportunity in the entire dataset.

**Population Density vs Transaction Volume**
District-level density data was merged with transaction data and a correlation analysis was run. The correlation turned out to be weak — density alone doesn't predict transaction volume in any reliable way. A scatter plot confirmed this visually with widely scattered data points showing no clear trend.

**Average Transaction Amount Per User**
Total transaction amounts were divided by registered users at the state level to derive average spend per user. States with strong industrial and commercial economies showed the highest figures. Top 5 and bottom 5 were visualised together for direct comparison.

**Device Brand Usage Ratio**
The share of each device brand's users as a proportion of total registered users was calculated for every state. Subplot bar charts — one per state — were built showing brand-level usage ratios side by side.

### Task 5 — Visualisations

- **Dual-axis line plot** — Transactions and amount over time for any selected state, both metrics on the same chart with separate Y-axes
- **Pie chart** — Transaction type distribution for any selected state, year, and quarter — fully dynamic based on user input
- **Bar chart** — Population density of all districts within any selected state

### Task 6 — Insights and Conclusions

- Transaction trend analysis with written insights covering growth phases, the COVID dip, and post-pandemic acceleration
- Correlation analysis between population density and transaction volume with scatter plot and written summary
- Full project summary with findings, observations, and six actionable recommendations written as a structured analytical narrative

---

## ⚠️ Data Challenges and How They Were Handled

### Challenge 1 — Messy Amount Columns
The `Amount (INR)` and `ATV (INR)` columns had commas embedded within numeric values (e.g., `"1,23,456"`) causing Pandas to read them as strings. Direct arithmetic was impossible until they were cleaned.

**Fix:** `.str.replace(",", "")` followed by `pd.to_numeric()` with `errors='coerce'`, then cast to `Int64` to preserve nullable integer behaviour. Forward fill was applied where values were genuinely missing.

---

### Challenge 2 — Date Column Reconstruction
No dataset had a ready-to-use date column. Dates existed as two separate columns — `Year` and `Quarter` — which had to be combined into a single usable period representation.

**Fix:** `pd.to_datetime(Year.astype(str) + '-Q' + Quarter.astype(str))` followed by `.dt.to_period('Q').astype(str)` to create clean quarter labels like `2020Q1` that sort and filter correctly.

---

### Challenge 3 — Misaligned Headers in Some Sheets
Certain sheets had actual column names stored in the first data row rather than as the proper header, causing all columns to load with incorrect labels.

**Fix:** Used `header=1` to examine the structure, then applied `df.columns = df.iloc[0]` to promote the first row as headers, followed by `df.drop(0).reset_index(drop=True)` to remove the duplicate and restore a clean index.

---

### Challenge 4 — Missing District Codes
The `District_Txn and Users` dataset had missing values in the `Code` column for certain districts — likely due to unmatched entries or data collection gaps at source.

**Fix:** Missing codes were filled with the placeholder `"Unknown"` to preserve the rows for aggregation without introducing join errors downstream.

---

### Challenge 5 — Cross-Level Data Verification
Before trusting any merged analysis, district-level and state-level figures needed to be verified against each other. Inconsistencies here would carry forward into every downstream result.

**Fix:** Both levels were aggregated independently, merged with suffixed column names, and absolute differences were computed for transactions, amounts, and users. Any row exceeding a tolerance of 1 was flagged. Result: fully consistent — zero discrepancies found.

---

### Challenge 6 — Dynamic Subplot Grid
Building one chart per state required a grid that adjusts its size based on however many states exist — hardcoding row or column counts would break for any different dataset.

**Fix:** `(len(states) + 2) // 3` dynamically computes the number of rows needed for a 3-column grid. Remaining empty subplot panels after the main loop are hidden using `axes[j].set_visible(False)`, with `j` starting from the last value of `i` retained in memory after loop completion.

---

### Challenge 7 — Weak Correlation Between Density and Transactions
The hypothesis going in was that higher population density would correlate with higher transaction volume. The data disagreed — and that needed proper investigation rather than assumption.

**Fix:** District-level density was merged with transaction counts, `.corr()` was computed on numeric columns, and the relationship was validated visually with a scatter plot. The weak correlation was confirmed both statistically and visually — and documented honestly as a finding.

---

## 📊 Key Findings at a Glance

| What We Looked At | What We Found |
|---|---|
| Overall transaction growth | Low Lakhs in Q1 2018 → nearly 4 Arabs by Q2 2021 |
| COVID-19 impact | Visible dip in 2020 Q2, followed by the fastest growth phase in the dataset |
| Top transaction states | Maharashtra, Karnataka, Telangana, Andhra Pradesh, Rajasthan |
| Dominant transaction type | Peer-to-Peer (P2P) across virtually all states and quarters |
| Leading device brand | Xiaomi — dominant in most states by registered user count |
| Highest user penetration | Maharashtra, Karnataka, Telangana |
| Biggest untapped markets | Uttar Pradesh, Bihar, Madhya Pradesh |
| Density vs transaction volume | Weak correlation — economic infrastructure matters far more than density |
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
Open the notebook and replace the hardcoded filepath at the top:
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
UP, Bihar, and MP have enormous populations but low digital payment adoption. Regional language support, simpler onboarding, and offline UPI features (UPI Lite) can open these markets meaningfully.

**2. The post-COVID momentum is a window — use it.**
The structural shift in payment behaviour post-2020 is not reversing. The opportunity now is converting app-active users into regular transactors, especially for merchant payments in Tier-2 and Tier-3 cities.

**3. Optimise for Xiaomi's ecosystem.**
Xiaomi users form the single largest user cohort across most states. MIUI-specific optimisations and pre-load partnerships would reach the widest audience at the lowest marginal cost.

**4. Build differently for high-ATV states.**
States with high average transaction values have a significant commercial user base. Features like instant settlement, GST-linked invoicing, and business dashboards would deepen platform dependency for these users.

**5. Don't plan expansion around density alone.**
Population density is a weak predictor of transaction volume. Expansion decisions should prioritise internet connectivity, banking infrastructure, and local merchant ecosystems — regardless of how densely a region is populated.

**6. Invest in north-eastern states and smaller union territories.**
Transaction volumes from these regions are low — but that's largely an infrastructure story, not a demand one. Targeted inclusion programs and simplified KYC can move the needle here over time.

---

## 🙌 Acknowledgements

- Data sourced from the **PhonePe Pulse open dataset** — one of the most detailed publicly available records of India's digital payment ecosystem
- Project completed as part of a Python Data Analysis curriculum at **Coding Ninjas**

---

## 📬 Connect

If you'd like to discuss the analysis, suggest improvements, or collaborate on a data project — feel free to reach out.

> ⭐ If this project was useful or interesting to you, a star on GitHub goes a long way — it helps others find it too.# 📱 PhonePe Pulse — Data Analysis Project
### Python | Pandas | NumPy | Matplotlib | Seaborn | Jupyter Notebook

> An end-to-end exploratory data analysis of PhonePe's transaction pulse data spanning Q1 2018 to Q2 2021 — covering 36 states, 700+ districts, and 14 quarters of India's digital payment revolution.

---

## 📌 What This Project Is About

India's shift to digital payments didn't happen in a straight line. There were periods of steady growth, a sudden pandemic-driven dip, and then an acceleration that caught everyone off guard. This project uses PhonePe's real pulse data to trace that journey — state by state, quarter by quarter — and understand what actually drove adoption, where the gaps still exist, and what the numbers suggest about where growth is headed.

This isn't just a collection of charts. Every analysis here was built from scratch — raw Excel sheets with messy formatting, columns that needed reconstruction, and datasets that had to be cross-verified before being trusted. The outcome is a clean, structured analysis that tells a coherent story about one of the most significant economic shifts in modern India.

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
> **Format:** Excel workbook with multiple sheets, wide-format date structures, inconsistent numeric formatting

---

## 🛠️ Tech Stack

| Tool | What It Was Used For |
|---|---|
| **Python 3.x** | Core language |
| **Pandas** | Data loading, cleaning, reshaping, merging, aggregation |
| **NumPy** | Numerical operations and edge case handling |
| **Matplotlib** | All visualisations — line plots, bar charts, scatter plots, pie charts |
| **Seaborn** | Color palettes and enhanced chart aesthetics |
| **Jupyter Notebook** | Interactive analysis and documentation |

---

## 🔍 What Was Analysed — Task by Task

### Task 1 — Data Loading and Understanding
Getting the data into a workable shape was the first real challenge. Each dataset came as a separate sheet inside an Excel workbook, and none of them were immediately ready for analysis. Date columns had to be reconstructed from separate Year and Quarter fields. Amount columns had embedded commas that broke numeric parsing. Some sheets had their actual header row buried inside the data rather than at the top.

Once cleaned, basic profiling was done across all five datasets — summary statistics, data type verification, and a thorough missing value audit. The data was then cross-verified between district and state levels to check internal consistency before any analysis began.

### Task 2 — Exploratory Data Analysis

**Transaction Trends Over Time**
Total transactions and amounts were aggregated by state and year to understand how volumes evolved over the 14-quarter period. The top 5 and bottom 5 states by transaction volume were identified — Maharashtra, Karnataka, Telangana, Andhra Pradesh, and Rajasthan led consistently, while smaller union territories and north-eastern states sat at the lower end.

**Most Common Transaction Types**
For each state and quarter, the dominant transaction type was identified. Peer-to-peer (P2P) transfers topped the list almost universally — which reflects how most people first engage with any digital payment platform. Merchant payments (P2M) showed consistent growth over time, particularly in commercially active states.

**Device Brand Analysis**
Xiaomi emerged as the dominant brand in terms of registered users across most Indian states — a direct reflection of its market share in the affordable smartphone segment. Samsung and Vivo were strong runners-up in multiple states, while premium brands appeared more prominently in wealthier geographies.

**District-Level Population Analysis**
For each state, the district with the highest population was identified. As expected, state capitals and primary commercial cities — Bengaluru Urban, Mumbai, Hyderabad — topped these lists. A column chart was built to visualise this distribution across all states.

**Average Transaction Value (ATV) by State**
ATV was computed for each state and the top 5 highest and bottom 5 lowest states were compared side by side. High transaction count doesn't always mean high transaction value — the two metrics paint different pictures of how a state's economy engages with digital payments.

**App Usage Trends**
App opens were tracked over time for each state. Maharashtra showed one of the steepest engagement curves. More interestingly, app opens didn't always scale proportionally with transactions — indicating users engage with the platform for balance checks, history viewing, and exploration beyond just transacting.

**Transaction Type Distribution (Most Recent Quarter)**
A subplot grid was built showing the distribution of transaction types for every state for the most recent quarter. Each state gets its own bar chart, making state-level comparisons easy at a glance.

**District Code Mapping**
A unique mapping between district names and their official census codes was extracted, verified, and exported as a clean CSV file for future reference or joining with external datasets.

### Task 3 — Data Quality Checks
District-level aggregates for transactions, amounts, and registered users were computed and directly compared against state-level figures. After applying a reasonable tolerance threshold, zero discrepancies were found — confirming the dataset is internally consistent and reliable for analysis.

### Task 4 — Merging and Advanced Analysis

**User-to-Population Ratio**
State-level registered users were merged with district demographics to calculate what percentage of each state's population is registered on PhonePe. High-population states like UP and Bihar showed significantly lower penetration ratios — pointing to the largest untapped opportunity in the entire dataset.

**Population Density vs Transaction Volume**
District-level density data was merged with transaction data and a correlation analysis was run. The correlation turned out to be weak — density alone doesn't predict transaction volume in any reliable way. A scatter plot confirmed this visually with widely scattered data points showing no clear trend.

**Average Transaction Amount Per User**
Total transaction amounts were divided by registered users at the state level to derive average spend per user. States with strong industrial and commercial economies showed the highest figures. Top 5 and bottom 5 were visualised together for direct comparison.

**Device Brand Usage Ratio**
The share of each device brand's users as a proportion of total registered users was calculated for every state. Subplot bar charts — one per state — were built showing brand-level usage ratios side by side.

### Task 5 — Visualisations

- **Dual-axis line plot** — Transactions and amount over time for any selected state, both metrics on the same chart with separate Y-axes
- **Pie chart** — Transaction type distribution for any selected state, year, and quarter — fully dynamic based on user input
- **Bar chart** — Population density of all districts within any selected state

### Task 6 — Insights and Conclusions

- Transaction trend analysis with written insights covering growth phases, the COVID dip, and post-pandemic acceleration
- Correlation analysis between population density and transaction volume with scatter plot and written summary
- Full project summary with findings, observations, and six actionable recommendations written as a structured analytical narrative

---

## ⚠️ Data Challenges and How They Were Handled

### Challenge 1 — Messy Amount Columns
The `Amount (INR)` and `ATV (INR)` columns had commas embedded within numeric values (e.g., `"1,23,456"`) causing Pandas to read them as strings. Direct arithmetic was impossible until they were cleaned.

**Fix:** `.str.replace(",", "")` followed by `pd.to_numeric()` with `errors='coerce'`, then cast to `Int64` to preserve nullable integer behaviour. Forward fill was applied where values were genuinely missing.

---

### Challenge 2 — Date Column Reconstruction
No dataset had a ready-to-use date column. Dates existed as two separate columns — `Year` and `Quarter` — which had to be combined into a single usable period representation.

**Fix:** `pd.to_datetime(Year.astype(str) + '-Q' + Quarter.astype(str))` followed by `.dt.to_period('Q').astype(str)` to create clean quarter labels like `2020Q1` that sort and filter correctly.

---

### Challenge 3 — Misaligned Headers in Some Sheets
Certain sheets had actual column names stored in the first data row rather than as the proper header, causing all columns to load with incorrect labels.

**Fix:** Used `header=1` to examine the structure, then applied `df.columns = df.iloc[0]` to promote the first row as headers, followed by `df.drop(0).reset_index(drop=True)` to remove the duplicate and restore a clean index.

---

### Challenge 4 — Missing District Codes
The `District_Txn and Users` dataset had missing values in the `Code` column for certain districts — likely due to unmatched entries or data collection gaps at source.

**Fix:** Missing codes were filled with the placeholder `"Unknown"` to preserve the rows for aggregation without introducing join errors downstream.

---

### Challenge 5 — Cross-Level Data Verification
Before trusting any merged analysis, district-level and state-level figures needed to be verified against each other. Inconsistencies here would carry forward into every downstream result.

**Fix:** Both levels were aggregated independently, merged with suffixed column names, and absolute differences were computed for transactions, amounts, and users. Any row exceeding a tolerance of 1 was flagged. Result: fully consistent — zero discrepancies found.

---

### Challenge 6 — Dynamic Subplot Grid
Building one chart per state required a grid that adjusts its size based on however many states exist — hardcoding row or column counts would break for any different dataset.

**Fix:** `(len(states) + 2) // 3` dynamically computes the number of rows needed for a 3-column grid. Remaining empty subplot panels after the main loop are hidden using `axes[j].set_visible(False)`, with `j` starting from the last value of `i` retained in memory after loop completion.

---

### Challenge 7 — Weak Correlation Between Density and Transactions
The hypothesis going in was that higher population density would correlate with higher transaction volume. The data disagreed — and that needed proper investigation rather than assumption.

**Fix:** District-level density was merged with transaction counts, `.corr()` was computed on numeric columns, and the relationship was validated visually with a scatter plot. The weak correlation was confirmed both statistically and visually — and documented honestly as a finding.

---

## 📊 Key Findings at a Glance

| What We Looked At | What We Found |
|---|---|
| Overall transaction growth | Low Lakhs in Q1 2018 → nearly 4 Arabs by Q2 2021 |
| COVID-19 impact | Visible dip in 2020 Q2, followed by the fastest growth phase in the dataset |
| Top transaction states | Maharashtra, Karnataka, Telangana, Andhra Pradesh, Rajasthan |
| Dominant transaction type | Peer-to-Peer (P2P) across virtually all states and quarters |
| Leading device brand | Xiaomi — dominant in most states by registered user count |
| Highest user penetration | Maharashtra, Karnataka, Telangana |
| Biggest untapped markets | Uttar Pradesh, Bihar, Madhya Pradesh |
| Density vs transaction volume | Weak correlation — economic infrastructure matters far more than density |
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
Open the notebook and replace the hardcoded filepath at the top:
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
UP, Bihar, and MP have enormous populations but low digital payment adoption. Regional language support, simpler onboarding, and offline UPI features (UPI Lite) can open these markets meaningfully.

**2. The post-COVID momentum is a window — use it.**
The structural shift in payment behaviour post-2020 is not reversing. The opportunity now is converting app-active users into regular transactors, especially for merchant payments in Tier-2 and Tier-3 cities.

**3. Optimise for Xiaomi's ecosystem.**
Xiaomi users form the single largest user cohort across most states. MIUI-specific optimisations and pre-load partnerships would reach the widest audience at the lowest marginal cost.

**4. Build differently for high-ATV states.**
States with high average transaction values have a significant commercial user base. Features like instant settlement, GST-linked invoicing, and business dashboards would deepen platform dependency for these users.

**5. Don't plan expansion around density alone.**
Population density is a weak predictor of transaction volume. Expansion decisions should prioritise internet connectivity, banking infrastructure, and local merchant ecosystems — regardless of how densely a region is populated.

**6. Invest in north-eastern states and smaller union territories.**
Transaction volumes from these regions are low — but that's largely an infrastructure story, not a demand one. Targeted inclusion programs and simplified KYC can move the needle here over time.

---

## 🙌 Acknowledgements

- Data sourced from the **PhonePe Pulse open dataset** — one of the most detailed publicly available records of India's digital payment ecosystem
- Project completed as part of a Python Data Analysis curriculum at **Coding Ninjas**

---

## 📬 Connect

If you'd like to discuss the analysis, suggest improvements, or collaborate on a data project — feel free to reach out.

> ⭐ If this project was useful or interesting to you, a star on GitHub goes a long way — it helps others find it too.
