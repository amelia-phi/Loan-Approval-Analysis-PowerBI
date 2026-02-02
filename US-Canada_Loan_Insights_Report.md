# Technical Documentation: Loan Approval & Credit Risk Engine
**Market Focus:** United States & Canada Portfolio Analysis  
**Prepared by:** Amelia Phi
**Tools:** Power BI, Power Query, DAX, GitHub

<div style="page-break-after: always;"></div>

## Table of Contents


## Project Objective & Business Problem
### Business Problem Overview
The institution's current credit approval framework relies heavily on "Knock-Out" (KO) criteria to manage risk across the US and Canadian portfolios. The most significant of these is a rigid Debt-to-Income (DTI) ceiling of 50% and an automatic rejection policy for any applicant with prior defaults.

While this conservative posture ensures high portfolio quality, a preliminary review suggests it has led to significant **Opportunity Cost**. By applying the same binary logic to Credit cards, Personal Loans and Lines of Credit, the institution is failing to differentiate between high-risk profiles and "Near-Prime" borrowers (Credit Scores 600-700) who may otherwise be creditworthy.

Key areas of concern include:

* **Market Competition**: High rejection rates in the Personal Loan segment—specifically for debt consolidation—are pushing viable customers toward more agile FinTech competitors.

* **Operational Friction**: Manual review requirement for Lines of Credit exceeding $50,000 is creating significant friction in the customer journey and increasing the cost-per-acquisition.

* **Growth Barriers**: Over-weighting "thin" credit files for Credit Card applications is preventing the bank from capturing younger demographics (Students/Early Career) who represent long-term revenue growth.




### Objective
The primary objective of this project is to develop a **Credit Risk Engine in Power BI** focusing on 4 key pillars: 

* **Optimisation Zone**: Identifying the subset of rejected applicants who passed all primary "Hard-Stop" rules (DTI < 50% and no defaults) to determine where discretionary criteria may be overly restrictive.

* **Product-Specific Risk Calibration**: Evaluating whether "Loan Intent" (e.g., Education vs. Business) correlates with lower default risk, justifying more flexible DTI thresholds for specific products.

* **Underwriting Efficiency**: Establishing clear "Auto-Approval" parameters for Lines of Credit under $50,000 to streamline the approval pipeline and reduce the manual workload for underwriters.

* **Portfolio Expansion**: Simulating the financial impact of adjusting approval thresholds to target a 5–10% increase in total loan disbursements without exceeding current delinquency benchmarks.

## Data Sources & Transformations
### About Dataset
The primary dataset used for this analysis is the **"Realistic Loan Approval Dataset | US & Canada"** sourced from [Kaggle](https://www.kaggle.com/datasets/parthpatel2130/realistic-loan-approval-dataset-us-and-canada).
The raw data was imported as a single flat table containing **20 columns**, in which includes 50K realistic loan applications of 3 product types (Credit Card, Personal Loan, Line of Credit).


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

### DAX


## Visuals & Key Insight
Capture images and describe, summarise the key insights, and provide recommendations if applicable.

## Interactive Features
List the main filters/slicers used, and describe how bookmarks, tooltips, or other interactive features were implemented (if available).
