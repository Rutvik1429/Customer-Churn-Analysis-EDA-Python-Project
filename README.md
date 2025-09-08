# Customer-Churn-Analysis-EDA-Python-Project
This repository contains a customer_churn_analysis using python(EDA-Exploratory Data Analysis).Churn Analysis is the process of identifying customers who are likely to stop using a company’s product or service.

### ✅ Project Overview
This project focuses on analyzing customer churn using exploratory data analysis (EDA) techniques in Python. Customer churn refers to customers who stop using a company's services or products. The primary aim is to identify patterns, trends, and factors that lead to customer attrition, helping businesses understand customer behavior and take proactive steps to reduce churn.

The dataset used in this project is the Telco Customer Churn dataset, which contains customer information, services subscribed, demographic details, and churn labels.

# 🎯 Objective
## The key objectives of this project are:
- ✅ To explore customer data and understand the distribution of features.
- ✅ To preprocess data by handling missing values, incorrect data types, and converting categorical variables.
- ✅ To visualize the relationships between customer attributes and churn behavior.
- ✅ To uncover patterns and insights that contribute to customer churn.
- ✅ To provide actionable insights that can help businesses improve customer retention.

# 📂 Dataset Description
## The dataset includes the following fields:
- Customer information: gender, senior citizen, tenure, etc.
- Services: Internet, phone service, online backup, etc.
- Charges: monthly and total charges.
- Churn label: whether the customer has churned (Yes/No).

# 🔍 Data Cleaning and Preprocessing
- Missing values in the TotalCharges column were replaced with 0.
- Data types were converted to appropriate formats for analysis.
- The SeniorCitizen feature was transformed from numerical values (0, 1) to categorical labels (No, Yes) for better interpretability.
- The dataset was checked for inconsistencies and corrected where necessary.

# 📊 Exploratory Data Analysis (EDA) Insights
## 1️⃣ Churn Distribution
```python
# Set the size of the plot (width=3 inches, height=4 inches)
plt.figure(figsize=(3, 4))

# Group the data by 'Churn' and count the occurrences
gp = df.groupby("Churn").agg({"Churn": "count"})

# Create a pie chart
# - Values to plot: the count of each churn category
# - Labels: the unique churn categories (Yes/No)
# - autopct: format to show percentage values with 2 decimal places
plt.pie(gp["Churn"], labels=gp.index, autopct="%1.2f%%")

# Add a title to the plot
plt.title("Percentage of Churned Customers")

# Save the plot as a high-resolution PNG file
# - dpi=2000 ensures very high quality
# - bbox_inches='tight' ensures no extra whitespace around the image
plt.savefig("Percentage of Churned Customers.png", dpi=2000, bbox_inches="tight")

# Display the plot
plt.show()
```
![Churn distribution](https://github.com/Rutvik1429/Customer-Churn-Analysis-EDA-Python-Project/blob/main/visual_plot/Percentage%20of%20Churned%20Customers.png)
- From the pie chart visualization, it was observed that 25.54% of customers have churned, while the remaining are still active.
- This indicates that customer attrition is significant and requires attention.

## 2️⃣ Tenure and Total Charges
```python
# Set the size of the plot (width=8 inches, height=4 inches)
plt.figure(figsize=(8, 4))

# Create a histogram to show the distribution of 'tenure'
# - x: 'tenure' values of customers
# - data: the dataset 'df'
# - bins: number of bins set to 72 for detailed distribution
# - hue: 'Churn' to differentiate churned vs non-churned customers
sns.histplot(x="tenure", data=df, bins=72, hue="Churn")

# Add a title to the plot to explain what it represents
plt.title("Churned by Tenure")

# Save the plot as a high-resolution PNG image
# - dpi=2000 ensures very sharp output
# - bbox_inches='tight' removes extra whitespace
plt.savefig("Churned by Tenure.png", dpi=2000, bbox_inches="tight")

# Display the plot on the screen
plt.show()
```
![Tenure and Total Charges](https://github.com/Rutvik1429/Customer-Churn-Analysis-EDA-Python-Project/blob/main/visual_plot/Churned%20by%20Tenure.png)
- A deeper analysis revealed that customers with lower tenure and lower total charges are more likely to churn.
- Long-tenured customers tend to stay, suggesting loyalty increases over time.
