# Bank Marketing Campaign Predictive Modeling

## Section 1: Understanding the Dataset

About the dataset - Find the best strategy to improve the next marketing campaign

Link: https://www.kaggle.com/janiobachmann/bank-marketing-dataset

**Data Description**

1 - Age<br/>
2 - Job: Type of job (categorical: 'admin.','blue-collar','entrepreneur','housemaid','management','retired','self-employed','services','student','technician','unemployed','unknown')<br/>
3 - Marital: marital status (categorical: 'divorced','married','single','unknown'; note: 'divorced' means divorced or widowed)<br/>
4 - Education: (categorical: primary, secondary, tertiary and unknown)<br/>
5 - Default: has credit in default? (categorical: 'no','yes','unknown')<br/>
6 - Housing: has housing loan? (categorical: 'no','yes','unknown')<br/>
7 - Loan: has personal loan? (categorical: 'no','yes','unknown')<br/>
8 - Balance: Balance of the individual<br/>
9 - contact: contact communication type (categorical: 'cellular','telephone')<br/>
10 - month: last contact month of year (categorical: 'jan', 'feb', 'mar', ..., 'nov', 'dec')<br/>
11 - day: last contact day of the week (categorical: 'mon','tue','wed','thu','fri')<br/>
12 - duration: last contact duration, in seconds (numeric)<br/>
13 - campaign: number of contacts performed during this campaign and for this client (numeric, includes last contact)<br/>
14 - pdays: number of days that passed by after the client was last contacted from a previous campaign (numeric; 999 means client was not previously contacted)<br/>
15 - previous: number of contacts performed before this campaign and for this client (numeric)<br/>
16 - poutcome: outcome of the previous marketing campaign (categorical: 'failure','nonexistent','success')<br/>
17 - y - has the client subscribed a term deposit? (binary: 'yes','no')<br/>

## Section 2: Exploratory Data Analysis (EDA)

1. Summary Statistics </br>

![1](https://user-images.githubusercontent.com/54965123/75123675-be2df000-5677-11ea-93e3-6dcc6990b97e.PNG)

2. Notes from Pandas Profiling</br>

- 11k rows </br>
- There are no missing values</br>
- There are no duplicate rows </br>
- Some outliers in the field 'balance' </br>
- Just one percent of the rows had a default</br>

3. Just 13% of the customers took loan </br>

![3](https://user-images.githubusercontent.com/54965123/75123677-bec68680-5677-11ea-86cb-fd97661fdf91.PNG)

4. Just 1.5% of the data points defaulted </br>

![2](https://user-images.githubusercontent.com/54965123/75123676-be2df000-5677-11ea-971c-3e3860ed14a4.PNG)

5. Those who default have low balance in their account </br>

![4](https://user-images.githubusercontent.com/54965123/75123743-43b1a000-5678-11ea-84d0-b43a53f01f71.PNG)

## Section 3: Data Pre-processing

Steps: </br>

1. Create target variables </br>
2. Drop the original target variable columns </br>
3. Encode the columns containing 'yes' and 'no' values </br>
4. Correlation check </br>
5. Separate features and target </br>
6. Standardization </br>
7. Train and Test split </br>

## Section 4: Model Building

### Results

![6](https://user-images.githubusercontent.com/54965123/75124052-9db36500-567a-11ea-8b34-1e0d506dbbc7.png)

## Section 5: Fairness-Bias Check using SHAP values

![7](https://user-images.githubusercontent.com/54965123/75124053-9e4bfb80-567a-11ea-9d27-51be063fa67d.png)

## Section 6: Understanding Causal Inference

### Chi square

![5](https://user-images.githubusercontent.com/54965123/75123862-3d6ff380-5679-11ea-81fc-49a7207a77d1.PNG)

Interpretation - 
The chart above visualizes our sample data. If there is truly no effect of the campaign by looking at the number of depsotis before it occured and after, then the data would show an even ratio split between 'deposit' and 'no deposit' for each time.</br>

**chi-square and p-value**
The chisquared value = 0.00824, p-value = ~1 and degrees of freedom = 2. With a p-value =1 , we are not able to reject the null hypothesis. This means that the campaign does not effect the number of deposits. Note that these numbers vary every time since we do not set a random split. In fact, re-running the code should yield wildly different answers. Therefore, we can expect that, depending on the split, the campaing to have or not to have an effect. As mentionned prior, the ideal scenario would be to use this dataset as past data and use data after a new campaign to asses the effect.

## Section 7: DoWhy: Double Machine Learning for Causal Inference

**Stratification**

The hypothesis we are looking to research is whether there or not there is a causal relationship between age and weather an individual will deposit. </br>
Looking only at AGE as a treatment variable, it seems that the causal effect of AGE is 0.001814747418610118. This would mean that for every unit increase in AGE, the probability that someone depsoits goes up by 0.18%. </br>
While this may seem shocking for some, this is likely not realistic. There may be some non-linearity effects or we must test using another method.</br>

**Regression**

The hypothesis we are looking to research is whether there or not there is a causal relationship between AGE and deposit_bool. </br></br>
We also look at the causal relationship of other predictors on depsoit_bool (such as "job" and "default"). </br></br>
Looking at AGE as the treament variable, we see that first it is a significant treamtent variable within 10% (p < 0.094) and its effect using a linear regression model is -0.0006593246127298835. </br></br>
This would imply that for every unit increase in AGE, the probability of someone depositing goes down by 0.07%. This estimate is much more realistic, as it seems ther is no age bias anymore. </br></br>
Here is the causal effect of each variable on the odds of depsoiting (deposit_bool) and the associated p-value: </br></br>
age = 0.001596470177772813 (p = 0.0010000000000000009)</br>
marital = -0.08611891032763919 (p < 0.001)</br>
balance = 0.1030394858277377 (p < 0.001)</br>
education (tertiary) = 0.06589147843681609 (p < 0.001)</br>
default = -0.08093474884816493 (p = 0.016)</br>
housing = -0.17525694004024445 (p < 0.001)</br>
loan = -0.11660829943692341 (p < 0.001) </br></br>
The biggest anomaly is the causal effect of housing. "housing" denotes if someone has a housing loan. The causal effect seems that if someone does has made a housing loan, the odds of them making a deposit after a marketing campaing goes down by 17%. This seems quite steep at first but, with reason makes sense. Someone that takes a housing loan is likely to have an account and funds are a major issue. Thus, when we run the campaign, the individual does not feel inclined to deposit but rather save up (or remain in their current situtaiton. Additionally, there might be some non-linear effect that is not captured properly.</br>

