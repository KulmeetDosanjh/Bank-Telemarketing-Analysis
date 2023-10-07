# Exploratory-Data-Analysis-Bank Loan CaseStudy
• This Case Study is basically from the Fintech industry. Banks and Fin-techs have to struggle a lot while 
  giving loans to clients/customers having insufficient credit history. 
• Due to lack of insufficient credit history some customers makes advantage and proves to be a defaulter by 
  not repaying the loan amounts on time. 
• This Case Study is aimed to analyze data on various factors such as income of the client, family status, past 
  loans etc to derive insights and see whether a particular customer will be able to repay the loan or not. 
• This decision making is important because companies don’t want to give loan to customers which might
  prove to be a defaulter and on the other hand they don’t want to miss on the customers who can repay
  the loan. 
• In short we will analyze the variables and bring out the driving factors which could lead to Defaulter in 
  repayment of loan.
## Assumptions: 
• I have tried to keep as many columns as I can. I have done a pre assignment research on different platforms like google and 
  went through many financial blogs to spot variables which mainly affects loan’s approval. 
• I myself is a Data Engineer in a Audit firm and I tried to connect with people from financial background to get knowledge of 
  various factors and how it could affect the analysis. 
• I have tried keeping as many columns as I could, except the columns having to many null values(40% and above) 
• I have not removed XNA and XAP values by considering as null 
• I have also gone through the data Dictionary provided and tried dropping columns that don’t make sense in our analysis 
  like the columns WEEKDAY_APPR_PROCESS_START, HOUR_APPR_PROCESS_START etc. 
• I have done data cleaning such as missing value treatment, outlier treatment etc of both the files individually and then 
  merged the file. 
• However I have tried analysing columns from app_data file with respect to TARGET column and columns in 
  previous_application with respect to NAME_CONTRACT_STATUS respectively.
## STEPS IN ANALYSIS: 
### Understanding the Domain/variables: 
• Before starting the Analysis it is very important to go through the data dictionary provided to understand the 
  attributes and also I did some research on the variables that banks and financial institutes evaluates before 
  approving loans so that I focus on those particular attributes more. 
• I have spent a good amount od time just to gain some domain knowledge so that I can bring out the best 
  insights from the data. 
### Import/Load the Data: 
• I have then loaded both the files into the pandas dataframe for Analysis.
  Check the Structure/Metadata of the data: 
• It is very important to check on few things before starting with the analysis. We should be aware of the shape 
  and size of the dataframe, we should also know the datatypes of the variables we have and if some datatype 
  is needs a change we should go ahead and change the data types. In this assignment all the columns were 
  already in correct format. 
• I have used functions like shape and info() for metadata Analysis. 
### Missing Value Check and Imputation: 
• There were lot of columns in app_data file that were missing. I have taken 40% as a threshold and after 
  proper research the what impact a particular column could make to my analysis I have dropped columns. 
• After dropping the columns I have checked the dataframe for the presence of null values using 
  df.isnull().sum().
• I have replaced nulls by ‘Retired’ for people NAME_INCOME_TYPE as pensioners.
• In previous_application file I have tried to replace missing values in most of the columns with default values like 0 or a 
  negative number. 
• The thought process in this is that for example if we see AMT_DOWN_PAYMENT column most of the blanks are for 
  NAME_CONTRACT_TYPE as Cash loans or Revolving loans. After some research I came to know that Most of the Cash 
  loans and Revolving loans typically does not need a down payment so the column might be left as null. Similarly 
  RATE_DOWN_PAYMENT is also null on similar places, so that is also replaces by 0. 
• AMT_GOODS_PRICE is also replaced with default value 0 as nulls are at places where NAME_CONTRACT_STATUS is 
  Cancelled 
• For AMT_ANNUITY in previous application file I am replacing nulls with 0.0 only where NAME_CONTRACT_STATUS is 
  Cancelled because if it would beApproved, Unused offer or Refused Annuity should have been there because the offer 
  was given.
### Value Conversion: 
• There are lot od columns in app_data file whose value is relative to loan signing date like DAYS_EMPLOYED, 
  DAYS_REGISTRATION, DAYS_ID_PUBLISH, DAYS_BIRTH. These are negative values so I have converted them 
  into positive absolute value in the form of years by dividing them by 365 and rounding them off 
  appropriately. 
• I have also used binning technique to convert numerical columns such as AGE(DAYS_BIRTH), 
  Total_Experience(DAYS_EMPLOYED), AMT_INCOME_TOTAL, AMT_CREDIT to categorical columns for better 
  insights.
### OUTLIER TREATMENT 
• I have analysed almost all the numerical columns for outliers 
• I have used box plot in order to visualize the outliers. 
• For some columns like AMT_CREDIT, AMT_ANNUITY, AMT_GOODS_PRICE etc the outliers are continuous the 
  this huge credit and Annuity are given to people with good income so it looked genuine value , for such values 
  I have not dropped the outliers 
• For some values such as AMT_TOTAL_INCOME and AMT_DOWN_PAYMENT the outliers are not continuous 
  and too far from the inter quartile range so I have removed these outliers from where the continuity of 
  outliers was broken. 
• In previous_application file also I have tried to analyse the numerical columns using box plots and taking in 
  consideration the continuity of data and how far is outlier points away from inter quartile range I have 
  dropped values from AMT_ANNUITY, AMT_CREDIT, AMT_DOWN_PAYMENT etc.
### DATA IMBALANCE: 
  Data Imbalance is seen when one Target value dominates over the other. In this case study we can see there is a data 
  imbalance as TARGET 0(Non Default Cases) are is dominating over TARGET 1(Deafult Cases). TARGET 0 is approximately 91% 
  of the data. 
### UNIVARIATE ANALYSIS: 
• For Univariate Analysis I have tried to plot count plot and bar plot for each major variable with respect to TARGET in for 
  app_data file and a similar kind of approach I have taken for variables in previous data_application data.This helped me 
  give a holistic view of each category present inside a column under Analysis with respect to TARGET.
### BIVARIATE ANALYSIS/MULTIVARIATE ANALYSIS 
For bivariate and multivariate analysis I have used a combination of scatter plot and line plots, to find correlation 
between different columns I have used correlation heatmaps. I have also used pair plots and to find correlation amongs 
few important columns such as AMT_TOTAL_INCOME, AMT_ANNUITY etc with each other and also with the TARGET. 
Some important visualizations are shown below. In the below graphs 1 represents defaulters while 0 represents non 
defaulter cases.
### Factors for Repayment: 
1. NAME_INCOME_TYPE: Students and Business men are the best category to give loans with no defaulters. 
2. CODE_GENDER: Females have better probability of return loan amount. 
3. AMT_INCOME_TOTAL: People with income more than 6LPA and above have less probability of default 
4. NAME_EDUCATION_TYPE: People with Academic degree is more likely to pay loan on time. 
5. REGION_RATING_CLIENT: People living in area rated as 1 makes least defaults. 
6. OCCUPATION_TYPE: Least defaults are made by people working as accountants. 
7. AGE: People who are 40 years plus have less probability of being a defaulter 
8. DAYS_EMPLOYED: People having 40 plus years of experience have least defaulter case 
9. CNT_CHILDREN: People having 0 to 2 kids have least probability of making a defaulter case. 
10. CNT_FAM_MEMBERS: People with lesser family members have more probability of repaying loans 
11. NAME_HOUSING_TYPE: people living in office apartment is more likely to replay the loan on time.
### Factors for Defaulter: 
1. NAME_INCOME_TYPE: Customer in category Maternity leave and Unemployed has highest defaulter cases.. 
2. CODE_GENDER: Men have more probability of not returning loan amount on time. 
3. AMT_INCOME_TOTAL: People with income less than 6LPA and have more probability of default 
4. NAME_EDUCATION_TYPE: People with lower secondary or secondary education are more likely to be a defaulter. 
5. REGION_RATING_CLIENT: People living in area rated as 3 makes the most defaults. 
6. OCCUPATION_TYPE: Most defaults are made by Low skill laborers and Drivers. 
7. AGE: People having age between 20 to 40 are more likely to make defaulter case. 
8. DAYS_EMPLOYED: People having less than 5 years of experience have most defaulter cases. 
9. CNT_CHILDREN: People having kids more than 9 have highest probability of making a defaulter case. 
10. CNT_FAM_MEMBERS: People having members more than 10 have highest probability of making a defaulter case. 
11. NAME_FAMILY_STATUS: people having civil marriage or are single have more probability of defaulter. 
12. NAME_HOUSING_TYPE: People living with parents the the most in defaulter cases followed by those who lives in 
rented apartments. 
13. AMT_CREDIT: People getting loan between 300000 to 600000 makes the most default cases

