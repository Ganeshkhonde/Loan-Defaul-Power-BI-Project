# Loan Default & Risk Analysis Dashboard

### Dashboard Link : (Add your Power BI Service link here)

## Problem Statement

This dashboard helps financial institutions understand loan distribution, customer demographics, and default risks. It provides insights into borrower behavior, helping identify high-risk segments and improve decision-making for loan approvals.

Through this dashboard, organizations can analyze how factors such as employment type, income, credit score, and demographics influence loan defaults. It also highlights trends in default rates over time, enabling better risk management strategies.

Since default rates vary significantly across employment types and years, financial institutions must focus on high-risk categories to reduce losses.

---

### Tools Used

- Power BI Desktop  
- Power Query Editor  
- DAX (Data Analysis Expressions)  
- Data Modeling  
- Data Visualization  

---

### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset contains loan and borrower details.
- Step 2 : Open Power Query Editor & enable "Column distribution", "Column quality" & "Column profile".
- Step 3 : Change profiling option to "based on entire dataset".
- Step 4 : Data cleaning was performed by handling null values in Loan Amount, Income, and Default columns.
- Step 5 : Created calculated columns such as Age Group and Credit Score Bins.
- Step 6 : Applied custom theme for dashboard design.
- Step 7 : Built visuals like line charts, area charts, donut charts, and bar charts.
- Step 8 : Added slicers for Employment Type, Income Bracket, and Credit Score Category.
- Step 9 : Created DAX measures for default rates, YOY changes, and aggregations.
- Step 10 : Designed report across three pages:
           (a) Loan Default & Overview
           (b) Applicant Demographics & Financial Profile
           (c) Financial Risk Metrics
- Step 11 : Published report to Power BI Service.

---

# Report Snapshot (Power BI DESKTOP)

### Page 1 : Loan Default & Overview
<img width="2395" height="1348" alt="Image" src="https://github.com/user-attachments/assets/e1287e98-9e60-468c-a896-dd4add6dc3a4" />

### Page 2 : Applicant Demographics & Financial Profile
<img width="2387" height="1346" alt="Image" src="https://github.com/user-attachments/assets/c23f73d9-e934-484a-bce1-b3bb4d610859" />

### Page 3 : Financial Risk Metrics
<img width="2400" height="1340" alt="Image" src="https://github.com/user-attachments/assets/c2cf5065-532b-4a86-a45a-4eed92176719" />

---

# DAX Measures

## Page 1 Measures

Average Income By Employment Type =  
CALCULATE(AVERAGE(Loan_default[Income]), ALLEXCEPT(Loan_default, Loan_default[EmploymentType]))

Default Rate by Year =  
VAR totalloans = CALCULATE(COUNTROWS(Loan_default), ALLEXCEPT(Loan_default, Loan_default[Year]))  
VAR default = CALCULATE(COUNTROWS(FILTER(Loan_default, Loan_default[Default]=TRUE())), ALLEXCEPT(Loan_default, Loan_default[Year]))  
RETURN DIVIDE(default, totalloans)*100

Default Rate by Employment Type =  
VAR totalrecords = COUNTROWS(ALL(Loan_default))  
VAR defaultrecords = COUNTROWS(FILTER(Loan_default, Loan_default[Default]=TRUE()))  
RETURN CALCULATE(DIVIDE(defaultrecords,totalrecords), ALLEXCEPT(Loan_default, Loan_default[EmploymentType]))*100

Loan Amount by Purpose =  
SUMX(FILTER(Loan_default, NOT(ISBLANK(Loan_default[LoanAmount]))), Loan_default[LoanAmount])

---

## Page 2 Measures

Count of Loans =  
COUNTROWS(FILTER(Loan_default, NOT(ISBLANK(Loan_default[LoanID]))))

Loan Amount (High Credit) =  
AVERAGEX(FILTER(Loan_default, Loan_default[Credit Score Bins]="High"), Loan_default[LoanAmount])

Median Loan Amount =  
MEDIAN(Loan_default[LoanAmount])

Total Amount (Middle Age Adults) =  
CALCULATE(SUM(Loan_default[LoanAmount]), Loan_default[Age Group]="Middle Age Adults")

Total Loan Amount (Adults) =  
CALCULATE(SUM(Loan_default[LoanAmount]), Loan_default[Age Group]="Adults")

---

## Page 3 Measures

YOY Default Loans Change =  
DIVIDE(  
CALCULATE(COUNTROWS(FILTER(Loan_default, Loan_default[Default]=TRUE())), Loan_default[Year]=YEAR(MAX(Loan_default[Loan Date])))  
-  
CALCULATE(COUNTROWS(FILTER(Loan_default, Loan_default[Default]=TRUE())), Loan_default[Year]=YEAR(MAX(Loan_default[Loan Date]))-1),  
CALCULATE(COUNTROWS(FILTER(Loan_default, Loan_default[Default]=TRUE())), Loan_default[Year]=YEAR(MAX(Loan_default[Loan Date]))-1),0)*100

YOY Loan Amount Change =  
DIVIDE(  
CALCULATE(SUM(Loan_default[LoanAmount]), Loan_default[Year]=YEAR(MAX(Loan_default[Loan Date])))  
-  
CALCULATE(SUM(Loan_default[LoanAmount]), Loan_default[Year]=YEAR(MAX(Loan_default[Loan Date]))-1),  
CALCULATE(SUM(Loan_default[LoanAmount]), Loan_default[Year]=YEAR(MAX(Loan_default[Loan Date]))-1),0)*100

YTD Loan Amount =  
CALCULATE(SUM(Loan_default[LoanAmount]), DATESYTD(Loan_default[Loan Date].[Date]), ALLEXCEPT(Loan_default, Loan_default[Credit Score Bins], Loan_default[MaritalStatus]))

---

# Insights

A multi-page report was created on Power BI Desktop & published to Power BI Service.

### [1] Loan Distribution

Loan amount is highest for Home loans followed by Business and Education.  
thus, majority of lending is concentrated in housing sector.

---

### [2] Default Rate Analysis

Default rate is highest among Unemployed individuals.  
Full-time employees show lowest default rate.  
thus, employment stability plays a major role.

---

### [3] Income & Risk

Higher income groups show better repayment behavior.  
Lower income groups have higher default probability.  

---

### [4] Credit Score Impact

Lower credit score segments show higher risk exposure.  
thus, credit score is a key financial indicator.

---

### [5] Demographics

Adults and Middle Age Adults dominate loan distribution.  

---

### [6] Yearly Trends

Default rates fluctuate significantly across years.  
thus, financial risk is dynamic and time-dependent.

---

# Conclusion

This dashboard provides a comprehensive analysis of loan behavior, customer segmentation, and financial risk. It enables better decision-making for loan approvals and risk mitigation strategies.


