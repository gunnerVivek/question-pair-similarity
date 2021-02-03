[toc]

<ol style="line-height: 10%; margin-bottom: 0.8em;">
    <li>
        <h5><a href="# 1. Problem Statement", style="text-decoration: none;">Problem Statement</a></h5>
    </li>
    <li>
        <h5><a href="# 2. Business Objectives and Constraints", style="text-decoration: none;">Business Objectives and Constraints</a></h5>
    </li>
    <li>
        <h5><a href="# 3. Machine Learning Problem", style="text-decoration: none;">Machine Learning Problem</a></h5>
        <ul>
            <li>
       		 	<h6><a href="# 3.1 DATA", style="text-decoration: none;">3.1Data</a></h6>
			</li>
            <li>
       		 	<h6><a href="# 3.2 Mapping Business Case to ML Problem", style="text-decoration: none;">3.2 Mapping Business Case to ML Problem</a></h6>
			</li>
		</ul>
	</li>
    <li>
        <h5><a href="# 4. Exploratory Data Analysis and Featurization", style="text-decoration: none;">Exploratory Data Analysis and Featurization</a></h5>
    </li>
    <li>
        <h5><a href="# 5. Machine Learning Models", style="text-decoration: none;">Machine Learning Models</a></h5>
    </li>
    <li>
        <h5><a href="# 6. Result Summary", style="text-decoration: none;">Result Summary</a></h5>
    </li>
</ol>






# 1. Problem Statement

Quora is a place to gain and share knowledge—about anything. It’s a platform to ask questions and connect with people who contribute unique insights and quality answers. This empowers people to learn 
from each other and to better understand the world.

Over 100 million people visit Quora every month, so it's no surprise that many people ask similarly worded questions. Multiple questions with the same intent can cause seekers to spend more time finding 
the best answer to their question, and make writers feel they need to answer multiple versions of the same question. Quora values canonical questions because they provide a better experience to active 
seekers and writers, and offer more value to both of these groups in the long term.



# 2. Business Objectives and Constraints

- Cost of Mis - classification can be very high.
- Probability of the question pair being duplicate is needed, so that a threshold of choice could be chosen.
- No strict latency constraints.
- Interpretability is partially - important. Business owner needs to have an idea why the pair is duplicate (or not), but customer does not care for the reasoning.



# 3. Machine Learning Problem



## 3.1 DATA

### 3.1.1 Data Overview
The goal is to predict which of the provided pairs of questions contain two questions with the same meaning. The ground truth is the set of labels that have been supplied by human experts. The ground truth labels are inherently subjective, as the true meaning of sentences can never be known with certainty. Human labelling is also a 'noisy' process, and reasonable people will disagree. As a result, the ground truth labels on this dataset should be taken to be 'informed' but not 100% accurate, and may include incorrect labelling. We believe the labels, on the whole, to represent a reasonable consensus, but this may often not be true on a case by case basis for individual items in the dataset.

id | qid1 | qid2 | question1 | question2 | is_duplicate
---|------|------|-----------|-----------|-------------
the id of a training set question pair | unique id of each question 1 | unique id of each question 2 | the full text of question 1 | the full text of question 2 |set to 1 if question1 and question2 have essentially the same meaning, and 0 otherwise. the **target** variable

### 3.1.2 Example data points
id | qid1 | qid2 | question1 | question2 | is_duplicate
---|------|------|-----------|-----------|-------------
0 | 1 | 2 | What is the step by step guide to invest in share market in india? | What is the step by step guide to invest in share market?| 0
1|3|4|What is the story of Kohinoor (Koh-i-Noor) Diamond?|What would happen if the Indian government stole the Kohinoor (Koh-i-Noor) diamond back?|0
7|15|16|How can I be a good geologist?|What should I do to be a great geologist?|1
11|23|24|How do I read and find my YouTube comments?|How can I see all my Youtube comments?|1

### 3.1.3 Data Link
Training data can be found [here](data/train.csv).



## 3.2 Mapping Business Case to ML Problem

### 3.2.1 Type of Machine Learning Problem
Given a pair of questions, we have to predict if they are duplicate or not. Thus it is a Binary Classification problem.

### 3.2.2 Performance Metric
Since we want probability of the class label. We will use the following Performance metrices:
- Log - loss
- Binary Confusion Matrix: To get a more detailed understanding of model performance

### 3.2.3 Train Test Split
There is a temporal nature to the problem, because the questions can change over time. However unfortunately timestamp is not available in the provided dataset. Hence we will use random splitting in the ratio of 70:30 or 80:20.



# 4. Exploratory Data Analysis and Featurization

Documentation and Code for Basic Statistics and Basic Feature Extraction can be found [here](notebooks/1_Quora.ipynb).

Documentation and Code for Text pre-processing and Advanced Feature Extraction can be found [here](notebooks/2_Quora_Preprocessing.ipynb)

Documentation and Code for Featurization of Text data can be found [here](notebooks/3_Q_Mean_W2V.ipynb) 



# 5. Machine Learning Models

This section describes the machine learning models used and the pre modelling steps and methodologies used in the project. 

Few of the pre modelling steps include Reading data from local file system and storing into a SQL table.  Converting categorical value to Numeric representation and creating  randomised train test split data sets.

Next a random model was constructed and the performance of the random model was measured. This serves as a base line model, based on which value of any future model will be evaluated.

The models that were used are : Random Baseline model, Logistic regression, Linear Support Vector Machines and XGBoost.

Detailed documentation and code of the modelling can be found [here](notebooks/4_Machine_Learning_Models.ipynb).



# 6. Result Summary



Model | Test Log loss
----------|-------------------
Random Model |0.89
Logistic Regression |0.52
SVM |0.49
XGBoost |**0.36**



Thus from above table we can see that, XGBoost gives best result. Thus using XGBoost we can be most assured of the similarities or dissimilarities among the question pairs.