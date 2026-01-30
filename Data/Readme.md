# 📁 Data

**Source:** CMS Hospital Compare (data.cms.gov)  
**Period:** January 1, 2023 – December 31, 2023

---

## Files

### Hospital_General_Information.csv
Hospital descriptive attributes for 4 hospitals in Bradenton-Sarasota, FL.

**Contains:**
- Facility ID (TEXT format)
- Hospital name, location, ownership
- Hospital type and ratings
- Emergency services indicator

---

### Medicare_Hospital_Spending_Per_Patient-Hospital.csv
Medicare Spending per Beneficiary (MSPB) scores for the same 4 hospitals.

**Contains:**
- Facility ID (INTEGER format)
- MSPB scores (efficiency ratio)
- Measurement period dates

---

## Data Quality Note

These files have **different Facility ID data types** (TEXT vs INTEGER), which is addressed during the Power Query transformation process.

See `/Documentation/03_data_quality_log.md` for details.

---

**Data License:** Public domain (CMS)

