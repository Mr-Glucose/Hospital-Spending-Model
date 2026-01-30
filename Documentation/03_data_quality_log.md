# 🔍 Data Quality Issues Log

**Project:** Hospital Medicare Spending Analysis  
**Analyst:** Arthur Dorvil  
**Date:** January 29, 2026  
**Data Source:** CMS Hospital Compare (data.cms.gov)

---

## 📋 Overview

This document records data quality issues encountered while integrating CMS Hospital Compare datasets into a Power BI data model.

**Each issue includes:**
- Business and technical impact
- Root cause analysis
- Resolution approach
- Validation steps

**Goal:** Ensure transparency, reproducibility, and trust in the final model.

---

## 📊 Issue Summary

| Issue ID | Description | Severity | Status |
|----------|-------------|----------|--------|
| DQ-001 | Facility ID type mismatch | 🔴 Critical | ✅ Resolved |
| DQ-002 | MSPB Score imported as text | 🟡 High | ✅ Resolved |
| DQ-003 | Date fields imported as text | 🟢 Medium | ✅ Resolved |

**Total:** 3 issues, 3 resolved (100%)

---

## 🚨 Issue DQ-001: Facility ID Type Mismatch

### Severity: 🔴 Critical

**Impact:** Relationship could not be created  
**Status:** ✅ Resolved  
**Resolution Date:** January 29, 2026

---

### Problem Description

When attempting to create a relationship between `Hospital_Dim` and `Medicare_Hospital_Spending_Fact` in Power BI Model View, the relationship **failed with zero matched rows**.

Although Facility ID values appeared visually identical across both tables, Power BI treated them as incompatible.

---

### Root Cause

**Inconsistent data typing across CMS datasets:**

| File | Data Type | Format | Example |
|------|-----------|--------|---------|
| Hospital_General_Information.csv | TEXT | With leading zeros | `"100035"` |
| Medicare_Hospital_Spending.csv | INTEGER | No leading zeros | `100035` |

**Why?** In Power BI, text `"100035"` ≠ integer `100035`

Relationships cannot be created between columns with mismatched data types.

**Common cause:** Government datasets exported from different backend systems that don't share consistent schemas.

---

### Business Impact

**Without resolution:**
- ❌ No hospitals would join to spending records
- ❌ All MSPB scores would appear blank in visuals
- ❌ Dashboard would be non-functional

**This was a project-blocking issue.**

---

### Resolution

Facility ID values were **standardized in Power Query** before modeling.

**Steps taken:**
1. Converted Facility ID to text where necessary
2. Ensured consistent formatting across both tables
3. Verified that leading zeros were preserved
4. Confirmed both columns shared the same data type

**Implementation:** No new columns were introduced; standardization was applied directly to existing Facility ID fields.

---

### Validation

✅ Relationship successfully created (One-to-Many)  
✅ No orphaned records observed (4/4 hospitals matched)  
✅ All hospitals displayed correct MSPB scores  
✅ Filters propagated correctly from Hospital_Dim to fact table

---

## 🟡 Issue DQ-002: MSPB Score Imported as Text

### Severity: 🟡 High

**Impact:** Calculations and aggregations would fail  
**Status:** ✅ Resolved  
**Resolution Date:** January 29, 2026

---

### Problem Description

The `Score` column in the Medicare spending dataset was imported as **text** instead of a numeric data type.

**Consequences:**
- ❌ Measures such as averages could not be calculated
- ❌ Sorting would behave alphabetically instead of numerically

---

### Root Cause

Power BI's automatic type detection interpreted the values as text due to CSV source format and lack of explicit type metadata.

---

### Resolution

**In Power Query:**
1. Selected the `Score` column
2. Changed data type from **Text** to **Decimal Number**
3. Verified no conversion errors occurred

---

### Validation

✅ Column correctly displays decimal data type  
✅ Aggregations compute as expected  
✅ Sorting reflects numeric order

---

## 🟢 Issue DQ-003: Date Fields Imported as Text

### Severity: 🟢 Medium

**Impact:** Time-based analysis not possible  
**Status:** ✅ Resolved  
**Resolution Date:** January 29, 2026

---

### Problem Description

`Start Date` and `End Date` fields were imported as **text** instead of date values.

---

### Business Impact

Although the current project analyzes a single year of data, leaving dates as text would prevent:
- ❌ Future time intelligence
- ❌ Proper sorting and filtering
- ❌ Model extensibility

---

### Resolution

**In Power Query:**
1. Selected `Start Date` and `End Date`
2. Changed data type to **Date**
3. Confirmed correct parsing

---

### Validation

✅ Date icons visible in Power Query  
✅ Fields available for future time-based logic

---

## 📊 Data Quality Summary

| Severity | Count | Resolved |
|----------|-------|----------|
| 🔴 Critical | 1 | 1 |
| 🟡 High | 1 | 1 |
| 🟢 Medium | 1 | 1 |
| **Total** | **3** | **3** |

**Overall Status:** ✅ All identified data quality issues resolved prior to model deployment.

**Success Rate:** 100%

---

## 🎓 Lessons Learned

1. **Visual similarity ≠ data compatibility** - IDs looked identical but had different types
2. **Verify data types first** - Check before creating relationships
3. **Government datasets need preprocessing** - Different systems export differently
4. **Document clearly** - Prevents repeat problems

---

## 🏭 Production Considerations

**For production deployment:**

| Current Approach | Production Approach |
|------------------|---------------------|
| Power Query standardization | ETL pipeline (upstream fix) |
| Manual validation | Automated quality checks |
| Ad-hoc fixes | Data standards documentation |

**Recommendations:**
- Identifier standardization should occur in ETL pipelines
- Automated data quality checks should validate joins before load
- Data standards should be documented and enforced upstream

---

**Document Owner:** Arthur Dorvil  
**Last Updated:** January 2026  
**Version:** 1.0  
**Previous:** `02_modeling_decisions.md` | **Next:** `04_validation_checks.md`
