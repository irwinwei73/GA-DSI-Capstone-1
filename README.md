# GA-DSI-Capstone
Capstone Project:<br><br>
**Predicting Whether Insurance Underwriting Gain Will Be Negative at the Close of the Reporting Period**
<br><br>

## Submissions
1) Capstone_Final_Presentation.pptx <br>
2) Notebook "01 Download files from MAS.ipynb" <br>
3) Notebook "02 Extract table from PDF files.ipynb" <br>
4) Notebook "03 Import from PDF to pandas.ipynb" <br>
5) Notebook "04 EDA and Feature Engineering.ipynb" <br>
6) Notebook "05 Models-Classification.ipynb" <br>
7) Notebook "06 Annex-1 Part 1 (Regression).ipynb" <br>
8) Notebook "06 Annex-1 Part 2 (Regression and Clustering).ipynb" <br>
9) Notebook "06 Annex-1 Part 3 (RFE-CV).ipynb" <br>
10) "data/source/" folder - the PDF documents downloaded from MAS
11) "data/output/" folder - the extracted tables as PDF documents

<br>The above filenames are self-explanatory.
<br>For the project, the Classification Models (Item 5) are used.
<br>Annex-1 (Items 7-9) forms the set of code used to explore Regression Models. However, the regression results were not acceptable. The code is nonetheless included in this submission for reference.<br><br>

# Background
There are 2 types of insurance, namely, Life Insurance and General Insurance, both of which operate independently of one another.<br><br>
Life Insurance policies would include term life insurance, investment-linked plans, critical illness, hospitalization and medical plans for individual consumers. General Insurance, on the other hand, mostly involve property and liability instead of individuals' well-being and/or investments. For examples, General Insurance policies may provide cover for cargo, construction projects, buildings, homes, liability, professional risks, vehicles and ships. General Insurance also covers workplace injury and group (corporate/company) health/accident. Although these relate to personal well-being, they are usually purchased by a company/organization to protect is employees/members.<br><br>

Life Insurance and General Insurance are subjected to different sets of regulatory requirements.<br><br>

**The scope of this project is limited to General Insurance only, hereafter referred to simply as 'insurance'. Companies that offer General Insurance coverage are referred to as 'insurers'. The insurance plans sold by insurers are called 'policies'. The type of insurance policy (e.g. motor, cargo, work injury etc.) is known as the 'insurance class'.**<br><br>

Insurers sell insurance policies to its customers, who pay a 'premium' (fee) for the insurance coverage. Each insurance policy typically (there are exceptions) provides coverage for 12 months. Upon expiry, the policy can be renewed (so that coverage will be extended for the next 12 months) for a premium, paid by the customer.<br><br>

While the insurance policy is in effect, should a legitimate claim arise, the insurer is obliged to reimburse the customer (provided all policy conditions are satisfied). Depending on the specific policy wordings/conditions, the insurer may be obliged to pay in part or in full. The adjudication of the claim may involve investigations by third-parties (e.g. surveyors, loss adjusters, forensic specialists etc.) and could take months (in some cases, years) to be fully resolved. Claims could be paid out in stages as well.

The total amount that Insurers collect as premiums, less the total amount paid out in claims, forms the basis of underwriting gain/loss. If within a given window (e.g. 12 months), the total premiums collected is greater than claims paid, then the result is an underwriting gain. Otherwise, it is an underwriting loss.

Meanwhile, what happens to all the premiums collected by an Insurer? Some of the amount will be put in 'reserve' to pay for known claims (that have already been notified) and future anticipated claims (calculated based on various statistical records). Some of the amount will be used for various operating expenses and/or capital expenditure. The remaining amount is usually invested in various financial instruments.<br><br>

As such, insurers have 2 streams of profit/loss:<br>
- Underwriting gain/loss
- Investment profit/loss

The 'Operating Result' of an insurer equals to: **Underwriting gain/loss PLUS Investment profit/loss**<br><br>

For best results, both the underwriting and investment activities should yield gain/profit. Should there be an underwriting loss, then the Operating Result of an insurer will depend on the investment returns being able to sufficiently make up for the underwriting loss.

## Risk Management and Reinsurance
Every insurer has a risk management strategy for minimizing the chances of posting an underwriting loss. This includes studying the risks in detail and calculating the likelihoods of claims arising and their claim amounts.<br><br>
On the other hand, insurers are also concerned with market share / reputation, and therefore may not wish to be seen as turning down business (even if their calculations predict that certain policies are likely to result in a claim beyond dome threshold value). A common method to manage the insurer's exposure to risk is to "re-insure" some of the risk to a reinsurer. The insure will, in turn, pay the reinsurer commissions (same concept as premiums) to assume the risk on their behalf. Re-insurers may in turn re-insurer part of their risks to other re-insurers and so on.

## Reporting to the Monetary Authority of Singapore (MAS)
Regardless of the insurer's financial year period, the insurer is required to submit its audited company returns to MAS every December. Relevant portions of the reports submitted by all insurers operating in Singapore are published at https://www.mas.gov.sg/statistics/insurance-statistics/insurance-company-returns <br><br>
Within each report, there is a table entitled "FORM 6 (SIF)" which provides a breakdown, for each insurance class sold by the insurer for coverage in Singapore, regarding the underwriting performance and investment performance for the 12-month period January to December that year.
<br><br>

## Is there a problem that needs solving?
Yes! Despite the risk management measures adopted by insurers, recent data suggests that an increasing number of insurance policies, across all insurance classes, are posting underwriting losses. Since 2007, the aggregate percentage of loss-making policies sold has been steadily increasing from about 20% (in 2007) to 44% in 2018. In other words, in 2018, nearly half of all general insurance policies sold resulted in an underwriting loss. Some of the worst performing insurance classes are marine/aviation, group health, motor, work injury and credit/political risk.

__Problem Statement:__
<br> To establish a proof-of-concept method, based only on publicly available data, for predicting whether the underwriting performance of any given insurance class is likely to result in an underwriting loss at the end of the current 12-month reporting period. This will allow underwriters to give special focus to specific insurance classes and adopt the necessary risk management measures.<br><br>

__Data Science Problem Statement:__
<br> Using data obtained only from the annual returns submitted by insurers to MAS from 2005 to 2018 as labeled data, to train a machine learning classifier model to predict whether the underwriting gain is negative.<br><br>

## Executive Summary
All insurance annual reports published on the MAS website were downloaded, from which the table "FORM 6 (SIF)"" was extracted and put into a dataframe. The dataframe was then exported to a CSV file.<br><br>

The data was explored, cleaned and iteratively feature-engineered while being tested on several regression models. It eventually became apparent that the nature of the data (distribution, profusion of outliers etc) was unable to support the regression models being developed. As such, the data was then tested on several classification models instead.<br><br>

The models that best addressed the problem statement were based on __Logistic Regression Classifier__ and __Extra Trees Classifier__  with tuned hyperparameters. The models performed about 6% to 9% better than the baseline accuracy. However, the __Logistic Regression Classifier__ yielded a significantly higher Recall (ratio of True Positives / All Positives ) score than the __Extra Trees Classifier__. <br><br>

## Data
Data was extracted from 1,085 PDF files which resulted in 16,140 rows x 38 columns.<br>
After cleaning, EDA and removing extreme outliers, the shape of data used for modeling was 4,347 rows x 33 columns.<br>

## Conclusion
Our opinion is that the data from the annual reports is extremely coarse-grained for the data science problem statement on hand. In spite of this, the above models were still able to out-perform the baseline accuracy. In view that insurers harbor much more underwriting and claims data (as compared to the annual reports) that can be fed to machine learning models, we believe that machine learning ought to be used by insurers to predict (and possibly regress) projected underwriting gains.

## Further Work
At the time of writing, regression modeling has been put on hold in favor of classification. However, we wish to explore regression after further grouping the data according insurers' attributes such as maturity, market share (depending on insurance class) etc.
