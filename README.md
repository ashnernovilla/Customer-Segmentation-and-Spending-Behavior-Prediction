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

### Step 3: Data Visualization (Power BI)

1.  **Configure Power BI:**
    * Open Power BI.
    * Go to `File > Options and settings > Options`.
    * Navigate to the `Python scripting` tab.
    * Set the "Python home directory" to the Anaconda environment you created (e.g., `C:\Users\YourName\anaconda3\envs\performance-env`).
2.  **Import Data using Python Script:**
    * In Power BI, click `Get Data > Other > Python script`.
    * Copy the entire Python code from your script (`.py` file) and paste it into the script window.
    * **Important:** In the script, make sure the line that reads the Excel file points to the correct location on your computer.
    * Power BI will run the script and show a Navigator with all the DataFrames created. Select the **final dataset** that includes your predictions.
3.  **Build the Dashboard:**
    * Load the data into Power BI.
    * Recreate the dashboard from the project document. It should include:
        * A scatter plot of `MonthlySalary` vs. `Openess_to_experience`, colored by cluster.
        * Pie charts showing the distribution of employees across clusters and predicted groups.
        * Bar charts showing employee counts by designation.
        * A table with detailed employee information.
