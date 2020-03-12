# Project:  UK Job Salary Prediction

Authors: Tao Ouyang, Xi Zheng

Proposed as a half-semester data science project

## Motivation

Today, people are used to seeking ideal jobs online since there are so many job-related websites like LinkedIn, Indeed, or Idealist, which provide great opportunities and large quantities of job information. However, when they are searching for jobs on these websites, they might find it distressing that most employers are not willing to list the salary in employment advertisements or deliberately provide a much lower salary than usual. For people looking for a job, this leads to a dilemma. They might risk wasting valuable time investigating a low paying job, or skip the advertisement and risk ignoring a great opportunity. This project is trying to solve the problem by thorough statistical analysis to estimate an accurate salary based on a job’s title, description and other related information.

## Dataset Overview

The dataset we’re using is collected by Adzuna, a London headquartered company which collected millions of job advertisements to provide smart search engines for employers and employees. The main dataset consists of a large number of records representing individual job advertisements, and a series of fields about each job advertisement. These fields include mostly unstructured and free text-based features, such as advertisement id, job title, job description, raw location of the job, normalized location created by Adzuna, contract type, hiring company, contract type, raw salary, normalized salary created by Adzuna and the source of advertisement. 

The normalized, annualized salary interpreted by Adzuna is the target value to be predicted in this project. It is a single value based on the midpoint of any range found in the raw salary. All data samples scraped by Adzuna company are real, live data used in job advertisements.[2] In order to make the data to more convenient for researchers, Adzuna has already divided the data into three datasets. There are 244768 data samples in the training dataset, 40663 samples in the validation dataset and 122463 samples in the test dataset.

Adzuna has used this dataset to build a prediction model and a web application on its website: https://www.adzuna.co.uk/jobs/salary-predictor.html. It can directly give an estimated salary number through typing a job title and job description. As a result, the company reported that through evaluating over hundreds of algorithms and machine-learning approaches, the predicted salary is expected to be within 10% of the actual wage, which is impressive.[4]

## Proposed Plan Of Research

This dataset is collected from real world job ads and is clearly subject to lots of noise including typos, incorrect fields and duplicates. Thus, we need to conduct data cleaning to remove anomalies in the dataset.[2] We also found that most missing values appear in the Contract Type, Contract Time and Company, so we may do some imputation on the dataset. In addition, properly removing stop words is an important step when dealing with free text features.

To solve the problem, let’s look at the predictor variables in the data. All predictor features are either categorical features or free text variables. For example, Title, FullDescription are provided by the job advertisers and could not be directly used in any machine learning methods. Natural Language Processing is one of the popular approaches to process this kind of data and extract relevant information from them for statistical analysis. We will utilize various NLP methods such as Bag-of-words to extract relevant words from them for statistical analysis. Bag-of-words model, which is one of the most basic and popular approaches, is to transform texts into numeric vectors. This model assumes the positions of words do not matter. The model could be appropriate for our project to extract relevant keywords from job description, such as area of profession, domain knowledges, required skills or certificates, profession hierarchy and seniority. Collocational feature, TF-IDF and Word2Vec model may also be applied to construct new vectors that reflect the relationships between different keywords or how the keywords’ positions influence the salary. We believe these features will give us new insights into the possible salary range of the job. 

As for LocationRaw, we could apply NLP methods to capture useful information for prediction, but we are also thinking about converting the locations into spatial coordinates (longitude and latitude) and apply machine learning methods to recognize regions that may have higher level of wages than others. We believe that this information reveals more information about the salary ranges in a particular area within certain industry. For model training, we consider neural network or xgboost model to be a good choice for predicting annual salary with lots of NLP features.

Since nowadays people are relying on job search engine heavily, it’s important to improve the transparency and accessibilities of the job market and information exchange with it. By extracting the semantics (such as skills required, domain knowledge) of the job ads, the candidates would be more prepared when negotiating with employers about the salary they should be paid.

In this project, exploring the practical application of natural language processing and machine learning methods in job market is put as the top goal. For further research, we may focus on finding the best matches between the two entities by extracting semantics from both job ads and candidate resumes, which could lead to faster and efficient employment.

## Preliminary Results

<p align="center">
  <img src="https://github.com/vbienridy/DS5500-Spring2020-Job-Salary-Prediction/blob/master/proposal_images/salary_distribution_for_contract_type.png">
</p>
<p align="center">
Figure 1: Salary distribution plot for different contract types
</p>

From the plot above, we see that most of the salary values for part-time jobs are centered and gathered around 12500 while the distribution of salary for full-time jobs is a smoother one with higher average annual salary. The distribution of salary for jobs with unknown ContractType is quite similar to the one for full-time jobs.

There are in total 29 job categories in the training set. To explore its relationship with Salary, a density plot was drawn for the selected four categories, i.e. “IT Jobs”, “Legal Jobs”, “Maintenance Jobs”, “Scientific & QA Jobs”.

<p align="center">
  <img src="https://github.com/vbienridy/DS5500-Spring2020-Job-Salary-Prediction/blob/master/proposal_images/salary_distribution_for_category.png">
</p>
<p align="center">
Figure 2: Salary distribution for selected job categories
</p>

From the plot above, we see that the job category variable contains useful information for predicting possible salary range. Jobs that require higher academic degree or specific domain knowledge are more likely to have higher annual salaries. Below are the box plots for all job categories in the dataset for reference.

<p align="center">
  <img src="https://github.com/vbienridy/DS5500-Spring2020-Job-Salary-Prediction/blob/master/proposal_images/box_plot_for_salary_with_category.png">
</p>
<p align="center">
Figure 3: Salary distribution for all job categories
</p>

## References

[1] Project Github Repository:
https://github.com/vbienridy/DS5500-Spring2020-Job-Salary-Prediction

[2] Source of Dataset:
“Job Salary Prediction.” Kaggle, Adzuna, 2013, https://www.kaggle.com/c/job-salary-prediction/data

[3] Sample web application for job salary prediction:
https://www.adzuna.co.uk/jobs/salary-predictor.html

[4] UK – ADZUNA ESTIMATES ONLINE VACANCY SALARIES. Staffing Industry Analysts, 26 July 2013, www2.staffingindustry.com/eng/Editorial/Daily-News/UK-Adzuna-estimates-online-vacancy-salaries-26628.

[5] Word2Vec Wikipedia: https://en.wikipedia.org/wiki/Word2vec

[6] Johnson, Catherine B., Matt L. Riggs, and Ronald G. Downey. "Fun with numbers: Alternative models for predicting salary levels." Research in Higher Education 27.4 (1987): 349-362.

[7] Khongchai, Pornthep, and Pokpong Songmuang. "Implement of salary prediction system to improve student motivation using data mining technique." 2016 11th International Conference on Knowledge, Information and Creativity Support Systems (KICSS). IEEE, 2016.

[8] Mikolov, Tomas, et al. "Efficient estimation of word representations in vector space." arXiv preprint arXiv:1301.3781 (2013).

[9] Mikolov, Tomas, et al. "Distributed representations of words and phrases and their compositionality." Advances in neural information processing systems. 2013.
