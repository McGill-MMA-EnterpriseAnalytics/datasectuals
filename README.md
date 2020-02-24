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

Baseline model result - 

## Section 5: Understanding Causal Inference

### Chi square

![5](https://user-images.githubusercontent.com/54965123/75123862-3d6ff380-5679-11ea-81fc-49a7207a77d1.PNG)

Interpretation - 
The chart above visualizes our sample data. If there is truly no effect of the campaign by looking at the number of depsotis before it occured and after, then the data would show an even ratio split between 'deposit' and 'no deposit' for each time.



