# sgh-technical-assessment

## **Introduction**

### **Research objectives**

The main objective of this research is to develop 3 Machine Learning Models which are able to predict those with diabetes (gh >= 6.5%) with the best predictability rate. The end-user of this ML system will be the medical professionals and potentially the patients who would like to know whether they could be having diabetes. By accurately predicting diabetes, this predictive models will help to ensure prompt intervention on patients with diabetes, thus ensuring better life outcomes for the patients and avert uncecessary further financial burden due to delayed treatment.

## **Getting Started**

The directory structure is as follows:

```plaintext
sgh-technical-assessment/
├── mlruns/
├── cleaned_data.db
├── descriptive_stats_raw_df.xlsx
├── DS Take home assignment - NhanesGh.pdf
├── eda-diabetes.ipynb
├── logs.log
├── modelling.ipynb
├── nhgh.tsv
├── README.md
├── tuned_dt_model.pkl
├── tuned_lasso_log_reg_model.pkl
├── tuned_rf_model.pkl
└── Understanding of RAW Data.html
```

> [!IMPORTANT] > **For ML modelling results, go to `modelling.ipynb` and for EDA, go to `eda-diabetes.ipynb`**

## **Project Implementation Workflow**

![CRISP-DM Framework](https://www.datascience-pm.com/wp-content/uploads/2021/02/CRISP-DM.png)

We adopt the Cross Industry Standard Process in Data Mining (CRISP-DM) Framework, which is a popular, well-organised framework for data mining which ensures an efficient workflow.

The implementation of the Machine Learning System to detect diabetes follows a structured process. Below is an overview of the steps taken from data sourcing to the final presentation of the model.

## Step-by-Step Breakdown:

1. **Data Understanding**

   - The process begins with gaining a thorough understanding of the data collected from the dataset.

2. **Data Preparation**

   - **Data Cleaning**: Cleansing the data to ensure quality.
   - **Data Pruning**: Removing irrelevant data points.
   - **Feature Engineering**: Developing new features to improve model accuracy.
   - **Feature Selection**: Choosing the most relevant features for modelling.

3. **Model Training**

   - Several Machine Learning approaches are employed, including:
     - Decision Tree Classifier
     - Random Forest Classifier
     - Logistic Regression Classifier

4. **Model Evaluation & Tuning**

   - After training, the models are evaluated and tuned to achieve the best performance possible.

5. **Report & Presentation**
   - The findings and model performance are documented and presented in a report.

## Iterative Improvements:

To enhance the ML system's performance, the following iterative approaches are taken:

- **X-AI Approach**: Utilising SHAP Analysis and feature importance metrics to explain model decisions.
- **Model Tuning**: Iterating on the model based on the evaluation metrics to refine and enhance its performance.

This systematic approach ensures a robust, transparent, and effective system to aid in the prediction of diabetes.

**Machine Learning Task and proposed models**

I will first need to create a target variable `has_diabetes` (tells us whether the patient is diabetic or not according to specified gh percentage), I will thus be adopting a supervised learning approach, since labels are already present, with a 70-30 train test split. To better explain the decision-making process behind each models (whether easily interpretable or not), I will also adopt the use of an Explainable-AI tool, which in my case is the SHAP, which stands for SHapley Additive exPlanations, which is to provide interpretable insights on how each of the feature impacts the model's decision making process. The benefit of such is that it can also educate the end-users on some of the key reasons and trends of identifying diabetes based on the unique attributes of patients. At the same time, it provides a human-over-the-loop monitoring for the team of data scientists/engineers to verify the decision-making process of the ML models, to ensure the ethics of AI and transparency of AI are upheld, especially important for the health sector. This is important to avert any biases in the model prediction.

Generally, the aim at the end of EDA process is to uncover key insights that will guide the modeling process and highlight the importance of each of the three ML models

Along the way in this notebook, we will also uncover some additional insights which will also aid us in the understanding of our data and how we frame our ML solutions to fulfill our research objectives.

**Predictive Performance (On test dataset) conclusion:**

| Model                     | Accuracy | AUC      | Recall   | Precision | F1 Score |
| ------------------------- | -------- | -------- | -------- | --------- | -------- |
| Lasso Logistic Regression | 0.904855 | 0.946421 | 0.829787 | 0.490566  | 0.616601 |
| Decision Tree             | 0.944090 | 0.818670 | 0.664894 | 0.710227  | 0.686813 |
| Random Forest             | 0.920549 | 0.939550 | 0.760638 | 0.550000  | 0.638393 |

1. Logistic Regression (Lasso-Penalised): I conclude that this is the best model, with the highest AUC score of 0.946 and highest Recall Score of 0.830 when fine-tuned and regularised to prevent overfitting. It is also highly interpretable.

2. Random Forest: I conclude that Random Forest Classifier is the second best model, with second highest AUC score and a decent recall of 0.761.

3. Decision Tree: Decision tree is the worst performing, with an AUC score being lowest and the recall score also the lowest. However, this is not to discredit this model as it is also highly explainable/interpretable. The AUC score and recall score can still be considered decent

**Conclusively, Logistic Regression (With Lasso Penalty) performs the best in terms of predictive performance.**

### **EXPLANATORY PERFORMANCE**

The differences in feature importance and SHAP plots between the Lasso Logistic Regression and the Random Forest/decision tree models are due to:

- The linear vs. non-linear nature of the models.
- The different methods of calculating feature importance.
- The handling of correlated features.

Consolidating the General findings from the lasso logistic regression model and random forest model SHAP models suggest that the following factors increases your risk of diabetes:

1. `tx` = 1, being treated with insulin/on diabetes med increases one risk of diabetes.

2. `dx` = 1, being diagnosed with PRE-DM or already diagnosed with DM increases risk of diabetes.

3. A higher `age`, being older, increases one's risk of diabetes.

4. A higher waistline circumference increases one's risk of diabetes.

5. If you are male individual, you are at an elevated risk of diabetes.

6. A lower income level may also elevate your risk of diabetes.

7. Having a lower albumin level also increases your risk of diabetes

**Conclusively, BOTH Logistic Regression (With Lasso Penalty) and RANDOM FOREST is a tie in terms of predictive performance since their decision making process is relatively different due to the linear (log reg) vs. non-linear (random forest) nature of the models.**
