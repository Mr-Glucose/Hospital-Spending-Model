# Power BI

**Model Type:** Star Schema (Dimensional)  
**Tools:** Power BI Desktop, Power Query, DAX

---

## Files

### Thinking Demo.pbix
Complete Power BI workbook containing:
- Data model (Hospital_Dim + Spending_Fact)
- Power Query transformations
- DAX measures
- Dashboard visualizations

**To open:** Requires Power BI Desktop (free download from Microsoft)

---

### Thinking Demo.pdf
Dashboard export showing:
- 4 KPI cards (Hospital Count, Avg/Max MSPB, Completeness)
- Hospital comparison table
- MSPB score bar chart
- Project context panel

**Format:** Static PDF for viewing without Power BI

---

## Model Highlights

**Tables:**
- Hospital_Dim (dimension)
- Medicare_Hospital_Spending_Fact (fact)

**Relationship:**
- One-to-Many (1:*)
- Single-direction filtering
- Key: Facility ID (standardized TEXT)

**Measures:**
- Hospital Count
- Avg Spending Score
- Max Spending Score
- Data Completeness %

---

See `/Documentation` for complete technical details.

