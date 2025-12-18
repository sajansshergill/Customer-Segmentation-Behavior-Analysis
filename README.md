# Customer Segmentation Behavior Analysis

## Problem Statement:-
### Digital advertising platforms generate large volumes of performance data, but advertisers struggle to understand which factors drive conversions and ROI. This project applies data mining techniques to analyze ad performance, identify meaningful patterns, segment ads, and build predictive insights to support better ad-spend decisions.

---

## Description of Dataset and the link for the dataset:-

Dataset: Facebook Ads Dataset (Kaggle) https://www.kaggle.com/datasets/madislemsalu/facebook-ad-campaign

Dataset Overview:
<img width="626" height="510" alt="image" src="https://github.com/user-attachments/assets/23ff9b5b-20d4-4c11-977d-d6566b88dfbc" />

Feature Description:
<img width="674" height="536" alt="image" src="https://github.com/user-attachments/assets/3dcdfa38-cbb2-4883-8c4c-97c45f282758" />

---

## Data Preprocessing Details:
<img width="858" height="356" alt="image" src="https://github.com/user-attachments/assets/8e7d2879-ce0d-46ec-8c3c-ee0201af217b" />

Handling Missing Values:
Only the conversion-related variables (total_conversion and approved_conversion) had missing values. The median, a reliable metric appropriate for skewed distributions, was used to impute these missing observations. The dataset had no missing values after imputation.

Removing or Correcting Outliers:
Box plots were used to identify and quantify outliers in numerical variables (interest1, interest2, interest3, impressions, clicks, spent, and conversion metrics) using the Interquartile Range (IQR) method. To lessen the impact of extreme values while maintaining overall data integrity, values outside of Q1 − 1.5×IQR and Q3 + 1.5×IQR were capped to the corresponding bounds.

Normalization / Standardization:
All numerical variables were standardized using z-score z-score normalization via StandardScaler to guarantee comparability across features and enhance model performance. This made the data appropriate for dimensionality reduction and distance-based algorithms by transforming each feature to have a mean of zero and a standard deviation of one.

Feature Selection and Feature Engineering:
Date variables were converted to datetime format, and a new feature representing campaign duration was engineered. Identifier columns (ad_id, campaign_id, fb_campaign_id) were removed as they do not provide predictive value. Categorical variables (age and gender) were transformed using one-hot encoding with drop_first=True to avoid multicollinearity, resulting in a structured feature set appropriate for modeling.

<img width="429" height="247" alt="image" src="https://github.com/user-attachments/assets/09bba460-d8fd-4fda-9378-afd10db7268e" />

<img width="468" height="185" alt="image" src="https://github.com/user-attachments/assets/d848e390-3f70-4965-9bb4-02ea14e18661" />

<img width="468" height="185" alt="image" src="https://github.com/user-attachments/assets/74ed1e27-8902-416a-a86c-c7d8432f9d4e" />

<img width="440" height="326" alt="image" src="https://github.com/user-attachments/assets/312af6a5-2288-4f18-adb1-6ea56aa2cafd" />

<img width="474" height="286" alt="image" src="https://github.com/user-attachments/assets/955c044b-005e-4aec-b6ad-7bc6b2dd32d2" />

---

## Exploratory Analysis Findings:

Exploratory data analysis revealed that key advertising performance metrics—impressions, clicks, and spend—exhibit strong right-skewed distributions, indicating that most advertisements generate low engagement while a small subset accounts for disproportionately high activity. This pattern persisted even after outlier capping and standardization, reflecting the inherent structure of real-world advertising data.
The Interquartile Range (IQR) method for outlier detection found extreme values in a variety of numerical features. By stabilizing the distributions and lowering variance, capping these values improved their suitability for clustering and predictive modeling. However, following imputation and outlier handling the total_conversion total_conversion feature became constant, highlighting a preprocessing-induced limitation and making it useless for further analysis.

Strong positive correlations between impressions, clicks, and spend were revealed by correlation analysis, suggesting high multicollinearity. These metrics showed moderately positive correlations with approved conversions, indicating that exposure and engagement are significant factors influencing conversion outcomes. Interest-related characteristics, on the other hand, showed weak linear correlations with performance metrics, indicating little direct impact on overall ad performance.

Analysis of categorical variables identified initial data quality issues in the age and gender fields, which were corrected by filtering invalid values. After cleaning, the 30–34 age group and male users were the most represented. Engagement metrics such as clicks and spend varied across age groups and genders, with higher values observed among certain demographics, while approved conversion rates remained relatively consistent, indicating that demographic effects are stronger in early engagement stages than in final conversion outcomes.

Finally, unsupervised clustering revealed distinct advertisement segments, confirming the presence of meaningful structure within the data. These findings directly informed feature selection, preprocessing decisions, and the choice of modeling techniques applied in later stages of the analysis.

<img width="468" height="389" alt="image" src="https://github.com/user-attachments/assets/278f9164-b3af-460c-b686-66e7d475d451" />

---






