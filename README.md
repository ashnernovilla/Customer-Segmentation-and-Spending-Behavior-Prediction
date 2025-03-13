## 📌 Overview
This repository is about Using Python to Build a Semi-Supervised Model for Customer Segmentation and Spending Behavior Prediction. It contains an analysis of multiple machine learning models used for classification. The goal is to To develop a semi-supervised machine learning model for customer segmentation and potential buyer prediction using spending data. This will help businesses identify high-value customers, optimize marketing strategies, and improve sales opportunities and evaluate and compare the performance of different algorithms to determine the best model for predictive accuracy and generalization.


## 📊 Model Performance Summary
| Model | Training Accuracy | Test Accuracy | Interpretation |
|--------|-----------------|--------------|----------------|
| **Logistic Regression** | 0.83 | 0.85 | Good baseline model, but slightly underfitting. |
| **Decision Tree** | 0.93 | 0.95 | Strong performance, risk of overfitting. |
| **K-NN** | 0.99 | 0.95 | Possible overfitting, but high test accuracy. |
| **Gaussian Naive Bayes** | 0.99 | 0.95 | Surprisingly good performance, assumes feature independence. |
| **Multinomial Naive Bayes** | 0.82 | 0.85 | Similar to Logistic Regression, works well with categorical data. |
| **Random Forest** | 0.93 | 0.95 | Balanced model with good generalization. |
| **AdaBoost** | 0.42 | 0.40 | Underperforming, needs tuning or better dataset suitability. |
| **XGBoost** | 0.99 | 0.95 | Top performer, slight overfitting risk. |

## 📌 Key Takeaways:
- **Best Performing Models:** Decision Tree, Random Forest, K-NN, Gaussian Naïve Bayes, XGBoost (**Test Accuracy: 0.95**)
- **Overfitting Risks:** K-NN and XGBoost (**Training Accuracy: 0.99, Test Accuracy: 0.95**)
- **Underperforming Model:** AdaBoost (**Needs tuning or may not be suitable**)
- **Balanced Models:** Random Forest and Decision Tree (**Good performance without excessive overfitting**)
- **Baseline Models:** Logistic Regression & Naïve Bayes (**Perform decently, but better models exist**)

## 🚀 How to Use
1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/your-repo.git
   cd your-repo
   ```
2. Open the Jupyter Notebook and run the model evaluation.
3. Modify `Data_Science_Project.ipynb` to test with different datasets.

## 🔮 Future Improvements
- Hyperparameter tuning for **AdaBoost** and **Decision Tree**.
- Feature engineering to improve model performance.
- Deploy the best model as an API using Flask or FastAPI.

## 📜 License
This project is open license.
