<body>
    <div class="project-info" style="max-width: 600px; margin: 40px auto; padding: 20px; background-color: #3a3a3a; border-radius: 10px; box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; color: #ffffff;">
        <h1 style="font-size: 28px; font-weight: bold; margin-bottom: 20px; text-align: center; color: #ffcc00;">Final Project</h1>
        <div class="presented-by" style="margin-bottom: 20px;">
            <strong style="display: block; font-size: 18px; margin-bottom: 10px; color: #ffcc00;">Presented By:</strong>
            <ul style="list-style-type: none; padding-left: 0;">
                <li style="margin-bottom: 10px; font-size: 16px;">Dheeraj Yadav</li>
                <li style="margin-bottom: 10px; font-size: 16px;">Sayed Mohd Mahdi</li>
            </ul>
        </div>
        <div class="guided-by">
            <strong style="display: block; font-size: 18px; margin-bottom: 10px; color: #ffcc00;">Guided By:</strong>
            <ul style="list-style-type: none; padding-left: 0;">
                <li style="margin-bottom: 10px; font-size: 16px;">Professor Michael Gilbert</li>
                <li style="margin-bottom: 10px; font-size: 16px;">G.A. Nisar Ahamad Killedar</li>
            </ul>
        </div>
    </div>
</body>

# Analysis On Default Credit Case Study


***
### Business Context - Banks primarily thrive on their money lending business. The more efficiently they can lend to individuals who repay with good interest, the better their revenue.
* **


### Objective : Building a model using the inputs/attributes which are general profile and historical records of a borrower to predict whether one is likely to have serious delinquency in the next 2 years 
* **
### Key Objectives:

Identify borrowers likely to face serious delinquency.
Enhance the bank's revenue and reputation by minimizing defaults.
* **
* We have a general profile about the borrower such as age, Monthly Income, Dependents and the historical data such as what is the Debt Ratio, what ratio of amount is owed wrt credit limit, and the no of times defaulted in the past one, two, three months.
* We will be using all these features to predict whether the borrower is likely to delinquent in the next 2 years or not.
* These kind of predictions will help banks to take necessary actions.

***


## Table of Contents

1. [Introduction](#introduction)
2. [Business Context](#business-context)
3. [Data Analysis](#Exploratory-DataAnalysis)
   
   - [SeriousDlqin2yrs Count Plot](#seriousdlqin2yrs-count-plot)
   - [Dataset Statistical Distribution](#dataset-statistical-distribution)
   - [Univariate Analysis using Training Numerical Dataset](#univariate-analysis-using-training-numerical-dataset)
   - [Distribution of Data for Skewness and Kurtosis](#distribution-of-data-for-skewness-and-kurtosis)
   - [Bivariate Analysis](#bivariate-analysis)
     
5. [Feature Engineering](#Feature-Engineering)
6. [Class Imbalance Problem](#class-imbalance-problem)
7. [Scaling](#Scaling)
8. [Machine Learning Models](#machine-learning-models)
9. [Predictions](#Predictions)
10. [Conclusion](#Conclusion)
11. [Future Scope](#FutureScope)
# Dataset Table


<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SeriousDlqin2yrs</th>
      <th>RevolvingUtilizationOfUnsecuredLines</th>
      <th>age</th>
      <th>NumberOfTime30-59DaysPastDueNotWorse</th>
      <th>DebtRatio</th>
      <th>MonthlyIncome</th>
      <th>NumberOfOpenCreditLinesAndLoans</th>
      <th>NumberOfTimes90DaysLate</th>
      <th>NumberRealEstateLoansOrLines</th>
      <th>NumberOfTime60-89DaysPastDueNotWorse</th>
      <th>NumberOfDependents</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0.766127</td>
      <td>45</td>
      <td>2</td>
      <td>0.802982</td>
      <td>9120.0</td>
      <td>13</td>
      <td>0</td>
      <td>6</td>
      <td>0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>0.957151</td>
      <td>40</td>
      <td>0</td>
      <td>0.121876</td>
      <td>2600.0</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>0.658180</td>
      <td>38</td>
      <td>1</td>
      <td>0.085113</td>
      <td>3042.0</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0.233810</td>
      <td>30</td>
      <td>0</td>
      <td>0.036050</td>
      <td>3300.0</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>0.907239</td>
      <td>49</td>
      <td>1</td>
      <td>0.024926</td>
      <td>63588.0</td>
      <td>7</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0</td>
      <td>0.213179</td>
      <td>74</td>
      <td>0</td>
      <td>0.375607</td>
      <td>3500.0</td>
      <td>3</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0</td>
      <td>0.305682</td>
      <td>57</td>
      <td>0</td>
      <td>5710.000000</td>
      <td>NaN</td>
      <td>8</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0</td>
      <td>0.754464</td>
      <td>39</td>
      <td>0</td>
      <td>0.209940</td>
      <td>3500.0</td>
      <td>8</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0</td>
      <td>0.116951</td>
      <td>27</td>
      <td>0</td>
      <td>46.000000</td>
      <td>NaN</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0</td>
      <td>0.189169</td>
      <td>57</td>
      <td>0</td>
      <td>0.606291</td>
      <td>23684.0</td>
      <td>9</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>


# Exploratory Data Analysis: 


### SeriousDlqin2yrs Count Plot:
![SeriousDlqin2yrs Count Plot](SeriousDlqin2yrs_countplot.png)

### Explanation:
- The pie chart on the left shows the proportion of borrowers who have and haven't experienced serious delinquency in the past two years.
- The count plot on the right shows the count of borrowers in each category of serious delinquency.
- The pie chart uses two colors, sky blue for 'No' and light green for 'Yes', with the 'Yes' slice exploded slightly for emphasis.
- The count plot is generated using the Seaborn library for a simple and clear representation of the count of each category.

6.683999999999999% of the borrrowers are failing in Serious Delinquency</p>


## Dataset Statistical Distribution


<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SeriousDlqin2yrs</th>
      <th>RevolvingUtilizationOfUnsecuredLines</th>
      <th>age</th>
      <th>NumberOfTime30-59DaysPastDueNotWorse</th>
      <th>DebtRatio</th>
      <th>MonthlyIncome</th>
      <th>NumberOfOpenCreditLinesAndLoans</th>
      <th>NumberOfTimes90DaysLate</th>
      <th>NumberRealEstateLoansOrLines</th>
      <th>NumberOfTime60-89DaysPastDueNotWorse</th>
      <th>NumberOfDependents</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>150000.000000</td>
      <td>150000.000000</td>
      <td>150000.000000</td>
      <td>150000.000000</td>
      <td>150000.000000</td>
      <td>1.202690e+05</td>
      <td>150000.000000</td>
      <td>150000.000000</td>
      <td>150000.000000</td>
      <td>150000.000000</td>
      <td>146076.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.066840</td>
      <td>6.048438</td>
      <td>52.295207</td>
      <td>0.421033</td>
      <td>353.005076</td>
      <td>6.670221e+03</td>
      <td>8.452760</td>
      <td>0.265973</td>
      <td>1.018240</td>
      <td>0.240387</td>
      <td>0.757222</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.249746</td>
      <td>249.755371</td>
      <td>14.771866</td>
      <td>4.192781</td>
      <td>2037.818523</td>
      <td>1.438467e+04</td>
      <td>5.145951</td>
      <td>4.169304</td>
      <td>1.129771</td>
      <td>4.155179</td>
      <td>1.115086</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000e+00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>0.000000</td>
      <td>0.029867</td>
      <td>41.000000</td>
      <td>0.000000</td>
      <td>0.175074</td>
      <td>3.400000e+03</td>
      <td>5.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.000000</td>
      <td>0.154181</td>
      <td>52.000000</td>
      <td>0.000000</td>
      <td>0.366508</td>
      <td>5.400000e+03</td>
      <td>8.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>0.000000</td>
      <td>0.559046</td>
      <td>63.000000</td>
      <td>0.000000</td>
      <td>0.868254</td>
      <td>8.249000e+03</td>
      <td>11.000000</td>
      <td>0.000000</td>
      <td>2.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.000000</td>
      <td>50708.000000</td>
      <td>109.000000</td>
      <td>98.000000</td>
      <td>329664.000000</td>
      <td>3.008750e+06</td>
      <td>58.000000</td>
      <td>98.000000</td>
      <td>54.000000</td>
      <td>98.000000</td>
      <td>20.000000</td>
    </tr>
  </tbody>
</table>
</div>






## Separating the Dataset into Train-Test Split

```python
X = df.drop(columns = ['SeriousDlqin2yrs'], axis=1)
y = df['SeriousDlqin2yrs']
```

## Shape of Train Dataset , Test Dataset
 ###   [ 120000, 11 ] | [ 30000, 11 ]


## Univariate Analysis using Training Numerical Dataset

### DebtRatio

![DebtRatio.png](DebtRatio.png)

skewness :  99.14282373943726
kurtosis :  14370.263366125106

###       AGE
    
![Age.png](Age.png)

skewness :  0.18619637326841987
kurtosis :  -0.498427938670404

### NumberOfTime30-59DaysPastDueNotWorse

![hist_boxplot_30_59.png](hist_boxplot_30_59.png)

skewness :  22.560050047962374
kurtosis :  520.586140091868

###  NumberOfTime60-89DaysPastDueNotWorse

![hist_boxplot_60_89.png](hist_boxplot_60_89.png)

skewness :  23.393598377179494
kurtosis :  548.632426633495

###  NumberOfTime90DaysLate

![hist_boxplot_90_days_late.png](hist_boxplot_90_days_late.png)

skewness :  23.155584699487473
kurtosis :  540.8745184818808


## DISTRIBUTION OF DATA FOR SKEWNESS AND KURTOSIS

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Skewness</th>
      <th>Kurtosis</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>MonthlyIncome</th>
      <td>122.587602</td>
      <td>21861.235155</td>
    </tr>
    <tr>
      <th>RevolvingUtilizationOfUnsecuredLines</th>
      <td>100.538203</td>
      <td>15559.574874</td>
    </tr>
    <tr>
      <th>DebtRatio</th>
      <td>99.142824</td>
      <td>14370.263366</td>
    </tr>
    <tr>
      <th>NumberOfTime60-89DaysPastDueNotWorse</th>
      <td>23.393598</td>
      <td>548.632427</td>
    </tr>
    <tr>
      <th>NumberOfTimes90DaysLate</th>
      <td>23.155585</td>
      <td>540.874518</td>
    </tr>
    <tr>
      <th>NumberOfTime30-59DaysPastDueNotWorse</th>
      <td>22.656445</td>
      <td>525.179814</td>
    </tr>
    <tr>
      <th>NumberRealEstateLoansOrLines</th>
      <td>3.752641</td>
      <td>71.087650</td>
    </tr>
    <tr>
      <th>NumberOfDependents</th>
      <td>1.598556</td>
      <td>3.178548</td>
    </tr>
    <tr>
      <th>NumberOfOpenCreditLinesAndLoans</th>
      <td>1.228632</td>
      <td>3.178869</td>
    </tr>
    <tr>
      <th>age</th>
      <td>0.186196</td>
      <td>-0.498428</td>
    </tr>
  </tbody>
</table>
</div>

* * Data distribution in the columns are highly right skewed with very high kurtosis value showing extreme outliers in those columns
* * Except age which is little normally distributed

* *From the above boxplot graphs we can observe:*
* **
* *In the columns NumberOfTime30-59DaysPastDueNotWorse , NumberOfTime60-89DaysPastDueNotWorse and NumberOfTimes90DaysLate, we see delinquency range beyond 90 which is common across all 3 features.*
* **
* *Treating outliers for the columns  --Debt Ratio, Age,  NumberOfTime30-59DaysPastDueNotWorse, NumberOfTime60-89DaysPastDueNotWorse and NumberOfTimes90DaysLate*

* Checking for DebtRatio

    <table>
  <thead>
    <tr>
      <th>Debt Ratio</th>
      <th>Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>count</td>
      <td>120000.000000</td>
    </tr>
    <tr>
      <td>mean</td>
      <td>352.271245</td>
    </tr>
    <tr>
      <td>std</td>
      <td>2093.709509</td>
    </tr>
    <tr>
      <td>min</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <td>25%</td>
      <td>0.175330</td>
    </tr>
    <tr>
      <td>50%</td>
      <td>0.366194</td>
    </tr>
    <tr>
      <td>75%</td>
      <td>0.860833</td>
    </tr>
    <tr>
      <td>max</td>
      <td>329664.000000</td>
    </tr>
  </tbody>
</table>

* The data is right skewed. So, we would check the potential outliers beyond 95% quantiles. However, since our data is 120,000,  we considerd 95% and 97.5% quantiles for our further analysis.


<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SeriousDlqin2yrs</th>
      <th>MonthlyIncome</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>6002.000000</td>
      <td>299.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.053149</td>
      <td>0.086957</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.224349</td>
      <td>0.282244</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</</th>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.000000</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>


 Observation
* Out of 6002 customers falling in the last 5 percentile of the data i.e. the number of times their debt is higher than their income, only 299 have Monthly Income values.
* The Max for Monthly Income is 1 and Min is 0 which makes us wonder that are data entry errors. Checking whether the Serious Delinquency in 2 years and Monthly Income values are equal.

260

* There are 260 out of 299 rows where Monthly Income is equal to the Serious Delinquencies in 2 years. Hence we remove these 260 outliers from our analysis as their current values aren't useful for our predictive modelling and will add to the bias and variance.

###    AGE

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>SeriousDlqin2yrs</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>119740.000000</td>
      <td>119740.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>52.292041</td>
      <td>0.066970</td>
    </tr>
    <tr>
      <th>std</th>
      <td>14.778070</td>
      <td>0.249971</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</</th>
      <td>41.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>52.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>63.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>109.000000</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>

* It can be observed that the data includes a record with age = 0 which is not a valid age ,updating the record with mode age.
* Replacing the error/odd value with the mode, that is 21.

###    NumberOfTime30-59, 60-89, 90DaysPastDueNotWorse

* The records in column 'NumberOfTime30-59, 60-89, 90DaysPastDueNotWorse' are more than 90, the other columns that records number of times payments are past due X days also have the same values.

![Uniquevalues.png](Uniquevalues.png)

* **
* Replacing them with the maximum value before 96 i.e. 12, 11 and 17*


![abc.png](abc.png)

#### Missing Value Treatment  

* Since MonthlyIncome is an integer value, replacing the nulls with the median values instead of mean as it was heavily right skewed.*
* Number of Dependents filling by mode which is 0.

### Correlation Matrix Analysis 
 
   ![Corelatiom.png](Corelation.png)
 
* From the correlation heatmap above, we can see the most correlated values to SeriousDlqin2yrs are NumberOfTime30-59DaysPastDueNotWorse , NumberOfTime60-89DaysPastDueNotWorse and NumberOfTimes90DaysLate.

* Number of Open Credit Lines and Loans and Number of Real Estate Loans or Lines also have a significant correlation

### Bivariate Analysis
<body>
    <h1>Box Plot and Violin Plot of Age</h1>
    <p>
        These plots compare the age distribution for individuals with and without serious delinquency in 2 years. The median age is lower for those with delinquency, with outliers present in both groups.
    </p>
</body>


![BI1.png ](BI1.png  )


<body>
    <h1>Box Plot and Violin Plot of NumberOfTime30-59DaysPastDueNotWorse</h1>
    <p>
        These plots show the distribution of the number of times 30-59 days past due not worse. The median is higher for those with delinquency, with significant outliers.
    </p>
</body>

![Bi4.png ](Bi4.png  )


 <body>
    <h1>Box Plot and Violin Plot of NumberOfTime60-89DaysPastDueNotWorse</h1>
    <p>
        These plots illustrate the number of times 60-89 days past due not worse. Higher incidence is observed in the serious delinquency group, with data heavily skewed towards zero.
    </p>
</body>

![Bi5.png ](Bi5.png  )

 
<body>
    <h1>Box Plot and Violin Plot of NumberOfTimes90DaysLate</h1>
    <p>
        These plots compare the number of times 90 days late between the two groups. The serious delinquency group shows more frequent late payments and more outliers.
    </p>
</body>

![Bi6.png ](Bi6.png  )


 

### Feature Engineering

* Combined features

  ```python
    data['CombinedPastDue']     = data['NumberOfTime30-59DaysPastDueNotWorse'] + data['NumberOfTime60-89DaysPastDueNotWorse'] + data['NumberOfTimes90DaysLate']
    data['CombinedCreditLoans'] = data['NumberOfOpenCreditLinesAndLoans'] + data['NumberRealEstateLoansOrLines']
  ```

 New_train.shape, New_test.shape
* [119542, 21] [29946, 21]

* New Features after feature Interaction 
 <table border="1" class="dataframe">
  <thead>
    <tr>
      <th>Index</th>
      <th>Columns</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>RevolvingUtilizationOfUnsecuredLines</td>
    </tr>
    <tr>
      <td>2</td>
      <td>age</td>
    </tr>
    <tr>
      <td>3</td>
      <td>NumberOfTime30-59DaysPastDueNotWorse</td>
    </tr>
    <tr>
      <td>4</td>
      <td>DebtRatio</td>
    </tr>
    <tr>
      <td>5</td>
      <td>MonthlyIncome</td>
    </tr>
    <tr>
      <td>6</td>
      <td>NumberOfOpenCreditLinesAndLoans</td>
    </tr>
    <tr>
      <td>7</td>
      <td>NumberOfTimes90DaysLate</td>
    </tr>
    <tr>
      <td>8</td>
      <td>NumberRealEstateLoansOrLines</td>
    </tr>
    <tr>
      <td>9</td>
      <td>NumberOfTime60-89DaysPastDueNotWorse</td>
    </tr>
    <tr>
      <td>10</td>
      <td>NumberOfDependents</td>
    </tr>
    <tr>
      <td>11</td>
      <td>SeriousDlqin2yrs</td>
    </tr>
    <tr>
      <td>12</td>
      <td>CombinedPastDue</td>
    </tr>
    <tr>
      <td>13</td>
      <td>CombinedCreditLoans</td>
    </tr>
    <tr>
      <td>14</td>
      <td>MonthlyIncomePerPerson</td>
    </tr>
    <tr>
      <td>15</td>
      <td>MonthlyDebt</td>
    </tr>
    <tr>
      <td>16</td>
      <td>isRetired</td>
    </tr>
    <tr>
      <td>17</td>
      <td>RevolvingLines</td>
    </tr>
    <tr>
      <td>18</td>
      <td>hasRevolvingLines</td>
    </tr>
    <tr>
      <td>19</td>
      <td>hasMultipleRealEstates</td>
    </tr>
    <tr>
      <td>20</td>
      <td>IsAlone</td>
    </tr>
  </tbody>
</table>


* Event rate of new dataset 
* 0.0670057385688712 , 0.06668670273158352

### Tackling Class Imbalance Problem using:
* **
    * Upsampling the minority class
    * Downsampling the majority class
    * SMOTE - synthethic sampling


#### Upsampling

![Upsampling.png ](Upsampling.png )

#### Downsampling

![Downsampling1.png ](Downsampling2.png  )

![Downsampling2.png ](Downsampling2.png  )

#### Smote

![Smote1.png ](Smote1.png  )

* Now the event rate in the training dataset is 50%

## Scaling
 * Log Transformation
 * Standaradization

#### Before Scaling Skewness Distribution
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>skew</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>MonthlyIncome</th>
      <td>152.433311</td>
    </tr>
    <tr>
      <th>MonthlyIncomePerPerson</th>
      <td>114.755089</td>
    </tr>
    <tr>
      <th>RevolvingUtilizationOfUnsecuredLines</th>
      <td>100.658816</td>
    </tr>
    <tr>
      <th>MonthlyDebt</th>
      <td>99.344320</td>
    </tr>
    <tr>
      <th>DebtRatio</th>
      <td>97.872765</td>
    </tr>
    <tr>
      <th>NumberOfTime60-89DaysPastDueNotWorse</th>
      <td>8.735995</td>
    </tr>
    <tr>
      <th>NumberOfTimes90DaysLate</th>
      <td>8.264560</td>
    </tr>
    <tr>
      <th>CombinedPastDue</th>
      <td>8.219034</td>
    </tr>
    <tr>
      <th>NumberOfTime30-59DaysPastDueNotWorse</th>
      <td>5.121509</td>
    </tr>
    <tr>
      <th>NumberRealEstateLoansOrLines</th>
      <td>3.598986</td>
    </tr>
    <tr>
      <th>isRetired</th>
      <td>2.558783</td>
    </tr>
    <tr>
      <th>NumberOfDependents</th>
      <td>1.412255</td>
    </tr>
    <tr>
      <th>hasMultipleRealEstates</th>
      <td>1.347083</td>
    </tr>
    <tr>
      <th>RevolvingLines</td>
      <td>1.280191</td>
    </tr>
    <tr>
      <th>NumberOfOpenCreditLinesAndLoans</td>
      <td>1.111764</td>
    </tr>
    <tr>
      <th>CombinedCreditLoans</td>
      <td>1.108994</td>
    </tr>
    <tr>
      <th>hasRevolvingLines</td>
      <td>-4.170414</td>
    </tr>
  </tbody>
</table>
</div>

#### After Scaling Skewness Distribution

<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>Index</th>
      <th>skew</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>RevolvingUtilizationOfUnsecuredLines</td>
      <td>10.123458</td>
    </tr>
    <tr>
      <td>NumberOfTime60-89DaysPastDueNotWorse</td>
      <td>4.190228</td>
    </tr>
    <tr>
      <td>NumberOfTimes90DaysLate</td>
      <td>3.325071</td>
    </tr>
    <tr>
      <td>isRetired</td>
      <td>2.558783</td>
    </tr>
    <tr>
      <td>DebtRatio</td>
      <td>1.895761</td>
    </tr>
    <tr>
      <td>NumberOfTime30-59DaysPastDueNotWorse</td>
      <td>1.858490</td>
    </tr>
    <tr>
      <td>CombinedPastDue</td>
      <td>1.445872</td>
    </tr>
    <tr>
      <td>hasMultipleRealEstates</td>
      <td>1.347083</td>
    </tr>
    <tr>
      <td>MonthlyDebt</td>
      <td>0.740007</td>
    </tr>
    <tr>
      <td>NumberOfDependents</td>
      <td>0.715397</td>
    </tr>
    <tr>
      <td>NumberRealEstateLoansOrLines</td>
      <td>0.504881</td>
    </tr>
    <tr>
      <td>RevolvingLines</td>
      <td>-0.763235</td>
    </tr>
    <tr>
      <td>NumberOfOpenCreditLinesAndLoans</td>
      <td>-0.885374</td>
    </tr>
    <tr>
      <td>CombinedCreditLoans</td>
      <td>-0.934095</td>
    </tr>
    <tr>
      <td>MonthlyIncomePerPerson</td>
      <td>-3.747514</td>
    </tr>
    <tr>
      <td>hasRevolvingLines</td>
      <td>-4.170414</td>
    </tr>
    <tr>
      <td>MonthlyIncome</td>
      <td>-5.001298</td>
    </tr>
  </tbody>
</table>

<body>
    <h1>Density Plots of Features</h1>
    <p>
        This image displays the density plots for various features in the dataset.
    </p>
    <ul>
        <li>Features include <strong>RevolvingUtilizationOfUnsecuredLines</strong>, <strong>age</strong>, <strong>NumberOfTime30-59DaysPastDueNotWorse</strong>, among others.</li>
        <li>The density plots help visualize the distribution of each feature.</li>
        <li>Many features exhibit skewed distributions, indicating potential outliers or non-normal distributions.</li>
        <li>Features like <strong>MonthlyIncome</strong> and <strong>NumberOfDependents</strong> show high variance.</li>
    </ul>
</body>

![AfterScaling.png ](AfterScaling.png  )

# Model Performance Comparison

## Training Log Transformed Dataset using ML Algorithms
- **Random Forest**: Highest mean accuracy (0.916), high precision, and recall.
- **Logistic Regression**: Lower accuracy (0.79) but decent precision and recall.
- **Decision Tree**: Moderate accuracy (0.859) with lower precision and recall compared to Random Forest.

## Training Standardized Dataset using ML Algorithms
- **Random Forest**: Highest mean accuracy (0.917), high precision, and recall.
- **Logistic Regression**: Improved accuracy (0.814), good precision, and recall.
- **Decision Tree**: Moderate accuracy (0.86) with lower precision and recall compared to Random Forest.

![LOGML.png ](LOGML.png  )

* Training Standaradized dataset using ML algorithms
  
![Standard.png ](Standard.png  )


<body>
    <h1>Receiver Operating Characteristic (ROC) Curve</h1>
    <p>
        The ROC curve compares the performance of three models: Random Forest, Logistic Regression, and Decision Tree.
    </p>
    <ul>
        <li><strong>Random Forest</strong>: Highest AUC (0.83), indicating the best performance.</li>
        <li><strong>Logistic Regression</strong>: Moderate AUC (0.78), showing good performance.</li>
        <li><strong>Decision Tree</strong>: Lowest AUC (0.64), indicating lower performance.</li>
    </ul>
    <p>
        The curve plots sensitivity (true positive rate) against 1-specificity (false positive rate) for each model.
    </p>
</body>

![ROCCurve.png ](ROCCurve.png  )

 <body>
    <h1>Random Forest Feature Importance</h1>
    <p>
        <ul>
            <li><strong>RevolvingUtilizationOfUnsecuredLines</strong> is the most important feature.</li>
            <li>Significant features include <strong>CombinedPastDue</strong> and <strong>NumberOfTime30-59DaysPastDueNotWorse</strong>.</li>
            <li>Features like <strong>IsAlone</strong> and <strong>hasMultipleRealEstates</strong> have low importance.</li>
        </ul>
    </p>
</body>

   
![FeatureImportance.png ](FeatureImportance.png  )


<body>
    <h1> Logistic Regression </h1>
    <p>
        <ul>
            <li>Positive coefficients: <strong>CombinedPastDue</strong> and <strong>NumberOfTime30-59DaysPastDueNotWorse</strong> increase likelihood.</li>
            <li>Negative coefficients: <strong>age</strong> and <strong>RevolvingLines</strong> decrease likelihood.</li>
            <li>The chart shows the relative importance of features.</li>
        </ul>
    </p>
</body>

![FeatureLogic.png ](FeatureLogic.png  )



<body>
    <h1>Decision Tree Feature Importance</h1>
    <p>
        <ul>
            <li><strong>RevolvingUtilizationOfUnsecuredLines</strong> is the top feature.</li>
            <li>Notable features are <strong>MonthlyDebt</strong> and <strong>CombinedCreditLoans</strong>.</li>
            <li><strong>IsAlone</strong> and <strong>hasMultipleRealEstates</strong> show minimal importance.</li>
        </ul>
    </p>
</body>
 ![FeatureDescsion Tree.png ](FeatureDecisionTree.png  )

<body>
    <h1>Prediction Probabilities</h1>
    <p>
        This image displays the prediction probabilities and feature contributions for a model.
    </p>
    <ul>
        <li>Prediction probabilities for classes 0 and 1 are 0.25 and 0.75, respectively.</li>
        <li>Key features influencing the prediction include <strong>CombinedPastDue</strong>, <strong>RevolvingUtilizationOfUnsecuredLines</strong>, and <strong>NumberOfTimes90DaysLate</strong>.</li>
        <li>The values of features such as <strong>age</strong>, <strong>MonthlyIncomePerPerson</strong>, and <strong>isRetired</strong> are shown.</li>
    </ul>
</body>

![Prediction2.png ](Prediction2.png  )
<body>
    <h1>Prediction Probabilities</h1>
    <p>
        This image displays the prediction probabilities and feature contributions for a model.
    </p>
    <ul>
        <li>Prediction probabilities for classes 0 and 1 are 0.73 and 0.27, respectively.</li>
        <li>Key features influencing the prediction include <strong>CombinedPastDue</strong>, <strong>NumberOfTimes90DaysLate</strong>, and <strong>NumberOfTime30-59DaysPastDueNotWorse</strong>.</li>
        <li>The values of features such as <strong>age</strong>, <strong>MonthlyIncomePerPerson</strong>, and <strong>isRetired</strong> are shown.</li>
    </ul>
</body>



![Prediction1.png ](Prediction1.png  )

<body>
    <h1>Conclusion</h1>
    <p>The analysis and model development have successfully demonstrated the ability to predict the likelihood of serious delinquency in the next two years using borrower profiles and historical data. The Random Forest model showed the highest accuracy and AUC, indicating its robustness for this prediction task. Key features such as RevolvingUtilizationOfUnsecuredLines, CombinedPastDue, and NumberOfTime30-59DaysPastDueNotWorse were identified as significant predictors.</p>
     <p>
    <h2>Future Scope</h2>
    <p>Future work can focus on the following aspects to enhance the model's performance and applicability:</p>
    <ul>
        <li><strong>Feature Engineering:</strong> Further refinement and creation of new features to capture complex patterns.</li>
        <li><strong>Model Tuning:</strong> Experimenting with hyperparameter tuning and advanced ensemble methods to improve prediction accuracy.</li>
        <li><strong>Real-Time Prediction:</strong> Developing a real-time prediction system that can be integrated into banking applications for instant risk assessment.</li>
        <li><strong>Explainability:</strong> Implementing techniques like SHAP values to provide more transparency and explainability to model predictions.</li>
        <li><strong>Additional Data:</strong> Incorporating more granular data such as transaction history, employment details, and credit score changes over time for more accurate predictions.</li>
    </ul>
</body>

