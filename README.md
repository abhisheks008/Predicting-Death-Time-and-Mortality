# A Machine Learning Approach for Predicting the Death Time and Mortality 

![image](https://github.com/abhisheks008/Predicting-Death-Time-and-Mortality/assets/68724349/7b74fc8f-c707-4fe8-8736-c6d874a1a037)

### 🚨 Abstract
The ICU mortality prediction models have traditionally focused on predicting mortality within 24 to 48 hours after hospital admission. However, this paper aims to address this limitation by developing a machine learning framework that predicts hospital mortality within 6 hours of ICU admission, allowing for a more timely prediction. Additionally, the model provides estimated time of death for critically ill patients, enabling doctors and medical staff to take necessary precautions. The model utilizes data from the MIMIC III dataset within the specified time frame. The mortality prediction model achieves an accuracy of 88%, while the death time prediction model achieves 77% accuracy based on the "Area Under the Operational Receiver Curve." The authors assert that this two-phase model will greatly benefit the healthcare system by providing accurate predictions to ensure timely and appropriate treatment for critical patients.

### 🧑🏽‍💻 Review Work 
- Over the past few decades, several ICU scoring systems have been developed using rule-based method / data mining approach, e.g. APACHE, SAPS, SOFA.<br>
- Recently, better mortality prediction models trained on larger input features have been developed using machine learning approach. E.g.
  1. Applying Latent Dirichlet Allocation to free-text hospital notes
  2. Using Recurrent Neural Network to build benchmark models
  3. Applying ensemble methods to improve mortality prediction
- However, most mortality models in the literature were designed for at least 24 hours or 48 hours after ICU admission.
- Could we predict in-hospital mortality in the early stage of ICU, say 6 hours since ICU admission?
- Also can we predict the death time for the critical patients?

### 🎯 Objective
- The goal is to build a two-phase model framework to predict<br>
        (1) in-hospital mortality and<br>
        (2) death hours since ICU admission<br>
during the early stage of ICU stay, i.e. first 6-hour since ICU admission.
- The model would be useful to promptly identify high-risk patients who might be dead within hours or days since ICU admission, so that resources can be efficiently allocated during the early stage of ICU stay.

### 📊 Exploratory Data Analysis
- The original dataset consists of 61,532 distinct ICU stays of 46,520 unique patients.
- To form our study population, we filtered out patients with
  - ICU stays < one hour
  - age less < 16 or age > 89
- The final study population consists of 49,632 ICU stays of 36,343 patients.
- Next, we consider only the dead patients with non-negative death time since ICU admission.
- There are 5,718 in-hospital mortality.
- Their average death time since ICU admission is 9.57 days, maximum death time is 206.38 days and minimum death time is 0 day.

![image](https://github.com/abhisheks008/Predicting-Death-Time-and-Mortality/assets/68724349/6c46ca32-59a9-4216-bccc-5bcd5e6ec00b)


### 🛠 Models Implemented

- **Phase 1**:
    - In Phase 1, the study population consists of 49,632 ICU stays. We split the data into 80% training set and 20% test set.
    -  We then built a custom machine learning pipeline to select features, transform data, impute missing values and train a Random Forest Classifier using grid search on 5-fold CV to predict the in-hospital mortality label.
    -  We also test the trained model (best parameter set from grid search) on the test set, and compare the model result using 6-hour, 12-hour and 24-hour data.
 
- **Phase 2**:
    - In Phase 2, we filtered out dead patients with negative death time. A total of 5,718 ICU stays of dead patients were split into 80% training set and 20% test set.
    - We label each data to one of the three specified classes, then built a custom machine learning pipeline to train a multiclass Random Forest Classifier using grid search on 5-fold CV to predict the death time label.
    - We also test the trained model (best parameter set from grid search) on the test set, and compare the model result using 6-hour, 12-hour and 24-hour data.
 
### 🚑 Result Analysis and Accuracy
- **Phase 1**: The predictive performance of the mortality model trained on 6-hour data has competitive performance (AUROC 0.88) with the same model trained on 12-hour and 24-hour data (AUROC 0.90 and 0.92 respectively).

![image](https://github.com/abhisheks008/Predicting-Death-Time-and-Mortality/assets/68724349/b1cb39a8-e44f-40f0-8a37-e0824de87fad)

- **Phase 2**: The death time multiclass classifier trained on 6-hour data also provides an effective base (micro-average AUROC 0.77) to give a rough estimate of death hours since ICU admission. The result is competitive to the models trained on 12-hour or 24-hour data (micro-average AUROC 0.79 and 0.82 respectively).

![image](https://github.com/abhisheks008/Predicting-Death-Time-and-Mortality/assets/68724349/c86c6ad2-9923-4de8-a0cd-e594e6937aed)

### 📑 Conclusion
- Although the models trained on the data in the first 24-hour since ICU admission give better performance, the first 6 hours of ICU data provides enough information for mortality prediction and a rough estimate of death hours since ICU admission.
- The proposed framework provides a base to promptly identify high-risk patients who might be dead within hours or days since ICU admission in the early stage of ICU stay, and there are potential avenues for improvement.

### 💉 Authors and Developers
<table align = 'center'>
  <tr>
<td align="center"><a href="https://github.com/abhisheks008"><img src="https://avatars.githubusercontent.com/u/68724349?v=4" width="80px;" alt=""/><br /><sub><b>Abhishek Sharma</b></sub></a></td>
<td align="center"><a href="https://github.com/Ishita-2001"><img src="https://avatars.githubusercontent.com/u/85105978?v=4" width="80px;" alt=""/><br /><sub><b> Ishita Pahari</b></sub></a></td>
<td align="center"><a href="https://github.com/UdayanMisra2000"><img src="https://avatars.githubusercontent.com/u/83898487?v=4" width="80px;" alt=""/><br /><sub><b>Udayan Misra</b></sub></a></td>
<td align="center"><a href="https://github.com/Digbijoy08"><img src="https://avatars.githubusercontent.com/u/83782347?v=4" width="80px;" alt=""/><br /><sub><b>Digbijoy Dasgupta</b></sub></a></td>
<td align="center"><a href="https://github.com/Shreya0011"><img src="https://avatars.githubusercontent.com/u/87656303?v=4" width="80px;" alt=""/><br /><sub><b>Shreya Bose</b></sub></a></td>
<td align="center"><a href="https://github.com/Raktim1246"><img src="https://avatars.githubusercontent.com/u/75154706?v=4" width="80px;" alt=""/><br /><sub><b>Raktim Karmakar</b></sub></a></td>   
  </tr>
</table>

#### © 2023 Abhishek Sharma
[![forthebadge](https://forthebadge.com/images/badges/built-with-love.svg)](https://forthebadge.com) [![forthebadge](https://forthebadge.com/images/badges/built-by-developers.svg)](https://forthebadge.com) [![forthebadge](https://forthebadge.com/images/badges/built-with-swag.svg)](https://forthebadge.com)  [![ForTheBadge makes-people-smile](http://ForTheBadge.com/images/badges/makes-people-smile.svg)](http://ForTheBadge.com)









