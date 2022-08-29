![mediocre-studio-1Gvog1VdtDA-unsplash](https://user-images.githubusercontent.com/72688726/187232061-26b99efe-2e5b-4cd3-a354-385624b1ed06.jpg)
Photo by [Mediocre Studio](https://unsplash.com/@paucasals?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/spam?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# Form Check: Webform Spam Filter Development
### Developing a spam filter for detecting web form spam applied with feature selection techniques and classification models

Master Thesis is submitted as part of the module for MSc in Applied Information and Data Science at School of Business, Lucerne University of Applied Science and Art.

## Summary
This research discusses theoretical aspects of spam filtering, web structure, and internet communication. Comparing web forms and email data structure lays the fundament for creating a spam filer architecture. Popular machine learning techniques with classification functions, namely non-linear statistical models and tree-based learning techniques, are reviewed; and three machine learning methods: **Logistic Regression, Decision Tree, and Random Forest**, are chosen for fitting models. **Confusion matrix** and **cross-validation** are deplyed to estimate the test errors of proposed models. The result shows, the Random Forest model has outperformed in classifying spam class and has **achieved 99% accuracy with the least test error rate 0.1%**. Insights generated through this research have provided recommendations for the future adjustment to the FormCheck spam filter.

# Background
With the increasing usage of websites, web form has also become a new target for malware. Spammers often dump bulk messages that will blow up one’s inbox and steal data or harm websites by setting bugs or displaying harmful messages on a webpage. All the above would result in more problematic outcomes that can hurt a business's reputation, digital presence and finiacial lost.

## Webform Spam Filter
webform Spam Filter, a rule-based spam filter system is designed for detecting spam web form. It utilizes a series of rules which includes: block list, IPs Addresses, domain providers, text categorization, and regular expression techniques to measure attributes and their properties.

## Problem Statment
A rule-based mechanism is very robost to catpture spam message, but it can make the spam filter highly sensitive to suspicious message and missclassify legitimate message into spam class. In addtion, the rule-system is adjust manualy which is insufficient with the increasing volume of web form spam, and therefore, a more efficient way to analyze web form data is needed.

## Solution
To address the above issues, applying data analysis to generate spam patterns and insights into current features is a prerequisite in the spam filter development process, then developing a classification model that can achieve high accuracy and low false positive rate. Lastly, essential features of the spam filter performance are provided, and recommendations are given accordingly.

# Methods

## Data Source
There are 60021 rows and 19 columns in the original dataset, the target variable `label`, is a binary data has two class `spam` and `ham`. The image below shows the spam and ham messages distribution in the original dataset. 

<img width="427" alt="label" src="https://user-images.githubusercontent.com/72688726/187207906-2581e40c-750f-444c-81dd-04a7d547ba24.png">

## Process
This project aims at incorporating machine learning for the use in contact form spam detection, therefore, the data-driven research design is chosen. The data-driven research combines a ground-up method and a deductive approach. The research process includes preprocessing, feature engineering, and data analytics, and modeling. 

![workflow](https://user-images.githubusercontent.com/72688726/187202318-91422f62-d3da-4065-93b8-a109feea42ab.png)

## Data Analysis
### Transform rule-based model using feature engineering
In the original database, the column `Flags` stores several strings which are rules that are used for spam checking. As the rules are essential features when it comes to detecting spam, hence are transformed into binary data for data analysis. 

To extract distinctive flags in each string, **Regular Expression** is applied, 64 flags (rules) are extracted and added as new columns. Feature engineering and one hot encode method are deployed by parsing each row of the data frame. itterow and `for-loop` were applied to iteratively match each row if it contains strings stored in flags; 1 refers to a flag existing in the column and 0 means a flag is absent. `pd.Series.split()` function is used to exact string in objects, and `len()` calculates the number of spam rules checked in each message.

### Header Analysis
As suggested by Bhowmick and Hazarika (2016), Sheu et al (2016), and Arras, Horn, Montavon, Muller, and Samel (2017), *header* information is an essential feature because it provides sender data that can effectively influence the performance of spam recognition. On the other hand, analyzing header is comparatively easy to implement compared to language process and text tokenization.

 - **Server protocol**: A server protocol with `HTTP/1.0` is not commonly used nowadays, and thus, it can be a critical indicator for spam detection. 
`server_protocol` with `HTTP/1.0`, `HTTP/1.1`, and unknown have a high account of the spam web form, whereas 95% of legitimate users use server_protocol `HTTP/2.0`. The image below indicates the number of web forms in each class and the corresponding server_protocol value.

<img width="727" alt="server_pprotocol" src="https://user-images.githubusercontent.com/72688726/187211702-bb381ba4-975f-46e4-aaed-808ef48f84b4.png">

 - **Accept Language**: Referes to the broswer language is used by the user. In many cases, this field is not exist in the header in spam messages.
 a`ccept_language = 0` means this field does not exist in metadata and is 100% likely to be spam; this can be a good indicator for detecting spam web forms. In contrast, if `accept_language = 1` exists in the metadata, it is 59% likely to be spam and 41% ha. The image below shows the number of web forms in each class and the corresponding accept_language value.
 
 <img width="681" alt="acceptlanguage" src="https://user-images.githubusercontent.com/72688726/187211758-3e78835a-ced8-4944-a084-476c50381367.png">
 
 - **Cookies**: Request header contains stored HTTP cookies, this field can be found in majority legitimae message
The header field `is_cookie` is empty and is very likely to be spam; one can confirm that near 100 % of `is_cookie = 0` is spam which can be used to separate forms. The below image shows the number of web forms in each class and the corresponding is_cookie value.

<img width="694" alt="cookies" src="https://user-images.githubusercontent.com/72688726/187211768-aea7deb9-1226-4b55-8720-b3200506c63e.png">

 - **Flag_count**: flag_count refers to the number of spam checks that have been applied in an observation. As seen in the graph below, the histogram on the left shows that the number of flag counts ranges from 4 to 14; in contracts, the number of flag counts in spam messages is 23 widespread from 3 to 25. More, the boxplot on the right indicates the quantile distribution of flag_count. It is visible that once a web form is checked with more than 14 rules, it is more likely to be spam. Therefore flag_count can be a good indicator for detecting spam forms.
 
<img width="857" alt="flag_count" src="https://user-images.githubusercontent.com/72688726/187214227-c5958f8a-fb91-43c5-9260-fc4b5cf0833a.png">

### Behaviour Analysis 
To identify spam patterns, analysis of sender behavior is one of the spam detection techniques, *occurrence*, *past activity* and *user networks* for instance IP addresses can effectively capture spam messages. User-related features for instance name, phone, email, contact frequency are calculated and transformed into a percentage, which represents the occurrence of each observation.

<img width="629" alt="form_box" src="https://user-images.githubusercontent.com/72688726/187214391-e6afcbd4-9b52-4be0-b33e-de4407882e8a.png">

According to the density graph, we found:
1. The number of flags applied to spam messages is varied from 0 up to 25. 
2. The spammer is active throughout the day, whereas legitimate users are more active from 7 am to 8 pm. 
3. The activities of spammers are spread out in each category, which means some repeated users are found in the spam web form. For instance, the occurrence of the name, domain name and hostname tend to be high compared to legitimate users
4. In contrast, regular users show a few repeatation accross all activties features, which means the legitimate user may use only one or twice contact forms to reach out web host, and spammers are more likely to continue sending junk messages.

<img width="719" alt="density" src="https://user-images.githubusercontent.com/72688726/187214280-267ee5e8-35a1-4115-94ed-9885a3afda6b.png">

# Modelling
![model building](https://user-images.githubusercontent.com/72688726/187214564-bf2be24e-28fc-4c9d-99f6-aac72049b318.png)

A summary of Selected Classification Algorithms for the Research
| Algorithm               | Logistic Regression                                      | Decision Tree                                       | Random Forest                                     |
| ----------------------- | -------------------------------------------------------- | --------------------------------------------------- | ------------------------------------------------- |
| Method                  | A combination of linear regression with a logit function | An algorithm taking recursive partitioning learning | An assembled algorithm based on  Decision Tree    |
| Type                    | Statistic Model                                          | Machine Learning Model                              | Machine Learning Model                            |
| Results                 | Probability of occurrence of an event                    | Output important features and association rules     | Decision is made with majority Votes              |
| Features Interpretation | p-value                                                  | Variables Importance                                | Variables Importance                              |
| Measurement             | AIC, deviance and residual                               | Confusion matrix, precision, Recall, and F1 Score   | Confusion matrix, precision, recall, and F1 Score |

## Feature Selection with Bourta
When building a machine learning model, having too many features brings issues such as the curse of dimensionality, besides the need for more memory, processing time, and power. Features selection is deployed as it focuses on finding essential features that can be used for modifying the current spam filter system. In this case, Boruta is used (Miron, 2020). It is one of the feature selection methods capable of working with any classification method. It outputs variable importance and decision based on the Random Forest mechanism. In addition, it can work with both categorical and numeric predictors and hence can provide a better outcome than applying a correlation matrix.
<img width="800" alt="Boruta" src="https://user-images.githubusercontent.com/72688726/187219980-049158da-6bf9-449d-b95e-9d988e08d8dc.png">

 - 72 variables appear with green color means those are the essential features to judge if a web form is spam or ham; while variables are colored in red means they do not have an influential impact on the decision process and therefore be dropped in fitting a logistic regression model

## Fitting Models 
 - **Experiment 1: Logistic Regression, and use three Features Selection Methods**
  - Method 1: use p-value select features which are statistic significat for fitting model 
  - Metood 2: use `drop1` method to get the lowest AIC
  - Metood 3: use `Boruta` to select important features

The Table below compares three methods with a full model `Logit.all`

| Model | Logit.all | Logit.82 | Logit.73 | Logit.b72 |
| ----- | --------- | -------- | -------- | --------- |
| AIC   | 6739.945  | 6007.072 | 5268.2   | 5268.2    |

AIC is used to select a logistic model, as the less features the better due to modeling efficeincy, hence, `Logit.b72` is selected to compete with tree-based models

 - **Experiment 2: Decision Tree**
Classification tree `tree()`, `rpart()` and condition interference tree `ctree()` 
The value of the complexity parameter (CP) is identified and the lowest cross-validation error.
An optimal decision tree created by using the values generated above. In this model, predictors namely server_protocol, MESSAGE_URL_SPAM, accept_language, is_cookies, and IP_REPUTATION are used as the terminal notes for decision making.
<img width="771" alt="pruning_tree" src="https://user-images.githubusercontent.com/72688726/187228602-c57f09e9-c93b-42f0-a141-e998575ea2bb.png">

 - **Experiment 3: Random Forest**
T RF model has firstly fitted all predictors with default settings in `randomForest()` package. To improve the false positive rate, pruning tree is critical in building tree models. A significant drop is observed when growing 100 trees. However, the error rate becomes less visible and cannot be improved after using 300 trees. `tuneRF` and parameter `mtry` are used for tuning tree.

<img width="795" alt="rf_pruning" src="https://user-images.githubusercontent.com/72688726/187229346-7afa54d6-da5f-4314-833c-0e178ed63746.png">

# Reslut
Confusion matrix, cross-validation, ROC, and AUC curves, are used to evaluate classifiers. The image below presents the performance of the FormCheck spam filter, Prediction refers to the value of the source column, and Target refers to the actual value of the label column.
<img width="573" alt="Cofusion_matrix" src="https://user-images.githubusercontent.com/72688726/187224895-0a8825b4-e431-4637-aab9-1da98f715790.png">

Three models: Logistic Regression, Decision Tree, and Radom Forest are evaluate with Accuracy, error rate, and false-positive rate.

**Evaluation FormCheck and proposed classifiers performance**
| Classifier    | Accuracy | Error Rate | FP rate | F1     |
| ------------- | -------- | ---------- | ------- | ------ |
| **FormCheck** | 0.9941   | 0.0059     | 0.0123  | 0.9040 |
| `logit.b72`   | 0.9985   | 0.0015     | 0.0325  | 0.9992 |
| `tree`        | 0.9974   | 0.0026     | 0.0195  | 0.9988 |
| `rforest`     | 0.9999   | 0.0010     | 0.0162  | 0.9995 |

The aim of this research is to find a model that maximizes the predictive performance of classifying spam web forms. Data were split into training and testing sets for model fitting, and were accessed by applying 10-fold cross-validation.
<img width="1010" alt="cv-test" src="https://user-images.githubusercontent.com/72688726/187224342-4c9298dd-5320-4570-a02d-a77ad954a97d.png">


#### Identify Important Features for Spam Filtering
In tree-based models the function `varImpPlot()` allow us to examine the important features of the proposed models with graphical output. Variable importance measures the contribution of each variable by assessing the mean decrease accuracy. The lower the value, the less critical toward a model; the mean decreased Gini measures the purity of the end nodes of branches in a model, the lower the Gini value, the better the feature can impact the decision.
<img width="661" alt="variable_importance" src="https://user-images.githubusercontent.com/72688726/187223129-f346f58a-34d3-4f91-ad39-8c3715394142.png">


**The Result of Variable Importance Measure of Proposed Models**
| Logistic Regression | Decision Tree    | Random Forest    |
| ------------------- | ---------------- | ---------------- |
| is_name             | accept_language  | server_protocol  |
| name_perc           | flag_count       | is_cookies       |
| SENDER_DOMAIN_NO_MX | ACCEPT_LANG_NULL | flag_count       |
| DOMAIN_PERIC        | server_protocal  | ACCEPT_LANG_NULL |
| MESSAGE_URL_LINKS   | is_cookies       | MESSAGE_URLS     |


Features used in the logistic regression are very different from the other two models, this would require further investigation and experiments to test with different combinations of variables. However, this approach allows us to confirm variables: server_protocol, is_cookies, accept_language, ACCEPT_LANG_NULL, flag_count, and MESSAGE_URLS are important for spam detection in this research.

# Conclusion & Recommadation
This research has shown an improvement in assessments such as acracy, error rate, and specificity with all proposed classifiers, which proves that a spam filter designed with a machine learning approach can achieve as good performance as a rule-based protocol and the spam classifier build with random forest model has the best performace amongest other classifiers. Nevertheless, as the evolution of spam detection techniques is changed from time to time, more advanced techniques or influential factors need to be considered. Three recommendations are provided as follows:

 - **Establish Data collection and processing strategies**
 
Through the research process, features extracted from the header fields play significant roles that impact on spam recognition process, which echoes the findings from previous research and study. Hence, having clear guidance and data collection strategies is essential to improve data quality and improve the spam filter system.

 - **Important Features and rules adjustment**
 
New features, namely `server_protocol`, `is_cookies`, `accept_language`, `ACCEPT_LANG_NULL`, `flag_count`, and `MESSAGE_URLS` are frequently appear when modeling decision trees and random forests and thus suggest adding to the existing rule-based system. However, these new features need to be compared with the existing rules to make sure no overlapping exists in the current system; on the other hand, duplicated attributes, for instance: message repeat words and message repeated texts, one should be dropped because both data is overlaid and will create additional weight on its scoring system.

 - **Apply alternative machine learning methods for handling multi-class tasks**
 
In the original data, a third class is identified during the labeling stage; those web forms have similar functions such as signing up for the newsletter, catalog requests, and user registration; in addition, these types of web forms have identical or similar contents in the body text area, which makes the labeling process challenging to judge without comparing external data. Although the end goal of the spam filter is to output binary values, a machine that can determine an uncertain message would help reduce the negative impact of labeling a legitimate user as a spammer. Therefore, machine learning methods such as deep learning or recursive learning techniques would be ideal for handling multi-class tasks.

# Project Reflection
From a methodological aspect, Logistic Regression, Decision Tree, and Random Forest are chosen for building spam detection models, which may not be diverse as there are several algorithms models, namely Naïve Bayes, Support Vector Machine, or Neural Network, are wide-used for handling classification problems. Therefore, the obtained results from this research can be questioned and vary depend on different methods. 

Nonetheless, the results with testing data showed that assessment metrics: accuracy, recall, precision, specificity, and F1 score had reached the desired outcome, which implied that the three classifiers proposed in this research had achieved satisfactory performance despite falling to improve the false-positive rate. Additionally, the research have yielded new insights into the research topic to answer the research question; essential features that dominate the decision-making of classifiers are identified, and therefore can be used to modify spam filter features.
