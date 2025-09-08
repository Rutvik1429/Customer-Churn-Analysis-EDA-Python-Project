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

## 3️⃣ Senior Citizens and Churn
```python
# Create a crosstab to count churn occurrences by 'SeniorCitizen'
ct = pd.crosstab(df["SeniorCitizen"], df["Churn"])

# Convert counts to percentages within each 'SeniorCitizen' group
ct_pct = ct.div(ct.sum(axis=1), axis=0) * 100

# Plot a stacked bar chart
# - kind="bar": create a bar plot
# - stacked=True: stack the bars to show cumulative percentage
# - figsize: set the size of the plot
ax = ct_pct.plot(kind="bar", stacked=True, figsize=(3, 4))

# Add title and labels
plt.title("Churn by Senior Citizen (Stacked Bar Plot)")
plt.ylabel("Percentage")

# Add percentage labels to each bar
for container in ax.containers:
    ax.bar_label(container, fmt="%.1f%%", label_type="center")

# Set x-axis tick labels: 0 → 'No', 1 → 'Yes'
ax.set_xticks(range(len(ct_pct.index)))
ax.set_xticklabels(["No", "Yes"])

# Adjust legend to make it clear
plt.legend(title="Churn", bbox_to_anchor=(0.9, 0.9))

# Save the figure as a high-resolution PNG file
# - dpi=2000 for clarity
# - bbox_inches="tight" to remove unnecessary padding
plt.savefig("Churn by SeniorCitizen(Stacked Bar Plot).png", dpi=2000, bbox_inches="tight")

# Display the plot
plt.show()
```
![Senior Citizens and Churn](https://github.com/Rutvik1429/Customer-Churn-Analysis-EDA-Python-Project/blob/main/visual_plot/Churn%20by%20SeniorCitizen(Stacke%20Bar%20plot).png)
- Senior citizens are slightly more prone to churn compared to younger customers, which can be addressed by targeted services.

## 4️⃣ Customer Paymentmethod Churn
```python
# Set the size of the plot (width=10 inches, height=4 inches)
plt.figure(figsize=(10, 4))

# Create a count plot to show the number of customers by 'PaymentMethod'
# - y="PaymentMethod": display categories on the y-axis
# - hue="Churn": separate the bars by churn status (Yes/No)
ax = sns.countplot(y="PaymentMethod", data=df, hue="Churn")

# Add labels on the bars to show the exact count values
ax.bar_label(ax.containers[0])  # Labels for the first group (e.g., 'No')
ax.bar_label(ax.containers[1])  # Labels for the second group (e.g., 'Yes')

# Add a title to the plot for clarity
plt.title("Churned Customers by Payment Method")

# Adjust x-axis ticks if necessary (though here it's rotated just in case)
plt.xticks(rotation=45)

# Position the legend outside the plot for better readability
plt.legend(bbox_to_anchor=(1, 1))

# Save the plot as a high-resolution PNG file
# - dpi=2000 ensures very sharp details
# - bbox_inches="tight" removes extra whitespace
plt.savefig("Churned Customers by PaymentMethod.png", dpi=2000, bbox_inches="tight")

# Display the plot
plt.show()
```
![Customer Paymentmethod Churn](https://github.com/Rutvik1429/Customer-Churn-Analysis-EDA-Python-Project/blob/main/visual_plot/Churned%20Customers%20by%20Paymentmathod.png)

## 5️⃣ Contract Types
```python
# Set the size of the plot (width=4 inches, height=4 inches)
plt.figure(figsize=(4, 4))

# Create a count plot to show the number of customers by 'Contract' type
# - x="Contract": display contract categories on the x-axis
# - hue="Churn": split the bars by churn status (Yes/No)
ax = sns.countplot(x="Contract", data=df, hue="Churn")

# Add labels on the bars to show the exact count for each contract type
ax.bar_label(ax.containers[0])  # Labels for the first group (e.g., 'No')

# Add a title to describe what the plot represents
plt.title("Count of Customers by Contract")

# Save the plot as a high-resolution PNG file
# - dpi=2000 ensures sharp image quality
# - bbox_inches="tight" removes unnecessary whitespace around the image
plt.savefig("Count of Customer By Contract.png", dpi=2000, bbox_inches="tight")

# Display the plot
plt.show()
```
![Contract Types](https://github.com/Rutvik1429/Customer-Churn-Analysis-EDA-Python-Project/blob/main/visual_plot/Count%20of%20Customer%20By%20Contract.png)
- Customers with month-to-month contracts exhibit higher churn rates, whereas those with one or two-year contracts tend to stay longer.

# 💡 Key Insights

### 📌 Customers on month-to-month contracts are at the highest risk of churning.
### 📌 Providing tech support, online security, and other services can enhance customer satisfaction and reduce churn.
### 📌 Tenure plays a major role in customer retention; customers who stay longer are less likely to churn.
### 📌 Senior citizens require special attention in retention strategies.
### 📌 Offering annual or long-term contracts can improve customer loyalty.
