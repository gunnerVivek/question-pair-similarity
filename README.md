# Problem Statement
Quora is a place to gain and share knowledge—about anything. It’s a platform to ask questions and connect with people who contribute unique insights and quality answers. This empowers people to learn 
from each other and to better understand the world.

Over 100 million people visit Quora every month, so it's no surprise that many people ask similarly worded questions. Multiple questions with the same intent can cause seekers to spend more time finding 
the best answer to their question, and make writers feel they need to answer multiple versions of the same question. Quora values canonical questions because they provide a better experience to active 
seekers and writers, and offer more value to both of these groups in the long term.

# 1. Business Objecives and Constraints
- Cost of Mis - classification can be very high.
- Probability of the question pair being duplicate is needed,
 so that a threshold of choice could be chosen.
- No strict latency constraints.
- Interpretability is partially - important. Business owner needs to have an idea why the pair is duplicate (or not), but customer does not care for the reasoning.

# 2. DATA
## 2.1 Data Overview
The goal is to predict which of the provided pairs of questions contain two questions with the same meaning. The ground truth is the set of labels that have been supplied by human experts. The ground truth labels are inherently subjective, as the true meaning of sentences can never be known with certainty. Human labeling is also a 'noisy' process, and reasonable people will disagree. As a result, the ground truth labels on this dataset should be taken to be 'informed' but not 100% accurate, and may include incorrect labeling. We believe the labels, on the whole, to represent a reasonable consensus, but this may often not be true on a case by case basis for individual items in the dataset.

id | qid1 | qid2 | question1 | question2 | is_duplicate
---|------|------|-----------|-----------|-------------
the id of a training set question pair | unique id of each question 1 | unique id of each question 2 | the full text of question 1 | the full text of question 2 |set to 1 if question1 and question2 have essentially the same meaning, and 0 otherwise. the **target** variable

## 2.2 Example data points
id | qid1 | qid2 | question1 | question2 | is_duplicate
---|------|------|-----------|-----------|-------------
0 | 1 | 2 | What is the step by step guide to invest in share market in india? | What is the step by step guide to invest in share market?| 0
1|3|4|What is the story of Kohinoor (Koh-i-Noor) Diamond?|What would happen if the Indian government stole the Kohinoor (Koh-i-Noor) diamond back?|0
7|15|16|How can I be a good geologist?|What should I do to be a great geologist?|1
11|23|24|How do I read and find my YouTube comments?|How can I see all my Youtube comments?|1
