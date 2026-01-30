# Data Modeling Decisions

## Model Pattern

The model follows a dimensional (star schema) design:

- Hospital_Dim (dimension)
- Medicare_Hospital_Spending_Fact (fact)

Hospital_Dim provides descriptive attributes.
The fact table stores MSPB scores and period information.

## Relationship Configuration

| Property | Value |
|---|---|
| From Table | Hospital_Dim |
| To Table | Medicare_Hospital_Spending_Fact |
| Key Column | Facility ID |
| Cardinality | One-to-Many (1:*) |
| Cross-filter Direction | Single |
| Active | Yes |

## Cardinality Rationale

Each MSPB score belongs to one hospital.
While the current dataset contains one record per hospital,
the model supports future years where multiple records may exist.

## Cross-filter Direction Rationale

Single-direction filtering (dimension → fact) was selected to:
- Avoid ambiguous filter paths
- Preserve predictable slicer behavior
- Support future expansion with additional fact tables

## Identifier Standardization

Facility ID values were standardized in Power Query prior to modeling.
Although both source files contained the same identifiers, they differed
in data type and formatting, which prevented relationship creation.

Standardization ensured:
- Matching data types
- Consistent identifier format
- Reliable joins
