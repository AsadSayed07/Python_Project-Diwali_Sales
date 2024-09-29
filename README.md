# Python Project - Diwali Sales Analysis

<img src="https://github.com/AsadSayed07/Python_Project-Weather_Data_Analysis/blob/main/weather_image.jpg?raw=true" width="1000" height="300">

## OVERVIEW
In this project we will work on the "Diwali Sales Dataset" which is a data set containing information about the sales done during the occassion of Diwali based on different factors. It covers an end-to-end process of understanding the dataset, uploading the file on **Jupyter Notebook** and using **Python librarires** like **Pandas**, **Matplotlib** and **Seaborn** for data analysis. The primary goal of this project is to use python libraries and generate valuable insights from the dataset.

## STEPS TAKEN TO DO THE PROJECT

### 1. DATA EXPLORATION
Before working on the dataset, it is important to understand the data thoroughly. The dataset contains attributes such as:
- `User id`, `Customer Name`, `Product ID`, `Gender`, `Age Group`, `Age`, `Marital Status`, `State`, `Zone`, `Occupation`, `Product Category`, `Orders`, `Amount`.

### 2. UPLOADING THE CSV FILE
After seeing the attributes, I uploaded the CSV file to Jupyter Notebook.

### 3. IMPORTING THE REQUIRED LIBRARIES
Imported Python Libraries for the following purpose:
- **Pandas** - For analyzing the dataset and solving the questions
- **Matplotlib** & **Seaborn** - For Graphical and Other Visual Representations

## THE ANALYSIS IS DONE BASED ON VARIOUS FACTORS <br> *(mentioned in their respective headers)*

**GENDER ANALYSIS**
```vim
---overview of all the columns
df.columns

---creating a bar chart showing the total count of Males and Females
ax = sns.countplot(x = "Gender", data = df)
for bars in ax.containers:
    ax.bar_label(bars)

---Finding the amount spent by males and females respectively
df.groupby(["Gender"], as_index = False) ["Amount"].sum().sort_values(by = "Amount", ascending =False)

---creating a bar chart showing the amount spent by both males and females respectively.
sales_gen = df.groupby(["Gender"], as_index=False) ["Amount"].sum().sort_values(by = "Amount", ascending = False)
sns.barplot(x="Gender", y="Amount", data= sales_gen)
```

Q2. **Find the number of times when the "Weather" is "Exactly Clear"**
```vim
#Value Counts
print("The weather was clear", df["Weather Condition"].value_counts()["Clear"],"times")

#Filtering
print("The weather was clear",len(df[df["Weather Condition"] == "Clear"]),"times")

#Group by
print("The Weather was exactly clear",len(df.groupby("Weather").get_group("Clear")),"times")
```
Q3. **Find the number of times when the "Wind Speed" was exactly 4 km/hr.**
```vim
print("The Wind Speed was 4km/h,", len(df[df["Wind Speed_km/h"]==4]),"times")
```
Q4. **Find all the null values in the data.**
```vim
print(df.isnull().sum())
```
Q5. **Rename the column, "Weather" in the dataframe to "Weather Condition".**
```vim
df.rename(columns = {"Weather" : "Weather Condition"}, inplace = True)
df.head(2)
```
Q6. **What is the mean "Visibility"?**
```vim
print("The mean value of 'Visibility_km/h' is", df["Visibility_km"].mean().round(2))
```
Q7. **What is the standard deviation of "Pressure" in this data?**
```vim
print("The standard deviation of 'Pressure' is",df["Press_kPa"].std().round(2))
```
Q8. **What is the variance of "Relative Humidity" in this data?**
```vim
print("The Variance of 'Relative Humidity' is", df["Rel Hum_%"].var().round(2))
```
Q9. **Find all instances when snow was recorded**
```vim
#Method 1 : Value Counts
print("Snow was recorded",df["Weather Condition"].value_counts()["Snow"],"times")

#Method 2: Filtering
print("Snow was recorded",len(df[df["Weather Condition"]=="Snow"]),"times")

#Method 3: Group By
print("Snow was recorded", len(df.groupby("Weather Condition").get_group("Snow")), "times")

#Method 4 Str.contains
print("With 'str.contains' method, snow has been recorded",len(df[df["Weather Condition"].str.contains("Snow")]),"times,
since it considers all the rows where snow is mentioned irrespective of other conditions along with it, for example:
Freezing drizzle, Snow")
```
Q10. **Find all instances when "Wind Speed" is about 24 and "Visibility" is 25.**
```vim
s = len(df[(df["Wind Speed_km/h"] == 24) & (df["Visibility_km"] == 25)])
print("The above instance has occured", s, "times")
```
Q11. **What is the mean value of each column against each "Weather Condition"?**
```vim
s = df.groupby("Weather Condition").mean(numeric_only = True)
print("Following are the mean values of each column against each 'Weather Condition':","\n")
s
```
Q12. **What is the minimum and maximum value of each column against each "Weather Condition"?**
```vim
#Minimum
a = df.groupby("Weather Condition").min()
print("Following are the minimum values ofeach column against each weather condition:","\n")
a

#Maximum
b = df.groupby("Weather Condition").max()
print("Following are the maximum values ofeach column against each weather condition:","\n")
b
```
Q13. **Show all the record where weather condition is fog.**
```vim
a = df[df["Weather Condition"].str.contains("Fog")]
print("Below are all the records where weather condition was 'Fog':","\n")
a
```
Q14. **Find all instances when "Weather is clear" or "Visibility" is above 40**
```vim
a = df[(df["Weather Condition"] == "Clear") | (df["Visibility_km"] > 40)]
print("The following records show all the instances where the weather was clear and visibility was 40:","\n")
a
```
Q15. **Find all instances when:**<br>
a) ***"Weather is Clear" and "Relative Humidity is greater than 50"*** <br>
**OR** <br>
b) ***"Visibility" is above 40"***
```vim
s = df[((df["Weather Condition"] == "Clear") & (df["Rel Hum_%"] > 50)) | (df["Visibility_km"] > 40)]
print("Below records show the records where Weather condition is clear and Relative Humidity is greater than 50
 or where visibility is greater than 40:","\n")
s
```
