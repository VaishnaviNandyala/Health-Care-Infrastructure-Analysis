# 🏥 Health Care Infrastructure Analysis

An end-to-end data analysis project on healthcare facilities in **Chhattisgarh (Bilaspur, Durg and Raipur districts)**, using data collected from the **Ayushman Bharat Digital Mission (ABDM)** Healthcare Facility Registry. The project covers data collection, cleaning, exploratory data analysis (EDA), a baseline regression model and an interactive dashboard.

---

## 📌 Objectives

- Understand the **mix of healthcare facilities** (hospitals, clinics, labs, dispensaries, etc.) across the districts.
- Analyse **infrastructure capacity**: beds and ventilators.
- Compare **Government vs Private** facilities.
- Measure **digital adoption** (ABDM-enabled facilities).
- Test whether **ventilator count can be predicted** from bed count, ownership and 24-hour availability.

---

## 📂 Repository Structure

| File | Description |
|---|---|
| `Hos_data.csv` | Raw dataset collected from the Ayushman Bharat facility registry |
| `Healthcare_Analysis.ipynb` | Cleaning, EDA, modelling and dashboard code |
| `healthcare_dashboard_hd.png` | Exported dashboard image |
| `Report.pdf` | Project report with findings |
| `Distribution_of_Hospitals` | Facility-type distribution chart |
| `System_of_medicine` | System-of-medicine distribution chart |

---

## 🗃️ Dataset

- **Source:** Ayushman Bharat (ABDM) Healthcare Facility Registry, collected manually by me
- **Size:** 99 records, 12 columns
- **Districts covered:** Bilaspur (55), Durg (32), Raipur (11)

| Column | Description |
|---|---|
| `Name` | Facility name |
| `District` | District of the facility |
| `ABDM_Enables` | Whether the facility is ABDM-enabled (True/False) |
| `Ownership` | Government / Private |
| `Facility_Type` | Hospital, Dental Clinic, Sub Centre, PHC, Pharmacy, etc. |
| `No_of_beds` | Number of beds |
| `Landline/mobile_phone` | Type of contact available |
| `No_of_Ventilators` | Number of ventilators |
| `System_of_Medicine` | Allopathy, Ayurveda, Homeopathy, Dentistry, etc. |
| `Address`, `Pincode` | Location details |
| `Open_24_hrs` | Whether the facility operates 24 hours |

---

## 🧹 Data Cleaning

- Standardised column names (stripped spaces, replaced with underscores, removed dots)
- Removed duplicate rows
- Replaced placeholders such as `NA`, `N/A`, `--` and `Not Available` with proper missing values
- Recoded the phone column (`2` → Landline/Mobile Phone, `mobile` → Mobile Phone)
- Converted `ABDM_Enables` and `Open_24_hrs` from Yes/No to boolean
- Converted beds and ventilators to numeric; filled missing ventilator counts with `0`
- Converted categorical columns to the `category` dtype and trimmed text fields

---

## 📊 Exploratory Data Analysis – Key Insights

- **Hospitals make up ~46%** of the records; the rest are clinics, dental clinics, sub centres, labs, pharmacies and Ayurveda/Homeopathy dispensaries.
- **Private facilities (69) outnumber Government facilities (27).**
- **Allopathy dominates**, with smaller shares for Ayurveda, Homeopathy and combined systems.
- **About 41% of facilities are ABDM-enabled.** Adoption is similar between Government and Private, with Government slightly ahead.
- **Beds and ventilators are positively correlated**, but many hospitals with 20–50 beds have **zero ventilators**, so bed capacity alone does not indicate critical-care readiness.
- **Capacity is highly concentrated**: AIIMS Raipur and Medical College Bilaspur hold most of the beds, and capacity drops sharply after the top few.
- **24-hour private hospitals** generally have more ventilators than non-24-hour ones.
- Facilities with both landline and mobile contact tend to be larger.

---

## 🤖 Model Building

**Goal:** Predict `No_of_Ventilators` from `No_of_beds`, `Ownership` and `Open_24_hrs`.

- Models: Linear Regression and Ridge Regression (scikit-learn)
- Data: only facilities with ventilators > 0 (19 rows), split 15 train / 4 test

| Model | R² | MAE | RMSE |
|---|---|---|---|
| Linear Regression | -2.044 | 3.235 | 3.489 |
| Ridge Regression | -3.717 | 2.643 | 4.344 |

**Takeaway:** Performance is poor because only 19 usable records remain after filtering. This is a baseline, not a reliable predictor. A larger dataset (more districts or states) and more features would be needed for a useful model.

---

## 📈 Dashboard

An interactive Plotly dashboard summarises:

- Districts covered, digitalization %, % open 24 hrs, highest bed capacity
- Top 10 facilities by bed capacity
- Beds vs ventilators
- Facility type distribution
- Bed distribution by contact availability

![Dashboard](healthcare_dashboard_hd.png)

---

## 🛠️ Tech Stack

Python · Pandas · NumPy · Matplotlib · Seaborn · Plotly · Scikit-learn · Jupyter Notebook

---

## ▶️ How to Run

```bash
git clone https://github.com/VaishnaviNandyala/Health-Care-Infrastructure-Analysis.git
cd Health-Care-Infrastructure-Analysis
pip install numpy pandas matplotlib seaborn plotly scikit-learn kaleido
jupyter notebook Healthcare_Analysis.ipynb
```

Make sure `Hos_data.csv` is in the same folder as the notebook.

---

## ⚠️ Limitations

- Small sample (99 facilities, 3 districts), so findings may not generalise to the whole state.
- Many missing values in beds, ventilators and phone fields.
- The model is trained on very few rows and should be treated as exploratory.

---

## 🚀 Future Work

- Collect data for more districts and states
- Add geospatial maps using pincodes/addresses
- Include population data to compute beds and ventilators per 1,000 people
- Try tree-based models once more data is available

---

## 👩‍💻 Author

**Nandyala Vaishnavi**
B.Tech, Data Science & Artificial Intelligence, IIT Bhilai
GitHub: [@VaishnaviNandyala](https://github.com/VaishnaviNandyala)
