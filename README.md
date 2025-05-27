# Cancer Hospitalizations and Multimorbidity Analysis in Chile (2019–2023)

This repository contains code used for the analysis of cancer-related hospitalization events and multimorbidity patterns among adult patients in Chile, based on data from the national FONASA Diagnosis-Related Groups (DRG) database (2019–2023).

## 📊 Overview

We analyze:
- ICD-10 based cancer classification across 13 tumor groups
- Frequency of hospitalizations by cancer type
- Multimorbidity patterns using 40+ chronic disease groups
- Stratification by age, sex, and diagnostic combinations

This analysis supports the manuscript:  
**“Multimorbidity patterns among cancer-related hospitalization events in younger and older patients: A large-scale nationwide database study”**

## 📁 Data

The data used originates from publicly available de-identified FONASA discharge records. Diagnosis codes are formatted in ICD-10.

- Main dataset: `data_2019_2023_edad.csv` (raw data compacted)
- Each row corresponds to a hospitalization event
- Diagnosis fields: `DIAGNOSTICO1` through `DIAGNOSTICO35`

> **Note**: You may access the original data from the [FONASA Tableau Portal](https://public.tableau.com/views/PropuestaTableroGRD/PropuestaTableroGRD?%3AshowVizHome=no#1).



## ⚙️ Code Structure

### 1. **Data Cleaning**
- Removes suffixes from `DIAGNOSTICO` fields (e.g., `.1`, `.2`)
- Creates a binary nationality variable
- Categorizes age into: `18_35`, `36_50`, and `51_o_mas`

### 2. **Cancer Classification**
- ICD-10 codes grouped into:
  - Digestive, Respiratory, Breast, Hematologic, etc.
- Flags binary presence of each cancer group
- Creates a `cancer` variable (`si` / `no`)
- Generates `tipo_cancer` (comma-separated list of tumor types per patient)

### 3. **Hospitalization Statistics**
- Filters adults (≥18 years)
- Computes mean and SD of hospitalizations per patient by cancer group

### 4. **Multimorbidity Construction**
- Defines 40+ chronic condition groups based on ICD-10
- Generates binary indicators for each
- Computes number of distinct comorbidities per patient
- Flags `multimorbilidad = 1` if patient has ≥2 chronic conditions

### 5. **Combination Encoding (Optional)**
- Uses `2^i` encoding for condition combinations
- Produces a `combinations` string per patient

## 🔍 Example Output Variables

| Variable             | Description                                 |
|----------------------|---------------------------------------------|
| `cancer`             | Binary indicator of any cancer (yes/no)     |
| `tipo_cancer`        | Comma-separated tumor groups                |
| `multimorbilidad`    | Binary: 1 if ≥2 chronic conditions          |
| `patologia_count`    | Total number of chronic condition groups    |
| `combinations`       | Encoded chronic condition profile           |

## 📦 Dependencies

- `dplyr` (data manipulation)
- Base R (≥ 3.6.0)

## 🧾 Citation

If you use or adapt this code, please cite:

> ----

## 📬 Contact

For questions or collaboration inquiries:  
**Yanara A. Bernal** – ybernalg@udd.cl


---
