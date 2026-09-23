Research Question: To what extent can behavioural, spatial, temporal, and environmental
features predict whether a squirrel is observed eating, and which factors are most influential 
in this prediction?

Dataset: 2018 Central Park Squirrel Census (squirrel.csv, hectare.csv)

========================================
IMPLEMENTATION 
========================================

The notebook implements data processing pipeline that merges the two
raw datasets, preprocesses, and applies correlation analysis, supervised
learning, and clustering to investigate the research question. 

It follows the main steps: 

1. Imports
   Loads all required Python libraries, including 
   pandas, matplotlib, seaborn, scikit-learn, and datetime.

2. Loading raw data
   Reads squirrel.csv and hectare.csv.

3. Data merging
   Merges squirrel observations with hectare contextual information using Hectare, Shift, and Date. 
   This allows individual squirrel behaviour to be analysed together with contextual variables.

4. Target variable analysis
   Examines the distribution of the target variable, Eating. 
   This shows the class imbalance between Eating and Not Eating observations.

5. Feature selection and preprocessing
   Removes irrelevant, highly sparse, redundant, or unstructured columns.
   Missing values are handled according to data type and missingness. 
   Categorical variables are encoded, Boolean variables are converted to integers, 
   and numerical features are prepared for analysis.

6. Feature engineering
   Creates additional variables such as Above Ground Height and Is Weekend. 
   Outliers in continuous variables are inspected and retained where they represent valid observations 
   rather than errors.

7. Scaling
   Creates a scaled version of the processed dataset for distance-based methods, 
   particularly KNN and K-Means clustering.

8. Saving processed data
   Saves:
   - preprocessed_squirrel.csv
   - preprocessed_squirrel_scaled.csv

9. Correlation and association analysis
   Uses Pearson correlation to examine directional associations between features and Eating. 
   Mutual Information and Normalized Mutual Information are used as feature relevance measures. 
   Pairwise feature-feature correlation is used to identify redundancy between predictors.

10. Supervised learning
   Defines Eating as the target variable and trains two classification models:
   - Decision Tree (DT)
   - K-Nearest Neighbours (KNN)

   The data is split into training, validation, and test sets using stratification. 
   Hyperparameters are tuned on the validation set, and final model performance is 
   evaluated on the test set. A majority-class baseline is included for comparison.

11. Feature importance
   Examines influential predictors using Decision Tree feature importance 
   and permutation importance for KNN.

12. Clustering
   Performs two clustering approaches:
   - Behavioural clustering, based on squirrel behaviour indicators.
   - Temporal/environmental clustering, based on contextual features.

   The elbow method is used to guide the choice of cluster number. 
   Clusters and Eating rates are then analysed to support interpretation patterns.


========================================
OUTPUTS AND REPORT CORRESPONDENCE
========================================
The notebook generates processed datasets and visualisations that correspond to the report sections.

Processed datasets:
- preprocessed_squirrel.csv
  Used as the cleaned dataset for correlation and supervised learning.

- preprocessed_squirrel_scaled.csv
  Used for distance-based analysis, especially KNN and clustering.

Preprocessing and target distribution:
- eating_distribution_percentage.png
  Supports the report discussion of the target variable distribution and class imbalance.

Correlation and association analysis:
- Top10_correlations.png
  Supports the Pearson correlation results by showing the strongest associations with Eating.

- Groups_average_correlation.png
  Summarises average absolute Pearson correlation by feature group.

- Top10_features_MI.png / top_mi_scores.png
  Supports the Mutual Information analysis by showing the features sharing the most information with Eating.

- Groups_average_MI.png
  Summarises average Mutual Information by feature group.

- Top10_features_NMI.png
  Supports the Normalized Mutual Information analysis.

- Groups_average_NMI.png
  Summarises average Normalized Mutual Information by feature group.

- Feature_feature_correlation.png
  Supports the feature-feature correlation discussion by showing redundancy or overlap between selected predictors.

- Feature_feature_NMI_heatmap.png
  Supports the feature redundancy discussion using Normalized Mutual Information between selected features.

Supervised learning:
- Decision Tree max_depth Tuning.png
  Shows validation performance across tree depths and supports the choice of max_depth.

- Decision Tree.png
  Shows the trained Decision Tree structure or top-level splits.

- KNN n_neighbors Tuning.png
  Shows validation performance across k values and supports the selected number of neighbours.

- Model_Performance_Comparison.png
  Supports the model comparison section by comparing accuracy, precision, recall, and F1-score 
  for the baseline, Decision Tree, and KNN.

- Confusion_Matrices.png
  Supports the model evaluation section by showing the types of correct and incorrect 
  predictions for each model.

- feature_importance_comparison.png
  Supports the feature influence discussion by comparing important predictors across the 
  Decision Tree and KNN.

Clustering:
- cluster_approach_1_elbow.png
  Supports the choice of cluster number for behavioural clustering.

- cluster0_behaviour.png, cluster1_behaviour.png, cluster2_behaviour.png, cluster3_behaviour.png
  Show the behavioural profiles of each behavioural cluster.

- b_clusters_against_location.png
  Shows how behavioural clusters are distributed across X and Y location coordinates.

- cluster_approach_2_elbow.png
  Supports the choice of cluster number for temporal/environmental clustering.

- cluster0_te_features.png, cluster1_te_features.png, cluster2_te_features.png, cluster3_te_features.png
  Show the temporal/environmental feature profiles of each cluster.

- te_clusters_against_location.png
  Shows how temporal/environmental clusters are distributed across X and Y location coordinates.

Reproducibility:
- Run the notebook from top to bottom to avoid missing variables from earlier sections.
- Random states are set in the modelling and clustering sections where relevant to improve reproducibility.
- The train, validation, and test split is stratified so that the Eating class distribution is preserved across splits.
- If using local Jupyter Notebook instead of Colab, update all /content/... paths to relative paths.
- Some figure filenames may be overwritten if a cell is rerun after modifying a plot. 
