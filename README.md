# 🚗 Customer Segmentation Analytics
### Automobile Bike Company — RFM Model + K-Means Clustering

![Python](https://img.shields.io/badge/Python-3.11+-blue?style=flat-square&logo=python)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.4+-orange?style=flat-square&logo=scikit-learn)
![Pandas](https://img.shields.io/badge/Pandas-2.0+-green?style=flat-square&logo=pandas)
![Plotly](https://img.shields.io/badge/Plotly-Dash-purple?style=flat-square&logo=plotly)
![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)

> **Rebuilt & modernized in 2025** — originally inspired by a 2019 project. This version adds K-Means Clustering, automated EDA, an interactive Plotly Dash dashboard, and a clean modular codebase.

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Key Highlights](#-key-highlights)
- [Project Structure](#-project-structure)
- [Datasets Used](#-datasets-used)
- [Tech Stack](#-tech-stack)
- [Analysis Workflow](#-analysis-workflow)
- [RFM Segments](#-rfm-customer-segments)
- [Key Insights](#-key-insights)
- [Getting Started](#-getting-started)
- [Dashboard Preview](#-dashboard-preview)
- [Future Improvements](#-future-improvements)
- [Author](#-author)

---

## 📖 Project Overview

This project performs a full **Customer Segmentation Analysis** for an Automobile Bike Company operating across Australia. The goal is to identify distinct customer groups based on purchasing behavior, so the business can:

- 🎯 Target the right customers with the right campaigns
- 💰 Maximize sales revenue and reduce marketing waste
- 🔁 Improve customer retention and loyalty

Customer segmentation is done using the **RFM (Recency, Frequency, Monetary)** model — a proven, behavior-based approach that scores every customer on three dimensions:

| Dimension | Question It Answers |
|---|---|
| **Recency (R)** | How recently did the customer purchase? |
| **Frequency (F)** | How often do they purchase? |
| **Monetary (M)** | How much do they spend in total? |

On top of RFM scoring, **K-Means Clustering** is applied to validate segments and discover natural groupings in the data.

---

## ✨ Key Highlights

- ✅ Full **Data Quality Assessment (DQA)** across 4 datasets
- ✅ **RFM Model** — customers divided into **11 behavioral segments**
- ✅ **K-Means Clustering** with Elbow Method for optimal cluster selection
- ✅ **Automated EDA Report** using `ydata-profiling`
- ✅ **Interactive Dashboard** built with Plotly Dash (replaces Tableau)
- ✅ Modular, clean code structure — notebooks + Python scripts
- ✅ `requirements.txt` and `venv` setup ready to go

---

## 📁 Project Structure

```
customer-segmentation/
│
├── data/
│   ├── raw/                          # Original Excel files (unchanged)
│   │   ├── Transactions_data.xlsx
│   │   ├── NewCustomerList.xlsx
│   │   ├── CustomerDemographic.xlsx
│   │   └── CustomerAddress.xlsx
│   └── cleaned/                      # Cleaned CSVs after DQA
│       ├── Transactions_Cleaned.csv
│       ├── NewCustomerList_Cleaned.csv
│       ├── CustomerDemographic_Cleaned.csv
│       └── CustomerAddress_Cleaned.csv
│
├── notebooks/
│   ├── 01_DQA_CustomerDemographic.ipynb
│   ├── 02_DQA_NewCustomerList.ipynb
│   ├── 03_DQA_Transactions.ipynb
│   ├── 04_DQA_CustomerAddress.ipynb
│   └── 05_RFM_Analysis.ipynb
│
├── src/
│   ├── data_cleaning.py              # All DQA + cleaning functions
│   ├── rfm_model.py                  # RFM scoring logic
│   ├── clustering.py                 # K-Means + Elbow method
│   └── visualizations.py            # Reusable chart functions
│
├── dashboard/
│   └── app.py                        # Plotly Dash interactive dashboard
│
├── reports/
│   └── eda_report.html               # Auto-generated ydata-profiling report
│
├── requirements.txt
├── .gitignore
└── README.md
```

---

## 🗃️ Datasets Used

All datasets are from a single Excel file (`Raw_data.xlsx`) with the following sheets:

| Dataset | Description |
|---|---|
| `Transactions_data.xlsx` | Customer transaction history across all Australian states |
| `NewCustomerList.xlsx` | New customers who visited the company recently |
| `CustomerDemographic.xlsx` | Full customer demographic details |
| `CustomerAddress.xlsx` | Customer address and state information |

---

## 🛠️ Tech Stack

| Tool / Library | Purpose |
|---|---|
| **Python 3.11+** | Core language |
| **Pandas 2.0+** | Data manipulation & cleaning |
| **NumPy** | Numerical operations |
| **Matplotlib & Seaborn** | Static visualizations |
| **Plotly & Dash** | Interactive dashboard |
| **Scikit-learn** | K-Means Clustering, preprocessing |
| **ydata-profiling** | Automated EDA report generation |
| **Jupyter Notebook** | Exploratory analysis |

---

## 🔄 Analysis Workflow

### Step 1 — Data Quality Assessment & Cleaning

Each dataset was assessed for data quality issues and cleaned accordingly:

**CustomerDemographic.xlsx**
- Dropped 1 irrelevant column
- Imputed or dropped missing values across 5 columns
- Standardized the `gender` column (removed inconsistent entries like "F", "Femal", "Female")
- Extracted `Age` and `Age Group` from Date of Birth; removed 1 outlier record
- Confirmed no duplicate records

**NewCustomerList.xlsx**
- Dropped 5 irrelevant columns
- Handled missing values in 4 columns
- Extracted `Age` and `Age Group` features
- Confirmed no duplicate records

**Transactions_data.xlsx**
- Converted `product_first_sold_date` from `int64` to `datetime`
- Handled missing values across 7 columns
- Created a new `Profit` feature: `List Price − Standard Price`
- Confirmed no duplicate records

**CustomerAddress.xlsx**
- Standardized `state` column values (e.g., "New South Wales" vs "NSW")
- Identified and handled customer IDs missing from the demographics table

---

### Step 2 — Exploratory Data Analysis (EDA)

After cleaning, EDA revealed the following patterns:

**Age Distribution (New vs Old Customers)**
- Peak age group for both new and old customers: **40–49 years**
- Lowest customer count: under 20 and above 80 age groups
- Steep drop in the **30–39 age group** among new customers

**Bike Purchases by Gender (Last 3 Years)**
- Female buyers account for **~51%** of all purchases
- Female purchases exceed male by approximately **10,000 units**

**Job Industry Distribution**
- Top industries: **Manufacturing** and **Financial Services** (~20% each)
- Lowest: **Agriculture** and **Telecom** (~3% each)

**Wealth Segmentation**
- **Mass Customer** segment is the largest across all age groups
- **Affluent segment** outperforms High Net Worth in the 40–49 age group

**Car Ownership by State**
- New South Wales: highest proportion of customers without a car
- Queensland: majority of customers own a car

---

### Step 3 — RFM Analysis & Customer Segmentation

RFM scores are calculated as follows:

```python
rfm_table = df.groupby('customer_id').agg({
    'transaction_date': lambda x: (reference_date - x.max()).days,  # Recency
    'product_id': 'count',                                           # Frequency
    'Profit': 'sum'                                                  # Monetary
})

# Each metric is divided into 4 quartiles (Q1–Q4)
# RFM Score = 100*R_quartile + 10*F_quartile + M_quartile
```

### Step 4 — K-Means Clustering (New in 2025)

K-Means clustering is applied on top of RFM scores to validate segments:

```python
from sklearn.cluster import KMeans
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
rfm_scaled = scaler.fit_transform(rfm_table[['Recency', 'Frequency', 'Monetary']])

# Elbow method to find optimal k
inertia = [KMeans(n_clusters=k, random_state=42).fit(rfm_scaled).inertia_ for k in range(1, 11)]
```

---

## 🏷️ RFM Customer Segments

Customers are divided into **11 segments** based on their RFM score:

| Segment | Description | Strategy |
|---|---|---|
| 🏆 **Platinum Customers** | Highest RFM score — best customers | Reward, VIP programs |
| 💛 **Very Loyal Customers** | High frequency & monetary | Upsell & cross-sell |
| 🆕 **Recent Customers** | Purchased recently, low frequency | Nurture & engage |
| 🌱 **Potential Customers** | Moderate scores, good potential | Targeted offers |
| 💚 **Becoming Loyal** | Increasing purchase frequency | Loyalty programs |
| 🌸 **Late Bloomers** | Low recency but rising monetary | Re-engage campaigns |
| ⚠️ **Almost Lost** | Haven't purchased in a while | Urgent win-back |
| 🔴 **High Risk Customers** | Declining engagement | Discount campaigns |
| 😤 **Evasive Customers** | Low on all three metrics | Investigate & test |
| 📉 **Losing Customers** | Was active, now fading | Personalized outreach |
| ❌ **Lost Customers** | Lowest RFM score | Low priority / drop |

---

## 💡 Key Insights

**Recency vs Monetary**
> Recent customers have purchased more frequently and generated relatively higher revenue than those who visited a while ago.

**Frequency vs Monetary**
> Platinum, Very Loyal, and Becoming Loyal segments generate the highest monetary value for the business.

**Business Recommendation**
> Focus marketing budgets on **Platinum** and **Very Loyal** customers for upselling, while running targeted win-back campaigns for **High Risk** and **Almost Lost** segments.

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/customer-segmentation
cd customer-segmentation
```

### 2. Create Virtual Environment

```bash
python -m venv venv

# Windows
venv\Scripts\activate

# Mac / Linux
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Run Notebooks

```bash
jupyter notebook
```
Open notebooks in order from `01_DQA_CustomerDemographic.ipynb` to `05_RFM_Analysis.ipynb`.

### 5. Launch Dashboard

```bash
cd dashboard
python app.py
```

Open your browser at `http://127.0.0.1:8050`

---

## 📊 Dashboard Preview

The interactive Plotly Dash dashboard includes:

- 📌 Customer segment distribution (pie + bar charts)
- 📌 RFM scatter plots (Recency vs Monetary, Frequency vs Monetary)
- 📌 Age group & gender breakdowns
- 📌 State-wise customer map
- 📌 Segment filter to drill down into individual groups

---

## 🔮 Future Improvements

- [ ] Add **Customer Lifetime Value (CLV)** prediction using BG-NBD model
- [ ] Integrate **Cohort Analysis** for retention tracking
- [ ] Deploy dashboard on **Render / Railway** for public access
- [ ] Add **email campaign automation** trigger per segment
- [ ] Experiment with **DBSCAN** as an alternative to K-Means

---

## 📦 requirements.txt

```
pandas>=2.0
numpy
matplotlib
seaborn
scikit-learn
plotly
dash
ydata-profiling
jupyter
openpyxl
```

---

## 👤 Author

**Your Name**
- GitHub: [@yourusername](https://github.com/yourusername)
- LinkedIn: [linkedin.com/in/yourprofile](https://linkedin.com/in/yourprofile)

---

## 🙏 Acknowledgements

> Original project concept by [Abhishek Chowdhury](https://github.com/AbhishekGit-hash) (2019).
> This version is fully rebuilt and modernized for 2025 with updated tools, ML integration, and a new interactive dashboard.

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.