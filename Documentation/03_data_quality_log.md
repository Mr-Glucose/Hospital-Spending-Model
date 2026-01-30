# Data Quality Issues Log

**Project:** CMS Hospital Spending, Messy Data Edition  
**Analyst:** Arthur Dorvil  
**Date:** January 29, 2026  
**Data Source:** CMS Hospital Compare (data.cms.gov)

---

## Overview

This document records data quality issues encountered while integrating
CMS Hospital Compare datasets into a Power BI data model.

Each issue includes:
- Business and technical impact
- Root cause analysis
- Resolution approach
- Validation steps

The goal is to ensure transparency, reproducibility, and trust in the
final model.

---

## Issue Summary

| Issue ID | Description | Severity | Status |
|--------|------------|----------|--------|
| DQ-001 | Facility ID data type and format mismatch | Critical | Resolved |
| DQ-002 | MSPB Score imported as text | High | Resolved |
| DQ-003 | Date fields imported as text | Medium | Resolved |

---

## Issue DQ-001: Facility ID Data Type and Format Mismatch

### Severity: Critical

**Impact:** Relationship could not be created  
**Status:** Resolved  
**Resolution Date:** January 29, 2026

---

### Problem Description

When attempting to create a relationship between `Hospital_Dim` and
`Medicare_Hospital_Spending_Fact` in Power BI Model View, the relationship
failed with zero matched rows.

Although Facility ID values appeared visually identical across both tables,
Power BI treated them as incompatible.

---

### Root Cause Analysis

The issue originated from inconsistent data typing across CMS datasets:

- **Hospital_General_Information.csv**
  - Facility ID stored as **text**
  - Leading zeros preserved

- **Medicare_Hospital_Spending_Per_Patient-Hospital.csv**
  - Facility ID stored as **integer**
  - Leading zeros removed

In Power BI, text `"100035"` and integer `100035` are not equivalent.
Relationships cannot be created between columns with mismatched data types.

This is a common integration issue when combining government datasets
exported from different backend systems.

---

### Business Impact

Without resolving this issue:
- No hospitals would join to spending records
- All MSPB scores would appear blank in visuals
- The dashboard would be non-functional

This was a **project-blocking issue**.

---

### Resolution

Facility ID values were standardized in **Power Query** before modeling.

Steps taken:
1. Converted Facility ID to text where necessary
2. Ensured consistent formatting across both tables
3. Verified that leading zeros were preserved
4. Confirmed both columns shared the same data type

No new columns were introduced; standardization was applied directly to
the existing Facility ID fields.

---

### Validation

- Relationship successfully created (One-to-Many)
- No orphaned records observed
- All hospitals displayed correct MSPB scores
- Filters propagated correctly from Hospital_Dim to the fact table

---

## Issue DQ-002: MSPB Score Imported as Text

### Severity: High

**Impact:** Calculations and aggregations would fail  
**Status:** Resolved  
**Resolution Date:** January 29, 2026

---

### Problem Description

The `Score` column in the Medicare spending dataset was imported as **text**
instead of a numeric data type.

As a result:
- Measures such as averages could not be calculated
- Sorting would behave alphabetically instead of numerically

---

### Root Cause Analysis

Power BI’s automatic type detection interpreted the values as text due to
the CSV source format and lack of explicit type metadata.

---

### Resolution

In Power Query:
1. Selected the `Score` column
2. Changed data type from **Text** to **Decimal Number**
3. Verified no conversion errors occurred

---

### Validation

- Column correctly displays decimal data type
- Aggregations compute as expected
- Sorting reflects numeric order

---

## Issue DQ-003: Date Fields Imported as Text

### Severity: Medium

**Impact:** Time-based analysis not possible  
**Status:** Resolved  
**Resolution Date:** January 29, 2026

---

### Problem Description

`Start Date` and `End Date` fields were imported as text instead of date values.

---

### Business Impact

Although the current project analyzes a single year of data, leaving dates
as text would prevent:
- Future time intelligence
- Proper sorting and filtering
- Model extensibility

---

### Resolution

In Power Query:
1. Selected `Start Date` and `End Date`
2. Changed data type to **Date**
3. Confirmed correct parsing

---

### Validation

- Date icons visible in Power Query
- Fields available for future time-based logic

---

## Data Quality Summary

| Severity | Count | Resolved |
|--------|-------|----------|
| Critical | 1 | 1 |
| High | 1 | 1 |
| Medium | 1 | 1 |
| **Total** | **3** | **3** |

**Overall Status:** All identified data quality issues resolved prior to
model deployment.

---

## Lessons Learned

- Visual similarity does not guarantee data compatibility
- Data types should be verified before creating relationships
- Government datasets frequently require preprocessing
- Resolving data quality upstream saves significant debugging time
- Clear documentation prevents repeat issues

---

## Production Considerations

In a production environment:
- Identifier standardization should occur in ETL pipelines
- Automated data quality checks should validate joins
- Data standards should be documented and enforced upstream

---

**Document Owner:** Arthur Dorvil  
**Last Updated:** January 29, 2026  
**Version:** 1.0
