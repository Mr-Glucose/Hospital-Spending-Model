# ✅ Model Validation Checks

**Project:** Hospital Medicare Spending Analysis  
**Analyst:** Arthur Dorvil  
**Date:** January 29, 2026

---

## 🎯 Purpose

This document outlines the validation steps performed to confirm that the Power BI data model is **accurate, reliable, and behaving as intended**.

**Validation focuses on:**
- Relationship integrity
- Filter propagation
- Metric correctness
- Data completeness

**Goal:** Ensure dashboard results can be trusted before sharing with stakeholders.

---

## 📊 Validation Scope

**Model components validated:**

| Component | Details |
|-----------|---------|
| **Tables** | Hospital_Dim, Medicare_Hospital_Spending_Fact |
| **Relationship** | Hospital_Dim → Spending_Fact |
| **Cardinality** | One-to-Many (1:*) |
| **Direction** | Single (Hospital → Spending) |
| **Status** | Active |

---

## 🧪 Test 1: Relationship Integrity

### Objective
Verify that every spending record successfully joins to a hospital record (no orphaned records).

### Method
Created table visual using:
- `Hospital_Dim[Facility Name]`
- `Medicare_Hospital_Spending_Fact[Score]`

### Expected Result
- All hospitals display corresponding MSPB scores
- No blank or null scores appear

### Actual Result

| Hospital | MSPB Score | Status |
|----------|------------|--------|
| Lakewood Ranch Medical Center | 1.10 | ✅ |
| HCA Florida Blake Hospital | 1.06 | ✅ |
| Manatee Memorial Hospital | 1.04 | ✅ |
| Sarasota Memorial Hospital | 1.03 | ✅ |

### Outcome
✅ **PASS** - All spending records successfully matched to hospitals  
✅ **PASS** - No orphaned records detected (4/4 matched)

---

## 🔢 Test 2: Cardinality Verification

### Objective
Confirm the relationship behaves as one-to-many.

### Method
- Inspected relationship properties in Model View
- Verified uniqueness of Facility ID values in Hospital_Dim
- Verified fact table can support multiple records per hospital

### Expected Result
- Hospital_Dim contains unique Facility ID values
- Spending_Fact allows multiple rows per Facility ID (future-ready)

### Actual Result
✅ **PASS** - One-to-Many (1:*) relationship enforced  
✅ **PASS** - Model supports future historical expansion

---

## 🔀 Test 3: Cross-Filter Direction

### Objective
Confirm filters propagate from dimension to fact only (not bidirectional).

### Method
1. Added slicer: `Hospital_Dim[Hospital Ownership]`
2. Selected: "Government – Hospital District or Authority"

### Expected Result
- Only Sarasota Memorial Hospital remains visible
- Corresponding MSPB score displays correctly (1.03)

### Actual Result
✅ **PASS** - Sarasota Memorial Hospital displayed  
✅ **PASS** - MSPB Score: 1.03  
✅ **PASS** - Other hospitals correctly filtered out

### Outcome
✅ **PASS** - Single-direction filtering works as designed  
✅ **PASS** - No unexpected reverse filtering behavior

---

## 📐 Test 4: Measure Accuracy

### Objective
Verify calculated measures return correct values.

### Measures Tested

| Measure | Expected | Actual | Status |
|---------|----------|--------|--------|
| Hospital Count | 4 | 4 | ✅ |
| Avg Spending Score | ~1.06 | 1.06 | ✅ |
| Max Spending Score | 1.10 | 1.10 | ✅ |

**Manual verification:**
- Hospital Count: 4 hospitals in dataset ✓
- Avg Score: (1.10 + 1.06 + 1.04 + 1.03) ÷ 4 = 1.0575 ≈ 1.06 ✓
- Max Score: Highest value = 1.10 (Lakewood Ranch) ✓

### Outcome
✅ **PASS** - All measures calculate correctly

---

## 📋 Test 5: Data Completeness

### Objective
Confirm dataset completeness for all selected hospitals.

### Checks Performed
- All hospitals have valid Facility IDs
- All spending records contain non-null scores
- Date fields are populated and correctly typed

### Results

| Check | Complete | Total | Percentage |
|-------|----------|-------|------------|
| Facility IDs | 4 | 4 | 100% |
| MSPB Scores | 4 | 4 | 100% |
| Date Fields | 4 | 4 | 100% |

### Outcome
✅ **PASS** - 100% data completeness

> 📌 **Note:** The full CMS dataset contains ~15% suppressed values for privacy reasons. Our filtered dataset is 100% complete.

---

## 📊 Validation Summary

| Test | Status | Evidence |
|------|--------|----------|
| **Relationship Integrity** | ✅ Pass | 0 orphaned records, 4/4 matched |
| **Cardinality** | ✅ Pass | 1:* enforced, future-ready |
| **Cross-Filter Direction** | ✅ Pass | Single direction working correctly |
| **Measure Accuracy** | ✅ Pass | All calculations verified manually |
| **Data Completeness** | ✅ Pass | 100% complete (4/4 hospitals) |

**Overall Status:** ✅ **Model validated and ready for reporting**

**Success Rate:** 100% (5/5 tests passed)

---

## 🎯 Conclusion

All validation checks confirm that:

✅ **Relationships** are correctly defined  
✅ **Filters** behave predictably  
✅ **Measures** aggregate accurately  
✅ **Data** is complete  
✅ **Model** is extensible and stable

The Power BI model is considered **production-ready** for the scope of this analysis.

---

**Document Owner:** Arthur Dorvil  
**Last Updated:** January 2026  
**Version:** 1.0  
**Previous:** `03_data_quality_log.md` | **Status:** ✅ All Tests Passed
- Relationship:
  - Hospital_Dim → Medicare_Hospital_Spending_Fact
  - Cardinality: One-to-Many (1:*)
  - Cross-filter direction: Single
  - Status: Active

---

## Validation Test 1: Relationship Integrity (No Orphaned Records)

### Objective
Verify that every spending record successfully joins to a hospital record.

### Method
A table visual was created using:
- Hospital_Dim[Facility Name]
- Medicare_Hospital_Spending_Fact[Score]

### Expected Result
- All hospitals display a corresponding MSPB score
- No blank or null scores appear

### Actual Result
- Lakewood Ranch Medical Center → 1.10
- HCA Florida Blake Hospital → 1.06
- Manatee Memorial Hospital → 1.04
- Sarasota Memorial Hospital → 1.03

### Outcome
✓ All spending records successfully matched to hospitals  
✓ No orphaned records detected

---

## Validation Test 2: Cardinality Verification

### Objective
Confirm the relationship behaves as one-to-many.

### Method
- Inspected relationship properties in Model View
- Verified uniqueness of Facility ID values in Hospital_Dim
- Verified fact table can support multiple records per hospital for future periods

### Expected Result
- Hospital_Dim contains unique Facility ID values
- Spending_Fact allows multiple rows per Facility ID

### Actual Result
✓ One-to-Many (1:*) relationship enforced  
✓ Model supports future historical expansion

---

## Validation Test 3: Cross-Filter Direction Behavior

### Objective
Confirm filters propagate from dimension to fact only.

### Method
1. Added slicer using Hospital_Dim[Hospital Ownership]
2. Selected "Government – Hospital District or Authority"

### Expected Result
- Only Sarasota Memorial Hospital remains visible
- Corresponding MSPB score displays correctly

### Actual Result
- Sarasota Memorial Hospital displayed ✓
- MSPB Score: 1.03 ✓
- Other hospitals correctly filtered out ✓

### Outcome
✓ Single-direction filtering works as designed  
✓ No unexpected reverse filtering behavior observed

---

## Validation Test 4: Measure Accuracy

### Objective
Verify calculated measures return correct values.

### Measures Tested
- Hospital Count
- Average Spending Score
- Maximum Spending Score

### Expected Results
- Hospital Count = 4
- Average MSPB Score ≈ 1.06
- Maximum MSPB Score = 1.10

### Actual Results
- Hospital Count: 4 ✓
- Avg Spending Score: 1.06 ✓
- Max Spending Score: 1.10 ✓

---

## Validation Test 5: Data Completeness

### Objective
Confirm dataset completeness for the selected hospitals.

### Checks Performed
- All hospitals have valid Facility IDs
- All spending records contain non-null scores
- Date fields are populated and correctly typed

### Results
- Facility IDs complete: 4 / 4 (100%)
- MSPB scores present: 4 / 4 (100%)
- Date fields valid: 4 / 4 (100%)

---

## Validation Summary

| Validation Area | Status |
|----------------|--------|
| Relationship integrity | ✓ Pass |
| Cardinality | ✓ Pass |
| Cross-filter direction | ✓ Pass |
| Measure correctness | ✓ Pass |
| Data completeness | ✓ Pass |

**Overall Status:** Model validated and ready for reporting.

---

## Conclusion

All validation checks confirm that:
- Relationships are correctly defined
- Filters behave predictably
- Measures aggregate accurately
- The model is extensible and stable

The Power BI model is considered **production-ready** for the scope of this
analysis.

---

**Document Owner:** Arthur Dorvil  
**Last Updated:** January 29, 2026  
**Version:** 1.0
