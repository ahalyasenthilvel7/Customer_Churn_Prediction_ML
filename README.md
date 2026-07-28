# 📊 Customer Churn Prediction using Machine Learning

## 📌 Project Overview

Customer churn is an important challenge for banks because losing existing customers can affect customer retention and business performance. This project focuses on building a **Machine Learning model to predict whether a customer is likely to churn** using customer demographics, product usage, account information, and transaction behavior.

The dataset consists of **10,127 customer records** with **21 features**, containing both numerical and categorical variables. The target variable, **`Attrition_Flag`**, classifies customers as either **Existing Customer** or **Attrited Customer**.

The project begins with **Exploratory Data Analysis (EDA)** to understand customer characteristics and identify patterns related to attrition. The analysis examines demographic factors, income levels, education, card categories, credit limits, transaction behavior, and customer activity.

After preprocessing and encoding the categorical variables, the dataset is divided into **70% training data and 30% testing data** using stratified sampling to maintain the proportion of existing and attrited customers.

Three Machine Learning classification algorithms are developed and compared:

* **Decision Tree Classifier**
* **Random Forest Classifier**
* **Gradient Boosting Classifier**

The models are evaluated using **Accuracy, Precision, Recall, and F1-Score**. Since missing an actual churn customer can result in losing that customer, **Recall is given particular importance** in this project.

Among the three models, **Gradient Boosting provides the best balance between training and test performance** and generalizes better than the Decision Tree and Random Forest models. Therefore, Gradient Boosting is selected as the final model.

The Gradient Boosting model is further **fine-tuned using GridSearchCV**, with **Recall as the scoring criterion**. The tuned model shows an improvement in test-set recall, making it better at identifying customers who are likely to churn.

---

## 🎯 Objectives

* Analyze customer information and identify patterns related to customer churn.
* Perform **Exploratory Data Analysis (EDA)** on demographic, product, and transaction-related features.
* Preprocess the dataset and encode categorical variables.
* Split the data into training and testing sets using stratified sampling.
* Build and compare multiple classification models.
* Evaluate models using **Accuracy, Precision, Recall, and F1-Score**.
* Focus on **Recall** to reduce false negatives and identify more potential churn customers.
* Select the best-performing model based on its generalization performance.
* Fine-tune the selected **Gradient Boosting model using GridSearchCV**.
* Identify the important factors influencing customer churn.
* Provide business recommendations for improving customer retention.

---

## 📂 Dataset

The dataset contains **10,127 records and 21 columns** describing customer demographics, banking products, account activity, and transaction behavior.

### Target Variable

**`Attrition_Flag`**

* `Existing Customer`
* `Attrited Customer`

### Demographic Features

* `Customer_Age`
* `Gender`
* `Dependent_count`
* `Education_Level`
* `Marital_Status`
* `Income_Category`

### Product and Account Features

* `Card_Category`
* `Months_on_book`
* `Total_Relationship_Count`
* `Months_Inactive_12_mon`
* `Contacts_Count_12_mon`
* `Credit_Limit`
* `Total_Revolving_Bal`
* `Avg_Open_To_Buy`
* `Avg_Utilization_Ratio`

### Transaction Features

* `Total_Amt_Chng_Q4_Q1`
* `Total_Trans_Amt`
* `Total_Trans_Ct`
* `Total_Ct_Chng_Q4_Q1`

---

## 🔍 Exploratory Data Analysis

The project performs EDA to understand the distribution of customer characteristics and their relationship with attrition.

The analysis includes:

* Numerical feature distributions
* Categorical feature distributions
* Box plots for identifying outliers
* Attrition percentage by gender
* Attrition percentage by income category
* Attrition percentage by education level
* Transaction amount vs. attrition
* Credit limit vs. attrition
* Card category vs. attrition
* Months inactive vs. attrition

The dataset contains **no missing values** and **no duplicate records**.

---

## 🧹 Data Preprocessing

The following preprocessing steps are performed:

1. **Categorical variables are encoded** into numerical representations.
2. The target variable is encoded as:

   * `0` → Existing Customer
   * `1` → Attrited Customer
3. The target variable is separated from the input features.
4. The dataset is divided into:

   * **70% Training Data**
   * **30% Testing Data**
5. **Stratified splitting** is used to maintain the same proportion of customer attrition in both training and testing datasets.

---

## 🤖 Machine Learning Models

### 1. Decision Tree Classifier

A Decision Tree classifier is trained to predict whether a customer is an Existing Customer or an Attrited Customer.

The model is easy to interpret and visualize, but the project observations indicate signs of **overfitting**.

### 2. Random Forest Classifier

Random Forest combines multiple decision trees to improve generalization and reduce overfitting.

The project achieved strong test performance with approximately:

* **Accuracy:** 0.96
* **Precision:** 0.92
* **Recall:** 0.80
* **F1-Score:** 0.85

However, the model still shows some difference between training and testing performance.

### 3. Gradient Boosting Classifier

Gradient Boosting builds models sequentially, where each new tree attempts to correct errors made by previous trees.

Among the three models, **Gradient Boosting provides the best balance between training and test performance**, with strong precision, recall, and F1-score on unseen data.

Therefore, **Gradient Boosting is selected as the final model**.

---

## 📏 Model Evaluation

The models are evaluated using:

* **Accuracy** – Measures the overall percentage of correct predictions.
* **Precision** – Measures how many predicted attrited customers are actually attrited customers.
* **Recall** – Measures how many actual attrited customers are correctly identified.
* **F1-Score** – Provides a balance between Precision and Recall.
* **Confusion Matrix** – Shows correct and incorrect predictions for each class.

### Why Recall is Important

In customer churn prediction, **False Negatives are costly** because a customer who is actually going to churn may be incorrectly classified as an existing customer.

Therefore, the project focuses on:

**Maximizing Recall → Identifying more actual churn customers → Reducing potential customer loss**

---

## ⚙️ Gradient Boosting Fine-Tuning

After selecting Gradient Boosting as the final model, **GridSearchCV** is used for hyperparameter tuning.

The parameters considered include:

* `n_estimators`
* `learning_rate`
* `max_depth`
* `subsample`

The GridSearchCV process uses:

**`scoring='recall'`**

to select the parameter combination that provides better churn detection.

The tuned Gradient Boosting model uses:

* **`max_depth = 4`**
* **`n_estimators = 125`**
* **`subsample = 0.5`**
* **`random_state = 42`**

After fine-tuning, the model shows an **improvement in test-set recall**, indicating better identification of customers likely to churn.

---

## ⭐ Important Features Influencing Customer Churn

Feature importance is extracted from the trained **Gradient Boosting model**.

The top features identified by the project are:

| Rank | Feature                      | Importance |
| ---- | ---------------------------- | ---------: |
| 1    | **Total_Trans_Ct**           |   **0.33** |
| 2    | **Total_Trans_Amt**          |   **0.19** |
| 3    | **Total_Revolving_Bal**      |   **0.19** |
| 4    | **Total_Relationship_Count** |   **0.11** |
| 5    | **Total_Ct_Chng_Q4_Q1**      |   **0.10** |
| 6    | `Total_Amt_Chng_Q4_Q1`       |       0.03 |
| 7    | `Contacts_Count_12_mon`      |       0.02 |
| 8    | `Customer_Age`               |       0.02 |
| 9    | `Months_Inactive_12_mon`     |       0.01 |
| 10   | `Avg_Open_To_Buy`            |       0.00 |

The project specifically identifies **Total Transaction Count, Total Transaction Amount, and Total Revolving Balance** as the **top three attributes influencing customer churn**.

---

# 🔎 Factors / Reasons Associated with Attrited Customers

Based on the **EDA and feature-importance analysis performed in this project**, the following factors are associated with higher customer attrition.

### 1. Low Transaction Count

**`Total_Trans_Ct`** is the most important feature in the Gradient Boosting model, with an importance of **0.33**.

The project identifies **low transaction activity as an indicator of customer disengagement**. Customers who use their banking services less frequently are more likely to become attrited customers.

**Insight:** Low transaction frequency can indicate reduced customer engagement.

---

### 2. Low Transaction Amount

**`Total_Trans_Amt`** has a feature importance of **0.19** and is one of the top three factors influencing churn.

The EDA shows that **customers with lower total transaction amounts are more likely to churn**, while customers spending approximately **more than $11,000** are less likely to churn.

**Insight:** Lower spending and reduced usage of banking services are associated with higher attrition.

---

### 3. High Revolving Balance

**`Total_Revolving_Bal`** has a feature importance of **0.19**, making it another major factor influencing churn.

The project associates **high revolving balances with potential financial strain and increased churn risk**.

**Insight:** Customers carrying higher revolving balances may require additional financial support or suitable repayment options.

---

### 4. Number of Products / Relationships with the Bank

**`Total_Relationship_Count`** has a feature importance of **0.11**.

This represents the total number of products held by a customer. The model identifies this feature as one of the important variables influencing churn.

**Insight:** The number of products a customer has with the bank is related to their likelihood of attrition.

---

### 5. Change in Transaction Count

**`Total_Ct_Chng_Q4_Q1`** has a feature importance of **0.10**.

This represents the change in transaction count between Q4 and Q1. Changes in transaction activity therefore contribute significantly to the churn prediction.

**Insight:** A change or reduction in transaction activity can be an important signal of changing customer engagement.

---

### 6. Customer Inactivity

The EDA of **`Months_Inactive_12_mon`** shows that customers inactive for **1–3 months** form a major portion of the attrited group, with attrition being highest at **3 months of inactivity**.

**Insight:** Increasing inactivity can be an early warning sign of potential churn, making early engagement important.

---

### 7. Gender

The project analysis shows:

* **Female attrition percentage:** 17.4%
* **Male attrition percentage:** 14.6%

Therefore, female customers show a higher attrition percentage in this dataset.

**Insight:** Gender shows a difference in attrition percentage, although it is not among the top features identified by the Gradient Boosting feature-importance analysis.

---

### 8. Income Category

The EDA shows different attrition percentages across income categories.

* **>$120K:** 17.4%
* **<$40K:** 17.2%
* **Unknown:** 16.8%
* **$80K–$120K:** 15.8%
* **$40K–$60K:** 15.1%
* **$60K–$80K:** 13.5%

The **>$120K** and **<$40K** groups have the highest attrition percentages, while the **$60K–$80K** group has the lowest attrition percentage among the listed categories.

---

### 9. Education Level

The analysis shows that **Doctorate-level customers have the highest attrition percentage at 21%**, followed by **Post-Graduate customers at 17.8%**.

Other groups show lower attrition percentages:

* Unknown: 16.8%
* Uneducated: 16.0%
* Graduate: 15.6%
* College: 15.4%
* High School: 15.2%

**Insight:** Education level shows differences in attrition percentage, with Doctorate-level customers having the highest rate in this dataset.

---

### 10. Card Category

The analysis of card categories shows that **Platinum cardholders have the highest churn rate**, while **Silver and Blue cardholders have the lowest churn rate**.

**Insight:** Card category is associated with differences in customer attrition in this dataset.

---

## 💡 Key Business Recommendations

Based on the project's findings:

### **Increase Customer Engagement**

Target customers with **low transaction counts** through:

* Targeted marketing campaigns
* Rewards for frequent transactions
* Loyalty points and benefits
* Cashback or discounts

### **Encourage Higher Spending**

For customers with **low transaction amounts**:

* Provide personalized spending promotions.
* Offer cashback and rewards.
* Cross-sell relevant banking products.
* Introduce rewards based on spending thresholds.

### **Support Customers with High Revolving Balances**

For customers with **high revolving balances**:

* Provide balance-transfer options.
* Offer financial counseling and budgeting support.
* Provide flexible repayment plans.

### **Proactive Retention**

Use the churn prediction model to identify **high-risk customers early** and provide personalized retention strategies before they become attrited customers.

---

## 🛠️ Technologies Used

**Python**
**Pandas**
**NumPy**
**Matplotlib**
**Seaborn**
**Scikit-learn**
**Google Colab**

---

## 📌 Conclusion

This project demonstrates a complete **Customer Churn Prediction workflow**, starting from data exploration and preprocessing to machine learning model development, evaluation, feature-importance analysis, and model fine-tuning.

The analysis shows that **customer transaction behavior is particularly important for predicting churn**, with **Total Transaction Count, Total Transaction Amount, and Total Revolving Balance** identified as the top three influential features.

The final **tuned Gradient Boosting model** provides an improved ability to identify potential churn customers, particularly through improved recall. These predictions can help the bank proactively identify at-risk customers and take appropriate actions to improve customer engagement and retention.
