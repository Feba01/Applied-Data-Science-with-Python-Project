**Marketing Campaign Analysis (Python • EDA • Hypothesis Testing)**

A practical, end-to-end exploratory data analysis project on a marketing campaign customer dataset. The goal is to **clean and prepare real-world customer data**, engineer useful features, explore relationships across demographics + purchase behavior, and **validate business hypotheses with statistical tests**.



**Repository Contents**
- **Notebook:** `Python for applied data science project_Marketing Campaign.ipynb` (main analysis)
- **Data (expected):** `marketing_data.csv` (place in the project root or update the path in the notebook)
- **Output (optional):** `updated_marketing_data_3.csv` (cleaned/encoded dataset export)



**Dataset Overview**
The dataset contains customer demographics, campaign responses, and multi-channel purchase behavior, including fields such as:
- **Customer profile:** `Year_Birth`, `Education`, `Marital_Status`, `Income`, `Country`
- **Household:** `Kidhome`, `Teenhome`
- **Spending by product:** `MntWines`, `MntFruits`, `MntMeatProducts`, `MntFishProducts`, `MntSweetProducts`, `MntGoldProds`
- **Purchases by channel:** `NumWebPurchases`, `NumCatalogPurchases`, `NumStorePurchases`
- **Campaign + service signals:** `AcceptedCmp1..5`, `Response`, `Complain`, `Recency`



**What I Did (Methodology)**
**1) Data loading**
- Imported `marketing_data.csv` into a Pandas DataFrame.

**2) Data cleaning + missing value handling**
- Cleaned categorical fields (e.g., fixing inconsistent labels / special characters).
- Addressed missing values in **Income** by imputing based on customers with similar **Education** and **Marital_Status** (group-based imputation).

**3) Feature engineering**
Created several analysis-ready features:
- **Age** derived from `Year_Birth`
- **Total_Children** = `Kidhome + Teenhome`
- **Total_Expenditure** = sum of all product spend columns (`Mnt*`)

**4) Distribution checks + outlier treatment**
- Used **boxplots** and **histograms** to understand distributions and detect outliers.
- Applied **IQR-based outlier treatment** (winsorizing to lower/upper bounds) to numeric features (excluding `Age` and `Total_Children`).

**5) Encoding for analysis**
- **Ordinal encoding** for `Education` with an explicit ranking: `Basic < Graduation < Master < PhD`
- **One-hot encoding** for nominal variables like `Marital_Status` and `Country`

**6) Correlation analysis**
- Computed **Spearman correlation** (appropriate when ordinal variables are present).
- Visualized correlations using a heatmap after removing identifiers and campaign/binary flags not intended for correlational analysis.

**7) Hypothesis testing (stats-driven insights)**
Used **t-tests** and **Kruskal–Wallis** to test behavioral hypotheses:

- **Hypothesis 1:** Older customers (Age ≥ 50) prefer shopping in-store  
  **Result:** t = 4.50, **p = 7.12e-06** → **Statistically significant difference** in store purchases.

- **Hypothesis 2:** Customers with kids prefer shopping online  
  **Result:** t = -3.54, **p = 0.000401** → **Statistically significant difference** in web purchases (direction indicated by negative t-stat).

- **Hypothesis 3:** Other channels cannibalize store sales (channel behavior differs)  
  **Result:** H = 1661.76, **p = 0.0** → **Strong evidence of differences** across channel purchase distributions.

- **Hypothesis 4:** US customers spend more than the rest of the world  
  **Result:** t = 0.308, **p = 0.758** → **Not statistically significant**.

**8) Visual analytics**
Created business-facing visualizations including:
- **Total revenue by product category**
- **Age vs. campaign acceptance (Response)**
- **Campaign acceptance by country**
- **Total expenditure vs. number of children**
- **Education background of customers who complained**



**Tech Stack**
- **Python**
- **Pandas / NumPy** (data wrangling)
- **Matplotlib / Seaborn** (visualization)
- **SciPy** (hypothesis testing)
- **scikit-learn** (encoding utilities)



**Key Takeaways**
- This project demonstrates an end-to-end workflow: **cleaning → feature engineering → outlier handling → encoding → correlation analysis → hypothesis testing → visualization**.
- The statistical testing section translates business questions into **testable hypotheses** and reports decisions using **p-values**.
- The final visuals support practical marketing insights across **products, channels, demographics, and geography**.

