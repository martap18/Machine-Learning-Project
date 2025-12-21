<font size="5"> <div class="alert alert-block alert-info"> Machine Learning Project - Group 27 </div> </font> 
<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ0dFut9RjhIwwK1LBIlU3h045PTD_tdwc6SA&s" style="float: right;" width="200">

  <font size="5"> Master in Data Science and Advanced Analytics </font>
 
  
  <font size="4"> **Gonçalo Rilhas, 20250490**</font><br>
  <font size="4"> **Guilherme Santos, 20250510**</font><br>
  <font size="4"> **Luana Pinto, 20250481**</font><br>
  <font size="4"> **Marta Pedro, 20250500**</font>

    
  <font size="3"> Instructors: Roberto Henriques, Ricardo Santos </font> 
  
  
  
 
  
  <font size="5"> <div class="alert alert-success" role="alert"> Cars 4 You: Expediting Car Evaluations with ML - Overview Notebook </div></font> 

### **Abstract**

The `Cars 4 You` machine learning project addresses the scalability challenge of an online car resale platform, where manual inspections have created a significant operational bottleneck. The primary objective is to develop a high-precision regression pipeline capable of estimating vehicle prices solely based on user-provided specifications, thereby automating initial valuations and optimizing operational efficiency.

Leveraging a historical dataset from 2020, the project follows a rigorous end-to-end data science workflow. It begins with a comprehensive Exploratory Data Analysis (EDA) that identified critical issues such as heteroscedasticity in the luxury segment and the presence of noisy features. A key contribution of this work was the implementation of a systematic Feature Pruning Strategy (our best model), which demonstrated that reducing dimensionality by removing weak predictors significantly improved model generalization compared to complex feature expansion.

For modeling, we benchmarked a wide range of algorithms, identifying Extra Trees (Bagging) and HistGradientBoosting (Boosting) as the top performers. While we experimented with complex Stacking architectures, our results showed that a *Weighted Blend* (60% Extra Trees + 40% HGB) trained on a refined feature set yielded the best balance between bias and variance. The workflow also introduced a validation protocol to rigorously address data leakage observed in earlier iterations.

Our open-ended section is a production-ready inference pipeline that pairs our best Regression Model with a novel Predictive Reliability System. This "Human-in-the-Loop" architecture automatically processes safe quotes while flagging high-risk predictions for manual review, ensuring financial safety without compromising automation speed.

### **Notebooks**

This project is consolidated into a single comprehensive notebook (`MLProject_Group27_Final.ipynb`) to ensure end-to-end reproducibility, from raw data ingestion to the final Kaggle submission. The workflow is structured into logical stages, detailed below:

1. **Exploratory Data Analysis (EDA) & Data Cleaning** – This section performs an in-depth analysis to understand feature distributions and assess data quality. It includes outlier detection and visualizes the relationship between independent variables and price, identifying the non-linear patterns and heteroscedasticity (variance increasing with price) that motivated the use of tree-based ensembles over linear models.

2. **Preprocessing & Feature Engineering** – Implements a robust preprocessing pipeline designed to maximize model performance. Key techniques include:
    - Scaling with StandardScaler and Missing Values with KNN Imputer.
    - Log-Transformation: Applying log(1+x) to the target variable (price) and skewed features (e.g., mileage) to normalize distributions.
    - Encoding: Strategic handling of categorical variables using One-Hot Encoding and ordinal mapping for key specifications.
</p></p>
4. **Model Assessment and Evaluation** – Benchmarks multiple regression algorithms, specifically focusing on Random Forest, Extra Trees and HistGradientBoosting. A major highlight of this section is the transition from a biased validation approach (Data Leakage). This ensured that our reported metrics (MAE) were realistic and aligned with the Kaggle test set. The final choice was a Weighted Blend (60% Extra Trees / 40% HGB).

5. **Honorable Mentions** – Throughout the development lifecycle, we implemented and tested advanced strategies such as Stacking Regressors (using RidgeCV and Linear Regression as meta-learners) and Cluster-Based approaches. While theoretically promising, these were ultimately outperformed by the simpler, pruned blending strategy. These attempts are documented to demonstrate the breadth of our experimental framework and the rationale behind rejecting unnecessary complexity.

6. **Deployment** – The final pipeline implementation. We retrain the selected champion models on the full dataset (Training + Validation) to maximize predictive power and generate the final submission.csv file.

7. **Open-Ended Section (Predictive Reliability System)** – To mitigate the financial risk of automated pricing, the group developed a "Human-in-the-Loop" safeguard system. We engineered a meta-feature called *model_uncertainty* (the disagreement between our component models) and trained a Random Forest Classifier to detect "Risky" predictions. This system acts as a traffic light: it automates ~85% of quotes (Safe Flow) with high precision while diverting the ~15% most difficult cases (Risky Flow) to human specialists, effectively preventing large financial losses.
