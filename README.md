# 🚚 End-to-End Supply Chain Lead Time & Risk Analytics Pipeline

## 📌 Project Overview
This project transforms raw, unorganized supply chain telemetry into an automated operational analytics and machine learning pipeline using **Databricks**, **Delta Lake**, **Spark SQL**, and **Scikit-Learn**. 

By shifting focus from static averages to **lead time variance** and **predictive probability scoring**, this pipeline provides actionable visibility into shipping bottlenecks, high-risk routes, and late delivery probability.

---

## 🏗️ Architecture & Pipeline Stages

[ Raw CSV Telemetry ]
│
▼
[ 01_Data_Ingestion_and_Cleaning ] ➔ (Date Formatting, Schema Enforcement, Upserts)
│
▼
[ 02_Star_Schema_and_Analytics ]   ➔ (Delta Star Schema & SQL Lead Time Variance)
│
▼
[ 03_Feature_Export ]               ➔ (Sampled Dataset Materialization)
│
▼
[ 04_Predictive_Risk_Model ]        ➔ (Scikit-Learn Logistic Regression & Risk Scoring)


1. **Data Ingestion & Cleaning:** Standardized dates (`M/d/yyyy H:m`), repaired string encoding artifacts, and handled null values using Delta Lake tables.
2. **Relational Modeling (Star Schema):** Modeled flat files into normalized tables (`fact_orders`, `fact_shipments`, `dim_products`, `dim_locations`, `dim_customers`) connected via Primary/Foreign Keys.
3. **SQL Analytics Layer:** Evaluated SLA delivery rates and isolated high-variance routes using SQL window functions (`VAR_SAMP`, `RANK()`).
4. **Predictive Risk Engine:** Trained a Logistic Regression classifier predicting shipment delay risk based on market, region, category, and seasonality.

---

## 📊 Key Findings & Machine Learning Results

### Model Performance
* **Accuracy:** 70.40%
* **ROC-AUC Score:** 0.7573
* **Late Delivery Precision:** 81% *(High confidence when flagging late shipments to prevent false alarms)*

### Key Risk Drivers (Logistic Regression Coefficients)
* **High-Risk Destination Lanes:** Orders bound for **East of USA** (+1.00) and **Southern Africa** (+0.75) exhibit the highest systemic delay probability.
* **High-Risk Categories:** Product categories like **Soccer** (+0.78) and **DVDs** (+0.73) experience higher shipping volatility.
* **Reliability Buffers:** Standardized modes (**Standard Class**, **Same Day**) serve as strong negative risk indicators due to clear operational buffer schedules.

---

## 🛠️ Tech Stack
* **Storage & Compute:** Databricks Serverless, Delta Lake, PySpark
* **Data Modeling & Querying:** Spark SQL, Relational Star Schema Design
* **Machine Learning:** Scikit-Learn, Pandas, NumPy
