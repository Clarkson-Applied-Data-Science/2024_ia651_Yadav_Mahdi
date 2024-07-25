* **Business Context** - Banks are primarily known for money lending business. The more money they lend to people whom they can get good interest with timely repayment, the more revenue is for the banks.
* **
* The more banks are able to identify borrowers going towards serious delinquency rate, the better will be the bank's money lending business which in turn will lead to better revenue and better image in the market and with respect to competitiors. 
* **
* * **Delinquent** in general is a slightly mild term where a borrower is not repaying charges and is behind by certain months whereas * **Default** is a term where a borrower has not been able to pay charges and is behind for a long period of months and is unlikely to repay the charges.
* **
* We have a general profile about the borrower such as age, Monthly Income, Dependents and the historical data such as what is the Debt Ratio, what ratio of amount is owed wrt credit limit, and the no of times defaulted in the past one, two, three months.
* We will be using all these features to predict whether the borrower is likely to delinquent in the next 2 years or not.
* These kind of predictions will help banks to take necessary actions.

***
* **Objective** : Building a model using the inputs/attributes which are general profile and historical records of a borrower to predict whether one is likely to have serious delinquency in the next 2 years 



<pre><code class="python">print(df['SeriousDlqin2yrs'].unique())
percentage_Serious_Deliquency = (df['SeriousDlqin2yrs']).sum()/ len(df) * 100
print('{}% of the borrrowers are failing in Serious Delinquency'.format(percentage_Serious_Deliquency))</code></pre>

<p>[1 0]
6.683999999999999% of the borrrowers are failing in Serious Delinquency</p>


## Data Analysis: Serious Delinquency in 2 Years


