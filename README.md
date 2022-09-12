# Identifying-GitHub-Expertise-Using-NLP
## Note: 
This is a MSR study as part of the MSR course 2022 at UniKo, CS department, SoftLang Team

## Name of the team: 
Whiskey

## Student names: 
- Aneesa Sulthana Jagaraspalli
- Irshad Hussain Mohammed
- Pavan Kumar Tokachichu

## Underlying paper:
https://dblp.org/rec/conf/kbse/KourtzanidisCA20

## Reproduced baseline:
  
### Objective of Reproduction

### Description : 
Training Microsoft LUIS with utterances of different technologies using NLP and  testing the acquired code chunks from github repositories  on the trained LUIS to find Precision, Recall and F-measure.

### Input data:  
Used GitHub REST API version 3, [REST API GITHUB](https://developer.github.com/v3/) to fetch input data(commit data) for testing LUIS 

Paper Code Repo: https://github.com/melkor54248/RepoSkillMiner

Our Git Project: [https://github.com/theirshadhussain/MSR-Assignment3_Whiskey](https://github.com/theirshadhussain/MSR-Assignment3_Whiskey)

### Output data: 
Evaluate Precision, Recall and F-measures for the derived technologies, by conducting a test in LUIS and reporting the results.

The   file contains calculated metrics on the results obtained.
  
### Findings of reproduction

### Process delta:
Our reproduction process differs from the process followed in the paper in the following ways:
- While training and testing LUIS, we have used SQL and Pyspark whereas in the paper they have used Linq, Entity Framework, Async Programming, Angular, and React. This is because we wanted to compare the precision, recall, and F-measure values of identification for different technologies especially which have similar syntaxes.
- We have used the single testing panel instead of the batch testing panel. This is because we wanted to check the results for individual lines of code and analyze them.

### Output delta :
Our output differs from what is described in the paper as the technologies we chose, produces less accuracy scores.
- Precision for pyspark is higher than for SQL (0.88, 0.64 respectively) 
- Recall for SQL is higher than for pyspark (1, 0.5 respectively)
- f-score for SQL is higher than for pyspark (0.78, 0.64 respectively). 

The metrics for classifying comments and other languages as 'none' also have less scores. (precision = 0.42, recall = 0.36, f1 score = 0.39)
Note: The reasons for such low scores of the model overall are having similarities between syntaxes and the relevance of comments to the queries.

Hence the the following Threats to Validity are evident by the results:
- 'Bias in identification of similar technologies from the commit files'
- 'Affect of the programming language present in the commit files on the identification of the technologies'

## MSR study enhancement:

- **Threat** — We have identified two threats to validity:
- When the technologies being trained have similar syntax the metric scores can be low. 
- Presence of programming language in the commit file can deviate the metric score of the intents.

- **Traces** — In the paper it is mentioned that  "We evaluate the precision, recall and f-measure for the derived technologies/frameworks, by conducting a batch test in LUIS and report the results". It could be a threat while evaluating as not all repositories are unbiased. Also, "We have created 98 example utterances for the 5 intents using existing or slightly altered existing samples from the official Microsoft, Angular and React documentation". In the last assignment, when we reproduced the paper we assumed that in case of similar technologies using more example utterances can help to yield high metric values. So we have considered using more example utterances to check if that works or not.

- **Theory** — We think these are threats because:
-  Training technologies with different syntax may yield high metric values(as in the paper), but when trained with technologies with similar syntax the metric scores were low during the Reproduction of the paper (assignment 2). Hence there is a bias in the identification of technologies and thus the model can misclassify or produce less accurate results.
-   We know that the commit files contain not just the technologies but also programming languages. The presence of programming languages in the commit files being tested can manipulate the results.

- **Methodology** — We plan to train model with  pyspark and sql repositories having lots of comments and test them in LUIS with code chunks of SQL, Pyspark, comments and also other programming languages (classify as 'none') to get precision, recall and f-score. This is to check if the threat still exists with the large training dataset.

- **Feasibility** — We would like to skip the part of showing the result in the software RepoSkillMiner as it might take more time to code an entire software and concentrate on evaluation of model trained in LUIS.

- **Process** —   We have trained LUIS with not just SQL and Pyspark but also alot of comments. After the training is done, we test using single panel testing instead of batch testing and calculate the precision, recall and f-score for the results. We tested using not just SQL, Pyspark but also comments, other languages like Java, C, HTML, javascript and so on to check if the output shows 'none' or not. We not only tested and calculated the metrics but also observed and analyzed the test cases when the output is wrong or less accurate. We tried to analyze when and why the result is wrong.   

- **Data** — We have trained LUIS with alot of SQL, Pyspark and also alot of comments. Other than this we have also used example codes from different languages to test for the result 'none'.

- **Results** — In the paper it is stated that 'We have created 98 example utterances for the 5 intents using existing or slightly altered existing samples from the official Microsoft, Angular and React documentation'. They have used 98 utterances for 5 intents but we have used 270 example utterances for 2 intents. 90 for SQL and 90 for Pyspark and also 90 utterances of comments for 'none' to train LUIS. Clearly we have used more utterances to train our intents than in the paper but still we have not got such high precision, recall and f-score metrics as in the paper. This might be because there can be bias in case of some intents being trained together. If the syntaxes of the languages is quite different the results can be quite accurate. But in case of languages where the syntaxes are quite similar, the results are no so accurate always. Since we performed single test panel testing instead of batch testing like in the paper, we got to observe the lines of code where the result is not correct. 

In case of basic SQL code tests, the results were very accurate

![SQL accurate results](https://user-images.githubusercontent.com/107684552/189632080-9dafe730-ac0d-418f-b8b0-a5cc21202794.png)

But in case of Pyspark, the results were not so accurate. Even a small change in the variable name would give a result 'none' instead of 'pyspark'.

![pyspark variable name conflict](https://user-images.githubusercontent.com/107684552/189644420-f9cf87da-61dd-4126-b53c-4d7807126e21.png)

Alot of pyspark codes were given a result of 'none' that too with as high intent as 0.986 which is bad in this case.

![pyspark none conflict](https://user-images.githubusercontent.com/107684552/189644455-4093e06b-969e-4cc6-8999-cf535ca16241.png)

Then when we tested comments to check whether we get the result as 'none', we did not attain the desired results. In case of single line comments of SQL we sometimes got a 'none' result with high intent of 0.923 but we also got a 'sql' result with high intent of 0.997 for a single line comment. Hence the results are not so accurate even in case of comments.

![comments conflict](https://user-images.githubusercontent.com/107684552/189645666-f23ae60e-039d-4ce4-9882-edc49cdbf8f2.png)

We also tested using codes from other languages like javascript, C, HTML, CSS, java etc., and the results were not at all accurate. We were expecting a result of 'none' but we got result 'sql' and 'pyspark' for these languages.

![other languages conflict](https://user-images.githubusercontent.com/107684552/189645596-0befc7f8-7084-4871-91bb-a5055b91a6cf.png)

![other languages conflict 1](https://user-images.githubusercontent.com/107684552/189645550-efaa742d-4566-4e36-b90a-70941ed208d9.png)

Hence we came to a conclusion that it is not possible to get such high metrics for all technologies using a small number of example utterances(98 utterances for 5 intents) as in the paper. There is a bias towards certain technologies whose syntax is unique. Hence our hypothesis of 'Is there a bias in identifying the technology from commit files?' yields a 'yes'. When we tested using codes of other languages we got a bad result like 'sql' for HTML, CSS, C etc and 'pyspark' for javascript. So we felt that when the commit files (which contain not just the code for technology but also the programming language) are being tested to find out the technologies used, the result will not always be accurate as the files also contain code of the programming languages which can be wrongly identified as the intents and not as 'none'. So our other hypothesis of 'Will the programming language present in the commit files affect the process of identification of technologies present in it?' also yields a 'yes'.

## Implementation
### Hardware Requirements :
- x86 64-bit CPU (Intel / AMD architecture)
- 4 GB RAM
- 1 GB free Disk space

### Software Requirements :
- Windows 7 or 10
- Mac OS X 10.11 or higher, 64-bit
- Linux: RHEL 6/7, 64-bit (almost all libraries also work in Ubuntu)
- Browser to access Microsoft Azure (Chrome, Bing, Firefox, Safari)

### Validation :
- The Technologies used by the authors produced more accurate results than the technologies chosen by us. We have chosen Pyspark and Sql to train LUIS and the reason to choose these two technologies is because these two technologies have a lot of similarities in their syntaxes. We wanted to check if the paper is biased with the technologies chosen by authors. As a result of our Reproduction, we found out that the metrics like Precision, Recall, F-measure were less for model differentiating SQL and Pyspark.This is because there were complex lines of code especially when provided by a Pyspark line of code internally having sql command. 
- We have used single line testing instead of batch testing to check the lines of code individually to better analyze their result and why it has occured. 
- We have used codes of other languages to check if the result is 'none' or not. This is because the commit files will contain even code from other programming languages other than the technology. We wanted to check if this would affect the result of identifying the technologies. Because if the code of other language yields a result of 'none' it is fine but if the result will be other technology intent then the result are not perfect. We wanted to test our hypothesis of 'Will the programming language present in the commit files affect the process of identification of technologies present in it?'

### Data :

#### Input   : 
For our Reproduction we have assumed the programming language of the commit files is already known and the input to our LUIS model is fetched from these commit files. 

#### Output  : 
The outputs are the metric values calculated on the Identification done by the reproduced LUIS model.
