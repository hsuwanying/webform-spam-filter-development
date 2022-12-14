<p align = "center">
<img width="600" src = "https://user-images.githubusercontent.com/72688726/187232061-26b99efe-2e5b-4cd3-a354-385624b1ed06.jpg">
</p>
<p align = "center">Photo by
 <a href="https://unsplash.com/@paucasals?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Mediocre Studio</a> on <a href="https://unsplash.com/s/photos/spam?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
</p>

# FromCheck - An effective spam filter alternative to reCapture
### Building a spam classier with a machine learning approach - A spam detection software for website owners

This research discusses theoretical aspects of spam filtering, web structure, and internet communication and comparing web forms and email data structure lays the fundament for creating a spam filter architecture. Popular machine learning techniques with classification functions, namely Logistic Regression, Decision Tree, and Random Forest, are chosen for fitting models. Confusion matrix and cross-validation are deployed to estimate the test errors of proposed models. The result shows the Random Forest model has outperformed in classifying spam classes and has achieved 99% accuracy with the least test error rate of 0.1%. Insights generated through this research have provided recommendations for future adjustments to the FormCheck spam filter. 
<br>


Master Thesis is submitted as part of the MSc in Applied Information and Data Science module at the School of Business, Lucerne University of Applied Science and Art.

# Author
 - [Carol Hsu](https://github.com/hsuwanying)

# Table of Content
 - [Background](https://github.com/hsuwanying/webform-spam-filter-development/blob/main/README.md#background)
 - [Business Problem](https://github.com/hsuwanying/webform-spam-filter-development/blob/main/README.md#business-problem)
 - [Solution](https://github.com/hsuwanying/webform-spam-filter-development/blob/main/README.md#solution)
 - [Methods](https://github.com/hsuwanying/webform-spam-filter-development/blob/main/README.md#methods)
 - [Result](https://github.com/hsuwanying/webform-spam-filter-development/blob/main/README.md#result)
 - [Conclustion & Recommadation](https://github.com/hsuwanying/webform-spam-filter-development/blob/main/README.md#Conclustion--Recommadation)
 - [Project Refelction](https://github.com/hsuwanying/webform-spam-filter-development/blob/main/README.md#Project-Refelction)
 
 # Background
With the increasing usage of websites, web form has also become a new target for malware. Spammers often dump bulk messages that will blow up one???s inbox, steal data, or harm websites by setting bugs or displaying harmful messages on a webpage. All the above would result in more problematic outcomes that can hurt a business's reputation, digital presence, and financial loss.

# Business Problem

[FormCheck](https://marketvision.ch/webdesign/formcheck-formular-spam-schutz/) - a spam classifier which is designed for detecting spam forms send via websites. It follow a rule-based mechanism with regular expression techniques to form a series of spam check includes: block list, DSN, IPs Addresses, domain providers and text categorization. Each rule is measured, then, a corresponding score is given based on some statistical calculations. Despite its robust system and outstanding performance for detecting spam messages, the machine is very sensitive to suspicious messages and misclassify legitimate ones into a spam class, in addtion, the predefine rules is currently adjusted manually by the developer, which is insufficien with the increasing volume of web form spam, therefore, a more efficient way to classify web form data is required.


# Solution
To address the above issues, applying data analysis to generate spam patterns and insights into current features is a prerequisite in the spam filter development process, then developing a classification model that can achieve high accuracy and low false positive rate. Lastly, essential features of the spam filter performance are provided, and recommendations are given accordingly.

# Methods
- Data Prepareration: Clean data for data analysis
- Feature Engeneering: 
  - Generate new features based on theortical background and previous research
  - Transform 64 Rule-Based feautres into 64 binary variables 
- Data Analysis: 
  - Apply statistc, mathmatical calcuation in **SQL** 
  - Graphical analysis (**Python** & **R**) to check data distribution, and finding meaningful features for modelling
- Building Classifier: Fitting **Logistic Regression**, **Classification Tree**, and **Randon Forest** models use **R**
- Evaluation: Use **Confusion Matrix**, **Cross-Validation**, **ROC**, **AUROC curve** to asscess classifiers

There are 60021 rows and 19 columns in the original dataset, and the target variable `label` is binary data with two classes, `spam,` and `ham`. The image below shows the spam and ham messages distribution in the original dataset. 

<p align = "center">
 <img width="600" alt="label" src = "https://user-images.githubusercontent.com/72688726/187207906-2581e40c-750f-444c-81dd-04a7d547ba24.png">
 </p><p align = "center">Target variable: Label
</p>

 - **Header Analysis**
As suggested by Bhowmick and Hazarika (2016), Sheu et al. (2016), and Arras, Horn, Montavon, Muller, and Samel (2017), header information is an essential feature because it provides sender data that can effectively influence the performance of spam recognition. On the other hand, analyzing header is comparatively easier to implement than language process and text tokenization.

 - **Server protocol**: A server protocol with `HTTP/1.0` is not commonly used nowadays, and thus; thus, it can be a critical indicator for spam detection. `server_protocol` with `HTTP/1.0`, `HTTP/1.1`, and `unknown` have a high account of the spam web form, whereas 95% of legitimate users have `server_protocol HTTP/2.0`. The image below indicates the number of web forms in each class and the corresponding `server_protocol` value.

<p align = "center">
 <img width="600" alt="server_pprotocol" src="https://user-images.githubusercontent.com/72688726/187211702-bb381ba4-975f-46e4-aaed-808ef48f84b4.png">
 </p><p align = "center">preditc variable: server_pprotocol
</p>

 - **Accept-Language**: Refers to the browser language used by the user. In many cases, this field does not exist in the header in spam messages. `accept_language = 0` means this field does not exist in metadata and is 100% likely to be spam; this can be a good indicator for detecting spam web forms. In contrast, if `accept_language = 1` found in the metadata, it is 59% likely to be spam and 41% to be ham. The image below shows the number of web forms in each class and the corresponding `accept_language` value.

<p align = "center">
 <img width="600" alt="acceptlanguage" src="https://user-images.githubusercontent.com/72688726/187211758-3e78835a-ced8-4944-a084-476c50381367.png">
 </p><p align = "center">preditc variable: accept_language
</p>

 - **Cookies**: The request header contains stored HTTP cookies; this field can be found in the majority of legitimate message header field, while if `is_cookie`can not be found in the header field, a message is very likely to be spam; one can confirm that nearly 100 % of `is_cookie = 0` is spam which can be used to separate forms. The below image shows the number of web forms in each class and the corresponding `is_cookie` value.

<p align = "center">
 <img width="600" alt="cookies" src="https://user-images.githubusercontent.com/72688726/187211768-aea7deb9-1226-4b55-8720-b3200506c63e.png">
 </p><p align = "center">preditc variable: accept_language
</p>

 - **flag_count**: refers to the number of spam checks applied in each observation. As seen in the graph below, the histogram on the left shows that the number of flag counts ranges from 4 to 14; in contracts, the number of flag counts in spam messages is 23, widespread from 3 to 25. More, the boxplot on the right indicates the quantile distribution of flag_count. It is visible that once a web form is checked with more than 14 rules, it is more likely to be spam. Therefore flag_count can be a good indicator for detecting spam forms.

<p align = "center">
 <img width="600" alt="flag_count" src="https://user-images.githubusercontent.com/72688726/187214227-c5958f8a-fb91-43c5-9260-fc4b5cf0833a.png">
 </p><p align = "center">preditc variable: accept_language
</p>

### Behaviour Analysis 

Analysing sender behaviour is one of the spam detection techniques to identify spam patterns. We can use user activity, past activity, and user connections to calculate the spam occurrence based on features such as name, phone, and email.

The boxplot below shows the occurrence value of each categorical as percentage.
<p align = "center">
 <img width="600" alt="continous variables" src="https://user-images.githubusercontent.com/72688726/187214391-e6afcbd4-9b52-4be0-b33e-de4407882e8a.png">
 </p><p align = "center">Box Plot: Continous variables
</p>

According to the density graph, we found:

1. The number of flags applied to spam messages is varied from 0 up to 25. 
2. The spammer is active throughout the day, whereas legitimate users are more active from 7 am to 8 pm. 
3. The activities of spammers are spread out in each category, which means some repeated users are found in the spam web form. For instance, the occurrence of the name, domain name, and hostname tends to be high compared to legitimate users.
4. In contrast, regular users show a few repetitions across all activity features, which means the legitimate user may use only one or twice contact forms to reach out to a web host. Spammers are more likely to continue sending junk messages.

<p align = "center">
<img width="600" alt="density" src="https://user-images.githubusercontent.com/72688726/187214280-267ee5e8-35a1-4115-94ed-9885a3afda6b.png">
 </p><p align = "center">Density Plot: Continous variables
</p>

## Model Building
**The table below summarised the selected classification algorithms for this research.** 

| Algorithm               | Logistic Regression                                      | Decision Tree                                       | Random Forest                                     |
| ----------------------- | -------------------------------------------------------- | --------------------------------------------------- | ------------------------------------------------- |
| Method                  | A combination of linear regression with a logit function | An algorithm taking recursive partitioning learning | An assembled algorithm based on  Decision Tree    |
| Type                    | Statistic Model                                          | Machine Learning Model                              | Machine Learning Model                            |
| Results                 | Probability of occurrence of an event                    | Output important features and association rules     | Decision is made with majority Votes              |
| Features Interpretation | p-value                                                  | Variables Importance                                | Variables Importance                              |
| Measurement             | AIC, deviance and residual                               | Confusion matrix, precision, Recall, and F1 Score   | Confusion matrix, precision, recall, and F1 Score |

## Feature Selection with Bourta
When building a machine learning model, having too many features brings issues such as the curse of dimensionality, besides the need for more memory, processing time, and power. In this case, Boruta (Miron, 2020) is applied as it can work with both categorical and numeric predictors and provide a better outcome than applying a correlation matrix, and it can be supplemetary method to select important features for fitting logistic regression model

<p align ="center">
 <img width="600" alt="Boruta" src="https://user-images.githubusercontent.com/72688726/187219980-049158da-6bf9-449d-b95e-9d988e08d8dc.png">
 </p><p align = "center"> Feature Selection: Boruta
</p>

## Fitting Models 

- **Experiment 1: Logistic Regression, and use three Features Selection Methods**
  - Model 1 `Logit.all`: fitting a full model with all feautres
  - Model 2 `Logit.82`: use p-value select features which are statistic significant for fitting model
  - Model 3 `Logit.73`: use the `drop1` method to get the lowest AIC
  - Model 4``Logit.b72`: use `Boruta` selected features to fit a logistic regression model

The Table below compares three methods with a complete model `Logit.all`
 

| Model | Logit.all | Logit.82 | Logit.73 | Logit.b72 |
| ----- | --------- | -------- | -------- | --------- |
| AIC   | 6739.945  | 6007.072 | 5268.2   | 5268.2    |

AIC is used to select a logistic model, as the fewer features, the better due to modeling efficiency; hence, `Logit.b72` is chosen to compete with tree-based models


- **Experiment 2: Decision Tree**
   Classification tree `tree()`, `rpart()` and condition interference tree `ctree()` 
   The complexity parameter (CP) value and the lowest cross-validation error are identified.
   An optimal decision tree is created by using the values generated above. In this model, predictors, namely server_protocol, MESSAGE_URL_SPAM, accept_language, is_cookies, and IP_REPUTATION, are used as terminal notes for decision-making.
   
<p align ="center">
 <img width="600" alt="pruning_tree" src="https://user-images.githubusercontent.com/72688726/187228602-c57f09e9-c93b-42f0-a141-e998575ea2bb.png">
 </p><p align = "center"> Classification Tree Pruning
</p>


- **Experiment 3: Random Forest**
   The RF model first fitted all predictors with default settings in the `randomForest()` package. To improve the false positive rate, pruning tree is critical in building tree models. A significant drop is observed when growing 100 trees. However, the error rate becomes less visible and cannot be improved after using 300 trees. `tuneRF` and parameter `entry` is used for tuning trees.
<p align ="center">
 <img width="600" alt="rf_pruning" src="https://user-images.githubusercontent.com/72688726/187229346-7afa54d6-da5f-4314-833c-0e178ed63746.png">
 </p><p align = "center"> Randon Forest Pruning
</p>

<br>
Confusion matrix, cross-validation, ROC, and AUC curves, are used to evaluate classifiers. The image below presents the performance of the FormCheck spam filter, Prediction refers to the value of the source column, and Target refers to the actual value of the label column.
<p align ="center">
 <img width="600" alt="Cofusion_matrix" src="https://user-images.githubusercontent.com/72688726/187224895-0a8825b4-e431-4637-aab9-1da98f715790.png">
 </p><p align = "center"> Confusion Matrix
</p>

# Result
Three models: Logistic Regression, Decision Tree, and Radom Forest, are evaluated with Accuracy, error rate, and false-positive rate.
## Evaluation FormCheck and proposed classifiers performance

| Classifier    | Accuracy | Error Rate | FP rate | F1     |
| ------------- | -------- | ---------- | ------- | ------ |
| **FormCheck** | 0.9941   | 0.0059     | 0.0123  | 0.9040 |
| `logit.b72`   | 0.9985   | 0.0015     | 0.0325  | 0.9992 |
| `tree`        | 0.9974   | 0.0026     | 0.0195  | 0.9988 |
| `rforest`     | 0.9999   | 0.0010     | 0.0162  | 0.9995 |

<br>
This research aims to find a model that maximizes the predictive performance of classifying spam web forms. Data were split into training and testing sets for model fitting and were accessed by applying 10-fold cross-validation.
<p align ="center">
 <img width="600" alt="cv-test" src="https://user-images.githubusercontent.com/72688726/187224342-4c9298dd-5320-4570-a02d-a77ad954a97d.png">
 </p><p align = "center"> Cross Validation
</p>

### Identify mportant Features for Spam Filtering

In tree-based models, the function `varImpPlot()` allows us to examine the essential features of the proposed models with graphical output. Variable importance measures the contribution of each variable by assessing the mean decrease in accuracy. The lower the value, the less critical toward a model; the mean decreased Gini measures the purity of the end nodes of branches in a model; the lower the Gini value, the better the feature can impact the decision.

<p align ="center">
 <img width="600" alt="variable_importance" src="https://user-images.githubusercontent.com/72688726/187223129-f346f58a-34d3-4f91-ad39-8c3715394142.png">
 </p><p align = "center"> Variable Importance
</p>

### The result of the `Variable Importance Measure` of proposed models

| Logistic Regression | Decision Tree    | Random Forest    |
| ------------------- | ---------------- | ---------------- |
| is_name             | accept_language  | server_protocol  |
| name_perc           | flag_count       | is_cookies       |
| SENDER_DOMAIN_NO_MX | ACCEPT_LANG_NULL | flag_count       |
| DOMAIN_PERIC        | server_protocal  | ACCEPT_LANG_NULL |
| MESSAGE_URL_LINKS   | is_cookies       | MESSAGE_URLS     |

Features used in the logistic regression are very different from the other two models. This would require further investigation and experiments to test with different combinations of variables. However, this approach allows us to confirm variables: `server_protocol`, `is_cookies`, `accept_language`, `ACCEPT_LANG_NULL`, `flag_count`, and `MESSAGE_URLS are essential for spam detection in this research.

# Conclusion & Recommadation
This research has shown an improvement in assessments such as accuracy, error rate, and specificity with all proposed classifiers, which proves that a spam filter designed with a machine learning approach can achieve as good performance as a rule-based protocol and the spam classifier built with random forest model has the best performance amongst other classifiers. Nevertheless, as spam detection techniques evolve from time to time, more advanced techniques or influential factors need to be considered. Three recommendations are provided as follows:

 - **Establish Data collection and processing strategies**
During the data preprocessing stage, we found mamy data fields are missing becasue there was no guideline in terms of data collection, hence, establishing a clear guidance and data collection strategies are essential to improve data quality of spam filter system.

 - **Essential Features and rules adjustment**
We found the header features play significant roles that impact the spam recognition process, which is echoing literatures and previous research, features namely `server_protocol`, `is_cookies`, `accept_language`, `ACCEPT_LANG_NULL`, `flag_count`, and `MESSAGE_URLS` frequently appear when modeling decision trees and random forest and thus suggest to add to the existing rule-based system. However, these new features need to be compared with the existing rules in case data overlapping and collinearity issues.

 - **Apply alternative machine learning methods for handling multi-class tasks**
Although the end goal of the spam filter is to output binary values, a machine that can determine an uncertain message would help reduce the negative impact of labeling a legitimate user as a spammer. Therefore, machine learning methods such as deep learning or recursive learning techniques would be ideal for handling multi-class tasks.


# Project Reflection
From a methodological aspect, I used alggorithm methods for building spam detection models, which may not be diverse as there are several algorithms models, namely Na??ve Bayes, Support Vector Machine, or Neural Network, are also popular for handling classification problems. Therefore, the obtained results from this research can be questioned. Nonetheless, the results with testing data has reached the desired outcome, which implied that the three classifiers proposed in this research had achieved satisfactory performance despite failing to improve the false-positive rate.
