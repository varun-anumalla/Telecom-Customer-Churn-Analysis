# 📊 Telecom Customer Churn Analysis

This project analyzes **customer churn behavior** for a telecom company using **Power BI, Excel, Power Query, and DAX**.  
The goal of this project is to help the business understand:

- **Why customers leave**
- **Who is more likely to churn**
- **Which customer segments are at risk**
- **What actions can reduce churn**

This is a complete end-to-end data analytics project — from data cleaning to dashboard building to insight generation.

---
## 📊 Dashboard – Page 1
<p align="center">
  <img src="https://github.com/varun-anumalla/Telecom-Customer-Churn-Analysis/blob/main/Dashboard-1%20Screenshot.png" alt="Telecom Customer Churn Dashboard Page 1" width="95%">
</p>

## 📈 Dashboard – Page 2 (Behavior & Insights)

<p align="center">
  <img src="https://github.com/varun-anumalla/Telecom-Customer-Churn-Analysis/blob/main/Dashboard-2%20Screenshot.png" alt="Telecom Customer Churn Dashboard Page 2" width="95%">
</p>

## 🎬 Project Walkthrough Video
[![Watch the full project walkthrough on YouTube](https://img.youtube.com/vi/I_jYbAE1lL0/0.jpg)](https://www.youtube.com/watch?v=I_jYbAE1lL0)

## 📌 1. Problem Statement

A telecom company is experiencing a high percentage of customer churn.  
The management wants to understand:

- What drives customers to leave?
- Which locations and demographics have the highest churn?
- How do bill amount, satisfaction score, and tenure influence churn?
- What actions can reduce churn and improve retention?

This project aims to build an **interactive Power BI dashboard** to answer these questions clearly.

---

## ❓ 2. Key Business Questions

The client wanted answers to these:

1. **Which customer age groups churn the most?**  
2. **What are the top reasons for churn?**  
3. **Which locations have the highest churn?**  
4. **How does churn vary across age groups, payment methods, and service types?**  
5. **What is the average tenure and satisfaction score of churned customers?**  
6. **Do prepaid or postpaid users churn more?**  
7. **Which payment channels are linked to higher churn?**  

---

## 📂 3. Dataset Description

The dataset contains nearly **6,000 rows** of data with the following columns:

- **CustomerID** — Unique customer identifier  
- **Churn_Status** — Yes / No  
- **Age_Group** — 18–25, 26–35, 36–50, 50+, Unknown  
- **Gender** — Male, Female, Other  
- **Telecom_Circle** — Customer location (state)  
- **Service_Type** — Prepaid / Postpaid  
- **Payment_Method** — UPI, Credit Card, Own App, Retail Store.
- **Monthly_Charges** — Monthly bill amount (numeric)  
- **Total_Charges** — Lifetime bill amount (numeric)  
- **Tenure_in_Months** — Months customer stayed (numeric)  
- **Customer_Satisfaction_Score** — 1–5 rating  
- **Churn_Reason** — Reason for leaving (if churned)

---

## 🧼 4. Data Cleaning (Excel + Power Query)

I cleaned the dataset using **Excel** and **Power Query**.  
Below are the steps I followed:

- Removed leading & trailing spaces using `TRIM()` / Power Query Trim + Clean  
- Handled missing values:
  - Payment_Method → filled with **UPI** (most common)
  - Age_Group → **Unknown**
  - Gender → **Other**
  - Customer_Satisfaction_Score → filled with **3**
  - Churn_Reason → filled with other reasons if not mrntioned
  - Telecom_Circle → ** if not mentioned Unknown**
  - Dependents → **No**
- Fixed numeric issues:
  - Removed `" Rs"` text from numeric columns
  - Converted Monthly_Charges, Total_Charges, Tenure_in_Months to numeric
  - Recalculated `Total_Charges = Monthly_Charges * Tenure_in_Months`
- Standardized categories for Service_Type, Payment_Method, Contract_Type
- Removed duplicates and invalid rows
- Loaded the final clean dataset into Power BI

---

## 🧮 5. DAX Measures Used

Below are the key DAX measures used in the Power BI report:

**Total Customers**
```dax
Total Customers = COUNTROWS('Telecom Data')
```

**Total Churned Customers**
```dax
Total Churned Customers =
CALCULATE(
  COUNTROWS('Telecom Data'),
  'Telecom Data'[Churn_Status] = "Yes"
)
```

**Churn Rate (%)**
```dax
Churn Rate = DIVIDE([Total Churned Customers], [Total Customers], 0)
```

**Avg Tenure of Churned Customers**
```dax
Avg Tenure of Churned Customers =
CALCULATE(
  AVERAGE('Telecom Data'[Tenure_in_Months]),
  'Telecom Data'[Churn_Status] = "Yes"
)
```

**Avg Monthly Charges of Churned Customers**
```dax
Avg Monthly Charges of Churned Customers =
CALCULATE(
  AVERAGE('Telecom Data'[Monthly_Charges]),
  'Telecom Data'[Churn_Status] = "Yes"
)
```

**Avg Satisfaction Score (Churned Only)**
```dax
Avg Satisfaction Score of Churned Customers =
CALCULATE(
  AVERAGE('Telecom Data'[Customer_Satisfaction_Score]),
  'Telecom Data'[Churn_Status] = "Yes"
)
```

---

## 📊 6. Dashboard Pages & Visuals

### Page 1 — Telecom Customer Churn Overview
Answers:
- What is the overall churn rate?
- Which locations have the most churn?
- Do certain age groups churn more?
- Which payment methods and service types show higher churn?

**Visuals:**
- KPI Cards: Total Customers, Total Churned, Churn Rate, Avg Monthly Charges, Avg Tenure  
- Donut: Churn Status breakdown  
- Bar: Churn by Telecom_Circle  
- Column: Churn by Age_Group  
- Bar: Churn by Payment_Method  
- Pie: Churn by Service_Type  
- Slicers: Telecom_Circle, Age_Group, Payment_Method, Service_Type

### Page 2 — Customer Behavior & Churn Insights
Explores reasons and behaviors driving churn.

**Visuals:**
- KPI Cards: Avg Tenure (Churned), Avg Satisfaction (Churned), Avg Monthly Charges (Churned)  
- Column: Tenure groups vs Churn count  
- Column: Customer_Satisfaction_Score vs Churn count  
- Column/Bar: Monthly_Charges bins vs Churn count  
- Bar: Churn_Reason (sorted by count)  
- Slicers: Telecom_Circle, Age_Group, Payment_Method, Service_Type

---

## 🔍 7. Key Insights

- **Churn Rate ≈ 20.6%** — Opportunity to improve retention.  
- **Age groups 26–35 and 36–50** show higher churn — target with retention offers.  
- **Top churn reasons:** Network Issues, High Price, Wrong Recharge Issues, Poor Customer Service, Competitor Offers.  
- **Certain circles (Gujarat, UP East, Delhi)** show higher churn — investigate network quality and competitor activity.  
- **Prepaid users** show different churn patterns than **postpaid**; target onboarding and first-month offers.  
- **UPI / Own App users churn more** than cash/retail-store users.  
- **Churned customers have lower avg satisfaction (~2.8)** and shorter tenure — focus on early engagement.

---

*Thank you for checking out my project. Feel free to reach out if you want collaboration.*
