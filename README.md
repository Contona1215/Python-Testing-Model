# Credit Line Increase Model Card

## Basic Information
 - Person or organization developing model: Group 31: xinyuduan@gwu.edu, fdu100@gwu.edu, xiaosong.yao@gwu.edu, hanning.yu@gwu.edu
 - Model date: August, 2022
 - Model version: Model version: 1.0(Python version: 3.7.13, sklearn version: 1.0.2)
 - License: MIT
 - Model implementation code: [DNSC_6301_Project_G31](https://github.com/Contona1215/DNSC-6301-Project-G31/blob/main/6301_Group_31.ipynb)

## Intended Use
 - Primary intended uses: This model is an example probability of default classifier, with an example use case for determining eligibility for a credit line increase.
 - Primary intended users: Group 31.
 - Out-of-scope use cases: Any use beyond an educational example is out-of-scope.

## Training Data
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

## Test Data
 - **Source of test data**: GWU Blackboard
 - **Number of rows in test data**: 7,500
 - **State any differences in columns between training and test data**: None

## Model details
 - **Columns used as inputs in the final model**: 'LIMIT_BAL', 'PAY_0', 'PAY_2', 'PAY_3', 'PAY_4', 'PAY_5', 'PAY_6', 'BILL_AMT1', 'BILL_AMT2', 'BILL_AMT3', 'BILL_AMT4', 'BILL_AMT5', 'BILL_AMT6', 'PAY_AMT1', 'PAY_AMT2', 'PAY_AMT3', 'PAY_AMT4', 'PAY_AMT5', 'PAY_AMT6'
 - **Column(s) used as target(s) in the final model**: 'DELINQ_NEXT'
 - **Type of model**: Decision Tree
 - **Software used to implement the model**: Python, scikit-learn
 - **Version of the modeling software**: Model version: 1.0(Python version: 3.7.13, sklearn version: 1.0.2)
 - **Hyperparameters or other settings of your model**:
```
DecisionTreeClassifier('ccp_alpha': 0.0,
 'class_weight': None,
 'criterion': 'gini',
 'max_depth': 6,
 'max_features': None,
 'max_leaf_nodes': None,
 'min_impurity_decrease': 0.0,
 'min_samples_leaf': 1,
 'min_samples_split': 2,
 'min_weight_fraction_leaf': 0.0,
 'random_state': 12345,
 'splitter': 'best')
```

## Quantitative Analysis
- **Metrics used to evaluate the final model**:
  - Confusion metrics
  - AUC & AIR graphs：
    AIR is an adverse impact ratio, calculates the adverse impact ratio as a quotient between protected and reference group acceptance rates.
- **The final values of the metrics for all data**:
  - Training AUC: 0.78
  - Validation AUC: 0.75
  - Test AUC: 0.74
  - Asian-to-White AIR: 1.00
  - Black-to-White AIR: 0.85
  - Female-to-Male AIR: 1.02
  - Hispanic-to-White AIR: 0.83

- **Correlation Heatmap**

![Heat_Map](https://user-images.githubusercontent.com/111463982/186793614-00bc10ba-5c20-4e33-bfe9-9498a22079f7.png)

  - The table shows how two variables are correlated with each other using Pearson correlation matrix, the light part shows the strong correlation is -1.
  - According to the heat map, we can see race the outcome are negatively correlated, indicating that there might be discrimination towards certian groups of people. We can also see that payment records are among the most influencial factors of the result. a lot of other factors contributes very little towards the result.

- **Histogram**

<img width="453" alt="截屏2022-08-27 下午6 01 11" src="https://user-images.githubusercontent.com/111463982/187049466-57d7d163-0f85-4453-b7a5-3c4ff6d3d2ba.png">


  - These are histograms, and it shows that most of the data is skewed in nature.

- **Final Iteration Plot**


![2](https://user-images.githubusercontent.com/111463982/186302745-7ac2f2e2-e1e6-4ad2-a7ad-16d2eed5f786.png)

  -  As we can see from the plot, AUC of training data continous to improve as the tree depth increases, while the AUC of validation data peaks at tree depth = 6. For the AIR of hispanic-to-white people, and we got an good result at tree depth = [5:7]. As a result, we think tree depth = 6 is the best choice. 

## Ethical Considerations

- **Describe potential negative impacts of using your model**:
  - **Math or software problems**: The data has an artificially high proportion of 1s (defaults), typically we would expect less than 1% 1s (default) in a credit default problem. 
  - **Real-world risks: who, what, when, or how**: The values of the adverse impact ratio for Black & Hispanic people might cause civil rights or gender equity controversy. When the model is used to increase people's credit limits, Black & Hispanic people receive fewer credit increases than similarly situated White people. The model might cause unacceptable legal or reputational risk.
- **Describe potential uncertainties relating to the impacts of using your model**:
  - **Math or software problems**: Implicit bias may exist in the model and data.
  - **Real-world risks: who, what, when, or how**: The model may be exposed to well-known risks such as DDOS or man-in-the-middle attacks, and packages it depends on could potentially be hacked to conceal an attack payload.
- **Describe any unexpected results**:
  - When running this model, even with the same SEED, the results change slightly every time. Also, the model might cause unacceptable reputational risk.



