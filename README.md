# Form Check: Webform Spam Filter Development
#### Developing a spam filter for detecting webform spam appled feature selection technique and classification models: Logistic Regestion, Decision Tree and Random Forest

Master Thesis is submitted as part of the module for MSc in Applied Information and Data Science at School of Business, Lucerne University of Applied Science and Art. Due to the no disclose agreement, some content cannot be shared.

## Project Summary
This research discusses theoretical aspects of spam filtering, web structure, and internet communication. Comparing web forms and email data structure lays the fundament for creating a spam filer architecture. Popular machine learning techniques with classification functions, namely non-linear statistical models and tree-based learning techniques, are reviewed; and three machine learning methods: **Logistic Regression, Decision Tree, and Random Forest**, are chosen for fitting models. **Confusion matrix** and **cross-validation** to estimate the test errors of proposed models found that the Random Forest model has outperformed in classifying spam class and has the least test error rate. Insights generated through this research have provided recommendations for the future adjustment to the FormCheck spam filter.

## Background
With the increasing usage of websites, web form has also become a new target for malware. Spammers often dump bulk messages that will blow up one’s inbox and steal data or harm websites by setting bugs or displaying harmful messages on a webpage. All the above would result in more problematic outcomes that can hurt a business's reputation, digital presence and finiacial lost.

### FormCheck
FormCheck, a rule-based spam filter system is designed for detecting spam web form. It utilizes a series of rules which includes: block list, IPs Addresses, domain providers, text categorization, and regular expression techniques to measure attributes and their properties.

### Problem Statment
A rule-based mechanism is very robost to catpture spam message, but it can make the spam filter highly sensitive to suspicious message and missclassify legitimate message into spam class. In addtion, the rule-system is adjust manualy which is insufficient with the increasing volume of web form spam, and therefore, a more efficient way to analyze web form data is needed.

## Solution
To address the above issues, applying data analysis to generate spam patterns and insights into current features is a prerequisite in the spam filter development process, then developing a classification model that can achieve high accuracy and low false positive rate. Lastly, essential features of the spam filter performance are provided, and recommendations are given accordingly.

## Data Source
There are 60021 rows and 19 columns in the original dataset, the target variable `label`, is a binary data has two class `spam` and `ham`. 
<img width="427" alt="label" src="https://user-images.githubusercontent.com/72688726/187207906-2581e40c-750f-444c-81dd-04a7d547ba24.png">

### Data Exploration and Modeling Process
This project aims at incorporating machine learning for the use in contact form spam detection, therefore, the data-driven research design is chosen. The data-driven research combines a ground-up method and a deductive approach. The research process includes preprocessing, feature engineering, and data analytics, and modeling. 

![workflow](https://user-images.githubusercontent.com/72688726/187202318-91422f62-d3da-4065-93b8-a109feea42ab.png)
![model_building](https://user-images.githubusercontent.com/72688726/187202356-a386df3e-ce83-426f-afec-ee4ea8d6c8fc.jpg)

#### Transform rule-based model using feature engineering
In the original database, the column `Flags` stores several strings which are rules that are used for spam checking. As the rules are essential features when it comes to detecting spam, hence are transformed into binary data for data analysis. 

To extract distinctive flags in each string, **Regular Expression** is applied, 64 flags (rules) are extracted and added as new columns. Feature engineering and one hot encode method are deployed by parsing each row of the data frame. itterow and `for-loop` were applied to iteratively match each row if it contains strings stored in flags; 1 refers to a flag existing in the column and 0 means a flag is absent. `pd.Series.split()` function is used to exact string in objects, and `len()` calculates the number of spam rules checked in each message.

#### Header Analysis
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


#### Behaviour Analysis 
To identify spam patterns, analysis of sender behavior is one of the spam detection techniques, *occurrence*, *past activity* and *user networks* for instance IP addresses can effectively capture spam messages. User-related features for instance name, phone, email, contact frequency are calculated and transformed into a percentage, which represents the occurrence of each observation. 

<img width="640" alt="form_hist" src="https://user-images.githubusercontent.com/72688726/187207629-4922d906-8a4a-4fe3-92c4-42384cad9294.png">
<img width="629" alt="form_box" src="https://user-images.githubusercontent.com/72688726/187201707-0c1f4b79-e577-41b1-bc94-bd896dfa1956.png">


<img width="452" alt="user_pattern" src="https://user-images.githubusercontent.com/72688726/187209271-0e474caa-0bbd-4967-9f81-4c68018820d6.png">
According to the density graph, we found:
1. The number of flags applied to spam messages is varied from 0 up to 25. 
2. The spammer is active throughout the day, whereas legitimate users are more active from 7 am to 8 pm. 
3. The activities of spammers are spread out in each category, which means some repeated users are found in the spam web form. For instance, the occurrence of the name, domain name and hostname tend to be high compared to legitimate users
4. In contrast, regular users show a few repeatation accross all activties features, which means the legitimate user may use only one or twice contact forms to reach out web host, and spammers are more likely to continue sending junk messages.

## Conclusion & Recommadation
This research has shown an improvement in assessments such as acracy, error rate, and specificity with all proposed classifiers, which proves that a spam filter designed with a machine learning approach can achieve as good performance as a rule-based protocol. Nevertheless, as the evolution of spam detection techniques is changed from time to time, more advanced techniques or influential factors need to be considered. Three recommendations are provided as follows:

### Establish Data collection and processing strategies
Through the research process, features extracted from the header fields play significant roles that impact on spam recognition process, which echoes the findings from previous research and study. Hence, having clear guidance and data collection strategies is essential to improve data quality and improve the spam filter system.

### Important Features and rules adjustment.
New features, namely server_protocol, is_cookies, accept_language, ACCEPT_LANG_NULL, flag_count, and MESSAGE_URLS are frequently appear when modeling decision trees and random forests and thus suggest adding to the existing rule-based system. However, these new features need to be compared with the existing rules to make sure no overlapping exists in the current system; on the other hand, duplicated attributes, for instance: message repeat words and message repeated texts, one should be dropped because both data is overlaid and will create additional weight on its scoring system.

### Apply alternative machine learning methods for handling multi-class tasks
In the original data, a third class is identified during the labeling stage; those web forms have similar functions such as signing up for the newsletter, catalog requests, and user registration; in addition, these types of web forms have identical or similar contents in the body text area, which makes the labeling process challenging to judge without comparing external data. Although the end goal of the spam filter is to output binary values, a machine that can determine an uncertain message would help reduce the negative impact of labeling a legitimate user as a spammer. Therefore, machine learning methods such as deep learning or recursive learning techniques would be ideal for handling multi-class tasks.

# Project Reflection
From a methodological aspect, Logistic Regression, Decision Tree, and Random Forest are chosen for building spam detection models, which may not be diverse as there are several algorithms models, namely Naïve Bayes, Support Vector Machine, or Neural Network, are wide-used for handling classification problems. Therefore, the obtained results from this research can be questioned and vary depend on different methods. 

Nonetheless, the results with testing data showed that assessment metrics: accuracy, recall, precision, specificity, and F1 score had reached the desired outcome, which implied that the three classifiers proposed in this research had achieved satisfactory performance despite falling to improve the false-positive rate. Additionally, the research have yielded new insights into the research topic to answer the research question; essential features that dominate the decision-making of classifiers are identified, and therefore can be used to modify spam filter features.
