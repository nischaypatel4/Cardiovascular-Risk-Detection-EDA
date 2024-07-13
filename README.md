# Cardio-Vascular Risk Detection

## Description
I investigated various **Unsupervised learning algorithms** using data related to cardiovascular risk detection. The objective was to aid in the early identification and prevention of cardiovascular risks, which are critical for global public health. This work aimed to facilitate more effective preventive strategies and informed medical interventions, ultimately reducing cardiovascular-related morbidity and improving overall patient care.

## Variables Description

### Demographic:

**Sex:** male or female ("M" or "F")  
**Age:** Age of the patient (Continuous - Even though recorded ages are whole numbers, age is conceptually continuous)  
**Education:** The level of education of the patient (categorical values - 1, 2, 3, 4)

### Behavioral:

1. **is_smoking:** whether or not the patient is a current smoker ("YES" or "NO")  
**Cigs Per Day:** the number of cigarettes smoked on average per day (Continuous as it can be any number, including fractions)  

### Medical (history):

2. **BP Meds:** whether or not the patient was on blood pressure medication (Nominal)  
**Prevalent Stroke:** whether or not the patient had previously had a stroke (Nominal)  
3. **Prevalent Hyp:** whether or not the patient was hypertensive (Nominal)  
**Diabetes:** whether or not the patient had diabetes (Nominal)  

### Medical (current):

4. **Tot Chol:** total cholesterol level (Continuous)  
5. **Sys BP:** systolic blood pressure (Continuous)  
6. **Dia BP:** diastolic blood pressure (Continuous)  
7. **BMI:** Body Mass Index (Continuous)  
8. **Heart Rate:** heart rate (Continuous, as it can take many possible values)  
9. **Glucose:** glucose level (Continuous)  

### Predict variable (desired target):

10. **10-year risk of coronary heart disease CHD (binary: “1” means “Yes”, “0” means “No”)**

<p align="center">
    <img src="Pics\Feature_HistPlot.png" width="800px"/>
</p>

## Data sources
The dataset was sourced from Kaggle. More information can be found [here.](https://www.kaggle.com/datasets/mamta1999/cardiovascular-risk-data)  
*Please add your `kaggle.json` to the root directory to access the data*  
The dataset provided information on over **4,000 patients and included 15 attributes**, each representing a potential risk factor for CHD. These attributes included demographic, behavioral, and medical risk factors.

## Exploratory Data Analysis
1. After loading the dataset, I conducted basic **Exploratory Data Analysis** (EDA). I started by visualizing various patterns in the data using **HistPlot and PairPlot** features in Seaborn.
<p align="center">
    <img src="Pics\Feature_PairPlot.png" height="500px" width="700px"/>
</p>

2. **Label Encoding** was performed on string features "sex" and "is_smoking". **Absolute value correlation** between every feature was analyzed and plotted as follows:
<p align="center">
    <img src="Pics\AbsValueCorelation_Plot.png" height="400px" width="600px"/>
</p>

3. **Skew transformation** was applied to skewed data using *log, square root, and boxcox* transformations.
<p align="center">
        <img src="Pics\Glucose_SkewTransformation.png" height="250px" width="250px"/> &emsp; <img src="Pics\sysBP_BoxCoxTransformation.png" height="250px" width="250px"/> &emsp; <img src="Pics\TotChol_SkewTransformation.png" height="250px" width="250px"/> 
</p>

4. To handle **outliers**, the data was scaled using **StandardScaler** to better fit the classification model. The difference is shown here:
<p align="center">
    <img src="Pics\Feature_Plot.png" height="400px" width="350px"/> &emsp; &emsp; <img src="Pics\FeatureScaled_Plot.png" height="400px" width="350px"/>
</p>

5. A **multicollinearity graph** provides more insight into the relationship between each feature.
<p align="center">
    <img src="Pics\Multicorrelation.png" height="400px" width="600px"/>
</p>

## Machine Learning Models and Accuracy
1. I applied the **K-Means Clustering algorithm** to the data, restricting the number of clusters to 2. The results were as follows:
<p align="center">
        <img src="Pics\sysBP_age_Clustering.png" height="300px" width="250px"/> &emsp; <img src="Pics\age_diaBP_Clustering.png" height="300px" width="250px"/> &emsp; <img src="Pics\diaBP_heartRate_cluster.png" height="300px" width="250px"/> 
</p>

2. Additionally, I applied **soft clustering** algorithms (which return probabilities of each data point belonging to all k clusters) like **GMM (Gaussian Mixture Model)**. Using a **Decision Tree Classifier** gave an accuracy score of 0.78.
<p align="center">
    <img src="Pics\sysBP_age_gmm.png" width="400px" height="400px">
</p>

3. **DBSCAN (density-based clustering non-parametric algorithm)** clustered data into 5 groups with 318 points of noise, performing poorly with the data. Similarly, **mean-shift clustering** failed to group the data effectively.

4. To reduce dimensions and work more efficiently with the data, **PCA (Principal Component Analysis)** was used. The plot shows the accumulated explained variance ratio for the fitted PCA object.
<p align="center">
    <img src="Pics\PCA.png" height="400px" width="500px"/> &emsp; &emsp; <img>
</p>

5. PCA analysis indicated that keeping the **first 12 components** and discarding the other 6 retains **>=99.0% of the explained variance**. Variance explained by dimensions (left) and Feature importance vs. Dimensions (right) is shown below. This improved the accuracy score when applied to the above algorithms to 0.84.
<p align="center">
    <img src="Pics\ExplainedByVariance_NoOfComponents.png" height="350px" width="45%"/> &emsp;<img src="Pics\Feature_Importance_vs_Dimensions.png" height="350px" width="45%"/>
</p>

## Conclusion
I conducted an in-depth exploration of diverse **Unsupervised learning algorithms utilizing Cardiovascular Risk data**, revealing compelling patterns. These findings have the potential to offer valuable insights into heart health, thereby informing medical institutions and guiding preventive measures.
