# 🏗️ Data Modeling Decisions

**Model Type:** Star Schema (Dimensional)  
**Analyst:** Arthur Dorvil  
**Date:** January 2026

---

## 🎯 Model Pattern

The model follows a **dimensional (star schema)** design:

**Tables:**
- `Hospital_Dim` (dimension) - Descriptive attributes
- `Medicare_Hospital_Spending_Fact` (fact) - MSPB measurements

```
Hospital_Dim (1) ────► (*) Medicare_Hospital_Spending_Fact
  Dimension                        Fact Table
```

---

## 🔗 Relationship Configuration

| Property | Value |
|----------|-------|
| **From Table** | Hospital_Dim |
| **To Table** | Medicare_Hospital_Spending_Fact |
| **Key Column** | Facility ID |
| **Cardinality** | One-to-Many (1:*) |
| **Cross-filter Direction** | Single (Hospital → Spending) |
| **Status** | Active |

---

## 🔢 Cardinality: One-to-Many (1:\*)

**Current state:** 1 hospital → 1 spending record (2023 data only)

**Future state:** 1 hospital → many spending records (multi-year support)

### Why One-to-Many?

Each MSPB score belongs to **exactly one** hospital. When historical years are added, each hospital will have multiple spending records (one per year).

**Example future scenario:**
```
Sarasota Memorial Hospital
  ├─ 2023: MSPB 1.03
  ├─ 2022: MSPB 1.05
  └─ 2021: MSPB 1.04
```

**Not Many-to-Many** because a single MSPB score never applies to multiple hospitals.

---

## 🔀 Cross-Filter Direction: Single

**Selected:** Single direction (Hospital_Dim → Spending_Fact)

### Why Single Direction?

**Advantages:**
- **Predictable behavior** - Filters always flow dimension → fact
- **Better performance** - Single direction is faster to evaluate
- **Avoids ambiguity** - Prevents circular dependencies with multiple tables
- **Semantically correct** - Hospitals filter spending, not vice versa

**When to use Bidirectional:**
- Many-to-many relationships
- Bridge tables
- Specific advanced scenarios

**For this model:** Single direction is correct and sufficient.

---

## 🔑 Identifier Standardization

**Challenge:** Source files had incompatible data types for Facility ID

| File | Original Type | Standardized To |
|------|---------------|-----------------|
| Hospital_General_Information.csv | TEXT | TEXT ✓ |
| Medicare_Hospital_Spending.csv | INTEGER | TEXT ✓ |

**Solution:** Standardized both to TEXT in Power Query

**Actions taken:**
1. Converted Facility ID to text where necessary
2. Ensured consistent formatting across both tables
3. Verified leading zeros were preserved
4. Confirmed both columns shared the same data type

**Result:** No new columns were introduced; standardization was applied directly to existing Facility ID fields.

---

## ✅ Why This Model Works

**Ensures:**
- ✓ Matching data types enable relationship creation
- ✓ Consistent identifier format across tables
- ✓ Reliable joins with 100% match rate
- ✓ Future-ready for multi-year expansion

---

## 🎯 Design Principles

### Star Schema vs. Snowflake

**Chosen:** Star schema  
**Why:** Simple, fast queries, easy to understand

**Not chosen:** Snowflake schema  
**Why:** Unnecessary complexity for only 4 hospitals

### Single vs. Bidirectional Filtering

**Chosen:** Single direction  
**Why:** Predictable, performant, semantically correct

**Not chosen:** Bidirectional  
**Why:** Could cause unexpected behavior, not needed here

---

**Document Owner:** Arthur Dorvil  
**Last Updated:** January 2026  
**Previous:** `01_data_sources.md` | **Next:** `03_data_quality_log.md`
