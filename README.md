# 🏥 Hospital Medicare Spending Model

**A focused Power BI data modeling case study using real CMS Hospital Compare data**

[![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![CMS Data](https://img.shields.io/badge/CMS-Hospital%20Compare-0078D4)](https://data.cms.gov)

**Analyst:** Arthur Dorvil | **Date:** January 2026

---

## 🎯 Overview

Demonstrates professional **data integration and quality management** using actual CMS Hospital Compare data for 4 hospitals in Bradenton-Sarasota, Florida.

**Key Achievement:** Resolved critical Facility ID format mismatch between CMS source files.

---

## 📊 Dashboard

![Hospital Medicare Spending Dashboard](dashboard.jpg)

**Analysis Results:**

| Hospital | MSPB | vs National Avg |
|----------|------|-----------------|
| Lakewood Ranch Medical Center | **1.10** | +10% ⬆️ |
| HCA Florida Blake Hospital | 1.06 | +6% |
| Manatee Memorial Hospital | 1.04 | +4% |
| Sarasota Memorial Hospital | 1.03 | +3% |

**Finding:** All hospitals exceed national average Medicare spending (1.00).

---

## 🔧 Technical Challenge

### The Problem

CMS source files had incompatible Facility ID data types:

| File | Data Type | Example |
|------|-----------|---------|
| Hospital_General_Information.csv | TEXT | `"100035"` |
| Medicare_Hospital_Spending.csv | INTEGER | `100035` |

**Impact:** 0% match rate → relationship creation failed.

---

### The Solution

```mermaid
flowchart LR
    A[Type Mismatch] -->|Power Query| B[Standardized to TEXT]
    B --> C[100% Match Rate]
    
    style A fill:#ff6b6b,color:#fff
    style B fill:#4ecdc4
    style C fill:#95e1d3
```

**Standardized both to TEXT in Power Query** → All 4 hospitals successfully joined.

---

## 🏗️ Data Model

**Star schema design:**

```mermaid
erDiagram
    HOSPITAL_DIM ||--o{ SPENDING_FACT : "one-to-many"
    
    HOSPITAL_DIM {
        text Facility_ID PK
        text Facility_Name
        text Hospital_Ownership
        int Hospital_Overall_Rating
    }
    
    SPENDING_FACT {
        text Facility_ID FK
        decimal Score
        date Start_Date
        date End_Date
    }
```

**Relationship Configuration:**
- **Key Column:** `Facility ID` (standardized TEXT in both tables)
- **Cardinality:** One-to-Many (1:*)
- **Direction:** Single (Hospital → Spending)
- **Status:** Active

---

## 📐 DAX Measures

```dax
Hospital Count = DISTINCTCOUNT(Hospital_Dim[Facility ID])

Avg Spending Score = AVERAGE(Spending_Fact[Score])

Max Spending Score = MAX(Spending_Fact[Score])

Data Completeness % = 
DIVIDE(
    CALCULATE([Hospital Count], NOT(ISBLANK(Spending_Fact[Score]))),
    [Hospital Count], 1
)
```

---

## ✅ Validation

**All tests passed:**

| Test | Status |
|------|--------|
| Relationship integrity (0 orphaned records) | ✅ |
| Cardinality (1:* enforced) | ✅ |
| Filter propagation (slicers working) | ✅ |
| Measure accuracy (all correct) | ✅ |
| Data completeness (100%) | ✅ |

**Result:** Model validated and production-ready.

---

## 📂 Repository Structure

```
Hospital-Spending-Model/
├── README.md                          ← You are here
├── LICENSE
├── Data/
│   ├── Hospital_General_Information.csv
│   └── Medicare_Hospital_Spending_Per_Patient-Hospital.csv
├── Documentation/
│   ├── readme.md                      ← Documentation guide
│   ├── 00_project_context.md         ← MSPB explained
│   ├── 01_data_sources.md            ← CMS data details
│   ├── 02_modeling_decisions.md      ← Star schema rationale
│   ├── 03_data_quality_log.md        ← Issue resolution
│   └── 04_validation_checks.md       ← Testing evidence
└── Power BI/
    ├── Thinking Demo.pbix             ← Data model + dashboard
    └── Thinking Demo.pdf              ← Dashboard export
```

---

## 🎯 Skills Demonstrated

**Technical Capabilities:**

| Category | Skills |
|----------|--------|
| **Data Integration** | Format standardization • Type conversion • Cross-system joins |
| **Data Modeling** | Star schema • Relationships • Cardinality |
| **Quality Assurance** | Issue resolution • Validation • Documentation |

**Technical:**
- Power Query transformations
- Dimensional modeling (star schema)
- DAX measure development
- Relationship configuration
- Data validation

**Professional:**
- Root cause analysis
- Systematic problem-solving
- Technical documentation
- Production thinking

---

## 🚀 Production Recommendations

| Current Approach | Production Approach |
|------------------|---------------------|
| Power Query fix | ETL pipeline (upstream) |
| Manual validation | Automated quality checks |
| In-memory model | DirectQuery/Composite |
| Full refresh | Incremental refresh |

---

## 📚 Documentation

Full technical documentation in `/Documentation`:

- **Project Context** - MSPB metric explained
- **Data Sources** - CMS file details and challenges
- **Modeling Decisions** - Star schema rationale
- **Data Quality Log** - Issue resolution process
- **Validation Checks** - Testing evidence

---

## 🎓 Why This Matters

This project shows the **technical foundation** that makes reliable analytics possible:

✓ Real-world data quality challenges  
✓ Systematic problem-solving  
✓ Professional documentation  
✓ Production-ready thinking

**Previous work** showed polished dashboards.  
**This project** shows the data modeling that makes them trustworthy.

---

**Data Source:** CMS Hospital Compare (public domain)  
**Period:** January 1, 2023 – December 31, 2023  
**Status:** ✅ Validated and production-ready
    B -->|Star Schema| C[Validated<br/>Model]
    
    style A fill:#ff6b6b,color:#fff
    style B fill:#4ecdc4
    style C fill:#95e1d3
```

**Key Achievement:** Resolved critical Facility ID format mismatch between CMS source files.

---

## 📊 Analysis Results

**Medicare Spending per Beneficiary (MSPB)** for 4 regional hospitals:

```mermaid
%%{init: {'theme':'base'}}%%
graph LR
    A[National<br/>Average<br/>1.00] 
    B[Lakewood<br/>Ranch<br/>1.10]
    C[HCA<br/>Blake<br/>1.06]
    D[Manatee<br/>Memorial<br/>1.04]
    E[Sarasota<br/>Memorial<br/>1.03]
    
    style A fill:#e0e0e0
    style B fill:#ffcccb
    style C fill:#ffe4b5
    style D fill:#fff8dc
    style E fill:#e0ffe0
```

| Hospital | MSPB | vs National Avg |
|----------|------|-----------------|
| Lakewood Ranch Medical Center | **1.10** | +10% ⬆️ |
| HCA Florida Blake Hospital | 1.06 | +6% |
| Manatee Memorial Hospital | 1.04 | +4% |
| Sarasota Memorial Hospital | 1.03 | +3% |

**Finding:** All hospitals exceed national average Medicare spending.

---

## 🔧 Technical Challenge

### The Problem

```mermaid
sequenceDiagram
    participant PBI as Power BI
    participant H as Hospital File
    participant S as Spending File
    
    PBI->>H: Read Facility ID
    H-->>PBI: TEXT "100035"
    PBI->>S: Read Facility ID
    S-->>PBI: INTEGER 100035
    PBI-->>PBI: ❌ Type mismatch<br/>Cannot create relationship
```

**Source file incompatibility:**
- `Hospital_General_Information.csv` → TEXT with leading zeros
- `Medicare_Hospital_Spending_Per_Patient-Hospital.csv` → INTEGER without leading zeros

**Impact:** 0% match rate → relationship creation failed.

---

### The Solution

**Standardized both to TEXT in Power Query:**

```mermaid
flowchart TD
    A[Load Both Files] --> B{Types<br/>Match?}
    B -->|No| C[Convert to TEXT]
    C --> D[Preserve Leading Zeros]
    D --> E[✓ 100% Match Rate]
    
    style B fill:#ffd93d
    style E fill:#6bcf7f
```

**Result:** All 4 hospitals successfully joined via One-to-Many relationship.

---

## 🏗️ Data Model

**Star schema design:**

```mermaid
erDiagram
    HOSPITAL_DIM ||--o{ SPENDING_FACT : "one-to-many"
    
    HOSPITAL_DIM {
        text Facility_ID PK
        text Facility_Name
        text Hospital_Ownership
        int Hospital_Overall_Rating
    }
    
    SPENDING_FACT {
        text Facility_ID FK
        decimal Score
        date Start_Date
        date End_Date
    }
```

**Relationship Configuration:**
- **Key Column:** `Facility ID` (standardized TEXT in both tables)
- **Cardinality:** One-to-Many (1:*)
- **Direction:** Single (Hospital → Spending)
- **Status:** Active

---

## 📐 DAX Measures

```dax
Hospital Count = DISTINCTCOUNT(Hospital_Dim[Facility ID])

Avg Spending Score = AVERAGE(Spending_Fact[Score])

Max Spending Score = MAX(Spending_Fact[Score])

Data Completeness % = 
DIVIDE(
    CALCULATE([Hospital Count], NOT(ISBLANK(Spending_Fact[Score]))),
    [Hospital Count], 1
)
```

---

## ✅ Validation

```mermaid
%%{init: {'theme':'base'}}%%
pie title "Validation Results"
    "Passed" : 5
    "Failed" : 0
```

**Confirmed:**
- ✅ Relationship integrity (0 orphaned records)
- ✅ Cardinality (1:* enforced)
- ✅ Filter propagation (slicers working)
- ✅ Measure accuracy (all correct)
- ✅ Data completeness (100%)

---

## 📂 Repository Structure

```
Hospital-Spending-Model/
├── README.md                          ← You are here
├── LICENSE
├── Data/
│   ├── Hospital_General_Information.csv
│   └── Medicare_Hospital_Spending_Per_Patient-Hospital.csv
├── Documentation/
│   ├── readme.md                      ← Documentation guide
│   ├── 00_project_context.md         ← MSPB explained
│   ├── 01_data_sources.md            ← CMS data details
│   ├── 02_modeling_decisions.md      ← Star schema rationale
│   ├── 03_data_quality_log.md        ← Issue resolution
│   └── 04_validation_checks.md       ← Testing evidence
└── Power BI/
    ├── Thinking Demo.pbix             ← Data model + dashboard
    └── Thinking Demo.pdf              ← Dashboard export
```

---

## 🎯 Skills Demonstrated

**Technical Capabilities:**

| Category | Skills |
|----------|--------|
| **Data Integration** | Format standardization • Type conversion • Cross-system joins |
| **Data Modeling** | Star schema • Relationships • Cardinality |
| **Quality Assurance** | Issue resolution • Validation • Documentation |

**Technical:**
- Power Query transformations
- Dimensional modeling (star schema)
- DAX measure development
- Relationship configuration
- Data validation

**Professional:**
- Root cause analysis
- Systematic problem-solving
- Technical documentation
- Production thinking

---

## 🚀 Production Recommendations

| Current Approach | Production Approach |
|------------------|---------------------|
| Power Query fix | ETL pipeline (upstream) |
| Manual validation | Automated quality checks |
| In-memory model | DirectQuery/Composite |
| Full refresh | Incremental refresh |

---

## 📚 Documentation

Full technical documentation in `/Documentation`:

- **Project Context** - MSPB metric explained
- **Data Sources** - CMS file details and challenges
- **Modeling Decisions** - Star schema rationale
- **Data Quality Log** - Issue resolution process
- **Validation Checks** - Testing evidence

---

## 🎓 Why This Matters

This project shows the **technical foundation** that makes reliable analytics possible:

✓ Real-world data quality challenges  
✓ Systematic problem-solving  
✓ Professional documentation  
✓ Production-ready thinking

**Previous work** showed polished dashboards.  
**This project** shows the data modeling that makes them trustworthy.

---

**Data Source:** CMS Hospital Compare (public domain)  
**Period:** January 1, 2023 – December 31, 2023  
**Status:** ✅ Validated and production-ready
