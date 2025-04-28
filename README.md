# Loan Default Data Analysis Dashboard

### 📊 Dashboard Link
[View the Dashboard](https://app.powerbi.com/links/eUSAH4vojS?ctid=902549a3-b690-4dc6-b1fc-d8522ac75e80&pbi_source=linkShare)

---

## 🛠 Problem Statement

Financial institutions consistently face the challenge of minimizing loan default risks.  
This dashboard provides a comprehensive analysis of customer loan data to identify patterns associated with loan defaults based on demographics, credit profiles, employment types, and financial behavior.

By leveraging these insights, lenders can build more robust risk mitigation strategies and optimize their lending portfolio effectively.

---

## 🛤 Steps Followed

- Data ingestion from **Power BI Dataflows** into Power BI Desktop.
- Data cleansing and transformation using **Power Query Editor**, ensuring:
  - Handling of missing/null values.
  - Standardization of data types.
- Creation of critical **DAX measures and calculated columns** for:
  - Average Loan Amount
  - Default Rate by Occupation, Year, and Demographics
  - YOY Changes in Loan Amount and Default Counts
- Designing multiple report pages to focus on:
  - Loan Default Overview
  - Applicant Demographics and Financial Profile
  - Financial Risk Metrics
- Usage of slicers for dynamic filtering based on:
  - Home Ownership Status
  - Loan Grade
  - Occupation
- A professional corporate theme was applied to maintain a clean, business-oriented presentation.
- Dashboard was published to **Power BI Service** for online access and sharing.

---

## 📈 Insights Derived

- **Loan Amount Purpose:**  
  Business, Home, Auto, and Education loans have similar loan amount distributions, each around 6500M.

- **Employment Type Default Rates:**  
  Unemployed customers exhibit the highest default rate (~3.39%), followed by part-time employees.

- **Age Group Analysis:**  
  Loan default rates are almost consistent across different age groups, with slight variations.

- **Yearly Trend:**  
  - The overall default rate remained steady around 11.5% from 2013 to 2018.
  - YOY loan amount changes fluctuate, with slight negative growth in 2015 and 2017.

- **Demographics and Financial Profile:**  
  - Customers with **low and medium credit scores** contributed to the major loan volumes.
  - Education level affects loan distribution, with Bachelor's and High School graduates forming the majority.

- **Financial Risk Metrics:**  
  - Highest loan amount concentration observed among customers with **high incomes** and **full-time employment**.
  - YOY loan amount and default changes are minimal, indicating market stabilization.

---

## 📸 Dashboard Visuals

### Dashboard 1 - Loan Default and Overview

Analysis of loan amounts by purpose, average income by employment type, default rates by employment type, and yearly default trends.

![Image](https://github.com/user-attachments/assets/8ea408ad-9f3f-4ab7-9f38-bc019f9c5949)

---

### Dashboard 2 - Applicant Demographics and Financial Profile

Analysis of applicants based on credit scores, marital status, education type, age groups, and dependents.

![Image](https://github.com/user-attachments/assets/207aaafb-938f-4b21-9703-b0864f783ef5)

---

### Dashboard 3 - Financial Risk Metrics

Year-over-year changes in loan amounts and defaults, segmentation by income brackets and employment types.

![Image](https://github.com/user-attachments/assets/e65071b8-9127-48f9-b22d-48d4a331a6d0)

---

## 🧠 Key DAX Measures Used

1. **Average Loan Amount by Employment Type:**
    ```DAX
    AvgLoanAmount = AVERAGE(LoanData[LoanAmount])
    ```

2. **Default Rate by Employment Type:**
    ```DAX
    DefaultRate = 
    DIVIDE(
        CALCULATE(COUNTROWS(LoanData), LoanData[Loan_Status] = "Defaulted"),
        COUNTROWS(LoanData),
        0
    ) * 100
    ```

3. **YOY Loan Amount Change:**
    ```DAX
    YOYChangeLoanAmount = 
    VAR CurrentYearLoan = SUM(LoanData[LoanAmount])
    VAR LastYearLoan = CALCULATE(SUM(LoanData[LoanAmount]), DATEADD(LoanData[Date], -1, YEAR))
    RETURN
    DIVIDE((CurrentYearLoan - LastYearLoan), LastYearLoan)
    ```

4. **YOY Default Change:**
    ```DAX
    YOYChangeDefault = 
    VAR CurrentYearDefaults = CALCULATE(COUNTROWS(LoanData), LoanData[Loan_Status] = "Defaulted")
    VAR LastYearDefaults = CALCULATE(COUNTROWS(LoanData), LoanData[Loan_Status] = "Defaulted", DATEADD(LoanData[Date], -1, YEAR))
    RETURN
    DIVIDE((CurrentYearDefaults - LastYearDefaults), LastYearDefaults)
    ```



