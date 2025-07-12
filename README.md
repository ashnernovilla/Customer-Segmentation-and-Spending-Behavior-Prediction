# Employee Performance Analysis & Prediction

## 1. Project Objective

The main goal of this project is to analyze an employee dataset to identify key factors related to performance. You will build a semi-supervised machine learning model to first group (cluster) employees and then predict which group a new employee belongs to. The final results will be visualized in a Power BI dashboard.

---

## 2. Dataset

* **File:** `Performance.xlsx`
* **Description:** This file contains performance metrics for 930 employees.
* **Columns:** `Promotion`, `EmployeeName`, `EmployeeID`, `Designation`, `Improvement_in_ExamScore`, `Working_hours`, `Personality_trait_score`, `Openess_to_experience`, `MonthlySalary`.

---

## 3. Requirements

### Software

* **Python:** Version 3.5 or higher.
* **Anaconda:** Recommended for managing Python environments and packages.
* **Power BI:** Version 2.88.621.0 or higher.

### Python Libraries

You will need to install the following Python libraries. You can install them all using one command in your terminal or Anaconda Prompt:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost
```

---

## 4. Step-by-Step Instructions

Follow these steps to complete the project from start to finish.

### Step 1: Set Up Your Environment

1.  **Install Anaconda:** Download and install Anaconda from the official website.
2.  **Create a New Environment (Recommended):** Open the Anaconda Prompt and create a dedicated environment for this project. This keeps your project dependencies organized.
    ```bash
    conda create -n performance-env python=3.8
    ```
3.  **Activate the Environment:**
    ```bash
    conda activate performance-env
    ```
4.  **Install Libraries:** Use the `pip` command from the section above to install the required libraries within your new environment.

### Step 2: Data Analysis and Machine Learning (Python)

You can use a Jupyter Notebook or any Python editor to perform these tasks. The provided `.py` script contains all the necessary code.

1.  **Load Data:** Use pandas to read the `Performance.xlsx` file.
2.  **Data Cleaning & Preparation:**
    * Drop the `EmployeeName` and `EmployeeID` columns as they are not needed for the model.
    * Convert categorical columns (`Designation`, `Promotion`, `Personality_trait_score`) into numerical values using mapping or label encoding.
    * Normalize the numerical features using **Min-Max Scaling**. This brings all values to a common scale.
3.  **Clustering (Unsupervised Learning):**
    * Use the **Elbow Method** to determine the best number of clusters for your data (the project identifies **3** as the optimal number).
    * Apply the **K-Means** algorithm to group the employees into 3 clusters based on their characteristics.
    * Add a new column named `means_cluster` to your dataset containing the cluster number for each employee.
4.  **Classification (Supervised Learning):**
    * The goal is to train a model that can predict the `means_cluster` you just created.
    * Prepare the data for classification by creating dummy variables (one-hot encoding) for categorical features.
    * Split your data: 70% for training and 30% for testing.
    * Train several classification models (e.g., Logistic Regression, Decision Tree, RandomForest, XGBoost).
    * Evaluate the accuracy of each model. The project documentation selected the **Decision Tree Classifier** as the final model because it provided high accuracy without overfitting.
5.  **Generate Final Predictions:**
    * Use your trained Decision Tree model to predict the cluster for all employees in the dataset.
    * Create a final DataFrame that includes the original employee data, the K-Means cluster, and the predicted cluster.

### Step 3: Data Visualization (using Python)

Instead of using an external tool like Power BI, you can create all the necessary visualizations directly within your Python script or Jupyter Notebook using libraries like `matplotlib`, `plotly` and `seaborn`.

1.  **Scatter Plot of Clusters:**
    * This plot helps you visualize the different employee clusters based on their monthly salary and openness to experience.
    * Use the `scatterplot` function from `seaborn`.

    ```python
    import matplotlib.pyplot as plt
    import seaborn as sns

    # Set the figure size for better readability
    plt.figure(figsize=(10, 6))

    # Create the scatter plot
    sns.scatterplot(
        x='MonthlySalary',
        y='Openess_to_experience',
        hue='means_cluster',  # Color points by their cluster
        palette='viridis',     # Choose a color scheme
        data=dataset_final,    # Use your final dataframe
        s=100,                 # Set marker size
        alpha=0.7              # Set marker transparency
    )

    plt.title('Employee Clusters based on Salary and Openness')
    plt.xlabel('Monthly Salary')
    plt.ylabel('Openness to Experience')
    plt.legend(title='Cluster')
    plt.show()
    ```

2.  **Bar Chart of Employee Designations:**
    * This chart shows the number of employees in each job designation.

    ```python
    plt.figure(figsize=(12, 7))

    # Create the count plot
    sns.countplot(y='Designation', data=dataset_final, order = dataset_final['Designation'].value_counts().index)

    plt.title('Number of Employees by Designation')
    plt.xlabel('Count')
    plt.ylabel('Designation')
    plt.show()
    ```

3.  **Pie Charts for Cluster Distribution:**
    * These charts show the percentage of employees in each cluster, both for the original K-Means clusters and the model's predictions.

    ```python
    # Create a figure with two subplots (side-by-side)
    fig, axes = plt.subplots(1, 2, figsize=(16, 8))

    # Pie chart for original K-Means clusters
    cluster_counts = dataset_final['means_cluster'].value_counts()
    axes[0].pie(cluster_counts, labels=cluster_counts.index, autopct='%1.1f%%', startangle=90)
    axes[0].set_title('Distribution of Original K-Means Clusters')

    # Pie chart for predicted clusters
    predicted_counts = dataset_final['Predicted'].value_counts()
    axes[1].pie(predicted_counts, labels=predicted_counts.index, autopct='%1.1f%%', startangle=90)
    axes[1].set_title('Distribution of Predicted Clusters')

    plt.show()
    
