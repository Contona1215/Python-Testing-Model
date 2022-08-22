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
| SEX          | demographic information |  | |


