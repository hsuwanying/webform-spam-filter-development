# Form Check: Webform Spam Filter Development
#### Developing a spam filter for detecting webform spam appled feature selection technique and classification models: Logistic Regestion, Decision Tree and Random Forest

Master Thesis is submitted as part of the module for MSc in Applied Information and Data Science at School of Business, Lucerne University of Applied Science and Art

This research discusses theoretical aspects of spam filtering, web structure, and internet communication. Comparing web forms and email data structure lays the fundament for creating a spam filer architecture. Popular machine learning techniques with classification functions, namely non-linear statistical models and tree-based learning techniques, are reviewed; and three machine learning methods: Logistic Regression, Decision Tree, and Random Forest, are chosen for fitting models.

In the research process, data preprocessing, data exploration and features engineering are deployed. Features selection is critical when fitting many variables to logistic regression. An application of the feature selection algorithm is sequential to train the logistic regression models. Confusion matrix and cross-validation to estimate the test errors of proposed models found that the Random Forest model has outperformed in classifying spam class and has the least test error rate. Insights generated through this research have provided recommendations for the future adjustment to the FormCheck spam filter.

## Background
With the increasing usage of websites, web form has also become a new target for malware. Most spammers would not only send one or two messages; they often dump bulk messages that will blow up one’s inbox and decrease work efficiency. In addition, attackers try to steal data stored on the server, sending spam to disrupt businesses and users. The growing number of spam can result in several issues. To handle bulk messages, web owners might need additional storage to house all submission, it is very costly and wastes resources. In addition, the offenders will not just want to blow up mailboxes; they crawl web pages with the intent to steal data or harm websites by setting bugs or displaying harmful messages on a webpage. All the above would result in more problematic outcomes that can hurt a business's reputation and digital presence.

### FormCheck
FormCheck, a spam filtering system, is particularly used to detect unsolicited electronic messages sent through contact forms on web browsers. The spam filter is designed based on a rule-based system, it utilizes a series of rules which includes: block list, IPs Addresses, domain providers, text categorization, and regular expression techniques to measure attributes and their properties.

### Problem Statment
When exploring the web form data, we found the data is highly skewed, in which the number of spam webforms accounts for more than 90% of the dataset; this is because the classification task is done based on a rule-based mechanism that makes the spam filter highly sensitive to suspicious messages. On the other hand, with an increasing volume of web form spam, a more efficient way to analyze web form data is needed.
<img width="427" alt="label" src="https://user-images.githubusercontent.com/72688726/187201956-f054f4d5-a293-42a8-a9ba-ce2647c6e078.png">

## Solution
To address the above issues, applying data analysis to generate spam patterns and insights into current features is a prerequisite in the spam filter development process, then developing a classification model that can achieve high accuracy and low false positive rate. Lastly, essential features of the spam filter performance are provided, and recommendations are given accordingly.

## Data Source
There are 60021 rows and 19 columns in the original dataset, the target variable source, a binary class of web form status. Due to the no disclose agreement, dataset and EDA cannot be shared, the R code for modeling can be seen in Rmd file.

### Data Exploration and Modeling Process
This project aims at incorporating machine learning for the use in contact form spam detection, therefore, the data-driven research design is chosen. The data-driven research combines a ground-up method and a deductive approach. The research process includes preprocessing, feature engineering, and data analytics, and modeling. 
![workflow](https://user-images.githubusercontent.com/72688726/187202318-91422f62-d3da-4065-93b8-a109feea42ab.png)
![model_building](https://user-images.githubusercontent.com/72688726/187202356-a386df3e-ce83-426f-afec-ee4ea8d6c8fc.jpg)

#### Transform rule-based model using feature engineering
In the original database, the column `Flags` stores several strings which are rules that are used for spam checking. As the rules are essential features when it comes to detecting spam, hence are transformed into binary data for data analysis. 

To extract distinctive flags in each string, **Regular Expression** is applied, 64 flags (rules) are extracted and added as new columns. Feature engineering and one hot encode method are deployed by parsing each row of the data frame. itterow and `for-loop` were applied to iteratively match each row if it contains strings stored in flags; 1 refers to a flag existing in the column and 0 means a flag is absent. `pd.Series.split()` function is used to exact string in objects, and `len()` calculates the number of spam rules checked in each message.
<img width="421" alt="flag_category_2" src="https://user-images.githubusercontent.com/72688726/187202121-d50fa4d0-667e-4f41-b081-f2e7a6eaf3b1.png">

#### Header Analysis
As suggested by Bhowmick and Hazarika (2016), Sheu et al (2016), and Arras, Horn, Montavon, Muller, and Samel (2017), *header* information is an essential feature because it provides sender data that can effectively influence the performance of spam recognition. On the other hand, analyzing header is comparatively easy to implement compared to language process and text tokenization.

 - **Server protocol**: A server protocol with HTTP/1.0 is not commonly used nowadays, and thus, it can be a critical indicator for spam detection. 
 - **Accept Language**: Referes to the broswer language is used by the user. In many cases, this field is not exist in the header in spam messages.
 - **Cookies**: Request header contains stored HTTP cookies, this field can be found in majority legitimae message
 
#### Behaviour Analysis 
To identify spam patterns, analysis of sender behavior is one of the spam detection techniques, *occurrence*, *past activity* and *user networks* for instance IP addresses can effectively capture spam messages. User-related features for instance name, phone, email, contact frequency are calculated and transformed into a percentage, which represents the occurrence of each observation. 


We found normal user will contact businesese in an avarge 1 - 5 times use the contact form searvice; while spammers would have more frequent, and repeate interatction with the contacform and therefore, contact frequcey can be a good indicator for building our model.
<img width="629" alt="form_box" src="https://user-images.githubusercontent.com/72688726/187201707-0c1f4b79-e577-41b1-bc94-bd896dfa1956.png">

### Model Selection & Fitting Model


## Conclusion & Recommadation
This research has shown an improvement in assessments such as acracy, error rate, and specificity with all proposed classifiers, which proves that a spam filter designed with a machine learning approach can achieve as good performance as a rule-based protocol. Nevertheless, as the evolution of spam detection techniques is changed from time to time, more advanced techniques or influential factors need to be considered. Three recommendations are provided as follows:

### Establish Data collection and processing strategies
Through the research process, features extracted from the header fields play significant roles that impact on spam recognition process, which echoes the findings from previous research and study. Hence, having clear guidance and data collection strategies is essential to improve data quality and improve the spam filter system.

### Important Features and rules adjustment.
New features, namely server_protocol, is_cookies, accept_language, ACCEPT_LANG_NULL, flag_count, and MESSAGE_URLS are frequently appear when modeling decision trees and random forests and thus suggest adding to the existing rule-based system. However, these new features need to be compared with the existing rules to make sure no overlapping exists in the current system; on the other hand, duplicated attributes, for instance: message repeat words and message repeated texts, one should be dropped because both data is overlaid and will create additional weight on its scoring system.

### Apply alternative machine learning methods for handling multi-class tasks
In the original data, a third class is identified during the labeling stage; those web forms have similar functions such as signing up for the newsletter, catalog requests, and user registration; in addition, these types of web forms have identical or similar contents in the body text area, which makes the labeling process challenging to judge without comparing external data. Although the end goal of the spam filter is to output binary values, a machine that can determine an uncertain message would help reduce the negative impact of labeling a legitimate user as a spammer. Therefore, machine learning methods such as deep learning or recursive learning techniques would be ideal for handling multi-class tasks.

# Project Reflection
From a methodological aspect, Logistic Regression, Decision Tree, and Random Forest are chosen for building spam detection models, which may not be diverse as there are several algorithms models, namely Naïve Bayes, Support Vector Machine, or Neural Network, are wide-used for handling classification problems. In practice, external sources such as DNS, ANS, blocklist, and allowlist are used simultaneously, this information may change in various periods; it could result in inaccuracy when executing spam checks that are relied on external data sources. Therefore, the obtained results from this research can vary and can be questioned.

Nonetheless, the results of this research with testing data showed that the ratios of assessment metrics: accuracy, recall, precision, specificity, and F1 score had reached the desired outcome, which implied that the three classifiers proposed in this research had achieved satisfactory performance despite falling to improve the false-positive rate. Additionally, essential features that dominate the decision-making of classifiers are identified, which can be used to enhance the rule-based features of FormCheck future.

The proposed research methods in this project have yielded new insights into the research topic to answer the research question; it also responds to the interests of the business side. The research process includes data analysis and model building presented and visualized in graphical formats, making this paper accessible for readers from different aspects. Also, it is a convent for the later researcher to review and enhancement the study.
