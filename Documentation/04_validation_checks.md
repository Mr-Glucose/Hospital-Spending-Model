# Model Validation Checks

**Project:** CMS Hospital Spending, Messy Data Edition  
**Analyst:** Arthur Dorvil  
**Date:** January 29, 2026  

---

## Purpose

This document outlines the validation steps performed to confirm that the
Power BI data model is accurate, reliable, and behaving as intended.

Validation focuses on:
- Relationship integrity
- Filter propagation
- Metric correctness
- Data completeness

These checks ensure the dashboard results can be trusted before sharing
with stakeholders.

---

## Validation Scope

The following model components were validated:

- Tables:
  - Hospital_Dim
  - Medicare_Hospital_Spending_Fact

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
