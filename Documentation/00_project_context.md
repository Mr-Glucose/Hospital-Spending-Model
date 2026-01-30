## Project Context

This project analyzes Medicare Spending per Beneficiary (MSPB) scores
across four hospitals in the Bradenton–Sarasota region using public CMS data.

The goal is to compare hospital-level Medicare spending while demonstrating
how real-world healthcare data must be cleaned and modeled before it can be trusted.

### What is MSPB?

MSPB stands for **Medicare Spending per Beneficiary**.

It is a CMS efficiency metric that measures how much Medicare spends
on a patient’s episode of care, starting shortly before a hospital admission
and extending after discharge.

CMS standardizes this measure so that:

- **1.00 represents the national average Medicare spending**
- Values **above 1.00** indicate higher-than-average spending
- Values **below 1.00** indicate lower-than-average spending

Importantly, MSPB is **not a dollar amount**.
It is a **ratio benchmarked against a national baseline** defined by CMS.

### How to interpret a score like 1.06

A score of **1.06** means that Medicare spending for that hospital’s patients
was approximately **6 percent higher than the national average**, after CMS
adjustments for patient mix and regional factors.

This benchmark is defined and maintained by CMS, not calculated locally
within this project.

### Why this matters

MSPB helps policymakers and hospital leaders understand:
- Relative cost efficiency
- Variation in care patterns
- Opportunities for cost reduction without sacrificing quality

This project focuses on **how to correctly model and interpret MSPB data**,
not on clinical judgment or hospital performance evaluation.
