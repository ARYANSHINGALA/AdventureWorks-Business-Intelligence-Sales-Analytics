# Data Model

## 1. Data Model Overview

The AdventureWorks Power BI project uses a structured analytical data model designed to support sales, customer, product, territory, and time-based business analysis.

The data model combines business data with lookup, dimension, parameter, and supporting tables to provide an interactive and scalable foundation for the Power BI report.

The model supports:

- Sales performance analysis
- Customer analysis
- Product analysis
- Product category analysis
- Product subcategory analysis
- Geographic analysis
- Time-based analysis
- KPI reporting
- Dynamic metric selection
- Customer-level analysis
- Product-level analysis
- Map-based analysis
- Drill-through analysis
- Interactive filtering
- Dashboard navigation
- DAX-based calculations


## 2. Data Modeling Objectives

The main objectives of the AdventureWorks data model are:

1. Create a structured and organized analytical model.
2. Separate descriptive information from business/transactional data.
3. Establish meaningful relationships between related tables.
4. Support accurate filtering and cross-filtering.
5. Enable reusable DAX measures.
6. Support interactive Power BI dashboards.
7. Improve report maintainability.
8. Provide customer, product, territory, and time analysis.
9. Support business KPI calculations.
10. Create a scalable foundation for future enhancements.


## 3. Data Model Architecture

The project follows a dimensional modeling approach.

The conceptual architecture is:

```text
                         ADVENTUREWORKS DATA
                                  |
                                  v
                         DATA PREPARATION
                                  |
                                  v
                          DATA MODELING
                                  |
              +-------------------+-------------------+
              |                   |                   |
              v                   v                   v
         CUSTOMER             PRODUCT             TERRITORY
         LOOKUP               LOOKUP               LOOKUP
              |                   |                   |
              |                   v                   |
              |             SUBCATEGORY              |
              |                   |                   |
              |                   v                   |
              |               CATEGORY                |
              |                   |                   |
              +-------------------+-------------------+
                                  |
                                  v
                         BUSINESS / SALES DATA
                                  |
                                  v
                             DAX MEASURES
                                  |
                                  v
                         POWER BI REPORT
                                  |
              +-------------------+-------------------+
              |                   |                   |
              v                   v                   v
       EXECUTIVE DASHBOARD   CUSTOMER DETAIL     PRODUCT DETAILS
              |
              v
        MAP / GEOGRAPHIC ANALYSIS


