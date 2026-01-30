# Documentation

This folder contains the complete technical documentation for the **Hospital Utilization & Payment Analysis: Messy Data Edition** project.

The purpose of this documentation is to clearly explain the reasoning, structure, and quality controls behind the data model and analysis. The focus is not only on results, but on *how* trustworthy results were achieved from real-world, imperfect CMS data.

This documentation is written to reflect professional business intelligence practices, including data modeling discipline, data quality remediation, and validation workflows.

---

## Project Overview

The project analyzes hospital-level **Medicare Spending Per Patient (MSPB)** data using public CMS datasets. It highlights how inconsistencies in source data, such as identifier formatting and mixed data types, can directly impact relationships, calculations, and analytical conclusions if not addressed correctly.

The workflow emphasizes:
- Controlled analytical scope
- Explicit key standardization
- Clear separation of dimensions and facts
- Validation-driven development

---

## End-to-End Workflow

```mermaid
flowchart LR
    A[Raw CMS CSV Files] --> B[Power Query Transformations]
    B --> C[Dimensional Modeling]
    C --> D[DAX Measures]
    D --> E[Validation Checks]
    E --> F[Final Power BI Dashboard]

