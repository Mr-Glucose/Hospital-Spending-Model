# 📊 Project Context

**Project:** Hospital Medicare Spending Analysis  
**Region:** Bradenton–Sarasota, Florida  
**Data Period:** January 1, 2023 – December 31, 2023

---

## 🎯 Overview

This project analyzes **Medicare Spending per Beneficiary (MSPB)** scores across four hospitals in the Bradenton–Sarasota region using public CMS data.

**Goal:** Compare hospital-level Medicare spending while demonstrating how real-world healthcare data must be cleaned and modeled before it can be trusted.

---

## 📖 What is MSPB?

**MSPB** stands for **Medicare Spending per Beneficiary**.

It's a CMS efficiency metric that measures how much Medicare spends on a patient's episode of care, starting shortly before hospital admission and extending after discharge.

### The MSPB Scale

```
< 1.00          1.00          > 1.00
Below Avg   National Avg   Above Avg
(Lower Cost)  (Baseline)   (Higher Cost)
```

**How it works:**
- **1.00** = National average Medicare spending
- **Above 1.00** = Higher-than-average spending
- **Below 1.00** = Lower-than-average spending

> ⚠️ **Important:** MSPB is **not a dollar amount**. It's a **ratio** benchmarked against a national baseline defined by CMS.

---

## 🔍 Interpreting Scores

### Example: MSPB Score of 1.06

A score of **1.06** means that Medicare spending for that hospital's patients was approximately **6 percent higher than the national average**, after CMS adjustments for patient mix and regional factors.

**Key points:**
- Benchmark (1.00) is defined by CMS, not calculated in this project
- Scores are **risk-adjusted** for patient complexity
- Accounts for **geographic price variations**

---

## 💡 Why This Matters

MSPB helps different stakeholders understand healthcare efficiency:

| Stakeholder | Use Case |
|-------------|----------|
| **Hospital Leaders** | Identify cost efficiency opportunities |
| **Policymakers** | Compare regional spending patterns |
| **CMS** | Monitor Medicare program costs |
| **Researchers** | Analyze variation in care delivery |

---

## 🎓 Project Focus

This project focuses on **how to correctly model and interpret MSPB data**, not on clinical judgment or hospital performance evaluation.

**Emphasis areas:**
- Data integration challenges
- Quality issue resolution
- Dimensional modeling
- Validation processes

---

## 🏥 Hospitals Analyzed

| Hospital | Ownership | MSPB Score |
|----------|-----------|------------|
| Lakewood Ranch Medical Center | Proprietary | **1.10** |
| HCA Florida Blake Hospital | Proprietary | 1.06 |
| Manatee Memorial Hospital | Proprietary | 1.04 |
| Sarasota Memorial Hospital | Government | 1.03 |

**Regional Finding:** All 4 hospitals exceed the national average (1.00) for Medicare spending.

---

**Document Owner:** Arthur Dorvil  
**Last Updated:** January 2026  
**Next:** See `01_data_sources.md` for dataset details
