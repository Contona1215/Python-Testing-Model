# Credit Line Increase Model Card

**Basic Information**
 - Person or organization developing model: Group 31: xinyuduan@gwu.edu, fdu100@gwu.edu, xiaosong.yao@gwu.edu, hanning.yu@gwu.edu
 - Model date: August, 2022
 - Model version: 1.0
 - License: Group 31
 - Model implementation code: [a link](https://github.com/Contona1215/DNSC-6301-Project-G31/blob/main/DNSC6301_Group_31.ipynb)

**Intended Use**
 - Primary intended uses: This model is an example probability of default classifier, with an example use case for determining eligibility for a credit line increase.
 - Primary intended users: Group 31.
 - Out-of-scope use cases: Any use beyond an educational example is out-of-scope.

**Training Data**
 - Data dictionary:
 
| **Name**     | **Modeling Role** | **Measurement Level** | **Description**                     |
|--------------|:----------------- |:--------------------- |:------------------------------------| 
| **ID**           | ID                |  int                  | unique row indentifier              |
| **LIMIT_BAL**    | input             |  floar                | amount of previously awarded credit |
| **SEX**          | demographic information | int | 1 = male; 2 = female |
| **RACE**         | demographic information | int | 1 = hispanic; 2 = black; 3 = white; 4 = asian |
| **EDUCATION**    | demographic information | int | 1 = graduate school; 2 = university; 3 = high school; 4 = others |
| **MARRIAGE**     | demographic information | int | 1 = married; 2 = single; 3 = others |
| **AGE**          | demographic information | int | age in years |
| **PAY_0, PAY_2 - PAY_6** | inputs | int | history of past payment; PAY_0 = the repayment status in September, 2005; PAY_2 = the repayment status in August, 2005; ...; PAY_6 = the repayment status in April, 2005. The measurement scale for the repayment status is: -1 = pay duly; 1 = payment delay for one month; 2 = payment delay for two months; ...; 8 = payment delay for eight months; 9 = payment delay for nine months and above |
| **BILL_AMT1 - BILL_AMT6** | inputs | float | amount of bill statement; BILL_AMNT1 = amount of bill statement in September, 2005; BILL_AMT2 = amount of bill statement in August, 2005; ...; BILL_AMT6 = amount of bill statement in April, 2005 |
| **PAY_AMT1 - PAY_AMT6** | inputs | float | amount of previous payment; PAY_AMT1 = amount paid in September, 2005; PAY_AMT2 = amount paid in August, 2005; ...; PAY_AMT6 = amount paid in April, 2005 | 
| **DELINQ_NEXT** | target | int | whether a customer's next payment is delinquent (late), 1 = late; 0 = on-time | 
 - **Source of training data**: GWU Blackboard
 - **How training data was divided into training and validation data**: 50% training, 25% validation, 25% test
 - **Number of rows in training and validation data**:
    - Training rows: 15,000
    - Validation rows: 7,500

**Test Data**
 - **Source of test data**: GWU Blackboard
 - **Number of rows in test data**: 7,500
 - **State any differences in columns between training and test data**: None

**Model details**
 - **Columns used as inputs in the final model**: 'LIMIT_BAL', 'PAY_0', 'PAY_2', 'PAY_3', 'PAY_4', 'PAY_5', 'PAY_6', 'BILL_AMT1', 'BILL_AMT2', 'BILL_AMT3', 'BILL_AMT4', 'BILL_AMT5', 'BILL_AMT6', 'PAY_AMT1', 'PAY_AMT2', 'PAY_AMT3', 'PAY_AMT4', 'PAY_AMT5', 'PAY_AMT6'
 - **Column(s) used as target(s) in the final model**: 'DELINQ_NEXT'
 - **Type of model**: Decision Tree
 - **Software used to implement the model**: Python, scikit-learn
 - **Version of the modeling software**: 0.22.2.post1
 - **Hyperparameters or other settings of your model**:
```
DecisionTreeClassifier(ccp_alpha=0.0, class_weight=None, criterion='gini',
                       max_depth=6, max_features=None, max_leaf_nodes=None,
                       min_impurity_decrease=0.0, min_impurity_split=None,
                       min_samples_leaf=1, min_samples_split=2,
                       min_weight_fraction_leaf=0.0, presort='deprecated',
                       random_state=12345, splitter='best')
```

**Correlation Heatmap**

![Heat_Map](https://user-images.githubusercontent.com/111463982/186301813-1189f491-f997-4e44-b9e7-97440a95ae04.png)


**Final Iteration Plot**


![2](https://user-images.githubusercontent.com/111463982/186302745-7ac2f2e2-e1e6-4ad2-a7ad-16d2eed5f786.png)


**Quantitative Analysis**
- **Metrics used to evaluate the final model**:
  - Confusion metrics
  - AUC graphs
- **The final values of the metrics for all data**:
  - Training AUC: 0.78
  - Validation AUC: 0.75
  - Test AUC: 0.74
  - Asian-to-White AIR: 1.00
  - Black-to-White AIR: 0.85
  - Female-to-Male AIR: 1.02
  - Hispanic-to-White AIR: 0.83

**Ethical Considerations**

- **Describe potential negative impacts of using your model**:
  - **Math or software problems**: The model consists more about the 0's in the target varibale than the 1's, which is a uncomprehensive result in the public.
  - **Real-world risks: who, what, when or how**: The relatively poor performance of the ratio of Black-to-White and Hispanic-to-White might cause the controversy of civil right or gender equity.    When the model is used to increase people's credit limits, blacks and Hispanics receive less credit increases than similarly matched whites.
- **Describe potential uncertainties relating to the impacts of using your model**:
  - **Math or software problems**: Implicit bias may exist in the model data.
  - **Real-world risks: who, what, when or how**: May exposed to well-known risks such as DDOS or man-in-the-middle attacks, and packages it depends on could potentially be hacked to conceal an attack payload.
- **Describe any unexpected or results**:
  - When running this model, even with the same SEED, the results change slightly everytime. Also, the model might cause unacceptable reputational risk.



