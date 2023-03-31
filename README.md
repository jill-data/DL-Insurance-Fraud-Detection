# Insurance fraud detection

Detect fraud in insurance claims using a range of methods, which are heuristics, tree-based machine learning models, and deep learning. The dataset and case description were provided by INSEAD.

## Contribution

- [@FanXia1227](https://github.com/FanXia1227): Report writing
- [@Hangbiob](https://github.com/Hangbiob): Heuristic model improvement, report writing, quality check
- [@jill-data](https://github.com/jill-data): Data cleaning, exploratory data analysis, ML and neural network models improvement, code merging, write up (Notebook and README)
- [@SoumyaO](https://github.com/SoumyaO): Auto Encoder model improvement, exploratory data analysis and cleaning
- [@Wayne599](https://github.com/Wayne599): Heuristic model, baselines for ML, neural network, and Auto Encoder models, data cleaning, exploratory data analysis

## Case description

White lies cost the insurance industry billions of dollars every year. Ironically, after investing heavily to automate workflow from policy subscription to claims processing, digitization has made fraud easier to commit and harder to catch. However, advances in artificial intelligence and machine learning (AI and ML) offer some hope to an industry drowning in data and paying out millions for fraudulent claims. As a senior operations professional at Shift, an insurtech unicorn, you are tasked with refining the company’s fraud detection algorithm, which is used by leading global insurers to fight fraudulent claims.

## Model performance summary

| model                | flag rate (%) | hit rate (%) | auc  | f1_score |
| -------------------- | ------------- | ------------ | ---- | -------- |
| Heuristic Model      | 5.94          | 13.16        | 0.87 | 0.29     |
| Decision Tree Model  | 8.26          | 9.44         | 0.91 | 0.17     |
| Random Forest Model  | 1.29          | 21.43        | 0.95 | 0.26     |
| Neural Network Model | 0.92          | 20.00        | 0.79 | 0.21     |
| Auto Encoder         | 26            | 17.00        | ---- | 0.26     |

- If we consider AUC as the main metric of model success, the Random Forest Model has the highest AUC, followed by the Decision Tree Model and the last one is the Heuristic Model

The decision tree model exhibits the relatively high detection rate, this leads to raised investigation cost and potentially undermining customer satisfactory rates. For random forest and neural network models, detection rate is nearing 1%, as a result hit rate is much higher. Whereas for the autoencoder model, detection rate is almost 25%, which is not feasible for business in real life because the company cannot afford to run investigations on that large of a scale. This suggests there is potential for further improvement for this model or method.
Once we have a better grasp of the cost of further investigations and return on spotting a true fraudulent case, then each model can be further evaluated to better reflect the specific business needs.

## Problem with using a neural network

The transparency of neural network is poor, it does not entail to what extent all the features are affecting the result of label prediction. This is problematic in our case because:

- When communicating with the policy holders during further investigations, it is difficult to explain why the case is being investigated, potentially causing confusion and lowering customer satisfactory rates.
- When investigating flagged cases further, it is unclear which direction to start with due to the lack of transparency lowering operation efficiency and resulting in higher cost.
- Neural network might be making decisions based on factors that are irrelevant or discriminatory. This could potentially lead to law suits against discrimination, damaging company brand name.
- Lack of transparency makes it difficult to adjust its architecture or parameters to improve its performance because we do not understand how neural networks is making its decisions. This is a significant issue because accuracy (detection rate, hit rate) is critical in our specific case.

## Other approaches in dealing with class imbalance

To address the class imbalance and improve the prediction of fraud, other approaches can be employed apart from threshold adjustment. Resampling methods such as over-sampling the minority class and under-sampling the majority class can be used for balanced classes.

Another approach is Cost-sensitive learning which assigns a cost value to misclassifications of various classes, based on a cost matrix that identifies different types of errors. This will help to adjust the cost function to account for the imbalanced data, giving more weight to the minority class.

Synthetic Minority Oversampling Technique (SMOTE) is one which generates synthetic instances from existing minority class data, creating a more balanced dataset. Ensemble approach can be particularly effective in dealing with imbalanced data because they allow for different models to be used for different subsets of the data, optimizing performance for each class. By utilizing a combination of these approaches, performance can be significantly improved.

## Analysis notebook

The analysis notebook can be found [here](./Notebook.ipynb)

## Dataset lexicon

| Column Name                    | Variable explanation                          |
| ------------------------------ | --------------------------------------------- |
| PolicyholderNumber             | Unique policy number for each policyholder    |
| FirstPartyVehicleNumber        | Vehicle number                                |
| PolicyholderOccupation         | Occupation of the policyholder                |
| FirstPolicySubscriptionDate    | Subscription date                             |
| FirstPartyVehicleType          | Type of vehicle (car, motorcycle, …)          |
| PolicyholderPostCode           | Postal code of the policyholder               |
| PolicyWasSubscribedOnInternet  | 1 if policy subscribed online; 0 otherwise    |
| NumberOfPoliciesOfPolicyholder | Number of subscribed policies                 |
| FpVehicleAgeMonths             | Month age of the car at time of incident      |
| PolicyHolderAge                | Age of the policyholder                       |
| FirstPartyLiability            | Percentage of first party liability           |
| ReferenceId                    | Unique claim number identifier                |
| ThirdPartyVehicleNumber        | Vehicle number of third party                 |
| InsurerNotes                   | Insurer notes about the incident (free text)  |
| LossDate                       | Date of the covered loss incident             |
| ClaimCause                     | Cause of the incident                         |
| ClaimInvolvedCovers            | Policy covers used by the claimant            |
| DamageImportance               | Importance of damages (assessed by an expert) |
| ConnectionBetweenParties       | Potential connection between parties          |
| LossPostCode                   | Address where the incident took place         |
