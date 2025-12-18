# Customer Segmentation Behavior Analysis

## Problem Statement:-
### Digital advertising platforms generate large volumes of performance data, but advertisers struggle to understand which factors drive conversions and ROI. This project applies data mining techniques to analyze ad performance, identify meaningful patterns, segment ads, and build predictive insights to support better ad-spend decisions.

---

## Description of Dataset and the link for the dataset:-

Dataset: Facebook Ads Dataset (Kaggle) https://www.kaggle.com/datasets/madislemsalu/facebook-ad-campaign

--

Dataset Overview:

<img width="626" height="510" alt="image" src="https://github.com/user-attachments/assets/23ff9b5b-20d4-4c11-977d-d6566b88dfbc" />

--

Feature Description:

<img width="674" height="536" alt="image" src="https://github.com/user-attachments/assets/3dcdfa38-cbb2-4883-8c4c-97c45f282758" />

---

## Data Preprocessing Details:
<img width="858" height="356" alt="image" src="https://github.com/user-attachments/assets/8e7d2879-ce0d-46ec-8c3c-ee0201af217b" />

- Handling Missing Values:
Only the conversion-related variables (total_conversion and approved_conversion) had missing values. The median, a reliable metric appropriate for skewed distributions, was used to impute these missing observations. The dataset had no missing values after imputation.

- Removing or Correcting Outliers:
Box plots were used to identify and quantify outliers in numerical variables (interest1, interest2, interest3, impressions, clicks, spent, and conversion metrics) using the Interquartile Range (IQR) method. To lessen the impact of extreme values while maintaining overall data integrity, values outside of Q1 − 1.5×IQR and Q3 + 1.5×IQR were capped to the corresponding bounds.

- Normalization / Standardization:
All numerical variables were standardized using z-score z-score normalization via StandardScaler to guarantee comparability across features and enhance model performance. This made the data appropriate for dimensionality reduction and distance-based algorithms by transforming each feature to have a mean of zero and a standard deviation of one.

- Feature Selection and Feature Engineering:
Date variables were converted to datetime format, and a new feature representing campaign duration was engineered. Identifier columns (ad_id, campaign_id, fb_campaign_id) were removed as they do not provide predictive value. Categorical variables (age and gender) were transformed using one-hot encoding with drop_first=True to avoid multicollinearity, resulting in a structured feature set appropriate for modeling.

<img width="429" height="247" alt="image" src="https://github.com/user-attachments/assets/09bba460-d8fd-4fda-9378-afd10db7268e" />

--

<img width="468" height="185" alt="image" src="https://github.com/user-attachments/assets/d848e390-3f70-4965-9bb4-02ea14e18661" />

--

<img width="468" height="185" alt="image" src="https://github.com/user-attachments/assets/74ed1e27-8902-416a-a86c-c7d8432f9d4e" />

--

<img width="440" height="326" alt="image" src="https://github.com/user-attachments/assets/312af6a5-2288-4f18-adb1-6ea56aa2cafd" />

--

<img width="474" height="286" alt="image" src="https://github.com/user-attachments/assets/955c044b-005e-4aec-b6ad-7bc6b2dd32d2" />

--

## Exploratory Analysis Findings:

Exploratory data analysis revealed that key advertising performance metrics—impressions, clicks, and spend—exhibit strong right-skewed distributions, indicating that most advertisements generate low engagement while a small subset accounts for disproportionately high activity. This pattern persisted even after outlier capping and standardization, reflecting the inherent structure of real-world advertising data.
The Interquartile Range (IQR) method for outlier detection found extreme values in a variety of numerical features. By stabilizing the distributions and lowering variance, capping these values improved their suitability for clustering and predictive modeling. However, following imputation and outlier handling the total_conversion total_conversion feature became constant, highlighting a preprocessing-induced limitation and making it useless for further analysis.

Strong positive correlations between impressions, clicks, and spend were revealed by correlation analysis, suggesting high multicollinearity. These metrics showed moderately positive correlations with approved conversions, indicating that exposure and engagement are significant factors influencing conversion outcomes. Interest-related characteristics, on the other hand, showed weak linear correlations with performance metrics, indicating little direct impact on overall ad performance.

Analysis of categorical variables identified initial data quality issues in the age and gender fields, which were corrected by filtering invalid values. After cleaning, the 30–34 age group and male users were the most represented. Engagement metrics such as clicks and spend varied across age groups and genders, with higher values observed among certain demographics, while approved conversion rates remained relatively consistent, indicating that demographic effects are stronger in early engagement stages than in final conversion outcomes.

Finally, unsupervised clustering revealed distinct advertisement segments, confirming the presence of meaningful structure within the data. These findings directly informed feature selection, preprocessing decisions, and the choice of modeling techniques applied in later stages of the analysis.

--

<img width="468" height="389" alt="image" src="https://github.com/user-attachments/assets/278f9164-b3af-460c-b686-66e7d475d451" />

--

<img width="788" height="358" alt="image" src="https://github.com/user-attachments/assets/d0e65048-88ef-45f0-b86a-c33a675676b9" />


---

## Methods Used (Algorithm + Justification)

This project applied a combination of **unsupervised and supervised data mining techniques** to analyze digital advertising performance, in alignment with the objectives of segmentation, pattern discovery, and prediction.

1. Clustering (K-Means)

Based on encoded demographic features and standardized performance metrics, different groups of ads were identified using K-Means clustering. This algorithm was chosen because it is effective and easy to understand when dealing with big numerical datasets. By grouping ads with similar engagement and spending patterns, clustering enabled the identification of meaningful performance segments such as low-engagement, high-spend, and relatively efficient ads. The optimal number of clusters was determined using the Elbow Method and validated with Silhouette Score, ensuring cluster quality and separation.

2. Dimensionality Reduction (Principal Component Analysis)

Principal Component Analysis (PCA) was applied to reduce the dimensionality of the feature space while preserving the majority of variance in the data. Given the high number of features resulting from one-hot encoding, PCA helped mitigate multicollinearity and improve computational efficiency. The resulting principal components also facilitated visualization of cluster separation and supported interpretability of underlying performance patterns.

3. Regression Modeling (Random Forest and Gradient Boosting)

Two ensemble-based regression models, **RandomForestRegressor** and **GradientBoostingRegressor**, were used to forecast authorized conversions. These models were selected due to their capacity to capture feature interactions and non-linear relationships that are frequently found in marketing data. Random Forest provided a strong baseline with robustness to noise and overfitting, while Gradient Boosting was selected to assess whether sequential error correction could improve predictive performance. Using two models enabled a comparative evaluation of ensemble approaches under identical preprocessing and data splits.

## Result & Evaluation
<img width="624" height="218" alt="image" src="https://github.com/user-attachments/assets/a48ff446-455d-4cb4-9c2a-823056821371" />

Two regression models—RandomForestRegressor and GradientBoostingRegressor—were trained to predict the scaled approved_conversion target variable using an 80/20 train–test split. Model performance was evaluated using Mean Absolute Error (MAE), Mean Squared Error (MSE), and R-squared (R²), along with visual inspection of actual versus predicted values.

The RandomForestRegressor achieved an MAE of 0.6021, an MSE of 0.7118, and an R² of 0.1554, indicating that approximately 15.5% of the variance in approved conversions was explained by the model. The GradientBoostingRegressor showed a marginal improvement, with an MAE of 0.5999, an MSE of 0.6829, and an R² of 0.1897, explaining roughly 19% of the variance. While Gradient Boosting outperformed Random Forest across all metrics, the improvement was modest.

The actual versus predicted plots for both models revealed a consistent pattern: predicted values were heavily clustered around lower conversion levels, while higher actual conversion values were frequently underestimated. This indicates limited ability of both models to capture the full variability of the target variable, particularly for higher conversion outcomes.

Regardless of model selection, the overall findings imply that predictive performance is constrained. The low R² values show that a significant amount of the variance in authorized conversions is still unaccounted for. This restriction is probably caused by the target variable's highly skewed distribution, the predominance of low conversion values, and possible information loss from preprocessing (such as outlier capping). Although ensemble approaches offered respectable baseline performance, more advancements are anticipated to necessitate improved feature engineering, different modeling approaches, or problem reformulation (e.g., classification instead of regression).

--

<img width="468" height="299" alt="image" src="https://github.com/user-attachments/assets/97f1cf00-5cf6-4bf7-a250-a96c7346ea6c" />

--

<img width="468" height="299" alt="image" src="https://github.com/user-attachments/assets/841a45e7-f895-4973-bf3f-6884ac9a8306" />

--

<img width="385" height="353" alt="image" src="https://github.com/user-attachments/assets/aece8985-d566-405e-b3c4-d22a4224680c" />

--

<img width="269" height="247" alt="image" src="https://github.com/user-attachments/assets/a1838714-144d-47d8-8961-205a8564a101" />

-- 

<img width="468" height="211" alt="image" src="https://github.com/user-attachments/assets/b7d43f76-a3e4-4d60-967b-1c85ad4bb15e" />

---

## Discussion of Insights

Several significant insights into ad performance, user engagement, and the limitations of predictive modeling in this context were uncovered by the analysis of digital advertising data. A small number of ads account for a disproportionate share of impressions, clicks, and conversions, according to exploratory analysis, which revealed highly skewed advertising outcomes. This concentration, which reflects typical real-world marketing dynamics, indicates that the majority of campaigns have little effect while only a small percentage produce significant results.

Clustering analysis revealed discrete ad segments with various performance profiles, emphasizing the existence of both more economical engagement-oriented ads and ineffective high-spend ads. According to these segments, advertisers may find it advantageous to shift their budgets from clusters that consistently perform poorly to those that show greater engagement efficiency.

Several significant insights into ad performance, user engagement, and the limitations of predictive modeling in this context were uncovered by the analysis of digital advertising data. A small number of ads account for a disproportionate share of impressions, clicks, and conversions, according to exploratory analysis, which revealed highly skewed advertising outcomes. This concentration, which reflects typical real-world marketing dynamics, indicates that the majority of campaigns have little effect while only a small percentage produce significant results.

Clustering analysis revealed discrete ad segments with various performance profiles, emphasizing the existence of both more economical engagement-oriented ads and ineffective high-spend ads. According to these segments, advertisers may find it advantageous to shift their budgets from clusters that consistently perform poorly to those that show greater engagement efficiency.

Overall, these insights emphasize that advertising performance is driven by complex, multi-dimensional factors. While quantitative metrics and demographic attributes provide valuable signals, they are insufficient on their own to fully explain conversion behavior. Effective advertising optimization therefore requires combining performance data with richer contextual and behavioral information.

---

## Limitations and Future Work
Although this study offers valuable insights into the effectiveness of digital advertising, a number of limitations should be noted. First, ad creatives, messaging, placement, and timing are not included in the dataset; instead, it is restricted to aggregated campaign-level metrics. These variables may account for the regression models' poor predictive power since they are known to have a major impact on user behavior and conversion rates.

Second, there was a significant concentration of low or zero values in the highly skewed distribution of the target variable, approved conversions. Preprocessing techniques like outlier capping and standardization may have decreased significant variance, further restricting model performance even though they were required for model stability. This demonstrates how difficult it is to use regression-based methods on sparse and unbalanced conversion data.

Third, a static snapshot of past advertising data was used for the analysis. It was difficult to model changes in performance over time because temporal dynamics like seasonality, learning effects, and budget pacing were not recorded. Furthermore, only age and gender were included in the demographic variables, giving only a partial picture of the characteristics of the audience.

These limitations could be addressed in a number of ways in future work. Predictive performance would probably be enhanced by adding richer feature sets, such as creative attributes, platform signals, and time-based variables. The structure of conversion data might be better captured by alternative modeling techniques like time-series analysis, zero-inflated regression, or classification models. Lastly, expanding the analysis to incorporate frameworks for budget optimization or causal inference may improve the findings' practical applicability and give decision-makers more useful information.

---

## Conclusion
- This project used a real-world dataset to analyze the performance of digital advertising using a full data mining workflow. Important patterns and performance segments were found using data preprocessing, exploratory analysis, clustering, dimensionality reduction, and regression modeling. 
- The results showed that advertising outcomes are highly skewed, with a small number of campaigns accounting for most engagement and conversions. Unsupervised methods revealed distinct advertisement segments, while supervised models demonstrated limited predictive power for approved conversions. 
- These findings indicate that conversion behavior is influenced by factors not fully captured in standard performance and demographic features. Overall, the project highlights both the value and limitations of data mining techniques for supporting data-driven decision-making in digital marketing.

## Reference & Tools Used

### References
1.	Kaggle. Facebook Ads Campaign Dataset.
https://www.kaggle.com/datasets/madislemsalu/facebook-ad-campaign

2.	Han, J., Kamber, M., & Pei, J. (2012). Data Mining: Concepts and Techniques (3rd ed.). Morgan Kaufmann.

3.	James, G., Witten, D., Hastie, T., & Tibshirani, R. (2021). An Introduction to Statistical Learning (2nd ed.). Springer.

4.	scikit-learn Developers. scikit-learn: Machine Learning in Python.
https://scikit-learn.org/stable/

5.	McKinney, W. (2010). Data Structures for Statistical Computing in Python. Proceedings of the 9th Python in Science Conference.

---

## Tools Used
●	Python – Primary programming language used for data preprocessing, analysis, and modeling
●	Jupyter Notebook – Interactive environment for code development and reproducibility
●	Pandas – Data manipulation, cleaning, and feature engineering
●	NumPy – Numerical computing and array operations
●	Matplotlib & Seaborn – Data visualization for EDA and result interpretation
●	scikit-learn – Implementation of machine learning algorithms (K-Means, PCA, Random Forest, Gradient Boosting), preprocessing, and evaluation metrics









