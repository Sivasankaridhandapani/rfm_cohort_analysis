# RFM and Cohort Analysis: Customer Segmentation and Retention

## 1. Project Overview
This project segments customers using **RFM (Recency, Frequency, Monetary)** analysis and studies retention using **Cohort Analysis**. It helps a business understand customer value, purchase behaviour and retention patterns, and decide whom to target with loyalty, upsell or win-back campaigns.

## 2. Dataset Details
- **Source:** UCI Online Retail dataset (https://archive.ics.uci.edu/dataset/352/online+retail)
- **Size:** about 541,909 transactions, Dec 2010 to Dec 2011 (UK-based online gift retailer)
- **Columns:** InvoiceNo, StockCode, Description, Quantity, InvoiceDate, UnitPrice, CustomerID, Country

## 3. Data Preprocessing
| Issue | How it was handled |
|---|---|
| Missing `CustomerID` | Rows removed (purchases cannot be linked to a customer) |
| Duplicate rows | Removed with `drop_duplicates()` |
| Cancelled orders (InvoiceNo starts with `C`) | Removed |
| Quantity <= 0 or UnitPrice <= 0 | Removed (returns / adjustments / errors) |
| Wrong data types | `InvoiceDate` converted to datetime, `CustomerID` converted to int |
| Feature engineering | `TotalPrice = Quantity x UnitPrice` |

Row counts after each step are shown in the notebook (Step 3). *(Add your real numbers here.)*

## 4. RFM Methodology
- **Snapshot date:** last transaction date + 1 day
- **Recency:** days between snapshot date and the customer's last purchase
- **Frequency:** number of unique invoices
- **Monetary:** total spend (sum of TotalPrice)
- **Scoring:** each metric split into quintiles, scored 1 to 5 (5 is best; Recency labels reversed)
- **Segments** (from R and F scores): Champions, Loyal Customers, Potential Loyalists, New Customers, Promising, At Risk, Cannot Lose Them, About to Sleep, Lost

## 5. Cohort Analysis Methodology
1. **Cohort month** = month of the customer's first purchase
2. **Cohort index** = months since the first purchase (1 = acquisition month)
3. Count unique active customers per cohort and index
4. **Retention rate** = active customers in month N / cohort size
5. Visualised as a retention heatmap and retention curves

## 6. Results
*(Paste your real charts and numbers here. Charts are saved in `outputs/`.)*

- RFM segment summary: `outputs/rfm_segment_summary.csv`, chart `05_rfm_segments.png`
- Cohort retention table: `outputs/cohort_retention_table.csv`, chart `08_cohort_retention_heatmap.png`
- Retention curves: `09_retention_curves.png`

## 7. Business Insights and Recommendations
*(Replace the numbers with those from your notebook.)*
1. Champions are a small share of customers but generate a large share of revenue. Protect them with a loyalty programme and early access.
2. Many new customers do not return after month 1. Add a welcome series and a second-purchase offer in the first 30 days.
3. At Risk and Cannot Lose Them segments hold meaningful revenue. Run personalised win-back campaigns.
4. The Lost segment contributes little revenue. Use only low-cost reactivation.

## 8. How to Run
```bash
pip install -r requirements.txt
jupyter notebook rfm_cohort_analysis.ipynb
```
Run all cells from top to bottom. The dataset is downloaded automatically from UCI. If the download fails, download it manually and place the file in `data/`.

## 9. Project Structure
```
rfm-cohort-analysis/
├── data/                       (dataset)
├── outputs/                    (charts and CSV results)
├── rfm_cohort_analysis.ipynb   (full analysis)
├── requirements.txt
└── README.md
```
