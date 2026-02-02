# Technical Documentation: Loan Approval & Credit Risk Engine
**Market Focus:** United States & Canada Portfolio Analysis  
**Prepared by:** Amelia Phi
**Tools:** Power BI, Power Query, DAX, GitHub

<div style="page-break-after: always;"></div>

## Table of Contents


## Project Objective & Business Problem
Define the main objective of the proejct and describe the specific business problem being addressed.

## Data Sources & Transformations
### About Dataset
The primary dataset used for this analysis is the **"Realistic Loan Approval Dataset | US & Canada"** sourced from [Kaggle](https://www.kaggle.com/datasets/parthpatel2130/realistic-loan-approval-dataset-us-and-canada).

The raw data was imported as a single flat table containing **20 columns**. Preliminary profiling revealed a mix of categorical (Employment Status, Loan Intent) and numerical (FICO, DTI, Income) variables.


### Data Clean
Before analysing the dataset, I performed the following transformation in Power Query to align the data with North American financial standards:

* **Schema Optimisation**: Defined data types for all 20 columns, ensuring financial metrics (income, loan amounts) were handled as fixed decimals and identifiers as strings.

* **Data Integrity Assurance**: Verified column quality and distribution to ensure a 0% error rate and 100% data density across all key financial fields, with no null or empty values. 

* **Metric Standardisation**: Standardised `interest_rate` column by applying a division transformation, converting raw basis points into a true percentage format.

* **Value Mapping**: Performed on the ``loan_status`` binary variable, replacing `0` and `1` with descriptive labels (`Rejected` and `Approved`) to improve report legibility for non-technical stakeholders.

* **Risk Segmentation**: Created `credit_tier` column based on standard Equifax/FICO scoring models to facilitate categorical risk analysis:
  * **Exceptional**: 800+
  * **Very Good**: 740–799
  * **Good**: 670–739
  * **Fair**: 580–669
  * **Poor**: <580

## Data Model & DAX
Describe the schema, relationships between tables, and highlight any important DAX measures creates.

## Visuals & Key Insight
Capture images and describe, summarise the key insights, and provide recommendations if applicable.

## Interactive Features
List the main filters/slicers used, and describe how bookmarks, tooltips, or other interactive features were implemented (if available).
