# Technical Documentation: Loan Approval & Credit Risk Engine
**Market Focus:** United States & Canada Portfolio Analysis  
**Prepared by:** Amelia Phi
**Tools:** Power BI, Power Query, DAX, GitHub

<div style="page-break-after: always;"></div>

## Table of Contents


## Project Objective & Business Problem
### Business Problem

### Project Objective
The primary objective of this project is to develop a comprehensive **Credit Risk and Loan Portfolio Dashboard** that provides insights into lending patterns and borrower behavior. This project enables the business to monitor portfolio health, evaluate the effectiveness of credit scoring, and identifying high-risk segments in real-time. 



## Data Sources & Transformations
### About Dataset
The primary dataset used for this analysis is the **"Realistic Loan Approval Dataset | US & Canada"** sourced from [Kaggle](https://www.kaggle.com/datasets/parthpatel2130/realistic-loan-approval-dataset-us-and-canada).

The raw data was imported as a single flat table containing **20 columns**. Preliminary profiling revealed a mix of categorical (Employment Status, Loan Intent) and numerical (FICO, DTI, Income) variables.


### Data Clean
Before analysing the dataset, I performed the following transformation in Power Query to align the data with North American financial standards:

* **Schema Optimisation**: Defined data types for all 20 columns, ensuring financial metrics (income, loan amounts) were handled as fixed decimals and identifiers as strings.

* **Data Integrity Assurance**: Verified column quality and distribution to ensure a 0% error rate and 100% data density across all key financial fields, with no null or empty values. 

* **Metric Standardisation**: Standardised `interest_rate` column by applying a division transformation, converting raw basis points into a true percentage format.

* **Value Mapping**: Performed on the `loan_status` binary variable, replacing `0` and `1` with descriptive labels (`Rejected` and `Approved`) to improve report legibility for non-technical stakeholders.

* **Risk Segmentation**: Created `credit_tier` column based on standard Equifax/FICO scoring models to facilitate categorical risk analysis:
  * **Exceptional**: 800+
  * **Very Good**: 740–799
  * **Good**: 670–739
  * **Fair**: 580–669
  * **Poor**: <580

## Data Model & DAX
### Data Normalisation & Schema Design
Following the data cleaning phase, the dataset is restructured into a Star Schema to enhance analytic performance.

The flat datastructure is decomposed into two distinct categories, separating descriptive attributes from transactional met5rics:
* **Dimension Table** (`Dim_Borrower`): including static borrower attributes, such as **age**, **income**, and **credit history**. Unique recored were ensured by removing duplicate entries based on `customer_id`.

* **Fact Table** (`Fact_Loans`): including all transactional data and measurable events, such as loan amounts, interest rates, and approval statuses. 
 
The integrity of the model is secured through the establishment of a One-to-many (1:*) relationship between the Dimension and Fact tables:
* `customer_id` is the Primary Key in `Dim_Borrower` and Foreign Key in Fact_Loans.

* A 1:* relationship is enforcfed, allowing unique borrower profile to be associated with multiple transactional loan records.

* Single direction is applied, flowing from `Dim_Borrower` to `Fact_Loans`. This ensures that filters applied to borrower demographics (e.g., `credit_tier`) correctly propagate to aggregate loan metrics without creating circular dependencies.


## Visuals & Key Insight
Capture images and describe, summarise the key insights, and provide recommendations if applicable.

## Interactive Features
List the main filters/slicers used, and describe how bookmarks, tooltips, or other interactive features were implemented (if available).
