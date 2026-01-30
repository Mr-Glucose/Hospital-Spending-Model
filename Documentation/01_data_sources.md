# 📁 Data Sources

**Data Provider:** Centers for Medicare & Medicaid Services (CMS)  
**Source:** data.cms.gov (Hospital Compare)  
**Data Period:** January 1, 2023 – December 31, 2023

---

## 📊 Source Files

### File 1: Hospital General Information

**Filename:** `Hospital_General_Information.csv`

**Contains:** Hospital descriptive attributes
- Facility ID
- Facility Name  
- Location (City, State, ZIP)
- Hospital Type
- Hospital Ownership
- Emergency Services
- Hospital Overall Rating

**Data Type Note:** Facility ID stored as **TEXT** with leading zeros preserved

---

### File 2: Medicare Hospital Spending

**Filename:** `Medicare_Hospital_Spending_Per_Patient-Hospital.csv`

**Contains:** Medicare spending efficiency metrics
- Facility ID
- Facility Name (reference)
- Score (MSPB ratio)
- Start Date
- End Date

**Data Type Note:** Facility ID stored as **INTEGER** without leading zeros

---

## ⚠️ Integration Challenge

**Issue:** Different CMS backend systems export data in different formats

| Aspect | Hospital File | Spending File |
|--------|---------------|---------------|
| **System Origin** | Registration/Admin | Analytics/Calculation |
| **Facility ID Type** | TEXT | INTEGER |
| **Example** | `"100035"` | `100035` |
| **Leading Zeros** | Preserved | Stripped |

**Impact:** Files cannot be joined without standardization.

**Why this happens:** Different systems optimize for different purposes:
- Administrative systems preserve text formatting (legacy compatibility)
- Analytical systems use numeric types (calculation efficiency)

This is a **common integration challenge** when merging government datasets from different source systems.

---

## 📦 Dataset Scope

**Geographic:** 4 hospitals in Bradenton-Sarasota, FL (filtered from ~5,400 nationwide)

**Temporal:** Single year (CY 2023)

**Completeness:** 100% (all 4 hospitals have complete MSPB scores)

> 📌 **Note:** The full CMS dataset contains ~15% suppressed values due to privacy rules (< 11 discharges). Our filtered dataset happens to be 100% complete.

---

## 🔗 How Files Connect

```
Hospital_General_Information.csv
         ↓ (Facility ID)
    [Standardized in Power Query]
         ↓ (Both TEXT)
    [Relationship Created]
         ↑ (Facility ID)
Medicare_Hospital_Spending_Per_Patient-Hospital.csv
```

**Solution:** Both files standardized to TEXT format in Power Query before creating model relationship.

---

**Document Owner:** Arthur Dorvil  
**Last Updated:** January 2026  
**Previous:** `00_project_context.md` | **Next:** `02_modeling_decisions.md`
