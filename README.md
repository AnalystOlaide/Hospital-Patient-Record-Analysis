
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

#### **4. Visualization & Dashboard Development**  ![image](https://github.com/user-attachments/assets/ffb5f5ff-1c64-4e2a-9ef1-82ae3edb3b4d) ![image](https://github.com/user-attachments/assets/71240052-2b16-456d-92ab-608489bd1642)


✔ Designed **interactive reports** to highlight trends in:  
  - **Admissions & Readmissions**  
  - **Hospital Costs & Financial Insights**  
  - **Insurance Coverage**  
  - **Patient Demographics & Conditions**  
✔ Used **charts, tables, and KPIs** to provide clear data insights.  

---

## **5. Key Insights**  

### **1. Patient Admissions & Readmissions**  
📌 **Total Admissions:** **974 patients**  
📌 **Total Readmissions:** **854 patients**  
📌 **Average Length of Stay:** **0.30 days**  
📌 **Average Cost Per Visit:** **$3.64K**  

### **2. Insurance Coverage**  
📌 **Total Procedures Covered by Insurance:** **14K**  
📌 **Highest Payment Coverage:** **Medicare ($19M total payments)**  

### **3. Patient Demographics**  
📌 **Gender Distribution:**  
  - Male: **50.72%**  
  - Female: **49.28%**  

📌 **Age Distribution:**  
  - **85-104 years**: **Largest group (368 patients)**  
  - **25-44 years**: **Least represented (106 patients)**  

📌 **Race & Ethnicity:**  
  - **White:** **69.82%**  
  - **Black:** **16.74%**  
  - **Asian:** **9.34%**  
  - **Hispanic Population:** **19.61%**  

📌 **Marital Status:**  
  - **Married:** **80.49%**  
  - **Single:** **19.4%**  

📌 **Top Patient Locations:**  
  - **Boston** has the highest number of patients (**541**).  
  - Quincy, Cambridge, Revere, and Chelsea follow.  

### **4. Patient Encounters**  
📌 **Encounter Types:**  
  - **Ambulatory Visits:** **12.5K (Highest)**  
  - **Inpatient Admissions:** **1.1K (Lowest)**  

📌 **Most Common Encounter:** **"Encounter for problem procedure" (4.3K cases)**  

### **5. Medical Conditions & Diagnosis**  
📌 **Top Diagnosed Conditions:**  
  - **Chronic Conditions:** **1.7K cases**  
  - **Hyperlipidemia:** **1.6K cases**  
  - **Normal Pregnancy:** **1.3K cases**  

📌 **Least Reported Conditions:**  
  - **Sinusitis & Asthma:** **Only 100 cases each**  

📌 **Unknown Diagnoses:** **19.5K cases labeled as "Unknown"** → **Indicates poor data documentation**.  

---

## **6. Conclusion**  
📌 The hospital **primarily serves elderly, White, and non-Hispanic patients**, with most being married.  
📌 **Boston is the main patient hub**, followed by Quincy, Cambridge, and Revere.  
📌 **Ambulatory services dominate**, while inpatient admissions are the least frequent.  
📌 **Medicare is the top insurance provider** covering medical procedures.  
📌 **Unknown reason codes** suggest **inconsistent documentation of diagnoses**.  
📌 **Chronic conditions and hyperlipidemia** are among the most common diagnoses.  

---

## **7. Recommendations**  

📌 **1. Improve Data Documentation**  
- Reduce **"Unknown"** reason codes to enhance data quality and diagnosis tracking.  

📌 **2. Optimize Ambulatory Services**  
- Since **ambulatory visits dominate**, allocate more resources to **outpatient services**.  

📌 **3. Strengthen Financial Strategy**  
- With **Medicare covering the majority of payments**, **strategic partnerships** with government-backed insurance providers could improve revenue flow.  

📌 **4. Enhance Geriatric Care**  
- Given the **high number of elderly patients**, **invest in specialized geriatric units** for better care.  

📌 **5. Implement Community Health Initiatives**  
- Since most patients are in **Boston**, **targeted health campaigns** can reduce hospital visits through **preventive care programs**.  

---

## **Final Thoughts**  
This analysis provides **valuable insights** into patient demographics, hospital encounters, and financial trends. By leveraging Power BI, hospitals can enhance **decision-making, resource allocation, and patient care strategies**.  

