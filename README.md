# Microfinance Behavioral Impact Analysis

## Project Overview

This project examines how small business owners perceive the impact of high-interest microfinance loans using primary survey data collected from 20 small businesses in Pakistan.

The analysis focuses on behavioral and structural patterns rather than causal inference or prediction. It explores how business characteristics (formality, size, age, industry) and loan characteristics (amount, duration, interest rate) relate to perceived outcomes such as profitability, cost reduction, and savings for growth.

The project is intentionally framed as a behavioral analytics study, prioritizing interpretability, methodological discipline, and real-world constraints over model complexity.

---

## Data Source

- Primary survey data collected via Google Forms (undergraduate research project)
- Cross-sectional, self-reported responses
- One observation per business

---

## Why This Project Uses an Imperfect Dataset

This project intentionally works with a small, incomplete, and imperfect survey dataset to reflect the realities of real-world business and policy data, where information is collected directly from individuals across diverse demographic backgrounds and practical constraints.

In this case, the data was gathered from small business owners in Pakistan, many of whom may not primarily operate in English and are not formally obligated to preserve strict data integrity. These conditions mirror common challenges in applied analytics, where analysts must work within respondent limitations rather than idealized data environments.

Instead of masking these limitations, the project treats them as analytical constraints and adapts the methodology accordingly:

- Missing values are preserved rather than imputed
- Categorical and ordinal data are handled conservatively
- Analysis remains descriptive and comparative, not predictive
- Findings are interpreted as patterns rather than population-level claims

---

## Data Cleaning and Preparation

### Timestamp Standardization
- Google Forms timestamps were reduced to survey dates only
- Time of day was removed as analytically irrelevant
- Final variable: `survey_date`

### Duplicate Handling
- One duplicated response was identified and removed
- Independence of observations was ensured

### Business Information Structuring
A free-text field was split into:
- `business_name`
- `city`
- `province`
- `industry`

Fields were populated only when explicitly provided. Missing values were intentionally retained to avoid assumptions or data fabrication.

### Industry Grouping
- Original responses preserved as `industry_raw`
- A standardized `industry_group` variable was created for analytical consistency
- No industry detail was inferred beyond respondent input

---

## Business Formality (NTN Encoding)

The question *“Do you have an NTN number?”* was converted from text to a binary variable:

- `1` = Formally registered business  
- `0` = Informal business  

This encoding:
- Enables direct comparison between formal and informal businesses
- Improves compatibility across Excel, SQL, Python, and Power BI
- Preserves meaning while improving analytical usability

---

## Microfinance Bank Data Consolidation

### Background
Microfinance bank information was collected using:
1. A predefined bank list  
2. A follow-up open-text field for unlisted institutions  

This resulted in overlapping responses and non-informative placeholders (e.g., “N/A”, “Above mentioned”).

### Cleaning Decision
Both fields were consolidated into a single variable: `microfinance_bank_final`

Rules applied:
- Retained valid bank names from either field
- Removed placeholder or non-informative responses
- Standardized spelling and formatting
- Where multiple banks were listed, retained the first valid institution
- No rows were duplicated or removed

This preserves respondent intent while maintaining a one-row-per-business structure suitable for descriptive analysis.

---

## Loan Characteristics Standardization

Loan attributes were collected as categorical ranges and standardized accordingly:

- Loan Amount: `loan_amount_category`
- Loan Duration: `loan_duration`
- Interest Rate: `interest_rate_band`

No exact numeric values were inferred. Missing values were retained, and original response meaning was preserved throughout.

---

## Outcome Variable Encoding (Likert Scores)

Survey questions measuring perceived business outcomes used a 5-point Likert scale and were converted into numeric ordinal scores:

| Response            | Score |
|---------------------|-------|
| Strongly Disagree   | 1     |
| Disagree            | 2     |
| Neutral             | 3     |
| Agree               | 4     |
| Strongly Agree      | 5     |

Converted outcome variables include:
- `product_improvement_score`
- `employee_training_score`
- `cost_reduction_score`
- `income_increase_score`
- `profit_increase_score`
- `savings_expansion_score`

These scores are treated strictly as ordered indicators of perception, not precise measurements or causal evidence.

---

## Analytical Framing

This study is:
- Descriptive and comparative
- Survey-based and self-reported
- Conservative in handling categorical and ordinal data
- Focused on behavioral trade-offs rather than forecasting

No causal inference or population-level generalization is attempted.

---

## Power BI: Visualization Strategy

Most research questions involve group-level comparisons (e.g., registered vs. unregistered, small vs. medium businesses). Clustered column charts were used to provide clear side-by-side comparisons aligned with Power BI business reporting standards.

---

## Key Analysis Findings

### Average Perceived Impact of Microfinance Loans by Business Outcome
Small businesses report generally positive perceived impacts across most operational outcomes, with average scores consistently above the neutral midpoint. Product improvement, income increase, profit increase, cost reduction, and employee training cluster around relatively strong agreement. In contrast, savings for future expansion scores noticeably lower, indicating that while microfinance supports short-term performance, it is less effective at enabling long-term growth under high-interest conditions.

### Loan Size Differences by Business Formality (NTN Status)
Informal businesses received slightly higher average loan amounts than registered businesses, suggesting that formal registration alone does not guarantee access to larger loans within this sample.

### Average Loan Amount by Business Size
Medium-sized businesses (>10 employees) received higher average loan amounts than smaller businesses, indicating that business scale may influence lending decisions.

### Average Loan Amount by Business Age
Loan size varies non-linearly by business age:
- Mid-age businesses (4–7 years) receive the largest loans
- New businesses receive moderate loan amounts
- Older businesses (8+ years) receive smaller loan amounts  

This suggests lenders may prioritize businesses in an active growth phase rather than purely older firms.

### Average Profit Increase by Interest Rate
Businesses with lower-interest loans (0–20%) report slightly higher average profit increase scores than those with higher-interest loans (20–30%). While both groups report positive outcomes overall, higher borrowing costs are associated with weaker profit growth.

### Average Savings for Expansion by Interest Rate
Lower-interest loans are associated with stronger savings capacity, while higher interest payments appear to constrain cash flow and limit long-term growth.

### Cost Reduction by Loan Duration
Businesses with medium-term loans (approximately two years) report slightly stronger cost reduction outcomes than those with short-term loans (around six months).

### Loan Outcome Effectiveness by Business Formality
Formally registered and informal businesses report nearly identical overall loan outcome scores, suggesting that legal formality alone does not improve a business’s ability to convert loans into tangible benefits.

### Behavioral Trade-Offs Across Industries
Industries vary in how loan benefits are allocated. Some prioritize short-term operational improvements at the expense of savings for future expansion, while others achieve more balanced outcomes. Industry context plays a significant role in how loan capital is deployed.

---

## Conclusion

Taken together, the Power BI visuals present a consistent narrative:
- Microfinance loans primarily support short-term operational stability
- Loan structure, particularly interest rate and duration, influences outcomes more than loan access alone
- Higher interest rates weaken long-term growth capacity
- Business size and lifecycle stage affect loan size, but not necessarily effectiveness
- Formal registration does not materially improve outcome conversion
- Industry context shapes behavioral trade-offs between immediate improvement and sustainability

Overall, under high-interest conditions, microfinance appears to function more as a stabilization tool than a scaling mechanism.

---

## Limitations

- Small sample size (n = 20)
- Self-reported perceptions rather than audited financials
- Cross-sectional design
- No causal inference

---

## Future Improvements

Potential extensions include:
- Expanding the sample size
- Introducing longitudinal data
- Further segmentation by industry and loan provider
- Incorporating objective financial indicators
- Exploring interaction effects (e.g., interest rate by business age or industry)
