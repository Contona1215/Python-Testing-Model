# Credit Line Increase Model Card

**Basic Information**
 - Person or organization developing model: Group 31: xinyuduan@gwu.edu, fdu100@gwu.edu, xiaosong.yao@gwu.edu, hanning.yu@gwu.edu
 - Model date: August, 2022
 - Model version: 1.0
 - License: Group 31
 - Model implementation code: 

**Intended Use**
 - Primary intended uses: This model is an example probability of default classifier, with an example use case for determining eligibility for a credit line increase.
 - Primary intended users: Group 31.
 - Out-of-scope use cases: Any use beyond an educational example is out-of-scope.

**Training Data**
 - Data dictionary:
 
| **Name**     | **Modeling Role** | **Measurement Level** | **Description**                     |
|--------------|:-----------------:|:---------------------:|------------------------------------:| 
| ID           | ID                |  int                  | unique row indentifier              |
| LIMIT_BAL    | input             |  floar                | amount of previously awarded credit |
| SEX          | demographic information | int | 1 = male; 2 = female |
| RACE         | demographic information | int | 1 = hispanic; 2 = black; 3 = white; 4 = asian |
| EDUCATION    | demographic information | int | 1 = graduate school; 2 = university; 3 = high school; 4 = others |
| MARRIAGE     | demographic information | int | 1 = married; 2 = single; 3 = others |
| AGE          | demographic information | int | age in years |
| PAY_0, PAY_2 - PAY_6 | inputs | int | history of past payment; PAY_0 = the repayment status in September, 2005; PAY_2 = the repayment status in August, 2005; ...; PAY_6 = the repayment status in April, 2005. The measurement scale for the repayment status is: -1 = pay duly; 1 = payment delay for one month; 2 = payment delay for two months; ...; 8 = payment delay for eight months; 9 = payment delay for nine months and above |



