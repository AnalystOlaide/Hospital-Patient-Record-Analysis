
# **Hospital Patient Records Analysis Using Power BI**  

## **1. Project Overview**  
This project analyzes synthetic patient data from Massachusetts General Hospital (2011-2022) to uncover trends in:  
- Patient admissions and readmissions  
- Hospital stays and associated costs  
- Insurance coverage for medical procedures  
- Common medical conditions and diagnoses  

### **Dataset Overview**  
The dataset includes five key tables:  
- **Patients** – Demographic information (age, gender, ethnicity, marital status, etc.).  
- **Encounters** – Hospital visits, associated costs, and payer details.  
- **Procedures** – Medical procedures performed, along with costs and descriptions.  
- **Payers** – Insurance provider details.  
- **Organizations** – Information on hospitals/clinics.  

---

## **2. Problem Statement**  
Hospitals handle vast amounts of patient data, making it challenging to:  
✅ Identify trends in **admissions and readmissions**.  
✅ Assess the **average length of hospital stays**.  
✅ Optimize **financial strategies** through cost analysis.  
✅ Evaluate **insurance coverage** for medical procedures.  

A data-driven approach can **streamline hospital operations**, **improve patient outcomes**, and **enhance decision-making**.  

---

## **3. Data Source**  
The dataset was sourced from **Maven Analytics**, a platform for real-world analytics projects.  

---

## **4. Methodology**  

### **Tools Used**  
- **Power BI** – Data visualization and dashboard creation.  
- **Power Query** – Data cleaning and transformation.  
- **DAX (Data Analysis Expressions)** – Custom calculations and key performance indicators (KPIs).  

### **Data Processing Steps**  

#### **1. Data Cleaning & Transformation**  
✔ Handled missing values and duplicate records.  
✔ Standardized date formats for consistency.  
✔ Categorized records for better segmentation and insights.  

#### **2. Data Modeling**  ![image](https://github.com/user-attachments/assets/059e5890-dfc8-463e-ae34-99cccd1b7aad)

✔ Established relationships between **Patients, Encounters, Procedures, Payers, and Organizations** for seamless analysis.  

#### **3. DAX Calculations**  
✔ Created calculated columns and measures for key metrics, including:  
  - **Length of Stay**  Avg_Length_of_Stay = 
VAR TotalDays = SUMX(
    encounters, 
    DATEDIFF(encounters[Start], encounters[Stop], HOUR) / 24
)
VAR TotalEncounters = COUNT(encounters[Id])

RETURN DIVIDE(TotalDays, TotalEncounters, 0)
  - **Average Cost Per Visit**  Avg_Cost_Per_Visit = 
VAR TotalCost = SUM(encounters[TOTAL_CLAIM_COST]) 
VAR TotalVisits = COUNT(encounters[Id]) 

RETURN DIVIDE(TotalCost, TotalVisits, 0)
  - **Readmission Rates**  Total_Readmissions = 
VAR ReadmittedPatients = 
    SUMX (
        VALUES(encounters[Patient]),  
        IF ( 
            CALCULATE ( COUNT(encounters[Id]), ALLEXCEPT(encounters, encounters[Patient]) ) > 1, 
            1, 
            0 
        )
    )
RETURN
    ReadmittedPatients

  - **Patient Admission** Total_Readmissions = 
VAR ReadmittedPatients = 
    SUMX (
        VALUES(encounters[Patient]),  
        IF ( 
            CALCULATE ( COUNT(encounters[Id]), ALLEXCEPT(encounters, encounters[Patient]) ) > 1, 
            1, 
            0 
        )
    )
RETURN
    ReadmittedPatients

  - **Procedure Insurance Coverage** Procedure Insurance  coverage = CALCULATE(COUNT(encounters[Id]), encounters[PAYER_COVERAGE]>0)

#### **4. Visualization & Dashboard Development**

![image](https://github.com/user-attachments/assets/ffb5f5ff-1c64-4e2a-9ef1-82ae3edb3b4d) ![image](https://github.com/user-attachments/assets/71240052-2b16-456d-92ab-608489bd1642)


✔ Designed **interactive reports** to highlight trends in:  
  - **Admissions & Readmissions**  
  - **Hospital Costs & Financial Insights**  
  - **Insurance Coverage**  
  - **Patient Demographics & Conditions**  
✔ Used **charts, tables, and KPIs** to provide clear data insights.  

---

# Key Insights

## Admissions & Readmissions: High Readmission Burden with Minimal Stay

Out of **974 patients admitted**, a striking **854 were readmitted**, suggesting potential lapses in discharge planning or care continuity.  
Despite the high volume of patient flow, the **average length of stay was only 0.30 days**, indicating quick turnover or low-acuity admissions.  
Each visit, however, incurred an **average cost of $3.64K**, making even short stays financially significant.

## Insurance Coverage: Medicare Leads in Financial Responsibility

Out of **14,000 procedures covered by insurance**, **Medicare accounted for the highest total payments — $19M**.  
This highlights Medicare as a dominant payer in the system and a key contributor to revenue, underlining the importance of maintaining compliance and outcome quality for this segment.

## Patient Demographics: Aging Population, Concentrated Geography

The majority of patients were in the **85–104 age group (368 patients)**, while the **25–44 age group** represented the smallest segment (**106 patients**), showing a skew toward elderly care demand.  
**White patients comprised 69.82%** of the total, followed by **Black (16.74%)**, **Asian (9.34%)**, and **Hispanic (19.61%)** populations.  
Gender distribution was nearly even: **Male (50.72%)**, **Female (49.28%)**.  
**Married patients made up 80.49%**, which may reflect access to caregiver support or family-based care decisions.  
Geographically, **Boston alone contributed 541 patients**, significantly more than surrounding cities like Quincy, Cambridge, Revere, and Chelsea.

## Patient Encounters: Heavy Reliance on Outpatient Services

The healthcare system saw **12.5K ambulatory visits**, significantly higher than **1.1K inpatient admissions**, indicating that most care was delivered in an outpatient setting.  
The most frequent encounter was **"Encounter for problem procedure" (4.3K cases)** — suggesting recurring complications or issues related to previous interventions that required follow-up care.

## Diagnoses & Conditions: Prevalence of Chronic Illness, Documentation Gaps

**Chronic conditions (1.7K cases)** and **hyperlipidemia (1.6K)** were the most commonly reported health issues, reflecting ongoing demand for long-term management.  
**Normal pregnancy (1.3K)** also featured prominently, indicating consistent maternal care activity.  
At the lower end, **sinusitis and asthma** were among the least recorded, with just **100 cases each**.  
Notably, **19.5K diagnoses were labeled “Unknown”**, pointing to serious gaps in data capture and documentation, which can undermine decision-making, reporting accuracy, and operational planning.


# Key Insights

## Admissions & Readmissions: High Readmission Burden with Minimal Stay

Out of **974 patients admitted**, a striking **854 were readmitted**, suggesting potential lapses in discharge planning or care continuity.  
Despite the high volume of patient flow, the **average length of stay was only 0.30 days**, indicating quick turnover or low-acuity admissions.  
Each visit, however, incurred an **average cost of $3.64K**, making even short stays financially significant.

## Insurance Coverage: Medicare Leads in Financial Responsibility

Out of **14,000 procedures covered by insurance**, **Medicare accounted for the highest total payments — $19M**.  
This highlights Medicare as a dominant payer in the system and a key contributor to revenue, underlining the importance of maintaining compliance and outcome quality for this segment.

## Patient Demographics: Aging Population, Concentrated Geography

The majority of patients were in the **85–104 age group (368 patients)**, while the **25–44 age group** represented the smallest segment (**106 patients**), showing a skew toward elderly care demand.  
**White patients comprised 69.82%** of the total, followed by **Black (16.74%)**, **Asian (9.34%)**, and **Hispanic (19.61%)** populations.  
Gender distribution was nearly even: **Male (50.72%)**, **Female (49.28%)**.  
**Married patients made up 80.49%**, which may reflect access to caregiver support or family-based care decisions.  
Geographically, **Boston alone contributed 541 patients**, significantly more than surrounding cities like Quincy, Cambridge, Revere, and Chelsea.

## Patient Encounters: Heavy Reliance on Outpatient Services

The healthcare system saw **12.5K ambulatory visits**, significantly higher than **1.1K inpatient admissions**, indicating that most care was delivered in an outpatient setting.  
The most frequent encounter was **"Encounter for problem procedure" (4.3K cases)** — suggesting recurring complications or issues related to previous interventions that required follow-up care.

## Diagnoses & Conditions: Prevalence of Chronic Illness, Documentation Gaps

**Chronic conditions (1.7K cases)** and **hyperlipidemia (1.6K)** were the most commonly reported health issues, reflecting ongoing demand for long-term management.  
**Normal pregnancy (1.3K)** also featured prominently, indicating consistent maternal care activity.  
At the lower end, **sinusitis and asthma** were among the least recorded, with just **100 cases each**.  
Notably, **19.5K diagnoses were labeled “Unknown”**, pointing to serious gaps in data capture and documentation, which can undermine decision-making, reporting accuracy, and operational planning.
 

## **7. Conclusion**  
📌 The hospital **primarily serves elderly, White, and non-Hispanic patients**, with most being married.  
📌 **Boston is the main patient hub**, followed by Quincy, Cambridge, and Revere.  
📌 **Ambulatory services dominate**, while inpatient admissions are the least frequent.  
📌 **Medicare is the top insurance provider** covering medical procedures.  
📌 **Unknown reason codes** suggest **inconsistent documentation of diagnoses**.  
📌 **Chronic conditions and hyperlipidemia** are among the most common diagnoses.  


## **Final Thoughts**  
This analysis provides **valuable insights** into patient demographics, hospital encounters, and financial trends. By leveraging Power BI, hospitals can enhance **decision-making, resource allocation, and patient care strategies**.  

