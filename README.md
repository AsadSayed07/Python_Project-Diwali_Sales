# Python Project - Diwali Sales Analysis

<p align="center">
  <img src="https://github.com/AsadSayed07/Python_Project-Diwali_Sales/blob/main/diwali%20sale.png?raw=true" height = 350 width= 600 >

## OVERVIEW
In this project we will work on the "Diwali Sales Dataset" which is a data set containing information about the sales done during the occassion of Diwali based on different factors. It covers an end-to-end process of understanding the dataset, uploading the file on **Jupyter Notebook** and using **Python librarires** like **Pandas**, **Matplotlib** and **Seaborn** for data analysis. The primary goal of this project is to use python libraries and generate valuable insights from the dataset.

## STEPS TAKEN TO DO THE PROJECT

### 1. DATA EXPLORATION
Before working on the dataset, it is important to understand the data thoroughly. The dataset contains attributes such as:
- `User id`, `Customer Name`, `Product ID`, `Gender`, `Age Group`, `Age`, `Marital Status`, `State`, `Zone`, `Occupation`, `Product Category`, `Orders`, `Amount`.

### 2. CLEANING THE DATASET
After seeing the attributes, the dataset had to be cleaned and organized.

### 3. IMPORTING THE REQUIRED LIBRARIES FOR ANALYSIS
Imported Python Libraries for the following purpose:
- **Pandas** - For analyzing the dataset and solving the questions
- **Matplotlib** & **Seaborn** - For Graphical and Other Visual Representations

## CLEANING THE DATASET
```vim
---removing columns "status" and "unanmed" from the data
df.drop(["Status","unnamed1"], axis=1, inplace=True)
```

```vim
---finding total number of null values 
pd.isnull(df).sum()
```

```vim
--removing the null values from the data
df.dropna(inplace=True)
```

###

## THE ANALYSIS IS DONE BASED ON VARIOUS FACTORS <br> *(mentioned in their respective headers)*

## GENDER ANALYSIS
```vim
---overview of all the columns
df.columns

---creating a bar chart showing the total count of Males and Females
ax = sns.countplot(x = "Gender", data = df)
for bars in ax.containers:
    ax.bar_label(bars)
```
![Gender Count](https://github.com/user-attachments/assets/ea0860b7-3407-463c-9c66-427e0a0fb9d0)

```vim
---Finding the amount spent by males and females respectively
df.groupby(["Gender"], as_index = False) ["Amount"].sum().sort_values(by = "Amount", ascending =False)

---creating a bar chart showing the amount spent by both males and females respectively.
sales_gen = df.groupby(["Gender"], as_index=False) ["Amount"].sum().sort_values(by = "Amount", ascending = False)
sns.barplot(x="Gender", y="Amount", data= sales_gen)
```
![Amount by Gender](https://github.com/user-attachments/assets/d842e77c-2c24-439f-8630-01e9764f009a)

***From the above two graphs we can see that there are more female buyers than male buyers. Also, females have a greater purchasing power.***


###

## AGE GROUP ANALYSIS
```vim
---overview of all the columns
df.columns

---creating a bar chart showing the total count of different age groups
sns.countplot(x="Age Group", data = df)
```
![Age Group Count](https://github.com/user-attachments/assets/b0a47768-65f0-442f-a20e-c0d9dfbf476a)

```vim
---creating a bar chart showing the total count of different age groups, gender-wise
ax = sns.countplot(x = "Age Group", hue = "Gender", data = df)
for bars in ax.containers:
    ax.bar_label(bars)
```
![Age Group by Gender](https://github.com/user-attachments/assets/8122735d-48c9-4602-af88-ec05a066be20)

```vim
---creating a bar chart showing the amount spent by different age groups respectively.
sales_age = df.groupby(["Age Group"], as_index = False) ["Amount"].sum().sort_values(by = "Amount", ascending=False)
sns.barplot(x = "Age Group", y= "Amount", data = sales_age)
```
![Age Group by Amount](https://github.com/user-attachments/assets/601b73ea-ebe0-444e-841e-c83af887acfe)

***From the above graph we can see that most of the buyers are from the age group 26-35yrs old Females.***

###

## STATE-WISE ANALYSIS
```vim
---overview of all the columns
df.columns

---finding the total number of order from top 10 states
orders_state = df.groupby(["State"], as_index=False) ["Orders"].sum().sort_values(by = "Orders", ascending = False).head(10)
sns.set(rc={"figure.figsize":(16,5)})
sns.barplot(x = "State", y = "Orders", data = orders_state)
```
![Orders by state](https://github.com/user-attachments/assets/f0edbaca-ef84-44b0-9216-30a25b1499f8)

```vim
---finding the total amount/ sales from the top 10 states
sales_state = df.groupby(["State"], as_index= False) ["Amount"].sum().sort_values(by="Amount", ascending = False).head(10)
sns.set(rc={"figure.figsize":(16,5)})
sns.barplot(x = "State" , y = "Amount", data = sales_state)
```
![Amount by state](https://github.com/user-attachments/assets/5dd9538d-7810-4060-a53d-74322998d1f3)

***From the above graphs we can see that most orders are from Uttar Pradesh, Maharashtra, and Karnataka respectively.***

###

## ANALYSIS BY MARITAL STATUS
```vim
---count of people that are married "0" and unmarried "1" respectively.
ax = sns.countplot(x = "Marital_Status", data = df)
sns.set(rc = {"figure.figsize":(4,5)})
for bars in ax.containers:
    ax.bar_label(bars)
```
![Marital Status](https://github.com/user-attachments/assets/45070930-5bf6-4b1b-894e-19987c641de5)

```vim
---Amount spent by people that are married "0" and unmarried "1" respectively.
sales_mar = df.groupby(["Marital_Status"], as_index = False) ["Amount"].sum().sort_values(by = "Amount",ascending=False)
sns.barplot(x = "Marital_Status", y="Amount", data = sales_mar)
```
![Marital status by amount](https://github.com/user-attachments/assets/aa1bf62b-d5ab-403c-96d8-a5016fbf7c7e)

```vim
---Amount spent by people that are married "0" and unmarried "1" respectively based on their gender
sales_margend = df.groupby(["Marital_Status", "Gender"], as_index=False) ["Amount"].sum().sort_values(by = "Amount", ascending = False)
sns.barplot(x="Marital_Status", y="Amount", data = sales_margend, hue = "Gender")
```
![Marital status by amount and Gender](https://github.com/user-attachments/assets/745a6c72-3b6d-48f9-8060-145135528184)

***From the above graphs we can see that Married Females hold the highest purchasing power.***

###

## OCCUPATION ANALYSIS
```vim
---overview of all the columns
df.columns
```
```vim
---count of people on the basis of their respective occupation.
ax = sns.countplot(x = "Occupation", data = df)
sns.set(rc={"figure.figsize":(21,6)})
for bars in ax.containers:
    ax.bar_label(bars)
```
![count of occupation](https://github.com/user-attachments/assets/a9ddf1f2-bd68-48f0-bbd1-8f4b7a57ffef)

```vim
---Amount spent by people on the basis of their respective occupation.
sales_occ = df.groupby(["Occupation"], as_index=False) ["Amount"].sum().sort_values(by = "Amount", ascending = False)
sns.barplot(x = "Occupation", y = "Amount", data = sales_occ)
```
![Amount by occupation](https://github.com/user-attachments/assets/e72f249c-24f9-4792-b3d5-f50db08dd7c4)

***From the above graphs we can see that the IT Sector, Healthcare Sector and Aviation Sector have recorded the highest purchases.***

###

## PRODUCT CATEGORY-BASED ANALYSIS
```vim
---overview of all the columns
df.columns
```

```vim
---count of Product Categories
ax = sns.countplot(x="Product_Category", data = df)
sns.set(rc={"figure.figsize":(30,5)})
for bars in ax.containers:
    ax.bar_label(bars)
```
![count of product categories](https://github.com/user-attachments/assets/05fab156-d357-42ea-a265-6d4ef55f12d7)

```vim
---amount/sales of Product Categories
sales_pc = df.groupby(["Product_Category"], as_index=False)["Amount"].sum().sort_values(by="Amount",ascending=False)
sns.barplot(x="Product_Category", y="Amount", data = sales_pc)
```
![sales of product categories](https://github.com/user-attachments/assets/10d1c428-7adc-4a3a-aa7f-b553e4a7647a)

***From the above graphs we can see that Clothes, food and electronic gadgets are bought more in their respective order however, the amount is spent more on food than on clothes.***
###

## PRODUCT_ID ANALYSIS
```vim
---overview of all the columns
df.columns
```

```vim
---top 10 products purchased
sales_product = df.groupby(["Product_ID"], as_index=False) ["Amount"].sum().sort_values(by = "Amount", ascending= False).head(10)
sns.set(rc = {"figure.figsize":(15,5)})
ax = sns.barplot(x="Product_ID", y = "Amount", data = sales_product)
for bars in ax.containers:
    ax.bar_label(bars)
```
![top 10 product id](https://github.com/user-attachments/assets/25ea379c-0dc5-4a62-aeaf-6501121f0129)

***Product_ID:P00265242 has the highest sales amounting to Rs. 5,40,136***

###

## TECHNOLOGY STACK
- **Database**: Jupyter Notebook
- **Tools**: Jupyter Notebook, Python, Pandas, Matplotlib, Seaborn





